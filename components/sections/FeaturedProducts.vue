<template>
  <section class="py-16 bg-white">
    <div class="container mx-auto px-4">
      <div class="text-center mb-12">
        <h2 class="text-3xl md:text-4xl font-bold text-gray-900 mb-4">
          قطعات بر اساس دستگاه
        </h2>
        <p class="text-lg text-gray-600 max-w-2xl mx-auto">
          دسته‌بندی تخصصی قطعات برای هر نوع دستگاه خانگی
        </p>
      </div>
      
      <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-5 gap-4">
        <div v-for="category in categories" :key="category.id"
             class="group bg-white border border-gray-200 rounded-2xl p-6 text-center hover:shadow-2xl hover:border-blue-500 transition-all duration-300 transform hover:-translate-y-2 cursor-pointer">
          <div class="w-20 h-20 bg-gradient-to-br from-blue-50 to-blue-100 rounded-2xl flex items-center justify-center mx-auto mb-4 group-hover:scale-110 transition-transform duration-300">
            <span class="text-3xl">{{ category.icon }}</span>
          </div>
          <h3 class="font-bold text-gray-900 text-lg mb-2">{{ category.name }}</h3>
          <p class="text-sm text-gray-500">{{ category.count }} قطعه</p>
          
          <div class="mt-4 pt-4 border-t border-gray-100">
            <div class="flex justify-between text-xs text-gray-500">
              <span>از {{ category.priceRange.from.toLocaleString() }}</span>
              <span>تا {{ category.priceRange.to.toLocaleString() }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
const categories = [
  { id: 1, name: 'یخچال و فریزر', icon: '❄️', count: 245, priceRange: { from: 150000, to: 2500000 } },
  { id: 2, name: 'ماشین لباسشویی', icon: '🧺', count: 189, priceRange: { from: 80000, to: 1800000 } },
  { id: 3, name: 'ماشین ظرفشویی', icon: '🍽️', count: 132, priceRange: { from: 120000, to: 1600000 } },
  { id: 4, name: 'اجاق گاز', icon: '🔥', count: 98, priceRange: { from: 50000, to: 1200000 } },
  { id: 5, name: 'کولر و تهویه', icon: '💨', count: 167, priceRange: { from: 100000, to: 2200000 } },
  { id: 6, name: 'آبگرمکن', icon: '🚿', count: 76, priceRange: { from: 60000, to: 900000 } },
  { id: 7, name: 'جاروبرقی', icon: '🧹', count: 112, priceRange: { from: 40000, to: 800000 } },
  { id: 8, name: 'مایکروویو', icon: '🍕', count: 54, priceRange: { from: 70000, to: 600000 } },
  { id: 9, name: 'قهوه ساز', icon: '☕', count: 45, priceRange: { from: 30000, to: 500000 } },
  { id: 10, name: 'وسایل برقی', icon: '🔌', count: 89, priceRange: { from: 20000, to: 400000 } }
]
</script>