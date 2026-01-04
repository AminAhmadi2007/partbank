<template>
  <div class="min-h-screen bg-gray-50 py-8">
    <div class="container mx-auto px-4 max-w-6xl">
      <!-- Header -->
      <div class="mb-8">
        <h1 class="text-2xl md:text-3xl font-bold text-gray-900 mb-2">
          افزودن آدرس جدید
        </h1>
        <p class="text-gray-600">
          آدرس تحویل سفارش خود را وارد کنید
        </p>
      </div>

      <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
        <!-- Left Side - Address Form -->
        <div class="lg:col-span-2">
          <!-- Method Selection -->
          <div class="bg-white rounded-2xl shadow-sm border border-gray-200 p-6 mb-6">
            <h2 class="text-lg font-bold text-gray-900 mb-4">روش وارد کردن آدرس</h2>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
              <button @click="selectMethod('manual')"
                      :class="[
                        'p-4 rounded-xl border-2 transition-all duration-300 text-right',
                        method === 'manual'
                          ? 'border-blue-500 bg-blue-50'
                          : 'border-gray-300 hover:border-gray-400 hover:bg-gray-50'
                      ]">
                <div class="flex items-center justify-between mb-3">
                  <div class="w-10 h-10 rounded-lg flex items-center justify-center"
                       :class="method === 'manual' ? 'bg-blue-100 text-blue-600' : 'bg-gray-100 text-gray-600'">
                    <span class="text-xl">✍️</span>
                  </div>
                  <div class="flex items-center gap-2">
                    <span v-if="method === 'manual'" class="w-3 h-3 bg-blue-500 rounded-full"></span>
                    <span class="text-sm font-medium text-gray-500">انتخاب دستی</span>
                  </div>
                </div>
                <h3 class="font-bold text-gray-900 mb-2">ورود دستی آدرس</h3>
                <p class="text-sm text-gray-600 leading-relaxed">
                  اطلاعات آدرس را به صورت دستی وارد کنید
                </p>
              </button>

              <button @click="selectMethod('map')"
                      :class="[
                        'p-4 rounded-xl border-2 transition-all duration-300 text-right',
                        method === 'map'
                          ? 'border-blue-500 bg-blue-50'
                          : 'border-gray-300 hover:border-gray-400 hover:bg-gray-50'
                      ]">
                <div class="flex items-center justify-between mb-3">
                  <div class="w-10 h-10 rounded-lg flex items-center justify-center"
                       :class="method === 'map' ? 'bg-blue-100 text-blue-600' : 'bg-gray-100 text-gray-600'">
                    <span class="text-xl">📍</span>
                  </div>
                  <div class="flex items-center gap-2">
                    <span v-if="method === 'map'" class="w-3 h-3 bg-blue-500 rounded-full"></span>
                    <span class="text-sm font-medium text-gray-500">انتخاب از نقشه</span>
                  </div>
                </div>
                <h3 class="font-bold text-gray-900 mb-2">انتخاب روی نقشه</h3>
                <p class="text-sm text-gray-600 leading-relaxed">
                  موقعیت خود را روی نقشه انتخاب کنید
                </p>
              </button>
            </div>
          </div>

          <!-- Address Form -->
          <div v-if="method === 'manual'" class="bg-white rounded-2xl shadow-sm border border-gray-200 p-6">
            <h2 class="text-lg font-bold text-gray-900 mb-6">اطلاعات آدرس</h2>
            
            <form @submit.prevent="saveAddress" class="space-y-6">
              <!-- Title -->
              <div>
                <label class="block text-gray-700 font-medium mb-2 text-sm">
                  عنوان آدرس
                  <span class="text-red-500 mr-1">*</span>
                </label>
                <input v-model="address.title"
                       type="text"
                       required
                       placeholder="مثال: منزل، محل کار"
                       class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 outline-none transition text-sm bg-gray-50">
              </div>

              <!-- Full Name -->
              <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                <div>
                  <label class="block text-gray-700 font-medium mb-2 text-sm">
                    نام تحویل گیرنده
                    <span class="text-red-500 mr-1">*</span>
                  </label>
                  <input v-model="address.firstName"
                         type="text"
                         required
                         placeholder="نام"
                         class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 outline-none transition text-sm bg-gray-50">
                </div>
                <div>
                  <label class="block text-gray-700 font-medium mb-2 text-sm">
                    نام خانوادگی تحویل گیرنده
                    <span class="text-red-500 mr-1">*</span>
                  </label>
                  <input v-model="address.lastName"
                         type="text"
                         required
                         placeholder="نام خانوادگی"
                         class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 outline-none transition text-sm bg-gray-50">
                </div>
              </div>

              <!-- Phone -->
              <div>
                <label class="block text-gray-700 font-medium mb-2 text-sm">
                  شماره تماس
                  <span class="text-red-500 mr-1">*</span>
                </label>
                <input v-model="address.phone"
                       type="tel"
                       required
                       placeholder="09123456789"
                       class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 outline-none transition text-sm bg-gray-50 text-left"
                       dir="ltr">
                <p class="text-xs text-gray-500 mt-2">
                  شماره تماس تحویل گیرنده را وارد کنید
                </p>
              </div>

              <!-- Address Details -->
              <div>
                <label class="block text-gray-700 font-medium mb-2 text-sm">
                  آدرس کامل
                  <span class="text-red-500 mr-1">*</span>
                </label>
                <textarea v-model="address.fullAddress"
                          required
                          rows="3"
                          placeholder="استان، شهر، خیابان، کوچه، پلاک، واحد"
                          class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 outline-none transition text-sm bg-gray-50 resize-none"></textarea>
              </div>

              <!-- Postal Code -->
              <div>
                <label class="block text-gray-700 font-medium mb-2 text-sm">
                  کد پستی
                  <span class="text-red-500 mr-1">*</span>
                </label>
                <input v-model="address.postalCode"
                       type="text"
                       required
                       placeholder="1234567890"
                       maxlength="10"
                       class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 outline-none transition text-sm bg-gray-50 text-left"
                       dir="ltr">
              </div>

              <!-- Location Picker Button -->
              <div>
                <button type="button"
                        @click="openMapModal"
                        class="w-full p-4 border-2 border-dashed border-gray-300 rounded-xl hover:border-blue-400 hover:bg-blue-50 transition flex items-center justify-center gap-3">
                  <span class="text-xl">📍</span>
                  <span class="text-gray-700 font-medium">انتخاب موقعیت روی نقشه</span>
                </button>
              </div>

              <!-- Default Address -->
              <div class="flex items-center gap-3">
                <input v-model="address.isDefault"
                       type="checkbox"
                       id="defaultAddress"
                       class="w-4 h-4 text-blue-600 rounded border-gray-300 focus:ring-blue-500">
                <label for="defaultAddress" class="text-gray-700 text-sm cursor-pointer">
                  این آدرس را به عنوان آدرس پیش‌فرض ذخیره کن
                </label>
              </div>

              <!-- Submit Button -->
              <div class="pt-6 border-t border-gray-200">
                <button type="submit"
                        :disabled="isSubmitting"
                        :class="[
                          'w-full py-4 rounded-xl font-bold text-white transition flex items-center justify-center gap-3',
                          isSubmitting
                            ? 'bg-blue-400 cursor-not-allowed'
                            : 'bg-blue-600 hover:bg-blue-700'
                        ]">
                  <span v-if="isSubmitting" class="flex items-center gap-2">
                    <svg class="w-5 h-5 animate-spin" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 4v5h.582m15.356 2A8.001 8.001 0 004.582 9m0 0H9m11 11v-5h-.581m0 0a8.003 8.003 0 01-15.357-2m15.357 2H15" />
                    </svg>
                    در حال ذخیره...
                  </span>
                  <span v-else class="flex items-center gap-2">
                    <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
                    </svg>
                    ذخیره آدرس
                  </span>
                </button>
              </div>
            </form>
          </div>

          <!-- Map Selection -->
          <div v-if="method === 'map'" class="bg-white rounded-2xl shadow-sm border border-gray-200 overflow-hidden">
            <!-- Map Header -->
            <div class="p-6 border-b border-gray-200">
              <h2 class="text-lg font-bold text-gray-900 mb-2">انتخاب موقعیت روی نقشه</h2>
              <p class="text-gray-600 text-sm">
                موقعیت دقیق خود را روی نقشه انتخاب کنید
              </p>
            </div>

            <!-- Map Container -->
            <div class="h-96 relative bg-gray-100">
              <!-- Map will be loaded here -->
              <div id="map" ref="mapContainer" class="w-full h-full"></div>
              
              <!-- Loading State -->
              <div v-if="mapLoading" class="absolute inset-0 flex items-center justify-center bg-gray-100">
                <div class="text-center">
                  <div class="w-16 h-16 mx-auto mb-4 border-4 border-blue-200 border-t-blue-600 rounded-full animate-spin"></div>
                  <p class="text-gray-600">در حال بارگذاری نقشه...</p>
                </div>
              </div>

              <!-- Error State -->
              <div v-if="mapError" class="absolute inset-0 flex items-center justify-center bg-gray-100">
                <div class="text-center p-8">
                  <div class="w-16 h-16 mx-auto mb-4 bg-red-100 rounded-full flex items-center justify-center">
                    <span class="text-2xl text-red-600">⚠️</span>
                  </div>
                  <h3 class="text-lg font-medium text-gray-900 mb-2">خطا در بارگذاری نقشه</h3>
                  <p class="text-gray-600 mb-4">{{ mapError }}</p>
                  <button @click="initMap"
                          class="px-4 py-2 bg-blue-600 hover:bg-blue-700 text-white rounded-lg">
                    تلاش مجدد
                  </button>
                </div>
              </div>

              <!-- Map Controls -->
              <div class="absolute top-4 left-4 flex flex-col gap-2 z-[1000]">
                <button @click="zoomIn"
                        class="w-10 h-10 bg-white rounded-lg shadow flex items-center justify-center hover:bg-gray-50 transition">
                  <span class="text-xl">+</span>
                </button>
                <button @click="zoomOut"
                        class="w-10 h-10 bg-white rounded-lg shadow flex items-center justify-center hover:bg-gray-50 transition">
                  <span class="text-xl">-</span>
                </button>
                <button @click="locateMe"
                        class="w-10 h-10 bg-white rounded-lg shadow flex items-center justify-center hover:bg-gray-50 transition">
                  <span class="text-xl">📍</span>
                </button>
              </div>
            </div>

            <!-- Map Address Form -->
            <div class="p-6">
              <div class="space-y-6">
                <!-- Search Address -->
                <div>
                  <label class="block text-gray-700 font-medium mb-2 text-sm">
                    جستجوی آدرس
                  </label>
                  <div class="relative">
                    <input type="text"
                           v-model="searchQuery"
                           @input="searchAddress"
                           placeholder="جستجوی آدرس یا نام مکان..."
                           class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 outline-none transition text-sm bg-gray-50 pr-10">
                    <svg class="absolute right-3 top-1/2 -translate-y-1/2 w-5 h-5 text-gray-400" 
                         fill="none" stroke="currentColor" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" 
                            d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" />
                    </svg>
                  </div>
                  
                  <!-- Search Results -->
                  <div v-if="searchResults.length > 0" 
                       class="mt-2 max-h-48 overflow-y-auto border border-gray-200 rounded-lg bg-white shadow-lg">
                    <div v-for="result in searchResults" 
                         :key="result.place_id"
                         @click="selectSearchResult(result)"
                         class="p-3 hover:bg-gray-50 cursor-pointer border-b border-gray-100 last:border-b-0 transition">
                      <p class="text-sm text-gray-700">{{ result.display_name }}</p>
                      <p class="text-xs text-gray-500 mt-1">{{ result.type }}</p>
                    </div>
                  </div>
                </div>

                <!-- Selected Address -->
                <div>
                  <label class="block text-gray-700 font-medium mb-2 text-sm">
                    آدرس انتخاب شده
                    <span v-if="selectedAddress" class="text-green-600 text-xs">✓</span>
                  </label>
                  <div class="p-4 bg-gray-50 rounded-lg border border-gray-300 min-h-[60px]">
                    <p v-if="selectedAddress" class="text-gray-700 text-sm">{{ selectedAddress }}</p>
                    <p v-else class="text-gray-400 text-sm">هنوز آدرسی انتخاب نشده است</p>
                    
                    <div v-if="coordinates" class="mt-2 text-xs text-gray-500 flex items-center gap-2">
                      <span>مختصات:</span>
                      <span>{{ coordinates.lat.toFixed(6) }}, {{ coordinates.lng.toFixed(6) }}</span>
                    </div>
                  </div>
                  
                  <div class="flex gap-2 mt-2">
                    <button @click="refineAddress"
                            :disabled="!selectedAddress"
                            class="text-blue-600 hover:text-blue-700 text-sm font-medium flex items-center gap-1 disabled:text-gray-400">
                      <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z" />
                      </svg>
                      ویرایش جزئیات آدرس
                    </button>
                    <button @click="clearMapSelection"
                            :disabled="!selectedAddress"
                            class="text-red-600 hover:text-red-700 text-sm font-medium flex items-center gap-1 disabled:text-gray-400">
                      <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
                      </svg>
                      حذف انتخاب
                    </button>
                  </div>
                </div>

                <!-- Additional Info -->
                <div>
                  <label class="block text-gray-700 font-medium mb-2 text-sm">
                    جزئیات تکمیلی (اختیاری)
                  </label>
                  <textarea v-model="mapAddress.extraInfo"
                            rows="2"
                            placeholder="طبقه، واحد، نام بلوک، راهنمای رسیدن"
                            class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 outline-none transition text-sm bg-gray-50 resize-none"></textarea>
                </div>

                <!-- Title -->
                <div>
                  <label class="block text-gray-700 font-medium mb-2 text-sm">
                    عنوان آدرس
                    <span class="text-red-500 mr-1">*</span>
                  </label>
                  <input v-model="mapAddress.title"
                         type="text"
                         required
                         placeholder="مثال: منزل، محل کار"
                         class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 outline-none transition text-sm bg-gray-50">
                </div>

                <!-- Save Button -->
                <button @click="saveMapAddress"
                        :disabled="isSubmitting || !selectedAddress || !mapAddress.title"
                        :class="[
                          'w-full py-4 rounded-xl font-bold text-white transition flex items-center justify-center gap-3',
                          isSubmitting || !selectedAddress || !mapAddress.title
                            ? 'bg-blue-400 cursor-not-allowed'
                            : 'bg-blue-600 hover:bg-blue-700'
                        ]">
                  <span v-if="isSubmitting" class="flex items-center gap-2">
                    <svg class="w-5 h-5 animate-spin" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 4v5h.582m15.356 2A8.001 8.001 0 004.582 9m0 0H9m11 11v-5h-.581m0 0a8.003 8.003 0 01-15.357-2m15.357 2H15" />
                    </svg>
                    در حال ذخیره...
                  </span>
                  <span v-else class="flex items-center gap-2">
                    <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
                    </svg>
                    {{ !selectedAddress ? 'لطفاً آدرس را انتخاب کنید' : !mapAddress.title ? 'عنوان آدرس را وارد کنید' : 'ذخیره آدرس از نقشه' }}
                  </span>
                </button>
              </div>
            </div>
          </div>
        </div>

        <!-- Right Side - Help & Saved Addresses -->
        <div class="lg:col-span-1">
          <!-- Help Card -->
          <div class="bg-white rounded-2xl shadow-sm border border-gray-200 p-6 mb-6">
            <h3 class="font-bold text-gray-900 mb-4 flex items-center gap-2">
              <span class="text-blue-600">💡</span>
              راهنمای آدرس دهی
            </h3>
            <div class="space-y-4">
              <div class="flex items-start gap-3">
                <div class="w-8 h-8 bg-blue-100 rounded-lg flex items-center justify-center flex-shrink-0">
                  <span class="text-blue-600 text-sm">📍</span>
                </div>
                <div>
                  <h4 class="font-medium text-gray-900 text-sm mb-1">روی نقشه کلیک کنید</h4>
                  <p class="text-gray-600 text-xs leading-relaxed">
                    برای انتخاب موقعیت، روی نقشه در محل مورد نظر کلیک کنید
                  </p>
                </div>
              </div>

              <div class="flex items-start gap-3">
                <div class="w-8 h-8 bg-blue-100 rounded-lg flex items-center justify-center flex-shrink-0">
                  <span class="text-blue-600 text-sm">🔍</span>
                </div>
                <div>
                  <h4 class="font-medium text-gray-900 text-sm mb-1">جستجوی آسان</h4>
                  <p class="text-gray-600 text-xs leading-relaxed">
                    نام خیابان، محله یا مکان را تایپ کنید تا پیدا شود
                  </p>
                </div>
              </div>

              <div class="flex items-start gap-3">
                <div class="w-8 h-8 bg-blue-100 rounded-lg flex items-center justify-center flex-shrink-0">
                  <span class="text-blue-600 text-sm">🎯</span>
                </div>
                <div>
                  <h4 class="font-medium text-gray-900 text-sm mb-1">موقعیت‌یابی خودکار</h4>
                  <p class="text-gray-600 text-xs leading-relaxed">
                    با دکمه موقعیت‌یابی، مکان فعلی شما شناسایی می‌شود
                  </p>
                </div>
              </div>
            </div>
          </div>

          <!-- Recent Addresses -->
          <div class="bg-white rounded-2xl shadow-sm border border-gray-200 p-6">
            <h3 class="font-bold text-gray-900 mb-4 flex items-center gap-2">
              <span class="text-blue-600">📝</span>
              آدرس‌های ذخیره شده
            </h3>
            
            <div v-if="savedAddresses.length > 0" class="space-y-4">
              <div v-for="addr in savedAddresses.slice(0, 3)" :key="addr.id"
                   @click="selectSavedAddress(addr)"
                   :class="[
                     'p-4 border rounded-xl cursor-pointer transition-all',
                     selectedSavedAddress?.id === addr.id
                       ? 'border-blue-500 bg-blue-50'
                       : 'border-gray-300 hover:border-gray-400 hover:bg-gray-50'
                   ]">
                <div class="flex items-start justify-between mb-2">
                  <h4 class="font-medium text-gray-900 text-sm">{{ addr.title }}</h4>
                  <span v-if="addr.isDefault" 
                        class="text-xs bg-blue-100 text-blue-700 px-2 py-1 rounded">
                    پیش‌فرض
                  </span>
                </div>
                <p class="text-gray-600 text-xs line-clamp-2 mb-2">{{ addr.fullAddress }}</p>
                <div class="flex items-center gap-2 text-xs text-gray-500">
                  <span>{{ addr.firstName }} {{ addr.lastName }}</span>
                  <span>•</span>
                  <span>{{ addr.phone }}</span>
                </div>
                <div v-if="addr.coordinates" class="mt-2 text-xs text-gray-400">
                  مختصات: {{ addr.coordinates.lat?.toFixed(4) }}, {{ addr.coordinates.lng?.toFixed(4) }}
                </div>
              </div>
              
              <button @click="showAllAddresses = true"
                      class="w-full py-3 border border-gray-300 hover:border-gray-400 rounded-xl text-gray-700 hover:text-gray-900 text-sm font-medium transition flex items-center justify-center gap-2">
                <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
                </svg>
                مشاهده همه آدرس‌ها
              </button>
            </div>
            
            <div v-else class="text-center py-8">
              <div class="w-16 h-16 mx-auto mb-4 bg-gray-100 rounded-full flex items-center justify-center">
                <span class="text-2xl">🏠</span>
              </div>
              <p class="text-gray-600 text-sm">هنوز آدرسی ذخیره نکرده‌اید</p>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Map Modal (for manual address form) -->
    <div v-if="showMapModal" class="fixed inset-0 bg-black/50 z-50 flex items-center justify-center p-4">
      <div class="bg-white rounded-2xl shadow-2xl w-full max-w-4xl max-h-[90vh] overflow-y-auto">
        <div class="p-6">
          <div class="flex items-center justify-between mb-6">
            <h3 class="text-xl font-bold text-gray-900">انتخاب موقعیت روی نقشه</h3>
            <button @click="closeMapModal"
                    class="text-gray-400 hover:text-gray-600">
              <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
              </svg>
            </button>
          </div>
          
          <div class="h-96 bg-gray-100 rounded-xl mb-6 relative" id="modalMap">
            <!-- Modal Map will be loaded here -->
          </div>
          
          <div v-if="modalSelectedAddress" class="mb-6 p-4 bg-gray-50 rounded-lg border border-gray-300">
            <p class="text-gray-700 text-sm">{{ modalSelectedAddress }}</p>
          </div>
          
          <div class="flex justify-end gap-3">
            <button @click="closeMapModal"
                    class="px-6 py-3 border border-gray-300 rounded-xl text-gray-700 hover:border-gray-400 hover:text-gray-900 transition">
              لغو
            </button>
            <button @click="confirmModalLocation"
                    class="px-6 py-3 bg-blue-600 hover:bg-blue-700 text-white rounded-xl transition">
              تأیید موقعیت
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted, nextTick } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()

// State
const method = ref('manual')
const isSubmitting = ref(false)
const showMapModal = ref(false)
const selectedSavedAddress = ref(null)
const showAllAddresses = ref(false)

// Map State
const mapLoading = ref(false)
const mapError = ref('')
const mapInstance = ref(null)
const modalMapInstance = ref(null)
const marker = ref(null)
const modalMarker = ref(null)
const searchQuery = ref('')
const searchResults = ref([])
const searchTimeout = ref(null)

// Address Data
const address = ref({
  title: '',
  firstName: '',
  lastName: '',
  phone: '',
  fullAddress: '',
  postalCode: '',
  isDefault: false
})

// Map Address Data
const mapAddress = ref({
  title: '',
  extraInfo: '',
  coordinates: {
    lat: null,
    lng: null
  }
})

const coordinates = ref(null)
const selectedAddress = ref('')
const modalSelectedAddress = ref('')
const modalCoordinates = ref(null)

// Saved Addresses
const savedAddresses = ref([])

// Load saved addresses from localStorage
const loadSavedAddresses = () => {
  const saved = localStorage.getItem('savedAddresses')
  if (saved) {
    savedAddresses.value = JSON.parse(saved)
  }
}

// Save addresses to localStorage
const saveToLocalStorage = () => {
  localStorage.setItem('savedAddresses', JSON.stringify(savedAddresses.value))
}

// Initialize Map (Leaflet)
const initMap = () => {
  try {
    mapLoading.value = true
    mapError.value = ''
    
    // مختصات تهران
    const defaultCenter = [35.715298, 51.404343]
    
    // ایجاد نقشه اصلی
    if (method.value === 'map') {
      mapInstance.value = L.map('map').setView(defaultCenter, 13)
      
      // اضافه کردن tile layer
      L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
        attribution: '© OpenStreetMap contributors',
        maxZoom: 19
      }).addTo(mapInstance.value)
      
      // ایجاد marker
      marker.value = L.marker(defaultCenter, {
        draggable: true
      }).addTo(mapInstance.value)
      
      // رویدادها
      marker.value.on('dragend', function() {
        const pos = marker.value.getLatLng()
        updateCoordinates(pos.lat, pos.lng)
      })
      
      mapInstance.value.on('click', function(e) {
        marker.value.setLatLng(e.latlng)
        updateCoordinates(e.latlng.lat, e.latlng.lng)
      })
      
      // موقعیت‌یابی
      mapInstance.value.locate({ setView: true, maxZoom: 16 })
      
      mapInstance.value.on('locationfound', function(e) {
        marker.value.setLatLng(e.latlng)
        updateCoordinates(e.latlng.lat, e.latlng.lng)
      })
    }
    
    mapLoading.value = false
  } catch (error) {
    console.error('Map initialization error:', error)
    mapError.value = 'خطا در بارگذاری نقشه. لطفاً دوباره تلاش کنید.'
    mapLoading.value = false
  }
}

// Initialize Modal Map
const initModalMap = () => {
  try {
    const defaultCenter = [35.715298, 51.404343]
    
    modalMapInstance.value = L.map('modalMap').setView(defaultCenter, 13)
    
    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
      attribution: '© OpenStreetMap contributors',
      maxZoom: 19
    }).addTo(modalMapInstance.value)
    
    modalMarker.value = L.marker(defaultCenter, {
      draggable: true
    }).addTo(modalMapInstance.value)
    
    modalMapInstance.value.on('click', function(e) {
      modalMarker.value.setLatLng(e.latlng)
      getAddressFromCoordinates(e.latlng.lat, e.latlng.lng, 'modal')
    })
    
    modalMarker.value.on('dragend', function() {
      const pos = modalMarker.value.getLatLng()
      getAddressFromCoordinates(pos.lat, pos.lng, 'modal')
    })
    
  } catch (error) {
    console.error('Modal map error:', error)
  }
}

// Get address from coordinates using Nominatim
const getAddressFromCoordinates = async (lat, lng, type = 'main') => {
  try {
    const response = await fetch(
      `https://nominatim.openstreetmap.org/reverse?format=json&lat=${lat}&lon=${lng}&zoom=18&addressdetails=1`
    )
    
    if (response.ok) {
      const data = await response.json()
      const addressText = data.display_name || `${lat.toFixed(6)}, ${lng.toFixed(6)}`
      
      if (type === 'modal') {
        modalSelectedAddress.value = addressText
        modalCoordinates.value = { lat, lng }
      } else {
        selectedAddress.value = addressText
        coordinates.value = { lat, lng }
        mapAddress.value.coordinates = { lat, lng }
      }
    }
  } catch (error) {
    console.error('Reverse geocoding error:', error)
    if (type === 'modal') {
      modalSelectedAddress.value = `${lat.toFixed(6)}, ${lng.toFixed(6)}`
    } else {
      selectedAddress.value = `${lat.toFixed(6)}, ${lng.toFixed(6)}`
    }
  }
}

// Update coordinates for main map
const updateCoordinates = (lat, lng) => {
  coordinates.value = { lat, lng }
  mapAddress.value.coordinates = { lat, lng }
  getAddressFromCoordinates(lat, lng, 'main')
}

// Search address
const searchAddress = () => {
  if (searchTimeout.value) {
    clearTimeout(searchTimeout.value)
  }
  
  if (!searchQuery.value.trim()) {
    searchResults.value = []
    return
  }
  
  searchTimeout.value = setTimeout(async () => {
    try {
      const response = await fetch(
        `https://nominatim.openstreetmap.org/search?format=json&q=${encodeURIComponent(searchQuery.value)}&limit=5&addressdetails=1`
      )
      
      if (response.ok) {
        const data = await response.json()
        searchResults.value = data
      }
    } catch (error) {
      console.error('Search error:', error)
      searchResults.value = []
    }
  }, 500)
}

// Select search result
const selectSearchResult = (result) => {
  const lat = parseFloat(result.lat)
  const lng = parseFloat(result.lon)
  
  if (mapInstance.value && marker.value) {
    mapInstance.value.setView([lat, lng], 16)
    marker.value.setLatLng([lat, lng])
    updateCoordinates(lat, lng)
  }
  
  searchQuery.value = ''
  searchResults.value = []
}

// Map controls
const zoomIn = () => {
  if (mapInstance.value) {
    mapInstance.value.zoomIn()
  }
}

const zoomOut = () => {
  if (mapInstance.value) {
    mapInstance.value.zoomOut()
  }
}

const locateMe = () => {
  if (mapInstance.value) {
    mapInstance.value.locate({ setView: true, maxZoom: 16 })
  }
}

const clearMapSelection = () => {
  coordinates.value = null
  selectedAddress.value = ''
  mapAddress.value = {
    title: '',
    extraInfo: '',
    coordinates: { lat: null, lng: null }
  }
  
  if (marker.value && mapInstance.value) {
    const defaultCenter = [35.715298, 51.404343]
    marker.value.setLatLng(defaultCenter)
    mapInstance.value.setView(defaultCenter, 13)
  }
}

// Modal functions
const openMapModal = () => {
  showMapModal.value = true
  nextTick(() => {
    initModalMap()
  })
}

const closeMapModal = () => {
  showMapModal.value = false
  if (modalMapInstance.value) {
    modalMapInstance.value.remove()
    modalMapInstance.value = null
  }
}

const confirmModalLocation = () => {
  if (modalSelectedAddress.value) {
    address.value.fullAddress = modalSelectedAddress.value
    closeMapModal()
  }
}

// Form methods
const selectMethod = (m) => {
  method.value = m
  if (m === 'map') {
    nextTick(() => {
      initMap()
    })
  }
}

const refineAddress = () => {
  method.value = 'manual'
  if (selectedAddress.value) {
    address.value.fullAddress = selectedAddress.value
  }
}

const selectSavedAddress = (addr) => {
  selectedSavedAddress.value = addr
  address.value = { ...addr }
  
  if (method.value === 'map' && addr.coordinates && mapInstance.value && marker.value) {
    const { lat, lng } = addr.coordinates
    mapInstance.value.setView([lat, lng], 16)
    marker.value.setLatLng([lat, lng])
    updateCoordinates(lat, lng)
    mapAddress.value.title = addr.title
    selectedAddress.value = addr.fullAddress
  }
}

// Validation
const validateAddress = (addressData) => {
  const errors = []
  
  if (!addressData.title?.trim()) {
    errors.push('عنوان آدرس الزامی است')
  }
  
  if (addressData.phone) {
    const phoneRegex = /^09[0-9]{9}$/
    if (!phoneRegex.test(addressData.phone)) {
      errors.push('شماره موبایل معتبر نیست')
    }
  }
  
  if (addressData.postalCode && addressData.postalCode.length !== 10) {
    errors.push('کد پستی باید ۱۰ رقم باشد')
  }
  
  return errors
}

// Save manual address
const saveAddress = async () => {
  const errors = validateAddress(address.value)
  if (errors.length > 0) {
    alert(errors.join('\n'))
    return
  }
  
  isSubmitting.value = true
  
  try {
    await new Promise(resolve => setTimeout(resolve, 1000))
    
    const newAddress = {
      id: Date.now(),
      ...address.value,
      coordinates: modalCoordinates.value || null
    }
    
    savedAddresses.value.unshift(newAddress)
    saveToLocalStorage()
    
    address.value = {
      title: '',
      firstName: '',
      lastName: '',
      phone: '',
      fullAddress: '',
      postalCode: '',
      isDefault: false
    }
    
    modalCoordinates.value = null
    modalSelectedAddress.value = ''
    
    alert('آدرس با موفقیت ذخیره شد')
    router.push('/checkout')
    
  } catch (error) {
    console.error('Error saving address:', error)
    alert('خطا در ذخیره آدرس')
  } finally {
    isSubmitting.value = false
  }
}

// Save map address
const saveMapAddress = async () => {
  if (!selectedAddress.value || !mapAddress.value.title) {
    alert('لطفاً آدرس را انتخاب کنید و عنوان را وارد نمایید')
    return
  }
  
  isSubmitting.value = true
  
  try {
    await new Promise(resolve => setTimeout(resolve, 1000))
    
    const newAddress = {
      id: Date.now(),
      title: mapAddress.value.title,
      firstName: address.value.firstName || 'کاربر',
      lastName: address.value.lastName || 'مهمان',
      phone: address.value.phone || '09123456789',
      fullAddress: selectedAddress.value,
      postalCode: address.value.postalCode || '1234567890',
      isDefault: address.value.isDefault || false,
      coordinates: coordinates.value,
      extraInfo: mapAddress.value.extraInfo
    }
    
    savedAddresses.value.unshift(newAddress)
    saveToLocalStorage()
    
    // Reset
    mapAddress.value = {
      title: '',
      extraInfo: '',
      coordinates: { lat: null, lng: null }
    }
    selectedAddress.value = ''
    coordinates.value = null
    
    alert('آدرس از نقشه با موفقیت ذخیره شد')
    router.push('/checkout')
    
  } catch (error) {
    console.error('Error saving map address:', error)
    alert('خطا در ذخیره آدرس')
  } finally {
    isSubmitting.value = false
  }
}

// Lifecycle
onMounted(() => {
  loadSavedAddresses()
  
  // Load Leaflet CSS
  const link = document.createElement('link')
  link.rel = 'stylesheet'
  link.href = 'https://unpkg.com/leaflet@1.9.4/dist/leaflet.css'
  document.head.appendChild(link)
  
  // Load Leaflet JS
  const script = document.createElement('script')
  script.src = 'https://unpkg.com/leaflet@1.9.4/dist/leaflet.js'
  script.onload = () => {
    if (method.value === 'map') {
      initMap()
    }
  }
  document.head.appendChild(script)
})

onUnmounted(() => {
  if (mapInstance.value) {
    mapInstance.value.remove()
  }
  if (modalMapInstance.value) {
    modalMapInstance.value.remove()
  }
})
</script>

<style scoped>
.line-clamp-2 {
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

/* Map container styling */
#map, #modalMap {
  z-index: 1;
}

/* Leaflet custom styling */
:deep(.leaflet-control-attribution) {
  font-size: 10px;
}

:deep(.leaflet-popup-content) {
  font-family: system-ui, -apple-system, sans-serif;
}

/* Animation for saving button */
.animate-spin {
  animation: spin 1s linear infinite;
}

@keyframes spin {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}

/* Custom scrollbar */
::-webkit-scrollbar {
  width: 6px;
}

::-webkit-scrollbar-track {
  background: #f1f1f1;
  border-radius: 3px;
}

::-webkit-scrollbar-thumb {
  background: #888;
  border-radius: 3px;
}

::-webkit-scrollbar-thumb:hover {
  background: #555;
}
</style>