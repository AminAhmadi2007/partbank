<template>
  <div class="min-h-screen bg-gray-50">
    <!-- Navbar -->
    <Navbar />
    
    <main class="container mx-auto px-4 py-8">
      <!-- Page Header -->
      <div class="mb-8">
        <div class="flex items-center gap-3 mb-4">
          <div class="w-12 h-12 bg-gradient-to-br from-blue-600 to-blue-800 rounded-xl flex items-center justify-center">
            <span class="text-white text-2xl font-bold">🛒</span>
          </div>
          <div>
            <h1 class="text-3xl font-bold text-gray-900">سبد خرید</h1>
            <p class="text-gray-600">مدیریت سفارش‌های شما</p>
          </div>
        </div>
      </div>

      <div class="grid lg:grid-cols-3 gap-8">
        <!-- Cart Items -->
        <div class="lg:col-span-2">
          <!-- Cart Items List -->
          <div v-if="cartItems.length > 0" class="space-y-4">
            <div v-for="item in cartItems" :key="item.id" 
                 class="bg-white rounded-xl shadow-md border border-gray-200 overflow-hidden hover:shadow-lg transition">
              <div class="p-6">
                <div class="flex flex-col md:flex-row gap-6">
                  <!-- Product Image -->
                  <div class="w-full md:w-32 h-32 flex-shrink-0">
                    <div :class="[
                      'w-full h-full rounded-lg flex items-center justify-center',
                      getCategoryClass(item.category)
                    ]">
                      <span class="text-4xl">{{ item.icon }}</span>
                    </div>
                  </div>
                  
                  <!-- Product Info -->
                  <div class="flex-1">
                    <div class="flex justify-between items-start">
                      <div>
                        <div class="flex items-center gap-2 mb-2">
                          <span class="text-xs bg-blue-50 text-blue-600 px-2 py-1 rounded">{{ item.category }}</span>
                          <span class="text-xs bg-gray-100 text-gray-600 px-2 py-1 rounded">{{ item.brand }}</span>
                        </div>
                        <h3 class="font-bold text-gray-900 text-lg mb-2">{{ item.name }}</h3>
                        <p class="text-sm text-gray-500 mb-3">{{ item.compatibility }}</p>
                      </div>
                      
                      <!-- Remove Button -->
                      <button @click="removeFromCart(item.id)" 
                              class="text-red-500 hover:text-red-700 p-2">
                        <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
                        </svg>
                      </button>
                    </div>
                    
                    <!-- Quantity & Price -->
                    <div class="flex items-center justify-between mt-4">
                      <!-- Quantity Controls -->
                      <div class="flex items-center gap-3">
                        <button @click="decreaseQuantity(item.id)" 
                                class="w-8 h-8 border border-gray-300 rounded-lg flex items-center justify-center hover:bg-gray-50">
                          <span class="text-lg">−</span>
                        </button>
                        
                        <span class="w-12 text-center font-semibold">{{ item.quantity }}</span>
                        
                        <button @click="increaseQuantity(item.id)" 
                                class="w-8 h-8 border border-gray-300 rounded-lg flex items-center justify-center hover:bg-gray-50">
                          <span class="text-lg">+</span>
                        </button>
                        
                        <span class="text-sm text-gray-500 mr-4">عدد</span>
                      </div>
                      
                      <!-- Price -->
                      <div class="text-left">
                        <div class="text-xl font-bold text-gray-900">{{ formatPrice(item.price * item.quantity) }}</div>
                        <div class="text-sm text-gray-500">تومان</div>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
            
            <!-- Empty Cart State -->
          </div>
          <div v-else class="bg-white rounded-xl shadow-md border border-gray-200 p-12 text-center">
            <div class="w-24 h-24 bg-gray-100 rounded-full flex items-center justify-center mx-auto mb-6">
              <span class="text-4xl">🛒</span>
            </div>
            <h3 class="text-xl font-bold text-gray-900 mb-3">سبد خرید شما خالی است</h3>
            <p class="text-gray-600 mb-6">می‌توانید با مراجعه به صفحه محصولات، قطعات مورد نیاز خود را انتخاب کنید</p>
            <a href="/" 
               class="inline-flex items-center gap-2 bg-gradient-to-r from-blue-600 to-blue-700 text-white px-6 py-3 rounded-lg font-semibold hover:from-blue-700 hover:to-blue-800 transition">
              <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 19l-7-7m0 0l7-7m-7 7h18" />
              </svg>
              بازگشت به فروشگاه
            </a>
          </div>
          
          <!-- Continue Shopping -->
          <div v-if="cartItems.length > 0" class="mt-8">
            <a href="/" class="inline-flex items-center gap-2 text-blue-600 hover:text-blue-700 font-medium">
              <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 19l-7-7m0 0l7-7m-7 7h18" />
              </svg>
              ادامه خرید
            </a>
          </div>
        </div>
        
        <!-- Order Summary -->
        <div class="lg:col-span-1">
          <div class="sticky top-8">
            <div class="bg-white rounded-xl shadow-lg border border-gray-200 p-6">
              <h3 class="font-bold text-gray-900 text-xl mb-6">خلاصه سفارش</h3>
              
              <!-- Order Details -->
              <div class="space-y-4 mb-6">
                <div class="flex justify-between items-center">
                  <span class="text-gray-600">تعداد محصولات</span>
                  <span class="font-semibold">{{ totalItems }} عدد</span>
                </div>
                
                <div class="flex justify-between items-center">
                  <span class="text-gray-600">جمع کل</span>
                  <span class="font-semibold">{{ formatPrice(subtotal) }} تومان</span>
                </div>
                
                <div class="flex justify-between items-center">
                  <span class="text-gray-600">تخفیف</span>
                  <span class="font-semibold text-green-600">- {{ formatPrice(discount) }} تومان</span>
                </div>
                
                <div class="border-t border-gray-200 pt-4">
                  <div class="flex justify-between items-center">
                    <span class="text-gray-900 font-bold text-lg">مبلغ قابل پرداخت</span>
                    <span class="text-2xl font-bold text-blue-600">{{ formatPrice(total) }} تومان</span>
                  </div>
                </div>
              </div>
              
              <!-- Checkout Button -->
              <button v-if="cartItems.length > 0" @click="proceedToCheckout" 
                      class="w-full bg-gradient-to-r from-blue-600 to-blue-700 hover:from-blue-700 hover:to-blue-800 text-white py-4 rounded-xl font-semibold text-lg transition-all duration-300 shadow-lg hover:shadow-xl mb-4">
                ادامه جهت تسویه حساب
              </button>
              
              <!-- Delivery Info -->
              <div class="bg-blue-50 border border-blue-200 rounded-lg p-4 mb-6">
                <div class="flex items-start gap-3">
                  <span class="text-blue-600 text-xl">🚚</span>
                  <div class="text-sm text-blue-800">
                    <p class="font-semibold mb-1">تحویل سریع</p>
                    <p>تهران: 3 ساعته | شهرستان: 24 ساعته</p>
                  </div>
                </div>
              </div>
              
              <!-- Payment Methods -->
              <div class="border-t border-gray-200 pt-6">
                <h4 class="font-semibold text-gray-900 mb-3">روش‌های پرداخت</h4>
                <div class="grid grid-cols-4 gap-3">
                  <div class="h-12 bg-gray-100 rounded-lg flex items-center justify-center">
                    <span class="text-xl">💳</span>
                  </div>
                  <div class="h-12 bg-gray-100 rounded-lg flex items-center justify-center">
                    <span class="text-xl">🏦</span>
                  </div>
                  <div class="h-12 bg-gray-100 rounded-lg flex items-center justify-center">
                    <span class="text-xl">📱</span>
                  </div>
                  <div class="h-12 bg-gray-100 rounded-lg flex items-center justify-center">
                    <span class="text-xl">💰</span>
                  </div>
                </div>
              </div>
            </div>
            
            <!-- Promo Code -->
            <div class="bg-white rounded-xl shadow-lg border border-gray-200 p-6 mt-6">
              <h4 class="font-semibold text-gray-900 mb-3">کد تخفیف</h4>
              <div class="flex gap-2">
                <input v-model="promoCode" type="text" placeholder="کد تخفیف" 
                       class="flex-1 px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 outline-none">
                <button @click="applyPromoCode" 
                        class="bg-blue-600 text-white px-4 py-3 rounded-lg font-medium hover:bg-blue-700 transition">
                  اعمال
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </main>
    
    <!-- Footer -->
    <Footer />
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()
const promoCode = ref('')

// Sample cart data
const cartItems = ref([
  {
    id: 1,
    name: 'کمپرسور یخچال سامسونگ مدل DA97-12606A',
    icon: '❄️',
    category: 'یخچال',
    brand: 'سامسونگ',
    compatibility: 'مناسب برای مدل‌های RS50, RS55, RS60',
    price: 1850000,
    quantity: 1
  },
  {
    id: 2,
    name: 'موتور ماشین لباسشویی ال جی',
    icon: '🧺',
    category: 'لباسشویی',
    brand: 'ال جی',
    compatibility: 'مناسب برای سری F4',
    price: 1250000,
    quantity: 2
  },
  {
    id: 3,
    name: 'ترموکوپل اجاق گاز اسنوا',
    icon: '🔥',
    category: 'اجاق گاز',
    brand: 'اسنوا',
    compatibility: 'تمام مدل‌های اسنوا',
    price: 85000,
    quantity: 1
  }
])

// Computed properties
const totalItems = computed(() => {
  return cartItems.value.reduce((sum, item) => sum + item.quantity, 0)
})

const subtotal = computed(() => {
  return cartItems.value.reduce((sum, item) => sum + (item.price * item.quantity), 0)
})

const discount = computed(() => {
  return subtotal.value * 0.1 // 10% discount for example
})

const total = computed(() => {
  return subtotal.value - discount.value
})

// Methods
const getCategoryClass = (category) => {
  const classes = {
    'یخچال': 'bg-gradient-to-br from-blue-100 to-blue-200',
    'لباسشویی': 'bg-gradient-to-br from-purple-100 to-purple-200',
    'ظرفشویی': 'bg-gradient-to-br from-green-100 to-green-200',
    'اجاق گاز': 'bg-gradient-to-br from-red-100 to-red-200'
  }
  return classes[category] || 'bg-gradient-to-br from-gray-100 to-gray-200'
}

const formatPrice = (price) => {
  return price.toLocaleString('fa-IR')
}

const increaseQuantity = (itemId) => {
  const item = cartItems.value.find(item => item.id === itemId)
  if (item) {
    item.quantity += 1
  }
}

const decreaseQuantity = (itemId) => {
  const item = cartItems.value.find(item => item.id === itemId)
  if (item && item.quantity > 1) {
    item.quantity -= 1
  }
}

const removeFromCart = (itemId) => {
  cartItems.value = cartItems.value.filter(item => item.id !== itemId)
}

const applyPromoCode = () => {
  if (promoCode.value.trim()) {
    alert(`کد تخفیف "${promoCode.value}" اعمال شد`)
    promoCode.value = ''
  }
}

const proceedToCheckout = () => {
  router.push('/checkout')
}
</script>