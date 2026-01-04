<template>
  <section class="py-16 bg-gradient-to-b from-gray-50 to-white">
    <div class="container mx-auto px-4">
      <div class="text-center mb-12">
        <div class="inline-flex items-center gap-2 bg-gradient-to-r from-yellow-50 to-yellow-100 text-yellow-700 px-6 py-2 rounded-full mb-4">
          <span class="text-xl">🏆</span>
          <span class="font-semibold">پرفروش‌ترین‌ها</span>
        </div>
        <h2 class="text-3xl md:text-4xl font-bold text-gray-900 mb-4">
          محصولات پرفروش
        </h2>
        <p class="text-lg text-gray-600 max-w-2xl mx-auto">
          قطعاتی که بیشترین استقبال را داشته‌اند
        </p>
      </div>
      
      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-8">
        <div v-for="(product, index) in bestSellingProducts" :key="product.id" 
             class="group relative">
          <!-- Rank Badge -->
          <div class="absolute -top-4 -right-4 z-20">
            <div :class="[
              'w-12 h-12 rounded-full flex items-center justify-center text-white font-bold text-lg shadow-xl transform group-hover:scale-110 transition-transform duration-300',
              index === 0 ? 'bg-gradient-to-br from-yellow-500 to-yellow-600' : 
              index === 1 ? 'bg-gradient-to-br from-gray-400 to-gray-500' : 
              index === 2 ? 'bg-gradient-to-br from-amber-600 to-amber-700' : 'bg-gradient-to-br from-blue-500 to-blue-600'
            ]">
              {{ index + 1 }}
            </div>
          </div>
          
          <div class="bg-white rounded-2xl shadow-lg hover:shadow-2xl transition-all duration-500 transform group-hover:-translate-y-2 h-full overflow-hidden border border-gray-200">
            <!-- Product Image -->
            <div class="relative h-48 overflow-hidden">
              <div :class="[
                'w-full h-full flex items-center justify-center transition-transform duration-700 group-hover:scale-110',
                index === 0 ? 'bg-gradient-to-br from-yellow-50 to-yellow-100' : 
                index === 1 ? 'bg-gradient-to-br from-gray-50 to-gray-100' : 
                index === 2 ? 'bg-gradient-to-br from-amber-50 to-amber-100' : 'bg-gradient-to-br from-blue-50 to-blue-100'
              ]">
                <div class="w-24 h-24 bg-white/80 rounded-2xl flex items-center justify-center shadow-lg">
                  <span class="text-4xl">{{ product.icon }}</span>
                </div>
              </div>
            </div>
            
            <!-- Product Info -->
            <div class="p-6 relative">
              <div class="flex items-center gap-2 mb-3">
                <span class="text-xs bg-blue-50 text-blue-600 px-3 py-1 rounded-full font-medium">{{ product.category }}</span>
              </div>
              
              <h3 class="font-bold text-gray-900 mb-3 line-clamp-2 text-lg group-hover:text-blue-700 transition-colors">{{ product.name }}</h3>
              
              <div class="flex items-center gap-2 mb-4">
                <div class="flex items-center">
                  <span v-for="i in 5" :key="i" 
                        :class="['text-lg', i <= Math.floor(product.rating) ? 'text-yellow-400' : 'text-gray-300']">
                    ★
                  </span>
                </div>
                <span class="text-sm text-gray-500">({{ product.sales }}+ فروش)</span>
              </div>
              
              <div class="flex items-center justify-between mb-4">
                <div>
                  <span class="text-2xl font-bold text-gray-900">{{ formatPrice(product.price) }}</span>
                  <span class="text-sm text-gray-500 mr-1">تومان</span>
                </div>
                
                <button @click="addToCart(product)" 
                        class="bg-gradient-to-r from-blue-500 to-blue-600 hover:from-blue-600 hover:to-blue-700 text-white p-3 rounded-lg transition-all duration-300 transform hover:scale-110 shadow-md">
                  <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6v6m0 0v6m0-6h6m-6 0H6" />
                  </svg>
                </button>
              </div>
              
              <!-- Sales Progress -->
              <div class="mt-6">
                <div class="flex justify-between text-sm mb-2">
                  <span class="text-gray-600">فروش این ماه</span>
                  <span class="font-bold text-gray-900">{{ product.monthlySales }} عدد</span>
                </div>
                <div class="w-full bg-gray-200 rounded-full h-2 overflow-hidden">
                  <div :class="[
                    'h-2 rounded-full transition-all duration-1000',
                    index === 0 ? 'bg-gradient-to-r from-yellow-500 to-yellow-600' : 
                    index === 1 ? 'bg-gradient-to-r from-gray-400 to-gray-500' : 
                    index === 2 ? 'bg-gradient-to-r from-amber-600 to-amber-700' : 'bg-gradient-to-r from-blue-500 to-blue-600'
                  ]" :style="{ width: `${Math.min(product.monthlySales / 500 * 100, 100)}%` }">
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'

const bestSellingProducts = ref([
  {
    id: 1,
    name: 'کمپرسور یخچال سامسونگ مدل DA97-12606A',
    icon: '❄️',
    price: 1850000,
    category: 'یخچال',
    rating: 4.8,
    sales: 128,
    monthlySales: 42
  },
  {
    id: 2,
    name: 'موتور ماشین لباسشویی ال جی مدل 4681EA2001T',
    icon: '🧺',
    price: 1250000,
    category: 'لباسشویی',
    rating: 4.6,
    sales: 95,
    monthlySales: 38
  },
  {
    id: 3,
    name: 'برد کنترل ماشین ظرفشویی بوش مدل SGV46A33',
    icon: '🍽️',
    price: 980000,
    category: 'ظرفشویی',
    rating: 4.9,
    sales: 87,
    monthlySales: 35
  },
  {
    id: 4,
    name: 'ترموکوپل اجاق گاز اسنوا مدل TC-105',
    icon: '🔥',
    price: 85000,
    category: 'اجاق گاز',
    rating: 4.4,
    sales: 156,
    monthlySales: 62
  }
])

const formatPrice = (price) => {
  return price.toLocaleString('fa-IR')
}

const addToCart = (product) => {
  console.log('Added to cart:', product.name)
  // Emit event or call store action
}
</script>