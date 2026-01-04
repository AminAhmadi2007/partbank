<template>
  <section class="relative py-12 md:py-20 bg-gradient-to-r from-blue-50 via-white to-gray-50 overflow-hidden">
    <!-- Background Pattern -->
    <div class="absolute inset-0 opacity-10">
      <div class="absolute top-10 left-10 w-72 h-72 bg-blue-300 rounded-full mix-blend-multiply filter blur-xl"></div>
      <div class="absolute bottom-10 right-10 w-72 h-72 bg-purple-300 rounded-full mix-blend-multiply filter blur-xl"></div>
    </div>
    
    <div class="container mx-auto px-4 relative">
      <div class="grid lg:grid-cols-2 gap-12 items-center">
        <!-- Content -->
        <div class="text-right">
          <div class="inline-flex items-center gap-2 bg-blue-100 text-blue-700 px-4 py-2 rounded-full mb-6">
            <span class="text-sm font-semibold">🛠️ مرجع تخصصی قطعات لوازم خانگی</span>
          </div>
          
          <h1 class="text-4xl md:text-5xl lg:text-6xl font-bold text-gray-900 leading-tight mb-6">
            <span class="text-blue-600">قطعات اورجینال</span><br>
            با کیفیت و گارانتی معتبر
          </h1>
          
          <p class="text-lg md:text-xl text-gray-600 mb-8 leading-relaxed">
            ارائه قطعات اصل با کیفیت عالی و تضمین اصالت کالا
            برای تمام برندهای داخلی و خارجی با ارسال سریع به سراسر کشور
          </p>
          
          <div class="flex flex-wrap gap-4 mb-8">
            <div class="flex items-center gap-2">
              <div class="w-8 h-8 bg-green-100 rounded-full flex items-center justify-center">
                <span class="text-green-600">✓</span>
              </div>
              <span class="text-gray-700">ضمانت اصالت کالا</span>
            </div>
            <div class="flex items-center gap-2">
              <div class="w-8 h-8 bg-green-100 rounded-full flex items-center justify-center">
                <span class="text-green-600">✓</span>
              </div>
              <span class="text-gray-700">ارسال سریع 24 ساعته</span>
            </div>
            <div class="flex items-center gap-2">
              <div class="w-8 h-8 bg-green-100 rounded-full flex items-center justify-center">
                <span class="text-green-600">✓</span>
              </div>
              <span class="text-gray-700">پشتیبانی 24/7</span>
            </div>
          </div>
          
          <div class="flex flex-col sm:flex-row gap-4">
            <button class="bg-blue-600 hover:bg-blue-700 text-white px-8 py-4 rounded-xl text-lg font-semibold shadow-lg hover:shadow-xl transition-all duration-300 transform hover:-translate-y-1 flex items-center justify-center gap-2">
              <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 11V7a4 4 0 00-8 0v4M5 9h14l1 12H4L5 9z" />
              </svg>
              خرید قطعات
            </button>
            <button class="bg-white hover:bg-gray-50 text-blue-600 border-2 border-blue-600 px-8 py-4 rounded-xl text-lg font-semibold shadow-md hover:shadow-lg transition-all duration-300 flex items-center justify-center gap-2">
              <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 12h.01M12 12h.01M16 12h.01M21 12c0 4.418-4.03 8-9 8a9.863 9.863 0 01-4.255-.949L3 20l1.395-3.72C3.512 15.042 3 13.574 3 12c0-4.418 4.03-8 9-8s9 3.582 9 8z" />
              </svg>
              مشاوره رایگان
            </button>
          </div>
        </div>
        
        <!-- Image/Illustration -->
        <div class="relative">
          <div class="relative bg-white rounded-2xl shadow-2xl overflow-hidden transform rotate-1 hover:rotate-0 transition-transform duration-300">
            <img src="https://images.unsplash.com/photo-1581094794329-c8112a89af12?auto=format&fit=crop&w=800&q=80" 
                 alt="قطعات لوازم خانگی"
                 class="w-full h-[500px] object-cover">
            <div class="absolute bottom-0 left-0 right-0 bg-gradient-to-t from-black/70 to-transparent p-6">
              <p class="text-white text-lg font-semibold">بیش از 5000 قطعه اورجینال در انبار</p>
            </div>
          </div>
          
          <!-- Floating Cards -->
          <div class="absolute -top-4 -right-4 bg-white p-4 rounded-xl shadow-lg">
            <div class="flex items-center gap-3">
              <div class="w-12 h-12 bg-blue-100 rounded-lg flex items-center justify-center">
                <span class="text-2xl">⚡</span>
              </div>
              <div>
                <p class="text-sm text-gray-500">ارسال سریع</p>
                <p class="font-bold text-gray-900">تهران 3 ساعته</p>
              </div>
            </div>
          </div>
          
          <div class="absolute -bottom-4 -left-4 bg-white p-4 rounded-xl shadow-lg">
            <div class="flex items-center gap-3">
              <div class="w-12 h-12 bg-green-100 rounded-lg flex items-center justify-center">
                <span class="text-2xl">🛡️</span>
              </div>
              <div>
                <p class="text-sm text-gray-500">گارانتی</p>
                <p class="font-bold text-gray-900">12 تا 24 ماه</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
// No data needed, just static content
</script>