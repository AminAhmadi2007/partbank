<template>
  <div class="min-h-screen bg-gray-50">
    <!-- Header -->
    <div class="bg-white shadow-sm border-b border-gray-200">
      <div class="container mx-auto px-4 py-6">
        <div class="flex flex-col md:flex-row md:items-center justify-between gap-6">
          <div>
            <h1 class="text-2xl md:text-3xl font-bold text-gray-900 mb-2">قطعات لوازم خانگی</h1>
            <p class="text-gray-600">دسته‌بندی تخصصی انواع قطعات اورجینال</p>
          </div>
          
          <!-- Search Box -->
          <div class="relative w-full md:w-96">
            <input type="text" 
                   v-model="searchQuery"
                   placeholder="جستجوی قطعه، مدل یا برند..." 
                   class="w-full pr-12 pl-4 py-3 border border-gray-300 rounded-xl focus:ring-2 focus:ring-blue-500 focus:border-blue-500 outline-none transition text-sm bg-gray-50">
            <svg class="absolute right-4 top-1/2 -translate-y-1/2 w-5 h-5 text-gray-400" 
                 fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" 
                    d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" />
            </svg>
          </div>
        </div>
      </div>
    </div>

    <main class="container mx-auto px-4 py-8">
      <div class="flex flex-col lg:flex-row gap-8">
        <!-- Sidebar Filters -->
        <aside class="lg:w-80 flex-shrink-0">
          <!-- Categories Card -->
          <div class="bg-white rounded-xl shadow-sm border border-gray-200 p-5 mb-6">
            <h3 class="font-bold text-gray-900 mb-4 text-lg flex items-center gap-2">
              <span class="text-blue-600">📁</span>
              دسته‌بندی‌ها
            </h3>
            <div class="space-y-1">
              <button v-for="category in categories" 
                      :key="category.id"
                      @click="selectCategory(category.id)"
                      :class="[
                        'w-full text-right px-4 py-3 rounded-lg transition-all text-sm flex items-center justify-between group',
                        selectedCategory === category.id 
                          ? 'bg-blue-50 text-blue-700 border-r-4 border-blue-600' 
                          : 'text-gray-700 hover:bg-gray-50'
                      ]">
                <div class="flex items-center gap-3">
                  <div class="w-10 h-10 rounded-lg overflow-hidden bg-gray-100 flex items-center justify-center flex-shrink-0">
                    <img :src="category.image" 
                         :alt="category.name"
                         class="w-full h-full object-cover group-hover:scale-110 transition-transform duration-300">
                  </div>
                  <div class="text-right">
                    <span class="font-medium block">{{ category.name }}</span>
                  </div>
                </div>
                <span class="text-gray-400 text-xs bg-gray-100 px-2 py-1 rounded">
                  {{ category.count }}
                </span>
              </button>
            </div>
          </div>

          <!-- Price Filter Card -->
          <div class="bg-white rounded-xl shadow-sm border border-gray-200 p-5 mb-6">
            <h3 class="font-bold text-gray-900 mb-4 text-lg flex items-center gap-2">
              <span class="text-blue-600">💰</span>
              محدوده قیمت
            </h3>
            <div class="space-y-4">
              <div>
                <label class="block text-gray-600 text-sm mb-2">از</label>
                <div class="relative">
                  <input type="number" 
                         v-model.number="priceRange.min"
                         class="w-full px-4 py-3 border border-gray-300 rounded-lg text-left text-sm bg-gray-50 focus:ring-2 focus:ring-blue-500 focus:border-blue-500 outline-none">
                  <span class="absolute left-3 top-1/2 -translate-y-1/2 text-gray-400 text-sm">تومان</span>
                </div>
              </div>
              <div>
                <label class="block text-gray-600 text-sm mb-2">تا</label>
                <div class="relative">
                  <input type="number" 
                         v-model.number="priceRange.max"
                         class="w-full px-4 py-3 border border-gray-300 rounded-lg text-left text-sm bg-gray-50 focus:ring-2 focus:ring-blue-500 focus:border-blue-500 outline-none">
                  <span class="absolute left-3 top-1/2 -translate-y-1/2 text-gray-400 text-sm">تومان</span>
                </div>
              </div>
              <button @click="applyPriceFilter"
                      class="w-full py-3 bg-blue-600 hover:bg-blue-700 text-white rounded-lg text-sm font-medium transition flex items-center justify-center gap-2">
                <span>اعمال فیلتر</span>
                <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
                </svg>
              </button>
            </div>
          </div>

          <!-- Brands Filter Card -->
          <div class="bg-white rounded-xl shadow-sm border border-gray-200 p-5">
            <h3 class="font-bold text-gray-900 mb-4 text-lg flex items-center gap-2">
              <span class="text-blue-600">🏷️</span>
              برندها
            </h3>
            <div class="space-y-3">
              <label v-for="brand in brands" 
                     :key="brand.id"
                     class="flex items-center gap-3 cursor-pointer hover:bg-gray-50 p-2 rounded-lg transition">
                <input type="checkbox" 
                       v-model="selectedBrands"
                       :value="brand.id"
                       class="w-4 h-4 text-blue-600 rounded border-gray-300 focus:ring-blue-500">
                <div class="flex items-center gap-3 flex-1">
                  <div class="w-8 h-8 rounded-lg overflow-hidden bg-gray-100 flex items-center justify-center">
                    <img :src="getBrandImage(brand.name)" 
                         :alt="brand.name"
                         class="w-full h-full object-cover">
                  </div>
                  <span class="text-gray-700 text-sm">{{ brand.name }}</span>
                </div>
                <span class="text-gray-400 text-xs bg-gray-100 px-2 py-1 rounded">{{ brand.count }}</span>
              </label>
            </div>
          </div>
        </aside>

        <!-- Main Content -->
        <div class="flex-1">
          <!-- Featured Categories Banner -->
          <div class="mb-8">
            <div class="grid grid-cols-2 md:grid-cols-4 gap-4">
              <div v-for="category in featuredCategories" 
                   :key="category.id"
                   @click="selectCategory(category.id)"
                   class="bg-white rounded-xl shadow-sm border border-gray-200 overflow-hidden cursor-pointer group hover:shadow-md transition-all">
                <div class="relative h-32 overflow-hidden">
                  <img :src="category.image" 
                       :alt="category.name"
                       class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-300">
                  <div class="absolute inset-0 bg-gradient-to-t from-black/50 to-transparent"></div>
                  <div class="absolute bottom-3 right-3 text-white">
                    <h3 class="font-bold text-lg">{{ category.name }}</h3>
                    <p class="text-sm opacity-90">{{ category.count }} محصول</p>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <!-- Filters Bar -->
          <div class="bg-white rounded-xl shadow-sm border border-gray-200 p-5 mb-6">
            <div class="flex flex-wrap items-center justify-between gap-4">
              <div class="flex items-center gap-4">
                <!-- Sort Dropdown -->
                <div class="flex items-center gap-2">
                  <span class="text-gray-600 text-sm">مرتب‌سازی:</span>
                  <div class="relative">
                    <select v-model="sortBy" 
                            class="appearance-none border border-gray-300 rounded-lg px-4 py-2.5 text-sm focus:ring-2 focus:ring-blue-500 focus:border-blue-500 outline-none pr-10 bg-gray-50">
                      <option value="newest">جدیدترین</option>
                      <option value="cheapest">ارزان‌ترین</option>
                      <option value="expensive">گران‌ترین</option>
                      <option value="popular">پرفروش‌ترین</option>
                    </select>
                    <svg class="absolute left-3 top-1/2 -translate-y-1/2 w-4 h-4 text-gray-400 pointer-events-none"
                         fill="none" stroke="currentColor" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
                    </svg>
                  </div>
                </div>

                <!-- View Toggle -->
                <div class="flex items-center border border-gray-300 rounded-lg overflow-hidden">
                  <button @click="viewMode = 'grid'"
                          :class="[
                            'px-4 py-2 transition',
                            viewMode === 'grid' ? 'bg-blue-600 text-white' : 'bg-gray-50 text-gray-600 hover:bg-gray-100'
                          ]">
                    <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2H6a2 2 0 01-2-2V6zM14 6a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2h-2a2 2 0 01-2-2V6zM4 16a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2H6a2 2 0 01-2-2v-2zM14 16a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2h-2a2 2 0 01-2-2v-2z" />
                    </svg>
                  </button>
                  <button @click="viewMode = 'list'"
                          :class="[
                            'px-4 py-2 transition',
                            viewMode === 'list' ? 'bg-blue-600 text-white' : 'bg-gray-50 text-gray-600 hover:bg-gray-100'
                          ]">
                    <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
                    </svg>
                  </button>
                </div>
              </div>

              <!-- Results Count -->
              <div class="text-sm text-gray-600">
                <span class="font-medium text-blue-600">{{ filteredProducts.length }}</span>
                محصول از 
                <span class="font-medium">{{ totalProducts }}</span>
              </div>
            </div>

            <!-- Active Filters -->
            <div v-if="activeFilters.length > 0" class="mt-4 pt-4 border-t border-gray-100">
              <div class="flex flex-wrap items-center gap-2">
                <span class="text-gray-600 text-sm">فیلترهای فعال:</span>
                <span v-for="filter in activeFilters" 
                      :key="filter"
                      class="inline-flex items-center gap-2 bg-blue-50 text-blue-700 px-3 py-1.5 rounded-full text-xs">
                  {{ filter }}
                  <button @click="removeFilter(filter)" 
                          class="text-blue-400 hover:text-blue-600 text-sm">
                    &times;
                  </button>
                </span>
                <button @click="clearFilters"
                        class="text-red-600 hover:text-red-700 text-xs font-medium">
                  حذف همه
                </button>
              </div>
            </div>
          </div>

          <!-- Products Grid/List -->
          <div v-if="filteredProducts.length > 0">
            <!-- Grid View -->
            <div v-if="viewMode === 'grid'" class="grid grid-cols-1 md:grid-cols-2 xl:grid-cols-3 gap-6">
              <div v-for="product in paginatedProducts" 
                   :key="product.id"
                   @click="$router.push(`/product/${product.id}`)"
                   class="bg-white rounded-xl shadow-sm border border-gray-200 hover:shadow-lg hover:border-blue-300 transition-all duration-300 cursor-pointer overflow-hidden group">
                
                <!-- Product Image -->
                <div class="relative overflow-hidden bg-gray-100 h-52">
                  <img :src="product.image" 
                       :alt="product.name"
                       class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-300">
                  
                  <!-- Badges -->
                  <div class="absolute top-3 right-3 flex flex-col gap-2">
                    <span v-if="product.isNew" 
                          class="bg-green-500 text-white px-3 py-1 rounded-full text-xs font-bold shadow-sm">
                      جدید
                    </span>
                    <span v-if="product.discount" 
                          class="bg-red-500 text-white px-3 py-1 rounded-full text-xs font-bold shadow-sm">
                      {{ product.discount }}% تخفیف
                    </span>
                  </div>
                  
                  <!-- Category Badge -->
                  <div class="absolute bottom-3 right-3">
                    <span class="text-xs bg-black/60 text-white px-2 py-1 rounded">
                      {{ product.category }}
                    </span>
                  </div>
                  
                  <!-- Quick Actions -->
                  <div class="absolute top-3 left-3 flex flex-col gap-2 opacity-0 group-hover:opacity-100 transition-opacity">
                    <button @click.stop="toggleWishlist(product.id)"
                            class="w-10 h-10 bg-white/90 hover:bg-white rounded-full flex items-center justify-center transition shadow-sm">
                      <svg :class="[
                            'w-5 h-5',
                            isInWishlist(product.id) ? 'text-red-500 fill-red-500' : 'text-gray-400'
                          ]" 
                           fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" 
                              d="M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.682a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z" />
                      </svg>
                    </button>
                    <button @click.stop="showQuickView(product)"
                            class="w-10 h-10 bg-white/90 hover:bg-white rounded-full flex items-center justify-center transition shadow-sm">
                      <svg class="w-5 h-5 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z" />
                      </svg>
                    </button>
                  </div>
                </div>

                <!-- Product Info -->
                <div class="p-5">
                  <!-- Brand -->
                  <div class="flex items-center gap-2 mb-3">
                    <div class="w-6 h-6 rounded overflow-hidden bg-gray-100 flex items-center justify-center">
                      <span class="text-xs font-bold text-gray-600">{{ product.brand.charAt(0) }}</span>
                    </div>
                    <span class="text-xs bg-gray-100 text-gray-600 px-2 py-1 rounded">{{ product.brand }}</span>
                  </div>

                  <!-- Product Name -->
                  <h3 class="font-bold text-gray-900 mb-3 line-clamp-2 text-base leading-relaxed">
                    {{ product.name }}
                  </h3>

                  <!-- Rating -->
                  <div class="flex items-center gap-1 mb-4">
                    <div class="flex text-yellow-400">
                      <span v-for="i in 5" :key="i" 
                            :class="['text-sm', i <= Math.floor(product.rating) ? 'text-yellow-400' : 'text-gray-300']">
                        ★
                      </span>
                    </div>
                    <span class="text-xs text-gray-500 mr-1">({{ product.reviews }})</span>
                  </div>

                  <!-- Price & Actions -->
                  <div class="flex items-center justify-between">
                    <div>
                      <div class="flex items-center gap-2">
                        <span class="text-xl font-bold text-gray-900">
                          {{ formatPrice(product.price) }}
                        </span>
                        <span v-if="product.originalPrice" 
                              class="text-sm text-gray-400 line-through">
                          {{ formatPrice(product.originalPrice) }}
                        </span>
                      </div>
                      <div class="text-xs text-gray-500 mt-1">تومان</div>
                    </div>
                    
                    <button @click.stop="addToCart(product)"
                            :disabled="product.stock === 0"
                            :class="[
                              'px-4 py-2.5 rounded-lg text-sm font-medium transition flex items-center gap-2',
                              product.stock > 0
                                ? 'bg-blue-600 hover:bg-blue-700 text-white'
                                : 'bg-gray-200 text-gray-500 cursor-not-allowed'
                            ]">
                      <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" 
                              d="M12 6v6m0 0v6m0-6h6m-6 0H6" />
                      </svg>
                      {{ product.stock > 0 ? 'خرید' : 'ناموجود' }}
                    </button>
                  </div>
                </div>
              </div>
            </div>

            <!-- List View -->
            <div v-else class="space-y-4">
              <div v-for="product in paginatedProducts" 
                   :key="product.id"
                   @click="$router.push(`/product/${product.id}`)"
                   class="bg-white rounded-xl shadow-sm border border-gray-200 hover:shadow-lg hover:border-blue-300 transition-all duration-300 cursor-pointer overflow-hidden group">
                
                <div class="flex flex-col md:flex-row">
                  <!-- Product Image -->
                  <div class="md:w-64 flex-shrink-0">
                    <div class="relative h-48 md:h-full">
                      <img :src="product.image" 
                           :alt="product.name"
                           class="w-full h-full object-cover">
                      <div class="absolute top-3 right-3">
                        <span v-if="product.isNew" 
                              class="bg-green-500 text-white px-2 py-1 rounded text-xs">
                          جدید
                        </span>
                      </div>
                    </div>
                  </div>

                  <!-- Product Info -->
                  <div class="flex-1 p-6">
                    <div class="flex flex-col h-full">
                      <!-- Header -->
                      <div class="flex items-start justify-between mb-4">
                        <div class="flex-1">
                          <!-- Category & Brand -->
                          <div class="flex items-center gap-2 mb-2">
                            <div class="w-6 h-6 rounded overflow-hidden bg-gray-100 flex items-center justify-center">
                              <span class="text-xs font-bold text-gray-600">{{ product.brand.charAt(0) }}</span>
                            </div>
                            <span class="text-xs bg-blue-50 text-blue-600 px-2 py-1 rounded">{{ product.category }}</span>
                            <span class="text-xs bg-gray-100 text-gray-600 px-2 py-1 rounded">{{ product.brand }}</span>
                          </div>
                          
                          <!-- Product Name -->
                          <h3 class="font-bold text-gray-900 text-lg mb-2">
                            {{ product.name }}
                          </h3>
                          
                          <!-- Description -->
                          <p class="text-gray-600 text-sm mb-4 line-clamp-2">
                            {{ product.description }}
                          </p>
                        </div>
                        
                        <!-- Quick Actions -->
                        <div class="flex items-center gap-2">
                          <button @click.stop="toggleWishlist(product.id)"
                                  class="w-10 h-10 bg-gray-100 hover:bg-gray-200 rounded-full flex items-center justify-center transition">
                            <svg :class="[
                                  'w-5 h-5',
                                  isInWishlist(product.id) ? 'text-red-500 fill-red-500' : 'text-gray-400'
                                ]" 
                                 fill="none" stroke="currentColor" viewBox="0 0 24 24">
                              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" 
                                    d="M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.682a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z" />
                            </svg>
                          </button>
                          <button @click.stop="showQuickView(product)"
                                  class="w-10 h-10 bg-gray-100 hover:bg-gray-200 rounded-full flex items-center justify-center transition">
                            <svg class="w-5 h-5 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
                              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z" />
                            </svg>
                          </button>
                        </div>
                      </div>

                      <!-- Footer -->
                      <div class="flex items-center justify-between mt-auto pt-4 border-t border-gray-100">
                        <div class="flex items-center gap-6">
                          <!-- Rating -->
                          <div class="flex items-center gap-2">
                            <div class="flex text-yellow-400">
                              <span v-for="i in 5" :key="i" 
                                    :class="['text-sm', i <= Math.floor(product.rating) ? 'text-yellow-400' : 'text-gray-300']">
                                ★
                              </span>
                            </div>
                            <span class="text-xs text-gray-500">({{ product.reviews }})</span>
                          </div>
                          
                          <!-- Stock -->
                          <span :class="[
                                'px-3 py-1 rounded-full text-xs font-medium',
                                product.stock > 0 
                                  ? 'bg-green-100 text-green-800' 
                                  : 'bg-red-100 text-red-800'
                              ]">
                            {{ product.stock > 0 ? `${product.stock} عدد در انبار` : 'ناموجود' }}
                          </span>
                        </div>
                        
                        <div class="flex items-center gap-4">
                          <!-- Price -->
                          <div class="text-right">
                            <div class="flex items-center gap-2">
                              <span class="text-xl font-bold text-gray-900">
                                {{ formatPrice(product.price) }}
                              </span>
                              <span v-if="product.originalPrice" 
                                    class="text-sm text-gray-400 line-through">
                                {{ formatPrice(product.originalPrice) }}
                              </span>
                            </div>
                            <div class="text-xs text-gray-500">تومان</div>
                          </div>
                          
                          <!-- Action Button -->
                          <button @click.stop="addToCart(product)"
                                  :disabled="product.stock === 0"
                                  :class="[
                                    'px-6 py-3 rounded-lg font-medium transition flex items-center gap-2',
                                    product.stock > 0
                                      ? 'bg-blue-600 hover:bg-blue-700 text-white'
                                      : 'bg-gray-200 text-gray-500 cursor-not-allowed'
                                  ]">
                            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" 
                                    d="M3 3h2l.4 2M7 13h10l4-8H5.4M7 13L5.4 5M7 13l-2.293 2.293c-.63.63-.184 1.707.707 1.707H17m0 0a2 2 0 100 4 2 2 0 000-4zm-8 2a2 2 0 11-4 0 2 2 0 014 0z" />
                            </svg>
                            {{ product.stock > 0 ? 'افزودن به سبد' : 'ناموجود' }}
                          </button>
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>

            <!-- Pagination -->
            <div class="mt-12 flex items-center justify-center">
              <div class="flex items-center gap-2">
                <button @click="prevPage"
                        :disabled="currentPage === 1"
                        :class="[
                          'w-10 h-10 rounded-lg flex items-center justify-center transition',
                          currentPage === 1
                            ? 'text-gray-400 cursor-not-allowed'
                            : 'text-gray-600 hover:bg-gray-100 border border-gray-300'
                        ]">
                  <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
                  </svg>
                </button>
                
                <div class="flex items-center gap-1">
                  <button v-for="page in visiblePages"
                          :key="page"
                          @click="currentPage = page"
                          :class="[
                            'w-10 h-10 rounded-lg flex items-center justify-center text-sm font-medium transition',
                            currentPage === page
                              ? 'bg-blue-600 text-white'
                              : 'text-gray-600 hover:bg-gray-100 border border-gray-300'
                          ]">
                    {{ page }}
                  </button>
                  
                  <span v-if="showEllipsis" class="px-2 text-gray-400">...</span>
                </div>
                
                <button @click="nextPage"
                        :disabled="currentPage === totalPages"
                        :class="[
                          'w-10 h-10 rounded-lg flex items-center justify-center transition',
                          currentPage === totalPages
                            ? 'text-gray-400 cursor-not-allowed'
                            : 'text-gray-600 hover:bg-gray-100 border border-gray-300'
                        ]">
                  <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
                  </svg>
                </button>
              </div>
            </div>
          </div>

          <!-- No Results -->
          <div v-else class="bg-white rounded-xl shadow-sm border border-gray-200 p-12 text-center">
            <div class="w-24 h-24 mx-auto mb-6 bg-gray-100 rounded-full flex items-center justify-center">
              <span class="text-4xl">🔍</span>
            </div>
            <h3 class="text-xl font-medium text-gray-900 mb-3">محصولی یافت نشد</h3>
            <p class="text-gray-600 mb-6 max-w-md mx-auto">
              متأسفانه هیچ محصولی مطابق با جستجوی شما یافت نشد. لطفاً فیلترها را تغییر دهید یا عبارت جستجوی خود را اصلاح کنید.
            </p>
            <button @click="clearFilters"
                    class="px-8 py-3 bg-blue-600 hover:bg-blue-700 text-white rounded-lg font-medium transition inline-flex items-center gap-2">
              <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
              </svg>
              حذف همه فیلترها
            </button>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()

// State
const searchQuery = ref('')
const selectedCategory = ref(null)
const priceRange = ref({ min: 0, max: 10000000 })
const selectedBrands = ref([])
const sortBy = ref('newest')
const viewMode = ref('grid')
const currentPage = ref(1)
const itemsPerPage = 12
const wishlist = ref([])

// Categories Data with Images
const categories = [
  { id: 1, image: "/cool.webp", name: 'یخچال و فریزر', icon: '❄️', count: 128 },
  { id: 2, image: "/machin-leb.jpg", name: 'ماشین لباسشویی', icon: '🧺', count: 96 },
  { id: 3, image: "/machin-zarf.jpg", name: 'ماشین ظرفشویی', icon: '🍽️', count: 75 },
  { id: 4, image: "/ojagh.jpg", name: 'اجاق گاز', icon: '🔥', count: 64 },
  { id: 5, image: "/hood.jpg", name: 'هود', icon: '💨', count: 42 },
  { id: 6, image: "/macro.jpg", name: 'مایکروویو', icon: '⚡', count: 38 },
  { id: 7, image: "/coffe.jpg", name: 'چای‌ساز و قهوه‌ساز', icon: '☕', count: 29 },
  { id: 8, image: "/cooler.png", name: 'کولر گازی', icon: '🌀', count: 56 }
]

// Featured Categories (first 4)
const featuredCategories = computed(() => categories.slice(0, 4))

// Brands Data
const brands = [
  { id: 1, name: 'ال‌جی', count: 45 },
  { id: 2, name: 'سامسونگ', count: 38 },
  { id: 3, name: 'بوش', count: 32 },
  { id: 4, name: 'دوو', count: 28 },
  { id: 5, name: 'اسنوا', count: 25 },
  { id: 6, name: 'هایسنس', count: 22 },
  { id: 7, name: 'جنرال', count: 20 },
  { id: 8, name: 'پارس خزر', count: 18 }
]

// Helper function to get category image by name
const getCategoryImage = (categoryName) => {
  const category = categories.find(c => c.name === categoryName)
  return category ? category.image : '/cool.webp'
}

// Helper function to get brand image (using first letter for now)
const getBrandImage = (brandName) => {
  // In real app, you would have brand images
  // For now, we'll use the category images as placeholders
  const imageMap = {
    'ال‌جی': '/cool.webp',
    'سامسونگ': '/machin-leb.jpg',
    'بوش': '/machin-zarf.jpg',
    'دوو': '/ojagh.jpg',
    'اسنوا': '/hood.jpg',
    'هایسنس': '/macro.jpg',
    'جنرال': '/coffe.jpg',
    'پارس خزر': '/cooler.png'
  }
  return imageMap[brandName] || '/cool.webp'
}

// Mock Products Data - Using only the 8 available images
const products = ref(Array.from({ length: 48 }, (_, i) => {
  const category = categories[i % categories.length]
  const brand = brands[i % brands.length]
  
  // Use the category image for all products in that category
  const productImage = category.image
  
  return {
    id: i + 1,
    name: `قطعه ${i + 1} - ${category.name} ${brand.name}`,
    category: category.name,
    brand: brand.name,
    image: productImage,
    price: Math.floor(Math.random() * 1000000) + 500000,
    originalPrice: Math.random() > 0.5 ? Math.floor(Math.random() * 1200000) + 600000 : null,
    rating: parseFloat((Math.random() * 2 + 3).toFixed(1)), // 3-5 stars
    reviews: Math.floor(Math.random() * 100),
    stock: Math.random() > 0.2 ? Math.floor(Math.random() * 50) + 5 : 0,
    discount: i % 4 === 0 ? 15 : i % 4 === 1 ? 20 : 0,
    isNew: i % 3 === 0,
    description: `قطعه اورجینال ${brand.name} برای ${category.name} با گارانتی معتبر ۱۸ ماهه. کیفیت بالا و عملکرد عالی.`
  }
}))

// Computed Properties
const filteredProducts = computed(() => {
  let filtered = [...products.value]
  
  // Search filter
  if (searchQuery.value) {
    const query = searchQuery.value.toLowerCase()
    filtered = filtered.filter(p => 
      p.name.toLowerCase().includes(query) ||
      p.category.toLowerCase().includes(query) ||
      p.brand.toLowerCase().includes(query) ||
      p.description.toLowerCase().includes(query)
    )
  }
  
  // Category filter
  if (selectedCategory.value) {
    const categoryName = categories.find(c => c.id === selectedCategory.value)?.name
    filtered = filtered.filter(p => p.category === categoryName)
  }
  
  // Brand filter
  if (selectedBrands.value.length > 0) {
    const brandNames = selectedBrands.value.map(id => 
      brands.find(b => b.id === id)?.name
    ).filter(Boolean)
    filtered = filtered.filter(p => brandNames.includes(p.brand))
  }
  
  // Price filter
  filtered = filtered.filter(p => 
    p.price >= priceRange.value.min && 
    p.price <= priceRange.value.max
  )
  
  // Sorting
  switch (sortBy.value) {
    case 'cheapest':
      filtered.sort((a, b) => a.price - b.price)
      break
    case 'expensive':
      filtered.sort((a, b) => b.price - a.price)
      break
    case 'popular':
      filtered.sort((a, b) => b.reviews - a.reviews)
      break
    default: // newest
      filtered.sort((a, b) => b.id - a.id)
  }
  
  return filtered
})

const totalProducts = computed(() => products.value.length)
const totalPages = computed(() => Math.ceil(filteredProducts.value.length / itemsPerPage))
const paginatedProducts = computed(() => {
  const start = (currentPage.value - 1) * itemsPerPage
  const end = start + itemsPerPage
  return filteredProducts.value.slice(start, end)
})

const activeFilters = computed(() => {
  const filters = []
  if (selectedCategory.value) {
    const category = categories.find(c => c.id === selectedCategory.value)
    if (category) filters.push(category.name)
  }
  if (selectedBrands.value.length > 0) {
    filters.push(`${selectedBrands.value.length} برند`)
  }
  if (priceRange.value.min > 0 || priceRange.value.max < 10000000) {
    filters.push('فیلتر قیمت')
  }
  return filters
})

const visiblePages = computed(() => {
  const pages = []
  const maxVisible = 5
  
  if (totalPages.value <= maxVisible) {
    for (let i = 1; i <= totalPages.value; i++) {
      pages.push(i)
    }
  } else {
    let start = Math.max(1, currentPage.value - 2)
    let end = Math.min(totalPages.value, start + maxVisible - 1)
    
    if (end - start + 1 < maxVisible) {
      start = Math.max(1, end - maxVisible + 1)
    }
    
    for (let i = start; i <= end; i++) {
      pages.push(i)
    }
  }
  
  return pages
})

const showEllipsis = computed(() => {
  return totalPages.value > visiblePages.value.length
})

// Methods
const formatPrice = (price) => {
  return new Intl.NumberFormat('fa-IR').format(price)
}

const selectCategory = (categoryId) => {
  selectedCategory.value = selectedCategory.value === categoryId ? null : categoryId
  currentPage.value = 1
}

const applyPriceFilter = () => {
  currentPage.value = 1
}

const clearFilters = () => {
  searchQuery.value = ''
  selectedCategory.value = null
  priceRange.value = { min: 0, max: 10000000 }
  selectedBrands.value = []
  sortBy.value = 'newest'
  currentPage.value = 1
}

const removeFilter = (filterName) => {
  if (filterName.includes('برند')) {
    selectedBrands.value = []
  } else if (filterName === 'فیلتر قیمت') {
    priceRange.value = { min: 0, max: 10000000 }
  } else {
    selectedCategory.value = null
  }
  currentPage.value = 1
}

const isInWishlist = (productId) => {
  return wishlist.value.includes(productId)
}

const toggleWishlist = (productId) => {
  if (isInWishlist(productId)) {
    wishlist.value = wishlist.value.filter(id => id !== productId)
  } else {
    wishlist.value.push(productId)
  }
  localStorage.setItem('wishlist', JSON.stringify(wishlist.value))
}

const addToCart = (product) => {
  if (product.stock > 0) {
    console.log('Added to cart:', product.name)
    alert(`محصول "${product.name}" به سبد خرید اضافه شد`)
  }
}

const showQuickView = (product) => {
  console.log('Quick view:', product.name)
}

const prevPage = () => {
  if (currentPage.value > 1) {
    currentPage.value--
  }
}

const nextPage = () => {
  if (currentPage.value < totalPages.value) {
    currentPage.value++
  }
}

// Initialize
onMounted(() => {
  const saved = localStorage.getItem('wishlist')
  if (saved) wishlist.value = JSON.parse(saved)
})
</script>

<style scoped>
.line-clamp-2 {
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.transition-all {
  transition-property: all;
  transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
  transition-duration: 300ms;
}

.transition-transform {
  transition-property: transform;
}

.duration-300 {
  transition-duration: 300ms;
}

.group:hover .group-hover\:scale-105 {
  transform: scale(1.05);
}

.opacity-0 {
  opacity: 0;
}

.group:hover .group-hover\:opacity-100 {
  opacity: 1;
}

/* Image hover effects */
img {
  transition: transform 0.3s ease-in-out;
}

/* Custom scrollbar */
::-webkit-scrollbar {
  width: 6px;
  height: 6px;
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

/* Brand icon styling */
.w-6.h-6.rounded {
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  font-weight: bold;
}
</style>