<template>
  <section class="py-16 bg-white">
    <div class="container mx-auto px-4">
      <div class="flex flex-col md:flex-row justify-between items-start md:items-center mb-12 gap-4">
        <div>
          <div class="inline-flex items-center gap-2 bg-gradient-to-r from-purple-50 to-purple-100 text-purple-700 px-6 py-2 rounded-full mb-4">
            <span class="text-xl">📚</span>
            <span class="font-semibold">مقالات آموزشی</span>
          </div>
          <h2 class="text-3xl md:text-4xl font-bold text-gray-900 mb-2">
            مقالات و آموزش‌ها
          </h2>
          <p class="text-lg text-gray-600">آموزش تعمیر و نگهداری لوازم خانگی</p>
        </div>
        
        <a href="/articles" class="text-blue-600 hover:text-blue-700 font-semibold flex items-center gap-2 group">
          همه مقالات
          <svg class="w-5 h-5 group-hover:translate-x-1 transition-transform" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3" />
          </svg>
        </a>
      </div>
      
      <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
        <div v-for="article in articles" :key="article.id" 
             class="group relative">
          <div class="bg-white rounded-2xl shadow-lg hover:shadow-2xl transition-all duration-500 transform hover:-translate-y-2 h-full overflow-hidden border border-gray-200">
            <!-- Article Image -->
            <div class="relative h-48 overflow-hidden">
              <div :class="[
                'w-full h-full flex items-center justify-center transition-transform duration-700 group-hover:scale-110',
                article.category === 'یخچال' ? 'bg-gradient-to-br from-blue-100 to-blue-200' :
                article.category === 'لباسشویی' ? 'bg-gradient-to-br from-purple-100 to-purple-200' :
                'bg-gradient-to-br from-green-100 to-green-200'
              ]">
                <div class="w-32 h-32 bg-white/80 rounded-2xl flex items-center justify-center shadow-lg">
                  <span class="text-6xl">{{ article.icon }}</span>
                </div>
              </div>
              <div class="absolute top-4 right-4">
                <span class="bg-white/90 backdrop-blur-sm text-gray-900 text-sm font-bold px-4 py-2 rounded-full shadow-sm">
                  {{ article.category }}
                </span>
              </div>
            </div>
            
            <!-- Article Content -->
            <div class="p-6">
              <div class="flex items-center gap-4 text-sm text-gray-500 mb-4">
                <div class="flex items-center gap-2">
                  <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z" />
                  </svg>
                  <span>{{ article.readTime }}</span>
                </div>
                <div class="flex items-center gap-2">
                  <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z" />
                  </svg>
                  <span>{{ article.date }}</span>
                </div>
              </div>
              
              <h3 class="text-xl font-bold text-gray-900 mb-4 line-clamp-2 group-hover:text-blue-700 transition-colors">{{ article.title }}</h3>
              <p class="text-gray-600 mb-6 line-clamp-3">{{ article.excerpt }}</p>
              
              <div class="flex items-center justify-between">
                <div class="flex items-center gap-3">
                  <div class="w-12 h-12 bg-gradient-to-br from-blue-500 to-blue-600 rounded-full flex items-center justify-center shadow-md">
                    <span class="text-white font-bold text-lg">{{ article.author.initials }}</span>
                  </div>
                  <div>
                    <p class="font-medium text-gray-900">{{ article.author.name }}</p>
                    <p class="text-xs text-gray-500">{{ article.author.role }}</p>
                  </div>
                </div>
                
                <a :href="article.link" 
                   class="text-blue-600 hover:text-blue-700 flex items-center gap-2 text-sm font-semibold group/link">
                  مطالعه مقاله
                  <svg class="w-4 h-4 group-hover/link:translate-x-1 transition-transform" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3" />
                  </svg>
                </a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
const articles = [
  {
    id: 1,
    title: 'آموزش تعویض کمپرسور یخچال در 7 مرحله',
    excerpt: 'کمپرسور قلب یخچال است. در این مقاله یاد می‌گیرید چگونه کمپرسور معیوب را تشخیص داده و آن را به درستی تعویض کنید.',
    icon: '❄️',
    category: 'یخچال',
    readTime: '8 دقیقه',
    date: '۱۴۰۲/۱۱/۱۵',
    author: {
      name: 'مهندس رضایی',
      role: 'متخصص تعمیرات',
      initials: 'م.ر'
    },
    link: '/articles/1'
  },
  {
    id: 2,
    title: 'شناسایی و تعویض برد کنترل ماشین لباسشویی',
    excerpt: 'برد کنترل مغز الکترونیکی لباسشویی است. با علائم خرابی آن آشنا شده و روش تعویض صحیح را بیاموزید.',
    icon: '🧺',
    category: 'لباسشویی',
    readTime: '10 دقیقه',
    date: '۱۴۰۲/۱۱/۱۲',
    author: {
      name: 'مهندس کریمی',
      role: 'تکنسین الکترونیک',
      initials: 'م.ک'
    },
    link: '/articles/2'
  },
  {
    id: 3,
    title: 'نگهداری و سرویس دوره‌ای کولر گازی',
    excerpt: 'با رعایت نکات ساده نگهداری، عمر کولر گازی خود را افزایش داده و از مصرف انرژی بی‌رویه جلوگیری کنید.',
    icon: '💨',
    category: 'کولر',
    readTime: '6 دقیقه',
    date: '۱۴۰۲/۱۱/۱۰',
    author: {
      name: 'مهندس محمدی',
      role: 'کارشناس تهویه',
      initials: 'م.م'
    },
    link: '/articles/3'
  }
]
</script>