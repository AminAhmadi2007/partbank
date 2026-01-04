<template>
  <div class="min-h-screen bg-gray-50">
    <!-- Breadcrumb -->
    <div class="bg-white border-b border-gray-200">
      <div class="container mx-auto px-4 py-3">
        <nav class="flex items-center gap-2 text-sm">
          <router-link to="/" class="text-blue-600 hover:text-blue-700 transition">خانه</router-link>
          <span class="text-gray-400">/</span>
          <router-link to="/category" class="text-blue-600 hover:text-blue-700 transition">دسته‌بندی</router-link>
          <span class="text-gray-400">/</span>
          <span class="text-gray-600">{{ product.category }}</span>
          <span class="text-gray-400">/</span>
          <span class="text-gray-900 font-medium truncate">{{ product.name }}</span>
        </nav>
      </div>
    </div>

    <main class="container mx-auto px-4 py-6">
      <div class="bg-white rounded-2xl shadow-sm border border-gray-200 overflow-hidden">
        <!-- Product Details -->
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 p-6">
          <!-- Image Gallery -->
          <div>
            <!-- Main Image -->
            <div class="relative rounded-xl overflow-hidden bg-gray-100 mb-4">
              <img :src="mainImage" 
                   :alt="product.name"
                   class="w-full h-96 object-contain">
              
              <!-- Badges -->
              <div class="absolute top-4 right-4 flex flex-col gap-2">
                <span v-if="product.isNew" 
                      class="bg-green-500 text-white px-4 py-1.5 rounded-full text-sm font-medium">
                  جدید
                </span>
                <span v-if="product.discount" 
                      class="bg-red-500 text-white px-4 py-1.5 rounded-full text-sm font-medium">
                  {{ product.discount }}% تخفیف
                </span>
              </div>
              
              <!-- Actions -->
              <div class="absolute top-4 left-4 flex flex-col gap-2">
                <button @click="toggleWishlist"
                        class="w-10 h-10 bg-white/80 hover:bg-white rounded-full flex items-center justify-center transition">
                  <svg :class="[
                        'w-6 h-6',
                        isInWishlist ? 'text-red-500 fill-red-500' : 'text-gray-400'
                      ]" 
                       fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" 
                          d="M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.682a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z" />
                  </svg>
                </button>
                
                <button @click="shareProduct"
                        class="w-10 h-10 bg-white/80 hover:bg-white rounded-full flex items-center justify-center transition">
                  <svg class="w-6 h-6 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" 
                          d="M8.684 13.342C8.886 12.938 9 12.482 9 12c0-.482-.114-.938-.316-1.342m0 2.684a3 3 0 110-2.684m0 2.684l6.632 3.316m-6.632-6l6.632-3.316m0 0a3 3 0 105.367-2.684 3 3 0 00-5.367 2.684zm0 9.316a3 3 0 105.368 2.684 3 3 0 00-5.368-2.684z" />
                  </svg>
                </button>
              </div>
            </div>

            <!-- Thumbnails -->
            <div class="flex gap-3 overflow-x-auto pb-2">
              <button v-for="(img, index) in product.images" 
                      :key="index"
                      @click="mainImage = img"
                      :class="[
                        'flex-shrink-0 w-20 h-20 rounded-lg border-2 overflow-hidden',
                        mainImage === img ? 'border-blue-500' : 'border-gray-300'
                      ]">
                <img :src="img" 
                     :alt="`تصویر ${index + 1}`"
                     class="w-full h-full object-cover">
              </button>
            </div>
          </div>

          <!-- Product Info -->
          <div>
            <!-- Title & Rating -->
            <div class="mb-6">
              <h1 class="text-2xl font-bold text-gray-900 mb-2">{{ product.name }}</h1>
              
              <div class="flex items-center gap-4 mb-4">
                <!-- Rating -->
                <div class="flex items-center gap-2">
                  <div class="flex text-yellow-400">
                    <svg v-for="star in 5" :key="star"
                         class="w-5 h-5"
                         :class="star <= product.rating ? 'fill-current' : 'fill-gray-300'"
                         viewBox="0 0 20 20">
                      <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z" />
                    </svg>
                  </div>
                  <span class="text-gray-600 text-sm">{{ product.rating }} از ۵</span>
                </div>
                
                <!-- Reviews -->
                <router-link to="#reviews" 
                             class="text-blue-600 hover:text-blue-700 text-sm">
                  ({{ product.reviews }} نظر)
                </router-link>
                
                <!-- Stock Status -->
                <span :class="[
                      'px-3 py-1 rounded-full text-xs font-medium',
                      product.stock > 0 
                        ? 'bg-green-100 text-green-800' 
                        : 'bg-red-100 text-red-800'
                    ]">
                  {{ product.stock > 0 ? 'موجود در انبار' : 'ناموجود' }}
                </span>
              </div>
              
              <!-- Brand & Code -->
              <div class="flex items-center gap-6 text-sm text-gray-600">
                <div class="flex items-center gap-2">
                  <span class="font-medium">برند:</span>
                  <span class="text-gray-900">{{ product.brand }}</span>
                </div>
                <div class="flex items-center gap-2">
                  <span class="font-medium">کد محصول:</span>
                  <span class="text-gray-900">{{ product.code }}</span>
                </div>
              </div>
            </div>

            <!-- Price -->
            <div class="mb-8 p-6 bg-blue-50 rounded-xl">
              <div class="flex items-center gap-4 mb-2">
                <span class="text-3xl font-bold text-gray-900">
                  {{ formatPrice(finalPrice) }} تومان
                </span>
                
                <span v-if="product.originalPrice" 
                      class="text-xl text-gray-400 line-through">
                  {{ formatPrice(product.originalPrice) }}
                </span>
                
                <span v-if="product.discount" 
                      class="text-lg font-bold text-red-600">
                  {{ product.discount }}% تخفیف
                </span>
              </div>
              
              <div class="text-sm text-gray-600">
                قیمت نهایی با احتساب مالیات و هزینه حمل و نقل
              </div>
            </div>

            <!-- Options -->
            <div class="space-y-6 mb-8">
              <!-- Quantity -->
              <div>
                <label class="block text-gray-700 font-medium mb-3">تعداد:</label>
                <div class="flex items-center gap-4">
                  <div class="flex items-center border border-gray-300 rounded-lg overflow-hidden">
                    <button @click="decreaseQuantity"
                            :disabled="quantity <= 1"
                            class="px-4 py-3 bg-gray-50 hover:bg-gray-100 disabled:opacity-50 disabled:cursor-not-allowed transition">
                      <span class="text-lg">-</span>
                    </button>
                    <input type="number" 
                           v-model.number="quantity"
                           min="1"
                           :max="product.stock"
                           class="w-20 text-center border-0 outline-none text-lg">
                    <button @click="increaseQuantity"
                            :disabled="quantity >= product.stock"
                            class="px-4 py-3 bg-gray-50 hover:bg-gray-100 disabled:opacity-50 disabled:cursor-not-allowed transition">
                      <span class="text-lg">+</span>
                    </button>
                  </div>
                  
                  <div class="text-sm text-gray-600">
                    {{ product.stock }} عدد در انبار موجود است
                  </div>
                </div>
              </div>

              <!-- Warranty -->
              <div>
                <label class="block text-gray-700 font-medium mb-3">گارانتی:</label>
                <div class="flex gap-3">
                  <button v-for="warranty in warranties" 
                          :key="warranty.months"
                          @click="selectedWarranty = warranty.months"
                          :class="[
                            'px-4 py-3 border-2 rounded-lg transition text-sm',
                            selectedWarranty === warranty.months
                              ? 'border-blue-500 bg-blue-50 text-blue-700'
                              : 'border-gray-300 hover:border-gray-400'
                          ]">
                    {{ warranty.label }}
                    <span class="block text-xs text-gray-500 mt-1">+{{ formatPrice(warranty.price) }} تومان</span>
                  </button>
                </div>
              </div>
            </div>

            <!-- Actions -->
            <div class="flex flex-col sm:flex-row gap-4">
              <button @click="addToCart"
                      :disabled="product.stock === 0"
                      :class="[
                        'flex-1 py-4 rounded-lg font-bold text-lg transition flex items-center justify-center gap-3',
                        product.stock > 0
                          ? 'bg-blue-600 hover:bg-blue-700 text-white'
                          : 'bg-gray-200 text-gray-500 cursor-not-allowed'
                      ]">
                <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" 
                        d="M3 3h2l.4 2M7 13h10l4-8H5.4M7 13L5.4 5M7 13l-2.293 2.293c-.63.63-.184 1.707.707 1.707H17m0 0a2 2 0 100 4 2 2 0 000-4zm-8 2a2 2 0 11-4 0 2 2 0 014 0z" />
                </svg>
                {{ product.stock > 0 ? 'افزودن به سبد خرید' : 'ناموجود' }}
              </button>
              
              <button @click="buyNow"
                      :disabled="product.stock === 0"
                      :class="[
                        'flex-1 py-4 rounded-lg font-bold text-lg transition',
                        product.stock > 0
                          ? 'bg-green-600 hover:bg-green-700 text-white'
                          : 'bg-gray-200 text-gray-500 cursor-not-allowed'
                      ]">
                خرید آنی
              </button>
            </div>

            <!-- Features -->
            <div class="mt-8 pt-8 border-t border-gray-200">
              <div class="grid grid-cols-2 gap-4">
                <div class="flex items-center gap-3">
                  <div class="w-10 h-10 bg-blue-100 rounded-lg flex items-center justify-center">
                    <span class="text-blue-600 text-xl">🚚</span>
                  </div>
                  <div>
                    <div class="font-medium text-gray-900">ارسال رایگان</div>
                    <div class="text-xs text-gray-600">برای خرید بالای ۵۰۰ هزار تومان</div>
                  </div>
                </div>
                
                <div class="flex items-center gap-3">
                  <div class="w-10 h-10 bg-green-100 rounded-lg flex items-center justify-center">
                    <span class="text-green-600 text-xl">🛡️</span>
                  </div>
                  <div>
                    <div class="font-medium text-gray-900">گارانتی ۱۸ ماهه</div>
                    <div class="text-xs text-gray-600">ضمانت بازگشت وجه</div>
                  </div>
                </div>
                
                <div class="flex items-center gap-3">
                  <div class="w-10 h-10 bg-purple-100 rounded-lg flex items-center justify-center">
                    <span class="text-purple-600 text-xl">🔧</span>
                  </div>
                  <div>
                    <div class="font-medium text-gray-900">نصب رایگان</div>
                    <div class="text-xs text-gray-600">در تهران و شهرستان‌ها</div>
                  </div>
                </div>
                
                <div class="flex items-center gap-3">
                  <div class="w-10 h-10 bg-orange-100 rounded-lg flex items-center justify-center">
                    <span class="text-orange-600 text-xl">📞</span>
                  </div>
                  <div>
                    <div class="font-medium text-gray-900">پشتیبانی ۲۴ ساعته</div>
                    <div class="text-xs text-gray-600">مشاوره تخصصی</div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Tabs -->
        <div class="border-t border-gray-200">
          <div class="flex border-b border-gray-200">
            <button v-for="tab in tabs" 
                    :key="tab.id"
                    @click="activeTab = tab.id"
                    :class="[
                      'px-8 py-4 font-medium text-lg transition-all',
                      activeTab === tab.id
                        ? 'text-blue-600 border-b-2 border-blue-600'
                        : 'text-gray-500 hover:text-gray-700'
                    ]">
              {{ tab.label }}
            </button>
          </div>

          <!-- Tab Content -->
          <div class="p-8">
            <!-- Description -->
            <div v-if="activeTab === 'description'" class="prose max-w-none">
              <h3 class="text-xl font-bold text-gray-900 mb-4">توضیحات محصول</h3>
              <div class="text-gray-700 leading-relaxed space-y-4">
                <p>{{ product.fullDescription }}</p>
                
                <div class="bg-gray-50 p-6 rounded-xl">
                  <h4 class="font-bold text-gray-900 mb-3">ویژگی‌های اصلی:</h4>
                  <ul class="space-y-2">
                    <li v-for="feature in product.features" 
                        :key="feature"
                        class="flex items-center gap-2">
                      <svg class="w-5 h-5 text-green-500" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
                      </svg>
                      {{ feature }}
                    </li>
                  </ul>
                </div>
                
                <div>
                  <h4 class="font-bold text-gray-900 mb-3">مشخصات فنی:</h4>
                  <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                    <div v-for="spec in product.specifications" 
                         :key="spec.name"
                         class="flex justify-between py-3 border-b border-gray-200">
                      <span class="text-gray-600">{{ spec.name }}:</span>
                      <span class="text-gray-900 font-medium">{{ spec.value }}</span>
                    </div>
                  </div>
                </div>
              </div>
            </div>

            <!-- Reviews -->
            <div v-else-if="activeTab === 'reviews'" id="reviews">
              <div class="flex flex-col lg:flex-row gap-8">
                <!-- Rating Summary -->
                <div class="lg:w-1/3">
                  <div class="bg-gray-50 p-6 rounded-xl">
                    <div class="text-center mb-6">
                      <div class="text-5xl font-bold text-gray-900 mb-2">{{ product.rating.toFixed(1) }}</div>
                      <div class="flex justify-center text-yellow-400 mb-2">
                        <svg v-for="star in 5" :key="star"
                             class="w-6 h-6"
                             :class="star <= product.rating ? 'fill-current' : 'fill-gray-300'"
                             viewBox="0 0 20 20">
                          <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z" />
                        </svg>
                      </div>
                      <div class="text-gray-600">بر اساس {{ product.reviews }} نظر</div>
                    </div>
                    
                    <div class="space-y-3">
                      <div v-for="rating in 5" :key="rating"
                           class="flex items-center gap-3">
                        <span class="text-sm text-gray-600 w-8">{{ 6 - rating }} ستاره</span>
                        <div class="flex-1 h-2 bg-gray-200 rounded-full overflow-hidden">
                          <div class="h-full bg-yellow-400" 
                               :style="{ width: `${((product.reviews * (6 - rating)) / (product.reviews * 5)) * 100}%` }"></div>
                        </div>
                        <span class="text-sm text-gray-600 w-12">%{{ Math.round(((product.reviews * (6 - rating)) / (product.reviews * 5)) * 100) }}</span>
                      </div>
                    </div>
                  </div>
                  
                  <button @click="showReviewModal = true"
                          class="w-full mt-4 py-3 bg-blue-600 hover:bg-blue-700 text-white rounded-lg font-medium transition">
                    ثبت نظر جدید
                  </button>
                </div>

                <!-- Reviews List -->
                <div class="lg:w-2/3">
                  <div class="space-y-6">
                    <div v-for="review in reviews" :key="review.id"
                         class="bg-white border border-gray-200 rounded-xl p-6">
                      <div class="flex items-start justify-between mb-4">
                        <div>
                          <div class="font-medium text-gray-900 mb-1">{{ review.author }}</div>
                          <div class="flex items-center gap-2">
                            <div class="flex text-yellow-400">
                              <svg v-for="star in 5" :key="star"
                                   class="w-4 h-4"
                                   :class="star <= review.rating ? 'fill-current' : 'fill-gray-300'"
                                   viewBox="0 0 20 20">
                                <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z" />
                              </svg>
                            </div>
                            <span class="text-sm text-gray-500">{{ formatDate(review.date) }}</span>
                          </div>
                        </div>
                        
                        <div v-if="review.verified" 
                             class="px-3 py-1 bg-green-100 text-green-800 rounded-full text-xs font-medium">
                          خریدار تایید شده
                        </div>
                      </div>
                      
                      <h4 class="font-medium text-gray-900 mb-2">{{ review.title }}</h4>
                      <p class="text-gray-700 leading-relaxed">{{ review.content }}</p>
                      
                      <div v-if="review.images && review.images.length > 0" 
                           class="mt-4 flex gap-2">
                        <button v-for="(img, index) in review.images" 
                                :key="index"
                                @click="openImage(img)"
                                class="w-16 h-16 rounded-lg overflow-hidden border border-gray-300">
                          <img :src="img" 
                               :alt="`تصویر نظر ${index + 1}`"
                               class="w-full h-full object-cover">
                        </button>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>

            <!-- FAQ -->
            <div v-else-if="activeTab === 'faq'" class="space-y-4">
              <div v-for="faq in faqs" :key="faq.id"
                   class="border border-gray-200 rounded-xl overflow-hidden">
                <button @click="toggleFAQ(faq.id)"
                        class="w-full px-6 py-4 text-right flex items-center justify-between hover:bg-gray-50 transition">
                  <span class="font-medium text-gray-900">{{ faq.question }}</span>
                  <svg class="w-5 h-5 text-gray-500 transition-transform"
                       :class="{ 'rotate-180': openFaq === faq.id }"
                       fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
                  </svg>
                </button>
                
                <div v-if="openFaq === faq.id" class="px-6 py-4 bg-gray-50 border-t border-gray-200">
                  <p class="text-gray-700 leading-relaxed">{{ faq.answer }}</p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Related Products -->
      <div class="mt-12">
        <div class="flex items-center justify-between mb-6">
          <h2 class="text-2xl font-bold text-gray-900">محصولات مرتبط</h2>
          <router-link to="/category" 
                       class="text-blue-600 hover:text-blue-700 font-medium flex items-center gap-2">
            مشاهده همه
            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 19l-7-7m0 0l7-7m-7 7h18" />
            </svg>
          </router-link>
        </div>
        
        <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
          <div v-for="related in relatedProducts" 
               :key="related.id"
               @click="$router.push(`/product/${related.id}`)"
               class="bg-white rounded-xl shadow-sm border border-gray-200 hover:shadow-lg hover:border-blue-300 transition-all duration-300 cursor-pointer overflow-hidden">
            <div class="p-4">
              <div class="w-full h-40 bg-gray-100 rounded-lg mb-4 overflow-hidden">
                <img :src="related.image" 
                     :alt="related.name"
                     class="w-full h-full object-cover hover:scale-105 transition-transform duration-300">
              </div>
              
              <h3 class="font-medium text-gray-900 text-sm mb-2 line-clamp-2">{{ related.name }}</h3>
              
              <div class="flex items-center justify-between">
                <div class="text-lg font-bold text-gray-900">
                  {{ formatPrice(related.price) }} تومان
                </div>
                
                <button @click.stop="addToCart(related)"
                        class="px-3 py-2 bg-blue-600 hover:bg-blue-700 text-white rounded-lg text-xs font-medium transition">
                  خرید
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </main>

    <!-- Review Modal -->
    <div v-if="showReviewModal" class="fixed inset-0 bg-black/50 z-50 flex items-center justify-center p-4">
      <div class="bg-white rounded-2xl shadow-2xl w-full max-w-2xl max-h-[90vh] overflow-y-auto p-6">
        <!-- Modal content here -->
        <h3 class="text-xl font-bold text-gray-900 mb-6">ثبت نظر جدید</h3>
        <!-- Add review form -->
      </div>
    </div>

    <!-- Image Viewer Modal -->
    <div v-if="selectedImage" class="fixed inset-0 bg-black/90 z-50 flex items-center justify-center">
      <button @click="selectedImage = null"
              class="absolute top-4 left-4 text-white hover:text-gray-300">
        <svg class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
        </svg>
      </button>
      <img :src="selectedImage" 
           class="max-w-full max-h-full object-contain">
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'
import { useRoute } from 'vue-router'

const route = useRoute()

// State
const mainImage = ref('')
const quantity = ref(1)
const selectedWarranty = ref(12)
const activeTab = ref('description')
const openFaq = ref(null)
const showReviewModal = ref(false)
const selectedImage = ref(null)
const isInWishlist = ref(false)

// Mock Data
const product = ref({
  id: 1,
  name: 'موتور اصلی ماشین لباسشویی سامسونگ مدل WD90J6',
  category: 'ماشین لباسشویی',
  brand: 'سامسونگ',
  code: 'SAMS-WD90J6-MOTOR',
  price: 1850000,
  originalPrice: 2200000,
  rating: 4.5,
  reviews: 42,
  stock: 15,
  discount: 15,
  isNew: true,
  images: [
    '/machin-leb.jpg',
    '/machin-leb.jpg',
    '/machin-leb.jpg',
    '/machin-leb.jpg'
  ],
  fullDescription: 'موتور اصلی ماشین لباسشویی سامسونگ مدل WD90J6 با کیفیت بالا و عملکرد بی‌نظیر. این موتور با تکنولوژی اینورتر دیجیتال طراحی شده است که مصرف انرژی را تا ۴۰٪ کاهش می‌دهد. دارای گارانتی ۱۸ ماهه و خدمات پس از فروش معتبر.',
  features: [
    'مصرف انرژی کم با تکنولوژی اینورتر',
    'عملکرد بی‌صدا و کم لرزش',
    'قابلیت تحمل بار تا ۹ کیلوگرم',
    'سرعت چرخش ۱۴۰۰ دور در دقیقه',
    'جنس بدنه از استیل ضدزنگ'
  ],
  specifications: [
    { name: 'نوع موتور', value: 'اینورتر دیجیتال' },
    { name: 'توان مصرفی', value: '۲۲۰ ولت / ۵۰ هرتز' },
    { name: 'سرعت چرخش', value: '۱۴۰۰ دور در دقیقه' },
    { name: 'حداکثر بار', value: '۹ کیلوگرم' },
    { name: 'ابعاد', value: '۶۰×۶۰×۸۵ سانتیمتر' },
    { name: 'وزن', value: '۴.۵ کیلوگرم' },
    { name: 'رنگ', value: 'سفید' },
    { name: 'گارانتی', value: '۱۸ ماه' }
  ]
})

const warranties = [
  { months: 12, label: 'گارانتی ۱۲ ماهه', price: 0 },
  { months: 18, label: 'گارانتی ۱۸ ماهه', price: 120000 },
  { months: 24, label: 'گارانتی ۲۴ ماهه', price: 200000 }
]

const tabs = [
  { id: 'description', label: 'توضیحات' },
  { id: 'reviews', label: 'نظرات (۴۲)' },
  { id: 'faq', label: 'سوالات متداول' }
]

const reviews = [
  {
    id: 1,
    author: 'محمد رضایی',
    rating: 5,
    date: '۱۴۰۲/۱۰/۱۵',
    title: 'کیفیت عالی',
    content: 'قطعه کاملاً اورجینال و با کیفیت بود. نصب سریع انجام شد و ماشین لباسشویی مثل روز اول کار می‌کند.',
    verified: true,
    images: ['https://picsum.photos/200/200?random=11']
  },
  {
    id: 2,
    author: 'فاطمه کریمی',
    rating: 4,
    date: '۱۴۰۲/۱۰/۱۰',
    title: 'قیمت مناسب',
    content: 'با وجود اینکه قیمت بالایی داشت اما نسبت به کیفیت و خدمات، کاملاً منطقی بود.',
    verified: true,
    images: []
  }
]

const faqs = [
  {
    id: 1,
    question: 'آیا این قطعه برای مدل‌های دیگر سامسونگ هم مناسب است؟',
    answer: 'خیر، این قطعه مخصوص مدل WD90J6 است. لطفاً قبل از خرید از تطابق قطعه با مدل دستگاه خود مطمئن شوید.'
  },
  {
    id: 2,
    question: 'نصب قطعه چگونه انجام می‌شود؟',
    answer: 'نصب توسط تکنسین‌های مجاز ما به صورت رایگان انجام می‌شود. در صورت تمایل می‌توانید خودتان نصب کنید که راهنمای نصب در بسته‌بندی موجود است.'
  }
]

const relatedProducts = Array.from({ length: 4 }, (_, i) => ({
  id: i + 100,
  name: `قطعه مرتبط ${i + 1}`,
  price: Math.floor(Math.random() * 2000000) + 1000000,
  image: `https://picsum.photos/400/300?random=${i + 100}`
}))

// Computed
const finalPrice = computed(() => {
  let price = product.value.price
  const warranty = warranties.find(w => w.months === selectedWarranty.value)
  if (warranty) price += warranty.price
  return price
})

// Methods
const formatPrice = (price) => {
  return new Intl.NumberFormat('fa-IR').format(price)
}

const formatDate = (date) => {
  return date // In real app, use a proper date formatter
}

const increaseQuantity = () => {
  if (quantity.value < product.value.stock) {
    quantity.value++
  }
}

const decreaseQuantity = () => {
  if (quantity.value > 1) {
    quantity.value--
  }
}

const toggleWishlist = () => {
  isInWishlist.value = !isInWishlist.value
  // Save to localStorage
}

const shareProduct = () => {
  if (navigator.share) {
    navigator.share({
      title: product.value.name,
      text: product.value.description,
      url: window.location.href
    })
  } else {
    // Fallback for browsers that don't support Web Share API
    navigator.clipboard.writeText(window.location.href)
    alert('لینک محصول در کلیپ‌بورد کپی شد')
  }
}

const addToCart = () => {
  const item = {
    ...product.value,
    quantity: quantity.value,
    warranty: selectedWarranty.value,
    finalPrice: finalPrice.value
  }
  // Dispatch to cart store
  console.log('Added to cart:', item)
}

const buyNow = () => {
  addToCart()
  // Navigate to checkout
  router.push('/checkout')
}

const toggleFAQ = (id) => {
  openFaq.value = openFaq.value === id ? null : id
}

const openImage = (img) => {
  selectedImage.value = img
}

// Initialize
onMounted(() => {
  mainImage.value = product.value.images[0]
  // Load wishlist status
  const wishlist = JSON.parse(localStorage.getItem('wishlist') || '[]')
  isInWishlist.value = wishlist.includes(product.value.id)
})
</script>

<style scoped>
.line-clamp-2 {
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

/* Smooth transitions */
.rotate-180 {
  transform: rotate(180deg);
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
</style>