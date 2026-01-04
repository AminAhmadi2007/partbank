<template>
  <section class="py-16 bg-gradient-to-b from-white to-gray-50">
    <div class="container mx-auto px-4">
      <div class="text-center mb-12">
        <div class="inline-flex items-center gap-2 bg-gradient-to-r from-orange-50 to-orange-100 text-orange-700 px-6 py-2 rounded-full mb-4">
          <span class="text-xl">🔧</span>
          <span class="font-semibold">دستگاه‌های پرتعمیر</span>
        </div>
        <h2 class="text-3xl md:text-4xl font-bold text-gray-900 mb-4">
          دستگاه‌های پرتعمیر و قطعات رایج
        </h2>
        <p class="text-lg text-gray-600 max-w-2xl mx-auto">
          قطعاتی که بیشترین درخواست تعمیر را دارند
        </p>
      </div>
      
      <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
        <div v-for="device in commonDevices" :key="device.id" 
             class="group relative">
          <div class="bg-white rounded-2xl shadow-lg hover:shadow-2xl transition-all duration-500 transform group-hover:-translate-y-2 h-full overflow-hidden border border-gray-200">
            <!-- Device Header -->
            <div class="bg-gradient-to-r from-blue-50 to-blue-100 p-6 relative overflow-hidden">
              <div class="absolute top-0 right-0 w-24 h-24 bg-blue-200/30 rounded-full -translate-y-12 translate-x-12"></div>
              <div class="absolute bottom-0 left-0 w-16 h-16 bg-blue-200/30 rounded-full translate-y-8 -translate-x-8"></div>
              
              <div class="relative z-10 flex items-center gap-4">
                <div class="w-20 h-20 bg-white rounded-2xl flex items-center justify-center shadow-lg">
                  <span class="text-4xl">{{ device.icon }}</span>
                </div>
                <div class="flex-1 text-right">
                  <h3 class="text-xl font-bold text-gray-900 mb-1">{{ device.name }}</h3>
                  <p class="text-gray-600">{{ device.description }}</p>
                </div>
              </div>
            </div>
            
            <!-- Common Parts -->
            <div class="p-6">
              <div class="flex items-center justify-between mb-6">
                <h4 class="font-bold text-gray-900 text-lg">قطعات پراستهلاک</h4>
                <span class="text-sm bg-blue-100 text-blue-600 px-4 py-2 rounded-full font-medium shadow-sm">
                  {{ device.commonParts.length }} قطعه
                </span>
              </div>
              
              <div class="space-y-4">
                <div v-for="part in device.commonParts" :key="part.id"
                     class="group/part flex items-center justify-between p-4 bg-gray-50 rounded-xl hover:bg-blue-50 transition-all duration-300 transform hover:-translate-y-1 cursor-pointer">
                  <div class="flex items-center gap-4">
                    <div class="w-12 h-12 bg-gradient-to-br from-blue-500 to-blue-600 rounded-xl flex items-center justify-center shadow-md">
                      <span class="text-xl text-white">🔩</span>
                    </div>
                    <div>
                      <p class="font-medium text-gray-900 group-hover/part:text-blue-700 transition-colors">{{ part.name }}</p>
                      <p class="text-xs text-gray-500 mt-1">{{ part.compatibility }}</p>
                    </div>
                  </div>
                  <div class="text-left">
                    <p class="font-bold text-gray-900 text-lg">{{ formatPrice(part.price) }}</p>
                    <p class="text-xs text-gray-500">تومان</p>
                  </div>
                </div>
              </div>
              
              <!-- Stats -->
              <div class="mt-8 pt-8 border-t border-gray-200">
                <div class="grid grid-cols-3 gap-4 text-center">
                  <div class="group/stat">
                    <p class="text-sm text-gray-500 mb-2">متوسط تعمیر</p>
                    <p class="font-bold text-gray-900 text-lg group-hover/stat:text-blue-700 transition-colors">{{ device.stats.avgRepair }}</p>
                  </div>
                  <div class="group/stat">
                    <p class="text-sm text-gray-500 mb-2">قطعات رایج</p>
                    <p class="font-bold text-gray-900 text-lg group-hover/stat:text-blue-700 transition-colors">{{ device.stats.commonPartsCount }}</p>
                  </div>
                  <div class="group/stat">
                    <p class="text-sm text-gray-500 mb-2">قیمت متوسط</p>
                    <p class="font-bold text-gray-900 text-lg group-hover/stat:text-blue-700 transition-colors">{{ formatPrice(device.stats.avgPrice) }}</p>
                  </div>
                </div>
              </div>
              
              <!-- View Button -->
              <button @click="viewDeviceParts(device)" 
                      class="mt-8 w-full bg-gradient-to-r from-blue-600 to-blue-700 hover:from-blue-700 hover:to-blue-800 text-white py-4 rounded-xl font-semibold transition-all duration-300 transform hover:scale-[1.02] shadow-lg hover:shadow-xl flex items-center justify-center gap-3 group/button">
                مشاهده قطعات این دستگاه
                <svg class="w-5 h-5 group-hover/button:translate-x-1 transition-transform" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3" />
                </svg>
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
const commonDevices = [
  {
    id: 1,
    name: 'یخچال و فریزر',
    icon: '❄️',
    description: 'قطعات سرمایشی و برقی',
    commonParts: [
      { id: 1, name: 'کمپرسور', compatibility: 'تمام برندها', price: 1850000 },
      { id: 2, name: 'ترموستات', compatibility: 'دماسنج', price: 75000 },
      { id: 3, name: 'فن اواپراتور', compatibility: 'تهویه داخلی', price: 320000 },
      { id: 4, name: 'برد کنترل', compatibility: 'مدار الکترونیکی', price: 980000 }
    ],
    stats: {
      avgRepair: '۲-۳ ساعت',
      commonPartsCount: 8,
      avgPrice: 850000
    }
  },
  {
    id: 2,
    name: 'ماشین لباسشویی',
    icon: '🧺',
    description: 'قطعات مکانیکی و الکتریکی',
    commonParts: [
      { id: 1, name: 'موتور (پمپ)', compatibility: 'الکتروموتور', price: 1250000 },
      { id: 2, name: 'المنت', compatibility: 'گرمایش آب', price: 145000 },
      { id: 3, name: 'تسمه', compatibility: 'انتقال نیرو', price: 45000 },
      { id: 4, name: 'سنسور سطح آب', compatibility: 'کنترل آب', price: 85000 }
    ],
    stats: {
      avgRepair: '۱-۲ ساعت',
      commonPartsCount: 12,
      avgPrice: 420000
    }
  },
  {
    id: 3,
    name: 'کولر گازی',
    icon: '💨',
    description: 'قطعات سرمایشی و تهویه',
    commonParts: [
      { id: 1, name: 'کمپرسور', compatibility: 'مدل R410A', price: 2150000 },
      { id: 2, name: 'فن داخلی', compatibility: 'پنل داخلی', price: 420000 },
      { id: 3, name: 'برد اینورتر', compatibility: 'کنترل دور', price: 1850000 },
      { id: 4, name: 'فیلتر', compatibility: 'تصفیه هوا', price: 65000 }
    ],
    stats: {
      avgRepair: '۲-۴ ساعت',
      commonPartsCount: 9,
      avgPrice: 1250000
    }
  }
]

const formatPrice = (price) => {
  return price.toLocaleString('fa-IR')
}

const viewDeviceParts = (device) => {
  console.log('View parts for:', device.name)
  // Navigate to device parts page
}
</script>