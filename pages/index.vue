<template>
  <div>
    <main>
      <!-- بخش قهرمان -->
      <HeroSection />
      
      <!-- دسته‌بندی‌های محبوب -->
      <CategoriesSection />
      
      <!-- محصولات ویژه -->
      <FeaturedProducts />
      
      <!-- محصولات پرفروش -->
      <BestSellingProducts />
      
      <!-- برندهای معتبر -->
      <BrandsSection />
      
      <!-- چرا ما -->
      <WhyUsSection />
      
      <!-- دستگاه‌های پرتعمیر -->
      <CommonRepairsSection />
      
      <!-- مقالات آموزشی -->
      <ArticlesSection />
      
      <!-- درخواست قطعه -->
      <RequestPartSection />
    </main>
  </div>
</template>

<script setup>
import '@fontsource/vazirmatn'
import ArticlesSection from '~/components/sections/ArticlesSection.vue';
import BestSellingProducts from '~/components/sections/BestSellingProducts.vue';
import BrandsSection from '~/components/sections/BrandsSection.vue';
import CategoriesSection from '~/components/sections/CategoriesSection.vue';
import CommonRepairsSection from '~/components/sections/CommonRepairsSection.vue';
import FeaturedProducts from '~/components/sections/FeaturedProducts.vue';
import HeroSection from '~/components/sections/HeroSection.vue';
import RequestPartSection from '~/components/sections/RequestPartSection.vue';
import WhyUsSection from '~/components/sections/WhyUsSection.vue';

useHead({
  htmlAttrs: {
    title:"partbank",
    lang: 'fa',
    dir: 'rtl'
  }
})
</script>

<style>
body {
  font-family: 'Vazirmatn', sans-serif;
}
</style>
