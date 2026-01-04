<template>
  <footer class="bg-gradient-to-b from-gray-900 to-black text-white">
    <!-- بخش بالایی فوتر -->
    <div class="container mx-auto px-4 py-12">
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8">
        
        <!-- ستون ۱: درباره آرا سرویس -->
        <div class="lg:col-span-2">
          <div class="flex items-center space-x-3 mb-6">
            <div class="flex items-center">
              <div class="text-3xl font-bold text-blue-400">آرا</div>
              <div class="text-3xl font-bold text-white mr-2">سرویس</div>
            </div>
            <span class="text-xs bg-gradient-to-r from-blue-600 to-blue-500 px-3 py-1 rounded-full">فروشگاه قطعات</span>
          </div>
          <p class="text-gray-300 mb-6 leading-relaxed">
            <span class="font-bold text-blue-300">آرا سرویس</span> با بیش از ۱۵ سال سابقه درخشان در زمینه خدمات لوازم خانگی، اکنون با راه‌اندازی فروشگاه تخصصی قطعات، کامل‌ترین مجموعه قطعات اصلی لوازم خانگی را با ضمانت اصالت و کیفیت ارائه می‌دهد. ما قطعات اورجینال برندهای معتبر جهانی را با بهترین قیمت و سریع‌ترین ارسال در اختیار شما قرار می‌دهیم.
          </p>
          
          <!-- اعتبار و گارانتی -->
          <div class="grid grid-cols-2 gap-4 mb-6">
            <div class="flex items-center gap-2">
              <div class="w-12 h-12 bg-blue-900/30 rounded-lg flex items-center justify-center">
                <svg class="w-6 h-6 text-blue-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
                </svg>
              </div>
              <div>
                <div class="text-sm text-gray-400">ضمانت</div>
                <div class="font-bold text-blue-300">۱۸ ماهه</div>
              </div>
            </div>
            
            <div class="flex items-center gap-2">
              <div class="w-12 h-12 bg-blue-900/30 rounded-lg flex items-center justify-center">
                <svg class="w-6 h-6 text-blue-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z" />
                </svg>
              </div>
              <div>
                <div class="text-sm text-gray-400">ارسال</div>
                <div class="font-bold text-blue-300">۲۴ ساعته</div>
              </div>
            </div>
          </div>
          
          <!-- شبکه‌های اجتماعی -->
          <div class="flex space-x-4 space-x-reverse">
            <a href="https://araservice.co" target="_blank" class="w-10 h-10 bg-gray-800 hover:bg-blue-600 rounded-full flex items-center justify-center transition-all duration-300 transform hover:-translate-y-1">
              <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24">
                <path d="M12 0c-6.627 0-12 5.373-12 12s5.373 12 12 12 12-5.373 12-12-5.373-12-12-12zm6.066 9.645c.183 4.04-2.83 8.544-8.164 8.544-1.622 0-3.131-.476-4.402-1.291 1.524.18 3.045-.244 4.252-1.189-1.256-.023-2.317-.854-2.684-1.995.451.086.895.061 1.298-.049-1.381-.278-2.335-1.522-2.304-2.853.388.215.83.344 1.301.359-1.279-.855-1.641-2.544-.889-3.835 1.416 1.738 3.533 2.881 5.92 3.001-.419-1.796.944-3.527 2.799-3.527.825 0 1.572.349 2.096.907.654-.128 1.27-.368 1.824-.697-.215.671-.67 1.233-1.263 1.589.581-.07 1.135-.224 1.649-.453-.384.578-.87 1.084-1.433 1.489z"/>
              </svg>
            </a>
            <a href="https://instagram.com/araservice" target="_blank" class="w-10 h-10 bg-gray-800 hover:bg-gradient-to-r from-purple-600 to-pink-600 rounded-full flex items-center justify-center transition-all duration-300 transform hover:-translate-y-1">
              <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24">
                <path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zm0-2.163c-3.259 0-3.667.014-4.947.072-4.358.2-6.78 2.618-6.98 6.98-.059 1.281-.073 1.689-.073 4.948 0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98 1.281.058 1.689.072 4.948.072 3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98-1.281-.059-1.69-.073-4.949-.073zM5.838 12a6.162 6.162 0 1112.324 0 6.162 6.162 0 01-12.324 0zM12 16a4 4 0 110-8 4 4 0 010 8zm4.965-10.405a1.44 1.44 0 112.881.001 1.44 1.44 0 01-2.881-.001z"/>
              </svg>
            </a>
            <a href="https://facebook.com/araservice" target="_blank" class="w-10 h-10 bg-gray-800 hover:bg-blue-700 rounded-full flex items-center justify-center transition-all duration-300 transform hover:-translate-y-1">
              <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24">
                <path d="M24 12.073c0-6.627-5.373-12-12-12s-12 5.373-12 12c0 5.99 4.388 10.954 10.125 11.854v-8.385H7.078v-3.47h3.047V9.43c0-3.007 1.792-4.669 4.533-4.669 1.312 0 2.686.235 2.686.235v2.953H15.83c-1.491 0-1.956.925-1.956 1.874v2.25h3.328l-.532 3.47h-2.796v8.385C19.612 23.027 24 18.062 24 12.073z"/>
              </svg>
            </a>
            <a href="https://araservice.co/contact" target="_blank" class="w-10 h-10 bg-gray-800 hover:bg-red-600 rounded-full flex items-center justify-center transition-all duration-300 transform hover:-translate-y-1">
              <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 4.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
              </svg>
            </a>
          </div>
        </div>

        <!-- ستون ۲: دسته‌بندی قطعات -->
        <div>
          <h3 class="text-xl font-bold mb-6 pb-3 border-b border-gray-700 flex items-center">
            <svg class="w-5 h-5 ml-2 text-blue-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 11H5m14 0a2 2 0 012 2v6a2 2 0 01-2 2H5a2 2 0 01-2-2v-6a2 2 0 012-2m14 0V9a2 2 0 00-2-2M5 11V9a2 2 0 012-2m0 0V5a2 2 0 012-2h6a2 2 0 012 2v2M7 7h10" />
            </svg>
            دسته‌بندی قطعات
          </h3>
          <ul class="space-y-3">
            <li v-for="category in categories" :key="category.id">
              <a :href="`https://araservice.co/category/${category.id}`" target="_blank" class="text-gray-300 hover:text-blue-400 transition-all duration-300 hover:pr-3 flex items-center group">
                <svg class="w-4 h-4 ml-2 text-gray-500 group-hover:text-blue-400 transform group-hover:translate-x-1 transition-transform" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
                </svg>
                {{ category.name }}
              </a>
            </li>
            <li>
              <a href="https://araservice.co/categories" target="_blank" class="text-blue-400 hover:text-blue-300 transition-colors flex items-center font-medium mt-4">
                <svg class="w-5 h-5 ml-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3" />
                </svg>
                مشاهده تمام دسته‌بندی‌ها در آرا سرویس
              </a>
            </li>
          </ul>
        </div>

        <!-- ستون ۳: خدمات آرا سرویس -->
        <div>
          <h3 class="text-xl font-bold mb-6 pb-3 border-b border-gray-700 flex items-center">
            <svg class="w-5 h-5 ml-2 text-blue-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z" />
            </svg>
            خدمات آرا سرویس
          </h3>
          <ul class="space-y-3">
            <li>
              <a href="https://araservice.co/services/repair" target="_blank" class="text-gray-300 hover:text-blue-400 transition-colors flex items-center group">
                <div class="w-2 h-2 bg-blue-500 rounded-full ml-3 group-hover:scale-125 transition-transform"></div>
                تعمیرات تخصصی لوازم خانگی
              </a>
            </li>
            <li>
              <a href="https://araservice.co/services/installation" target="_blank" class="text-gray-300 hover:text-blue-400 transition-colors flex items-center group">
                <div class="w-2 h-2 bg-blue-500 rounded-full ml-3 group-hover:scale-125 transition-transform"></div>
                نصب و راه‌اندازی حرفه‌ای
              </a>
            </li>
            <li>
              <a href="https://araservice.co/services/maintenance" target="_blank" class="text-gray-300 hover:text-blue-400 transition-colors flex items-center group">
                <div class="w-2 h-2 bg-blue-500 rounded-full ml-3 group-hover:scale-125 transition-transform"></div>
                سرویس دوره‌ای و نگهداری
              </a>
            </li>
            <li>
              <a href="https://araservice.co/services/consultation" target="_blank" class="text-gray-300 hover:text-blue-400 transition-colors flex items-center group">
                <div class="w-2 h-2 bg-blue-500 rounded-full ml-3 group-hover:scale-125 transition-transform"></div>
                مشاوره فنی رایگان
              </a>
            </li>
            <li>
              <a href="https://araservice.co/services/warranty" target="_blank" class="text-gray-300 hover:text-blue-400 transition-colors flex items-center group">
                <div class="w-2 h-2 bg-blue-500 rounded-full ml-3 group-hover:scale-125 transition-transform"></div>
                خدمات گارانتی و پس از فروش
              </a>
            </li>
          </ul>
          
          <!-- دکمه خدمات اصلی -->
          <div class="mt-6">
            <a href="https://araservice.co" target="_blank" class="inline-flex items-center px-4 py-2 bg-gradient-to-r from-blue-600 to-blue-700 hover:from-blue-700 hover:to-blue-800 rounded-lg transition-all duration-300 transform hover:-translate-y-1 hover:shadow-lg">
              <svg class="w-5 h-5 ml-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z" />
              </svg>
              مشاهده همه خدمات آرا سرویس
            </a>
          </div>
        </div>

        <!-- ستون ۴: تماس با آرا سرویس -->
        <div>
          <h3 class="text-xl font-bold mb-6 pb-3 border-b border-gray-700 flex items-center">
            <svg class="w-5 h-5 ml-2 text-blue-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z" />
            </svg>
            ارتباط با آرا سرویس
          </h3>
          <div class="space-y-4">
            <div class="flex items-start group">
              <div class="w-10 h-10 bg-blue-900/30 rounded-lg flex items-center justify-center ml-3 group-hover:bg-blue-600 transition-colors">
                <svg class="w-5 h-5 text-blue-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z" />
                </svg>
              </div>
              <div>
                <div class="text-gray-400 text-sm">پشتیبانی تلفنی</div>
                <a href="tel:02188888888" class="text-lg font-bold hover:text-blue-300 transition-colors">۰۲۱-۸۸۸۸۸۸۸۸</a>
                <div class="text-xs text-gray-500 mt-1">شنبه تا پنجشنبه ۸ الی ۲۲</div>
              </div>
            </div>
            
            <div class="flex items-start group">
              <div class="w-10 h-10 bg-blue-900/30 rounded-lg flex items-center justify-center ml-3 group-hover:bg-blue-600 transition-colors">
                <svg class="w-5 h-5 text-blue-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 4.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
                </svg>
              </div>
              <div>
                <div class="text-gray-400 text-sm">ایمیل پشتیبانی</div>
                <a href="mailto:support@araservice.co" class="text-lg hover:text-blue-300 transition-colors">support@araservice.co</a>
              </div>
            </div>
            
            <div class="flex items-start group">
              <div class="w-10 h-10 bg-blue-900/30 rounded-lg flex items-center justify-center ml-3 group-hover:bg-blue-600 transition-colors">
                <svg class="w-5 h-5 text-blue-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z" />
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z" />
                </svg>
              </div>
              <div>
                <div class="text-gray-400 text-sm">دفتر مرکزی</div>
                <div class="text-sm">تهران، خیابان ولیعصر، پلاک ۱۲۳۴</div>
                <a href="https://maps.google.com/?q=آدرس+آرا+سرویس" target="_blank" class="text-xs text-blue-400 hover:text-blue-300 mt-1 inline-flex items-center">
                  مشاهده روی نقشه
                  <svg class="w-3 h-3 mr-1" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14" />
                  </svg>
                </a>
              </div>
            </div>
          </div>
          
          <!-- خبرنامه آرا سرویس -->
          
        </div>
      </div>
    </div>

    <!-- بخش میانی: اعتبارسنجی -->
    

    <!-- بخش پایینی -->
    <div class="bg-black/50 py-6">
      <div class="container mx-auto px-4">
        <div class="flex flex-col md:flex-row items-center justify-between space-y-4 md:space-y-0 border-t border-gray-800 pt-6">
          <!-- کپی‌رایت و لینک اصلی -->
          <div class="text-gray-400 text-sm text-center md:text-right">
            <p class="mb-2">
              <a href="https://araservice.co" target="_blank" class="text-blue-400 hover:text-blue-300 font-bold">آرا سرویس</a> 
              - ارائه‌دهنده خدمات تخصصی لوازم خانگی از سال ۱۳۸۸
            </p>
            <p>کلیه حقوق این وب‌سایت متعلق به مجموعه <span class="text-blue-300">آرا سرویس</span> می‌باشد © ۱۴۰۳</p>
          </div>
          
          <!-- قوانین و لینک‌ها -->
          <div class="flex flex-wrap justify-center gap-4 text-sm">
            <a href="https://araservice.co/privacy" target="_blank" class="text-gray-400 hover:text-white transition-colors hover:underline">
              حریم خصوصی
            </a>
            <a href="https://araservice.co/terms" target="_blank" class="text-gray-400 hover:text-white transition-colors hover:underline">
              قوانین و مقررات
            </a>
            <a href="https://araservice.co/faq" target="_blank" class="text-gray-400 hover:text-white transition-colors hover:underline">
              سوالات متداول
            </a>
            <a href="https://araservice.co/contact" target="_blank" class="text-blue-400 hover:text-blue-300 transition-colors font-medium">
              تماس با آرا سرویس
            </a>
          </div>
        </div>
      </div>
    </div>
  </footer>
</template>

<script setup>
// استفاده از همان داده‌های نوبار برای سازگاری
const categories = [
  { id: 1, name: 'قطعات یخچال و فریزر' },
  { id: 2, name: 'قطعات ماشین لباسشویی' },
  { id: 3, name: 'قطعات ماشین ظرفشویی' },
  { id: 4, name: 'قطعات اجاق گاز' },
  { id: 5, name: 'قطعات کولر و تهویه' },
  { id: 6, name: 'بردهای الکترونیکی' }
]
</script>

<style scoped>
/* انیمیشن‌های حرفه‌ای */
footer {
  direction: rtl;
}

.transition-all {
  transition-property: all;
}

/* سایه‌های زیبا */
.shadow-lg {
  box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
}

/* هایلایت لینک‌ها */
.hover\:underline:hover {
  text-decoration: underline;
}

/* استایل برای اینپوت ایمیل */
input:focus {
  outline: none;
  box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.1);
}

/* گرادیانت زیبا */
.bg-gradient-to-b {
  background-image: linear-gradient(to bottom, var(--tw-gradient-stops));
}

/* استایل‌های سفارشی */
.group:hover .group-hover\:translate-x-1 {
  transform: translateX(4px);
}

/* انیمیشن دکمه‌های اجتماعی */
.transform {
  transition-duration: 300ms;
}
</style>