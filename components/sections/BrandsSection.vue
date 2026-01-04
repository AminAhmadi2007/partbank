<template>
  <section class="py-16 bg-gradient-to-r from-gray-50 to-blue-50">
    <div class="container mx-auto px-4">
      <div class="text-center mb-12">
        <div class="inline-flex items-center gap-2 bg-gradient-to-r from-purple-50 to-purple-100 text-purple-700 px-6 py-2 rounded-full mb-4">
          <span class="text-xl">🏷️</span>
          <span class="font-semibold">برندهای معتبر</span>
        </div>
        <h2 class="text-3xl md:text-4xl font-bold text-gray-900 mb-4">
          برندهای معتبر
        </h2>
        <p class="text-lg text-gray-600 max-w-2xl mx-auto">
          قطعات اصل و با کیفیت از معتبرترین برندهای داخلی و خارجی
        </p>
      </div>
      
      <div class="grid grid-cols-3 md:grid-cols-4 lg:grid-cols-6 gap-8">
        <div v-for="brand in brands" :key="brand.id" 
             class="group relative">
          <div class="bg-white rounded-2xl shadow-lg p-6 flex items-center justify-center hover:shadow-2xl transition-all duration-500 transform hover:-translate-y-2 cursor-pointer border border-gray-200 overflow-hidden">
            <div class="absolute inset-0 bg-gradient-to-br from-blue-50/50 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300"></div>
            
            <div class="relative z-10 text-center">
              <div class="w-20 h-20 mx-auto mb-4">
                <div class="w-full h-full bg-gradient-to-br from-blue-500 to-blue-600 rounded-2xl flex items-center justify-center transform group-hover:scale-110 group-hover:rotate-3 transition-all duration-500 shadow-lg">
                  <span class="text-3xl text-white font-bold">{{ brand.icon }}</span>
                </div>
              </div>
              <h3 class="font-bold text-gray-900 text-lg group-hover:text-blue-700 transition-colors">{{ brand.name }}</h3>
              <p class="text-sm text-gray-500 mt-2">{{ brand.count }} قطعه</p>
            </div>
            
            <!-- Hover Effect -->
            <div class="absolute bottom-0 left-0 right-0 h-1 bg-gradient-to-r from-blue-500 to-purple-500 transform scale-x-0 group-hover:scale-x-100 transition-transform duration-300"></div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
const brands = [
  { id: 1, name: 'سامسونگ', icon: 'S', count: 356 },
  { id: 2, name: 'ال جی', icon: 'LG', count: 298 },
  { id: 3, name: 'بوش', icon: 'B', count: 245 },
  { id: 4, name: 'اسنوا', icon: 'SN', count: 187 },
  { id: 5, name: 'پارس خزر', icon: 'PK', count: 162 },
  { id: 6, name: 'دوو', icon: 'DW', count: 134 },
  { id: 7, name: 'جنرال', icon: 'G', count: 98 },
  { id: 8, name: 'ایندیزیت', icon: 'I', count: 87 },
  { id: 9, name: 'کنوود', icon: 'K', count: 76 },
  { id: 10, name: 'فلر', icon: 'F', count: 65 },
  { id: 11, name: 'بکو', icon: 'BK', count: 54 },
  { id: 12, name: 'آاگ', icon: 'AEG', count: 43 }
]
</script>