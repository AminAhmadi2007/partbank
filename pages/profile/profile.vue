<template>
  <div class="min-h-screen bg-gradient-to-br from-gray-50 to-blue-50/30 py-6 md:py-10">
    <div class="container mx-auto px-4 max-w-7xl">
      <!-- Header with Breadcrumb -->
      <div class="mb-8">
        <nav class="flex items-center gap-2 text-sm text-gray-500 mb-4">
          <router-link to="/" class="hover:text-blue-600 transition">خانه</router-link>
          <span class="text-gray-400">/</span>
          <span class="text-gray-900 font-medium">حساب کاربری</span>
        </nav>
        
        <div class="flex flex-col md:flex-row md:items-center justify-between gap-4">
          <div>
            <h1 class="text-3xl md:text-4xl font-bold text-gray-900 mb-2 bg-gradient-to-l from-blue-600 to-blue-800 bg-clip-text text-transparent">
              حساب کاربری
            </h1>
            <p class="text-gray-600 max-w-2xl">
              مدیریت اطلاعات شخصی، سفارش‌ها و آدرس‌های شما
            </p>
          </div>
          
          <div class="flex items-center gap-2">
            <div class="relative">
              <div class="w-10 h-10 rounded-full bg-gradient-to-br from-blue-500 to-blue-700 flex items-center justify-center">
                <span class="text-white font-bold">{{ user?.initials || '?' }}</span>
              </div>
              <span class="absolute bottom-0 right-0 w-3 h-3 bg-green-500 border-2 border-white rounded-full"></span>
            </div>
            <div class="text-right">
              <div class="font-bold text-gray-900">{{ user?.fullName || 'کاربر' }}</div>
              <div class="text-xs text-gray-500 flex items-center gap-1">
                <span class="text-yellow-500">★</span>
                سطح {{ user?.membershipLevel || 'عادی' }}
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Main Content -->
      <div class="grid grid-cols-1 lg:grid-cols-4 gap-6">
        <!-- Sidebar Navigation -->
        <div class="lg:col-span-1">
          <div class="sticky top-6 space-y-6">
            <!-- Profile Card -->
            <div class="bg-gradient-to-br from-white to-blue-50 rounded-2xl shadow-lg border border-blue-100 overflow-hidden">
              <div class="p-6">
                <div class="flex flex-col items-center text-center mb-6">
                  <div class="relative mb-4">
                    <div class="w-24 h-24 rounded-full bg-gradient-to-br from-blue-100 to-blue-200 border-4 border-white shadow-lg flex items-center justify-center">
                      <span class="text-4xl text-blue-700 font-bold">{{ user?.initials || '?' }}</span>
                    </div>
                    <button @click="router.push('/profile/edit')" 
                            class="absolute bottom-2 left-2 w-10 h-10 bg-white rounded-full shadow-md flex items-center justify-center hover:bg-blue-50 transition group">
                      <svg class="w-5 h-5 text-blue-600 group-hover:scale-110 transition" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z" />
                      </svg>
                    </button>
                  </div>
                  <h3 class="text-xl font-bold text-gray-900 mb-1">{{ user?.fullName || 'کاربر' }}</h3>
                  <p class="text-gray-600 text-sm">{{ user?.email || 'ایمیل ثبت نشده' }}</p>
                  <div class="mt-2 px-3 py-1 bg-gradient-to-r from-yellow-50 to-amber-50 border border-yellow-200 rounded-full text-xs text-yellow-700">
                    عضویت از {{ user?.joinDate || 'تاریخ نامشخص' }}
                  </div>
                </div>
              </div>
            </div>

            <!-- Navigation Menu -->
            <div class="bg-white rounded-2xl shadow-lg border border-gray-200 overflow-hidden">
              <nav class="p-3 space-y-1">
                <button v-for="item in menuItems" 
                        :key="item.id"
                        @click="activeTab = item.id"
                        :class="[
                          'w-full text-right px-4 py-4 rounded-xl transition-all duration-300 flex items-center justify-between group',
                          activeTab === item.id
                            ? 'bg-gradient-to-l from-blue-600 to-blue-700 text-white shadow-md transform scale-[1.02]'
                            : 'text-gray-700 hover:bg-gray-50 hover:pr-6'
                        ]">
                  <div class="flex items-center gap-4">
                    <span :class="[
                      'text-xl transition-transform',
                      activeTab === item.id ? 'scale-110' : 'group-hover:scale-110'
                    ]">
                      {{ item.icon }}
                    </span>
                    <span class="font-medium">{{ item.title }}</span>
                  </div>
                  <div class="flex items-center gap-2">
                    <span v-if="item.badge" 
                          :class="[
                            'text-xs px-2.5 py-1 rounded-full font-medium',
                            activeTab === item.id
                              ? 'bg-white/20 text-white'
                              : 'bg-blue-100 text-blue-700'
                          ]">
                      {{ item.badge }}
                    </span>
                    <svg class="w-5 h-5 transition-transform" 
                         :class="{ 'rotate-180': activeTab === item.id }"
                         fill="none" stroke="currentColor" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
                    </svg>
                  </div>
                </button>
              </nav>

              <!-- Logout Button -->
              <div class="p-4 border-t border-gray-100">
                <button @click="logout"
                        class="w-full py-3 border border-red-100 bg-gradient-to-r from-white to-red-50 text-red-600 hover:from-red-50 hover:to-red-100 rounded-xl font-medium transition-all duration-300 flex items-center justify-center gap-3 group hover:shadow-sm">
                  <svg class="w-5 h-5 group-hover:rotate-12 transition-transform" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 16l4-4m0 0l-4-4m4 4H7m6 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h4a3 3 0 013 3v1" />
                  </svg>
                  <span>خروج از حساب</span>
                </button>
              </div>
            </div>
          </div>
        </div>

        <!-- Main Content Area -->
        <div class="lg:col-span-3 space-y-6">
          <!-- Overview Tab -->
          <transition name="fade" mode="out-in">
            <div v-if="activeTab === 'overview'" class="space-y-6">
              <!-- Stats Grid -->
              <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
                <div v-for="stat in stats" :key="stat.id"
                     @click="activeTab = stat.action"
                     class="bg-white rounded-2xl shadow-lg border border-gray-200 p-6 hover:shadow-xl hover:border-blue-300 transition-all duration-300 cursor-pointer group">
                  <div class="flex items-center justify-between mb-4">
                    <div :class="[
                      'w-14 h-14 rounded-xl flex items-center justify-center transition-transform group-hover:scale-110',
                      stat.colorClass
                    ]">
                      <span class="text-2xl">{{ stat.icon }}</span>
                    </div>
                    <div class="text-right">
                      <div class="text-3xl font-bold text-gray-900 mb-1">{{ stat.value }}</div>
                      <div class="text-sm text-gray-500">{{ stat.label }}</div>
                    </div>
                  </div>
                  <div class="flex items-center justify-between">
                    <span class="text-sm text-gray-600">{{ stat.description }}</span>
                    <svg class="w-5 h-5 text-gray-400 group-hover:text-blue-600 group-hover:translate-x-1 transition" 
                         fill="none" stroke="currentColor" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
                    </svg>
                  </div>
                </div>
              </div>

              <!-- Quick Actions -->
              <div class="bg-gradient-to-r from-white to-blue-50 rounded-2xl shadow-lg border border-blue-100 p-6">
                <h3 class="text-xl font-bold text-gray-900 mb-6 flex items-center gap-3">
                  <span class="w-2 h-2 bg-blue-600 rounded-full"></span>
                  اقدامات سریع
                </h3>
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4">
                  <button v-for="action in quickActions" 
                          :key="action.id"
                          @click="handleQuickAction(action)"
                          class="bg-white hover:bg-gradient-to-br hover:from-white hover:to-blue-50 border border-gray-200 rounded-xl p-4 text-center group hover:shadow-md hover:border-blue-300 transition-all">
                    <div :class="[
                      'w-12 h-12 mx-auto mb-3 rounded-lg flex items-center justify-center text-2xl transition-transform group-hover:scale-110',
                      action.colorClass
                    ]">
                      {{ action.icon }}
                    </div>
                    <div class="font-medium text-gray-900 mb-1">{{ action.title }}</div>
                    <div class="text-xs text-gray-500">{{ action.description }}</div>
                  </button>
                </div>
              </div>

              <!-- Recent Activity -->
              <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
                <!-- Recent Orders -->
                <div class="bg-white rounded-2xl shadow-lg border border-gray-200 overflow-hidden">
                  <div class="p-6 border-b border-gray-200 flex items-center justify-between">
                    <h3 class="text-lg font-bold text-gray-900 flex items-center gap-2">
                      <svg class="w-5 h-5 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2" />
                      </svg>
                      سفارش‌های اخیر
                    </h3>
                    <router-link to="/orders" class="text-blue-600 hover:text-blue-700 text-sm font-medium flex items-center gap-1">
                      مشاهده همه
                      <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
                      </svg>
                    </router-link>
                  </div>
                  <div class="p-6">
                    <div v-if="recentOrders?.length > 0" class="space-y-4">
                      <div v-for="order in recentOrders" :key="order.id"
                           class="flex items-center justify-between p-4 rounded-lg border border-gray-100 hover:border-blue-200 hover:bg-blue-50/30 transition group">
                        <div class="flex items-center gap-4">
                          <div :class="[
                            'w-12 h-12 rounded-lg flex items-center justify-center',
                            getStatusColor(order.status).bg
                          ]">
                            <span :class="getStatusColor(order.status).text">
                              📦
                            </span>
                          </div>
                          <div>
                            <div class="font-medium text-gray-900">{{ order.productName }}</div>
                            <div class="text-sm text-gray-500">{{ order.date }}</div>
                          </div>
                        </div>
                        <div class="text-left">
                          <div class="font-bold text-gray-900 mb-1">{{ formatPrice(order.price) }}</div>
                          <span class="text-xs px-2 py-1 rounded-full" :class="getStatusColor(order.status).badge">
                            {{ getStatusText(order.status) }}
                          </span>
                        </div>
                      </div>
                    </div>
                    <div v-else class="text-center py-8">
                      <div class="w-20 h-20 mx-auto mb-4 bg-gray-100 rounded-full flex items-center justify-center">
                        <span class="text-3xl">📦</span>
                      </div>
                      <p class="text-gray-600">هنوز سفارشی ثبت نکرده‌اید</p>
                    </div>
                  </div>
                </div>

                <!-- Account Summary -->
                <div class="bg-white rounded-2xl shadow-lg border border-gray-200 overflow-hidden">
                  <div class="p-6 border-b border-gray-200">
                    <h3 class="text-lg font-bold text-gray-900 flex items-center gap-2">
                      <svg class="w-5 h-5 text-purple-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z" />
                      </svg>
                      خلاصه حساب
                    </h3>
                  </div>
                  <div class="p-6">
                    <div class="space-y-4">
                      <div class="flex items-center justify-between p-3 rounded-lg bg-gray-50">
                        <span class="text-gray-600">نام و نام خانوادگی</span>
                        <span class="font-medium">{{ user?.fullName || 'ثبت نشده' }}</span>
                      </div>
                      <div class="flex items-center justify-between p-3 rounded-lg bg-gray-50">
                        <span class="text-gray-600">ایمیل</span>
                        <span class="font-medium direction-ltr text-left">{{ user?.email || 'ثبت نشده' }}</span>
                      </div>
                      <div class="flex items-center justify-between p-3 rounded-lg bg-gray-50">
                        <span class="text-gray-600">شماره تماس</span>
                        <span class="font-medium">{{ user?.phone || 'ثبت نشده' }}</span>
                      </div>
                      <div class="flex items-center justify-between p-3 rounded-lg bg-gray-50">
                        <span class="text-gray-600">سطح حساب</span>
                        <span class="font-medium text-blue-600">{{ user?.membershipLevel || 'عادی' }}</span>
                      </div>
                    </div>
                    <button @click="router.push('/profile/edit')"
                            class="w-full mt-6 py-3 bg-gradient-to-r from-blue-600 to-blue-700 hover:from-blue-700 hover:to-blue-800 text-white rounded-lg font-medium transition-all flex items-center justify-center gap-2 group">
                      <svg class="w-5 h-5 group-hover:rotate-12 transition-transform" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z" />
                      </svg>
                      ویرایش اطلاعات حساب
                    </button>
                  </div>
                </div>
              </div>
            </div>

            <!-- Orders Tab -->
            <div v-else-if="activeTab === 'orders'" class="bg-white rounded-2xl shadow-lg border border-gray-200">
              <div class="p-6 border-b border-gray-200">
                <h2 class="text-lg font-bold text-gray-900">همه سفارش‌ها</h2>
              </div>
              
              <div class="p-6">
                <!-- Order Filters -->
                <div class="flex flex-wrap items-center gap-4 mb-6">
                  <button v-for="filter in orderFilters" 
                          :key="filter.value"
                          @click="selectedOrderFilter = filter.value"
                          :class="[
                            'px-4 py-2 rounded-lg text-sm font-medium transition',
                            selectedOrderFilter === filter.value
                              ? 'bg-blue-600 text-white'
                              : 'bg-gray-100 text-gray-700 hover:bg-gray-200'
                          ]">
                    {{ filter.label }}
                  </button>
                </div>
                
                <!-- Orders Table -->
                <div class="overflow-x-auto">
                  <table class="w-full min-w-full">
                    <thead>
                      <tr class="border-b border-gray-200">
                        <th class="text-right py-3 px-4 text-sm font-medium text-gray-700">شماره سفارش</th>
                        <th class="text-right py-3 px-4 text-sm font-medium text-gray-700">تاریخ</th>
                        <th class="text-right py-3 px-4 text-sm font-medium text-gray-700">مبلغ</th>
                        <th class="text-right py-3 px-4 text-sm font-medium text-gray-700">وضعیت</th>
                        <th class="text-right py-3 px-4 text-sm font-medium text-gray-700">عملیات</th>
                      </tr>
                    </thead>
                    <tbody>
                      <tr v-if="filteredOrders && filteredOrders.length > 0">
                        <td colspan="5">
                          <div v-for="order in filteredOrders" :key="order.id" 
                               class="border-b border-gray-100 hover:bg-gray-50 py-4">
                            <div class="flex flex-col md:flex-row md:items-center justify-between gap-4 px-4">
                              <div class="flex-1">
                                <div class="font-medium text-gray-900">{{ order.orderNumber }}</div>
                                <div class="text-sm text-gray-500 mt-1">{{ order.date }}</div>
                              </div>
                              <div class="flex-1">
                                <div class="font-medium text-gray-900">{{ formatPrice(order.price) }}</div>
                              </div>
                              <div class="flex-1">
                                <span class="text-xs px-3 py-1 rounded-full" :class="getStatusColor(order.status).badge">
                                  {{ getStatusText(order.status) }}
                                </span>
                              </div>
                              <div class="flex-1">
                                <button @click="viewOrder(order.id)"
                                        class="text-blue-600 hover:text-blue-700 text-sm font-medium">
                                  مشاهده
                                </button>
                              </div>
                            </div>
                          </div>
                        </td>
                      </tr>
                      <tr v-else>
                        <td colspan="5" class="py-12 text-center">
                          <div class="w-20 h-20 mx-auto mb-4 bg-gray-100 rounded-full flex items-center justify-center">
                            <span class="text-3xl">📦</span>
                          </div>
                          <h3 class="text-lg font-medium text-gray-900 mb-2">سفارشی یافت نشد</h3>
                          <p class="text-gray-600">هیچ سفارشی با این فیلتر وجود ندارد</p>
                        </td>
                      </tr>
                    </tbody>
                  </table>
                </div>
              </div>
            </div>

            <!-- Wishlist Tab -->
            <div v-else-if="activeTab === 'wishlist'" class="bg-white rounded-2xl shadow-lg border border-gray-200">
              <div class="p-6 border-b border-gray-200">
                <h2 class="text-lg font-bold text-gray-900">لیست علاقه‌مندی‌ها</h2>
              </div>
              
              <div class="p-6">
                <div v-if="wishlistItems && wishlistItems.length > 0" class="grid grid-cols-1 md:grid-cols-2 gap-6">
                  <div v-for="item in wishlistItems" :key="item.id"
                       class="border border-gray-200 rounded-xl p-4 hover:border-blue-300 transition">
                    <div class="flex items-start gap-4">
                      <div class="w-20 h-20 bg-gray-100 rounded-lg overflow-hidden flex-shrink-0">
                        <img :src="item.image || '/placeholder.jpg'" :alt="item.name" class="w-full h-full object-cover">
                      </div>
                      
                      <div class="flex-1">
                        <h4 class="font-medium text-gray-900 mb-1">{{ item.name }}</h4>
                        <p class="text-sm text-gray-500 mb-2">{{ item.category }}</p>
                        
                        <div class="flex items-center justify-between">
                          <div class="text-lg font-bold text-gray-900">{{ formatPrice(item.price) }} تومان</div>
                          
                          <div class="flex items-center gap-2">
                            <button @click="removeFromWishlist(item.id)"
                                    class="text-red-600 hover:text-red-700">
                              <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16" />
                              </svg>
                            </button>
                            
                            <button @click="addToCart(item)"
                                    class="px-3 py-1.5 bg-blue-600 hover:bg-blue-700 text-white text-sm rounded-lg">
                              خرید
                            </button>
                          </div>
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
                
                <div v-else class="text-center py-12">
                  <div class="w-20 h-20 mx-auto mb-4 bg-gray-100 rounded-full flex items-center justify-center">
                    <span class="text-3xl">❤️</span>
                  </div>
                  <h3 class="text-lg font-medium text-gray-900 mb-2">لیست علاقه‌مندی‌ها خالی است</h3>
                  <p class="text-gray-600 mb-6">محصولات مورد علاقه خود را اینجا ذخیره کنید</p>
                  <router-link to="/category"
                               class="px-6 py-3 bg-blue-600 hover:bg-blue-700 text-white rounded-lg font-medium inline-flex items-center gap-2">
                    <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 3h2l.4 2M7 13h10l4-8H5.4M7 13L5.4 5M7 13l-2.293 2.293c-.63.63-.184 1.707.707 1.707H17m0 0a2 2 0 100 4 2 2 0 000-4zm-8 2a2 2 0 11-4 0 2 2 0 014 0z" />
                    </svg>
                    مشاهده محصولات
                  </router-link>
                </div>
              </div>
            </div>

            <!-- Addresses Tab -->
            <div v-else-if="activeTab === 'addresses'" class="bg-white rounded-2xl shadow-lg border border-gray-200">
              <div class="p-6 border-b border-gray-200 flex items-center justify-between">
                <h2 class="text-lg font-bold text-gray-900">آدرس‌های ذخیره شده</h2>
                <router-link to="/addAddress"
                             class="px-4 py-2 bg-blue-600 hover:bg-blue-700 text-white rounded-lg text-sm font-medium flex items-center gap-2">
                  <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6v6m0 0v6m0-6h6m-6 0H6" />
                  </svg>
                  افزودن آدرس جدید
                </router-link>
              </div>
              
              <div class="p-6">
                <div v-if="addresses && addresses.length > 0" class="grid grid-cols-1 md:grid-cols-2 gap-6">
                  <div v-for="addr in addresses" :key="addr.id"
                       class="border border-gray-200 rounded-xl p-4 hover:border-blue-300 transition">
                    <div class="flex items-start justify-between mb-3">
                      <h4 class="font-medium text-gray-900">{{ addr.title }}</h4>
                      <div class="flex items-center gap-2">
                        <span v-if="addr.isDefault" 
                              class="text-xs bg-blue-100 text-blue-700 px-2 py-1 rounded">
                          پیش‌فرض
                        </span>
                        <button @click="editAddress(addr)"
                                class="text-blue-600 hover:text-blue-700">
                          <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z" />
                          </svg>
                        </button>
                      </div>
                    </div>
                    
                    <p class="text-sm text-gray-600 mb-3">{{ addr.fullAddress }}</p>
                    
                    <div class="flex items-center gap-4 text-sm text-gray-500">
                      <span>{{ addr.firstName }} {{ addr.lastName }}</span>
                      <span>•</span>
                      <span>{{ addr.phone }}</span>
                    </div>
                    
                    <div class="flex gap-2 mt-4">
                      <button @click="setDefaultAddress(addr.id)"
                              :disabled="addr.isDefault"
                              :class="[
                                'px-3 py-1.5 text-xs rounded-lg transition',
                                addr.isDefault
                                  ? 'bg-gray-100 text-gray-500 cursor-not-allowed'
                                  : 'bg-gray-100 hover:bg-gray-200 text-gray-700'
                              ]">
                        تنظیم به عنوان پیش‌فرض
                      </button>
                      <button @click="deleteAddress(addr.id)"
                              class="px-3 py-1.5 text-xs bg-red-50 hover:bg-red-100 text-red-600 rounded-lg transition">
                        حذف
                      </button>
                    </div>
                  </div>
                </div>
                
                <div v-else class="text-center py-12">
                  <div class="w-20 h-20 mx-auto mb-4 bg-gray-100 rounded-full flex items-center justify-center">
                    <span class="text-3xl">🏠</span>
                  </div>
                  <h3 class="text-lg font-medium text-gray-900 mb-2">هیچ آدرسی ثبت نشده است</h3>
                  <p class="text-gray-600 mb-6">برای سفارش‌دهی راحت‌تر، آدرس خود را ذخیره کنید</p>
                  <router-link to="/addAddress"
                               class="px-6 py-3 bg-blue-600 hover:bg-blue-700 text-white rounded-lg font-medium inline-flex items-center gap-2">
                    افزودن اولین آدرس
                  </router-link>
                </div>
              </div>
            </div>
          </transition>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, reactive, onMounted } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()

// State
const activeTab = ref('overview')
const selectedOrderFilter = ref('all')
const loading = ref(false)

// User Data with safe defaults
const user = ref({
  fullName: '',
  email: '',
  phone: '',
  initials: '',
  joinDate: '',
  membershipLevel: 'عادی'
})

// Stats with safe defaults
const stats = ref([
  { id: 1, label: 'سفارش‌ها', value: 0, icon: '📦', colorClass: 'bg-blue-100 text-blue-600', description: 'تعداد سفارش‌های شما', action: 'orders' },
  { id: 2, label: 'علاقه‌مندی‌ها', value: 0, icon: '❤️', colorClass: 'bg-red-100 text-red-600', description: 'محصولات مورد علاقه', action: 'wishlist' },
  { id: 3, label: 'آدرس‌ها', value: 0, icon: '🏠', colorClass: 'bg-green-100 text-green-600', description: 'آدرس‌های ذخیره شده', action: 'addresses' }
])

// Quick Actions
const quickActions = ref([
  { id: 1, title: 'ویرایش پروفایل', icon: '👤', description: 'تغییر اطلاعات شخصی', action: 'editProfile', colorClass: 'bg-blue-100 text-blue-600' },
  { id: 2, title: 'افزودن آدرس', icon: '📍', description: 'افزودن آدرس جدید', action: 'addAddress', colorClass: 'bg-green-100 text-green-600' },
  { id: 3, title: 'سفارش جدید', icon: '🛒', description: 'ثبت سفارش جدید', action: 'newOrder', colorClass: 'bg-purple-100 text-purple-600' },
  { id: 4, title: 'تغییر رمز', icon: '🔒', description: 'تغییر رمز عبور', action: 'changePassword', colorClass: 'bg-yellow-100 text-yellow-600' }
])

// Menu Items
const menuItems = computed(() => [
  { id: 'overview', title: 'نمای کلی', icon: '📊' },
  { id: 'orders', title: 'سفارش‌ها', icon: '📦', badge: stats.value[0].value },
  { id: 'wishlist', title: 'علاقه‌مندی‌ها', icon: '❤️', badge: stats.value[1].value },
  { id: 'addresses', title: 'آدرس‌ها', icon: '🏠', badge: stats.value[2].value },
])

// Orders Data with safe defaults
const orders = ref([])

// Recent Orders (first 3)
const recentOrders = computed(() => {
  return orders.value?.slice(0, 3) || []
})

// Order Filters
const orderFilters = [
  { value: 'all', label: 'همه' },
  { value: 'pending', label: 'در انتظار' },
  { value: 'processing', label: 'در حال پردازش' },
  { value: 'delivered', label: 'تحویل شده' },
  { value: 'cancelled', label: 'لغو شده' }
]

// Filtered Orders
const filteredOrders = computed(() => {
  if (!orders.value) return []
  if (selectedOrderFilter.value === 'all') {
    return orders.value
  }
  return orders.value.filter(order => order.status === selectedOrderFilter.value)
})

// Wishlist Items with safe defaults
const wishlistItems = ref([])

// Addresses with safe defaults
const addresses = ref([])

// Settings
const settings = reactive({
  emailNotifications: true,
  smsNotifications: true,
  newsletter: true
})

// Methods
const formatPrice = (price) => {
  return new Intl.NumberFormat('fa-IR').format(price || 0)
}

const getStatusText = (status) => {
  const statusMap = {
    pending: 'در انتظار',
    processing: 'در حال پردازش',
    delivered: 'تحویل شده',
    cancelled: 'لغو شده'
  }
  return statusMap[status] || status
}

const getStatusColor = (status) => {
  const colors = {
    pending: { bg: 'bg-yellow-50', text: 'text-yellow-600', badge: 'bg-yellow-100 text-yellow-700' },
    processing: { bg: 'bg-blue-50', text: 'text-blue-600', badge: 'bg-blue-100 text-blue-700' },
    delivered: { bg: 'bg-green-50', text: 'text-green-600', badge: 'bg-green-100 text-green-700' },
    cancelled: { bg: 'bg-red-50', text: 'text-red-600', badge: 'bg-red-100 text-red-700' }
  }
  return colors[status] || { bg: 'bg-gray-50', text: 'text-gray-600', badge: 'bg-gray-100 text-gray-700' }
}

const handleQuickAction = (action) => {
  switch (action.action) {
    case 'editProfile':
      router.push('/profile/edit')
      break
    case 'addAddress':
      router.push('/addaddress')
      break
    case 'newOrder':
      router.push('/category')
      break
    case 'changePassword':
      router.push('/profile/edit')
      break
  }
}

const viewOrder = (orderId) => {
  router.push(`/order/${orderId}`)
}

const editAddress = (address) => {
  router.push(`/address/edit/${address.id}`)
}

const setDefaultAddress = (addressId) => {
  addresses.value.forEach(addr => {
    addr.isDefault = addr.id === addressId
  })
  localStorage.setItem('userAddresses', JSON.stringify(addresses.value))
}

const deleteAddress = (addressId) => {
  if (confirm('آیا از حذف این آدرس مطمئن هستید؟')) {
    addresses.value = addresses.value.filter(addr => addr.id !== addressId)
    stats.value[2].value = addresses.value.length
    localStorage.setItem('userAddresses', JSON.stringify(addresses.value))
  }
}

const removeFromWishlist = (itemId) => {
  if (confirm('آیا از حذف این محصول از علاقه‌مندی‌ها مطمئن هستید؟')) {
    wishlistItems.value = wishlistItems.value.filter(item => item.id !== itemId)
    stats.value[1].value = wishlistItems.value.length
    localStorage.setItem('userWishlist', JSON.stringify(wishlistItems.value))
  }
}

const addToCart = (product) => {
  console.log('Added to cart:', product.name)
  // Add to cart logic
}

const saveSettings = () => {
  localStorage.setItem('userSettings', JSON.stringify(settings))
  alert('تنظیمات با موفقیت ذخیره شد')
}

const logout = () => {
  if (confirm('آیا مطمئن هستید که می‌خواهید خارج شوید؟')) {
    localStorage.removeItem('authToken')
    localStorage.removeItem('user')
    router.push('/login')
  }
}

// Initialize with safe data loading
const initializeData = async () => {
  try {
    // Load user data with fallback
    const savedUser = localStorage.getItem('user')
    if (savedUser) {
      const parsedUser = JSON.parse(savedUser)
      user.value = {
        fullName: parsedUser.fullName || 'کاربر',
        email: parsedUser.email || '',
        phone: parsedUser.phone || '',
        initials: parsedUser.initials || '?',
        joinDate: parsedUser.joinDate || 'تاریخ نامشخص',
        membershipLevel: parsedUser.membershipLevel || 'عادی'
      }
    }

    // Load orders
    const savedOrders = localStorage.getItem('userOrders')
    orders.value = savedOrders ? JSON.parse(savedOrders) : [
      {
        id: 1,
        orderNumber: 'ORD-2023-001',
        date: '۱۴۰۲/۱۱/۲۰',
        productName: 'کمپرسور یخچال سامسونگ',
        price: 1850000,
        quantity: 1,
        status: 'delivered'
      }
    ]

    // Load wishlist
    const savedWishlist = localStorage.getItem('userWishlist')
    wishlistItems.value = savedWishlist ? JSON.parse(savedWishlist) : [
      {
        id: 1,
        name: 'کمپرسور یخچال سامسونگ',
        category: 'یخچال و فریزر',
        price: 1850000,
        image: '/cool.webp'
      }
    ]

    // Load addresses
    const savedAddresses = localStorage.getItem('userAddresses')
    addresses.value = savedAddresses ? JSON.parse(savedAddresses) : [
      {
        id: 1,
        title: 'منزل',
        firstName: 'کاربر',
        lastName: 'کاربری',
        phone: '09123456789',
        fullAddress: 'تهران، منطقه ۲، خیابان شهید مطهری، کوچه گلستان، پلاک ۲۵',
        isDefault: true
      }
    ]

    // Load settings
    const savedSettings = localStorage.getItem('userSettings')
    if (savedSettings) {
      Object.assign(settings, JSON.parse(savedSettings))
    }

    // Update stats
    stats.value[0].value = orders.value.length
    stats.value[1].value = wishlistItems.value.length
    stats.value[2].value = addresses.value.length

  } catch (error) {
    console.error('Error loading user data:', error)
    // Set fallback data
    user.value = {
      fullName: 'کاربر مهمان',
      email: 'guest@example.com',
      phone: '',
      initials: 'گ',
      joinDate: 'امروز',
      membershipLevel: 'عادی'
    }
    
    // Set default data for other sections
    orders.value = []
    wishlistItems.value = []
    addresses.value = []
  }
}

// Initialize
onMounted(() => {
  initializeData()
})
</script>

<style scoped>
/* Smooth transitions */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease, transform 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  transform: translateY(10px);
}

.direction-ltr {
  direction: ltr;
}

/* Custom scrollbar */
::-webkit-scrollbar {
  width: 8px;
}

::-webkit-scrollbar-track {
  background: #f1f1f1;
  border-radius: 4px;
}

::-webkit-scrollbar-thumb {
  background: #888;
  border-radius: 4px;
}

::-webkit-scrollbar-thumb:hover {
  background: #555;
}

/* Ensure table responsiveness */
@media (max-width: 768px) {
  .min-w-full {
    min-width: 100%;
  }
}
</style>