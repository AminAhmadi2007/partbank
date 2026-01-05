<template>
  <div class="min-h-screen bg-gray-50">
    <!-- Hero Section -->
    <div class="bg-gradient-to-br from-blue-600 to-blue-800 text-white">
      <div class="container mx-auto px-4 py-16 md:py-24">
        <div class="max-w-4xl mx-auto text-center">
          <!-- Breadcrumb -->
          <nav class="flex items-center justify-center gap-2 text-sm text-blue-200 mb-8">
            <router-link to="/" class="hover:text-white transition">خانه</router-link>
            <span>/</span>
            <span class="font-medium">درباره ما</span>
          </nav>
          
          <!-- Title -->
          <h1 class="text-4xl md:text-5xl font-bold mb-6">
            درباره شرکت ما
          </h1>
          
          <!-- Description -->
          <p class="text-xl text-blue-100 mb-8 max-w-2xl mx-auto">
            بیش از ۱۰ سال تجربه در ارائه خدمات با کیفیت به مشتریان عزیز
          </p>
          
          <!-- Stats -->
          <div class="grid grid-cols-2 md:grid-cols-4 gap-6 mt-12">
            <div class="text-center">
              <div class="text-3xl font-bold mb-2">۱۲+</div>
              <div class="text-blue-200">سال تجربه</div>
            </div>
            <div class="text-center">
              <div class="text-3xl font-bold mb-2">۵۰۰۰+</div>
              <div class="text-blue-200">مشتری</div>
            </div>
            <div class="text-center">
              <div class="text-3xl font-bold mb-2">۹۸%</div>
              <div class="text-blue-200">رضایت</div>
            </div>
            <div class="text-center">
              <div class="text-3xl font-bold mb-2">۵۰+</div>
              <div class="text-blue-200">همکار</div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Our Story -->
    <div class="py-16">
      <div class="container mx-auto px-4">
        <div class="max-w-6xl mx-auto">
          <div class="grid grid-cols-1 lg:grid-cols-2 gap-12 items-center">
            <!-- Image -->
            <div class="relative">
              <div class="rounded-2xl overflow-hidden shadow-lg">
                <img src="https://images.unsplash.com/photo-1552664730-d307ca884978?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&q=80" 
                     alt="تیم ما" 
                     class="w-full h-80 object-cover">
              </div>
            </div>
            
            <!-- Content -->
            <div>
              <div class="inline-flex items-center gap-2 px-4 py-2 bg-blue-50 text-blue-700 rounded-full text-sm font-medium mb-6">
                <span>📖</span>
                داستان ما
              </div>
              
              <h2 class="text-3xl font-bold text-gray-900 mb-6">
                از یک ایده ساده شروع کردیم
              </h2>
              
              <p class="text-gray-600 mb-4">
                در سال ۱۳۹۰، گروهی از دوستان با اشتراک علاقه به تکنولوژی و خدمات، شرکت ما را تاسیس کردند. هدف ما ساده بود: ارائه بهترین خدمات با مناسب‌ترین قیمت.
              </p>
              
              <p class="text-gray-600 mb-6">
                امروز با افتخار اعلام می‌کنیم که تیم ما به ۵۰ متخصص مجرب در حوزه‌های مختلف تبدیل شده و توانسته‌ایم به بیش از ۵۰۰۰ مشتری رضایت ارائه دهیم.
              </p>
              
              <div class="flex items-center gap-4">
                <div class="flex items-center gap-2">
                  <div class="w-8 h-8 bg-green-100 rounded-lg flex items-center justify-center">
                    <span class="text-green-600">✓</span>
                  </div>
                  <span>کیفیت عالی</span>
                </div>
                <div class="flex items-center gap-2">
                  <div class="w-8 h-8 bg-blue-100 rounded-lg flex items-center justify-center">
                    <span class="text-blue-600">🤝</span>
                  </div>
                  <span>پشتیبانی ۲۴/۷</span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Our Values -->
    <div class="py-16 bg-white">
      <div class="container mx-auto px-4">
        <div class="max-w-4xl mx-auto text-center mb-12">
          <div class="inline-flex items-center gap-2 px-4 py-2 bg-blue-50 text-blue-700 rounded-full text-sm font-medium mb-4">
            <span>💎</span>
            ارزش‌های ما
          </div>
          <h2 class="text-3xl font-bold text-gray-900 mb-4">
            اصولی که باور داریم
          </h2>
          <p class="text-gray-600 max-w-2xl mx-auto">
            این اصول، راهنمای کار ما در تمام پروژه‌ها هستند
          </p>
        </div>
        
        <div class="grid grid-cols-1 md:grid-cols-3 gap-8 max-w-5xl mx-auto">
          <!-- Value 1 -->
          <div class="bg-gray-50 rounded-xl p-6 border border-gray-200">
            <div class="w-12 h-12 bg-blue-100 rounded-xl flex items-center justify-center mb-4">
              <span class="text-2xl text-blue-600">🎯</span>
            </div>
            <h3 class="text-xl font-bold text-gray-900 mb-3">مشتری اول</h3>
            <p class="text-gray-600">
              رضایت مشتریان در اولویت اول همه تصمیمات ما قرار دارد.
            </p>
          </div>
          
          <!-- Value 2 -->
          <div class="bg-gray-50 rounded-xl p-6 border border-gray-200">
            <div class="w-12 h-12 bg-green-100 rounded-xl flex items-center justify-center mb-4">
              <span class="text-2xl text-green-600">✨</span>
            </div>
            <h3 class="text-xl font-bold text-gray-900 mb-3">کیفیت بالا</h3>
            <p class="text-gray-600">
              از هیچ کاری برای ارائه بهترین کیفیت دریغ نمی‌کنیم.
            </p>
          </div>
          
          <!-- Value 3 -->
          <div class="bg-gray-50 rounded-xl p-6 border border-gray-200">
            <div class="w-12 h-12 bg-purple-100 rounded-xl flex items-center justify-center mb-4">
              <span class="text-2xl text-purple-600">🚀</span>
            </div>
            <h3 class="text-xl font-bold text-gray-900 mb-3">نوآوری</h3>
            <p class="text-gray-600">
              همیشه در حال یادگیری و استفاده از جدیدترین تکنولوژی‌ها هستیم.
            </p>
          </div>
        </div>
      </div>
    </div>

    <!-- Team -->
    <div class="py-16 bg-gray-50">
      <div class="container mx-auto px-4">
        <div class="max-w-4xl mx-auto text-center mb-12">
          <div class="inline-flex items-center gap-2 px-4 py-2 bg-blue-50 text-blue-700 rounded-full text-sm font-medium mb-4">
            <span>👥</span>
            تیم ما
          </div>
          <h2 class="text-3xl font-bold text-gray-900 mb-4">
            با تیم ما آشنا شوید
          </h2>
          <p class="text-gray-600 max-w-2xl mx-auto">
            متخصصان با تجربه‌ای که در کنار هم کار می‌کنند
          </p>
        </div>
        
        <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6 max-w-5xl mx-auto">
          <!-- Member 1 -->
          <div class="bg-white rounded-xl shadow-md overflow-hidden">
            <div class="h-48 overflow-hidden">
              <img src="https://images.unsplash.com/photo-1560250097-0b93528c311a?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&q=80" 
                   alt="مدیر عامل" 
                   class="w-full h-full object-cover">
            </div>
            <div class="p-4">
              <h3 class="font-bold text-gray-900">علی احمدی</h3>
              <div class="text-blue-600 text-sm mb-2">مدیر عامل</div>
              <p class="text-gray-600 text-sm">
                ۱۵ سال سابقه در مدیریت
              </p>
            </div>
          </div>
          
          <!-- Member 2 -->
          <div class="bg-white rounded-xl shadow-md overflow-hidden">
            <div class="h-48 overflow-hidden">
              <img src="https://images.unsplash.com/photo-1573496359142-b8d87734a5a2?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&q=80" 
                   alt="مدیر فنی" 
                   class="w-full h-full object-cover">
            </div>
            <div class="p-4">
              <h3 class="font-bold text-gray-900">فاطمه محمدی</h3>
              <div class="text-blue-600 text-sm mb-2">مدیر فنی</div>
              <p class="text-gray-600 text-sm">
                متخصص در توسعه نرم‌افزار
              </p>
            </div>
          </div>
          
          <!-- Member 3 -->
          <div class="bg-white rounded-xl shadow-md overflow-hidden">
            <div class="h-48 overflow-hidden">
              <img src="https://images.unsplash.com/photo-1551836026-d5c2c0b4d8a1?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&q=80" 
                   alt="مدیر بازاریابی" 
                   class="w-full h-full object-cover">
            </div>
            <div class="p-4">
              <h3 class="font-bold text-gray-900">رضا کریمی</h3>
              <div class="text-blue-600 text-sm mb-2">مدیر بازاریابی</div>
              <p class="text-gray-600 text-sm">
                متخصص در دیجیتال مارکتینگ
              </p>
            </div>
          </div>
          
          <!-- Member 4 -->
          <div class="bg-white rounded-xl shadow-md overflow-hidden">
            <div class="h-48 overflow-hidden">
              <img src="https://images.unsplash.com/photo-1580489944761-15a19d654956?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&q=80" 
                   alt="مدیر فروش" 
                   class="w-full h-full object-cover">
            </div>
            <div class="p-4">
              <h3 class="font-bold text-gray-900">سارا نجفی</h3>
              <div class="text-blue-600 text-sm mb-2">مدیر فروش</div>
              <p class="text-gray-600 text-sm">
                متخصص در توسعه کسب‌وکار
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- CTA -->
    <div class="py-16 bg-white">
      <div class="container mx-auto px-4">
        <div class="max-w-3xl mx-auto text-center">
          <h2 class="text-3xl font-bold text-gray-900 mb-6">
            آماده همکاری هستید؟
          </h2>
          
          <p class="text-gray-600 mb-8 max-w-2xl mx-auto">
            اگر به دنبال راه‌حلی برای کسب‌وکار خود هستید، با ما تماس بگیرید.
          </p>
          
          <div class="flex flex-col sm:flex-row gap-4 justify-center">
            <router-link to="/contact"
                         class="px-6 py-3 bg-blue-600 hover:bg-blue-700 text-white rounded-lg font-medium shadow hover:shadow-md transition">
              تماس با ما
            </router-link>
            
            <router-link to="/services"
                         class="px-6 py-3 border border-gray-300 hover:border-blue-400 text-gray-700 hover:text-blue-700 rounded-lg font-medium transition">
              خدمات ما
            </router-link>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
// Simple component - no complex logic needed
</script>

<style scoped>
/* Simple styling */
.container {
  max-width: 1200px;
}

/* Responsive adjustments */
@media (max-width: 768px) {
  .text-5xl {
    font-size: 2.5rem;
  }
  
  .text-3xl {
    font-size: 2rem;
  }
}
</style>