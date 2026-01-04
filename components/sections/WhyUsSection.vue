<template>
  <section class="py-16 bg-white">
    <div class="container mx-auto px-4">
      <div class="text-center mb-12">
        <div class="inline-flex items-center gap-2 bg-gradient-to-r from-green-50 to-green-100 text-green-700 px-6 py-2 rounded-full mb-4">
          <span class="text-xl">✨</span>
          <span class="font-semibold">چرا ما؟</span>
        </div>
        <h2 class="text-3xl md:text-4xl font-bold text-gray-900 mb-4">
          چرا قطعه بازار را انتخاب کنید؟
        </h2>
        <p class="text-lg text-gray-600 max-w-2xl mx-auto">
          مزایای خرید از بزرگترین مرجع قطعات لوازم خانگی
        </p>
      </div>
      
      <div class="grid md:grid-cols-2 lg:grid-cols-4 gap-8">
        <div v-for="feature in features" :key="feature.id" 
             class="group relative">
          <div class="bg-white rounded-2xl p-8 text-center hover:shadow-2xl transition-all duration-500 transform hover:-translate-y-2 h-full border border-gray-200 overflow-hidden">
            <!-- Background Effect -->
            <div class="absolute inset-0 bg-gradient-to-br from-blue-50/30 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300"></div>
            
            <div class="relative z-10">
              <div class="w-24 h-24 mx-auto mb-6">
                <div class="w-full h-full bg-gradient-to-br from-blue-500 to-blue-600 rounded-2xl flex items-center justify-center transform group-hover:scale-110 group-hover:rotate-3 transition-all duration-500 shadow-lg">
                  <span class="text-4xl text-white">{{ feature.icon }}</span>
                </div>
              </div>
              <h3 class="text-xl font-bold text-gray-900 mb-4 group-hover:text-blue-700 transition-colors">{{ feature.title }}</h3>
              <p class="text-gray-600 leading-relaxed mb-6">{{ feature.description }}</p>
              
              <div class="mt-6 pt-6 border-t border-gray-200">
                <div class="flex items-center justify-center gap-6 text-sm">
                  <div class="flex items-center gap-2">
                    <div class="w-3 h-3 bg-green-500 rounded-full"></div>
                    <span class="text-gray-700 font-medium">{{ feature.stats.value1 }}</span>
                  </div>
                  <div class="flex items-center gap-2">
                    <div class="w-3 h-3 bg-blue-500 rounded-full"></div>
                    <span class="text-gray-700 font-medium">{{ feature.stats.value2 }}</span>
                  </div>
                </div>
              </div>
            </div>
            
            <!-- Hover Effect -->
            <div class="absolute bottom-0 left-0 right-0 h-1 bg-gradient-to-r from-blue-500 to-purple-500 transform scale-x-0 group-hover:scale-x-100 transition-transform duration-300"></div>
          </div>
        </div>
      </div>
      
      <!-- Stats Section -->
      <div class="mt-16 bg-gradient-to-r from-blue-600 to-blue-700 rounded-2xl p-8 text-white shadow-2xl">
        <div class="grid grid-cols-2 md:grid-cols-4 gap-8">
          <div v-for="stat in stats" :key="stat.id" class="text-center group">
            <div class="text-4xl md:text-5xl font-bold mb-2 transform group-hover:scale-110 transition-transform duration-300">{{ stat.value }}</div>
            <p class="text-blue-100 group-hover:text-white transition-colors">{{ stat.label }}</p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
const features = [
  {
    id: 1,
    icon: '🛡️',
    title: 'گارانتی معتبر',
    description: 'تمامی قطعات با گارانتی 12 تا 24 ماهه ارائه می‌شوند',
    stats: { value1: '12-24 ماه', value2: 'ضمانت اصالت' }
  },
  {
    id: 2,
    icon: '🚚',
    title: 'ارسال سریع',
    description: 'ارسال به سراسر ایران در کوتاه‌ترین زمان ممکن',
    stats: { value1: 'تهران 3 ساعته', value2: 'شهرستان 24 ساعته' }
  },
  {
    id: 3,
    icon: '🔧',
    title: 'مشاوره تخصصی',
    description: 'تیم فنی متخصص برای تشخیص و انتخاب قطعه مناسب',
    stats: { value1: '24/7', value2: 'رایگان' }
  },
  {
    id: 4,
    icon: '📦',
    title: 'انبار کامل',
    description: 'بیش از 5000 نوع قطعه اورجینال در انبار آماده',
    stats: { value1: '5000+', value2: 'اورجینال' }
  }
]

const stats = [
  { id: 1, value: '۵۰۰۰+', label: 'نوع قطعه' },
  { id: 2, value: '۱۲۴۵۶', label: 'مشتری راضی' },
  { id: 3, value: '۹۸%', label: 'رضایت مشتری' },
  { id: 4, value: '۲۴/۷', label: 'پشتیبانی' }
]
</script>