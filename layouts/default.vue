<template>
  <div class="min-h-screen flex flex-col">
    <!-- Navbar -->
    <Navbar />

    <!-- Page Content -->
    <main class="flex-grow">
      <slot />
    </main>

    <!-- Footer -->
    <Footer />
  </div>
</template>

<script setup>
import Navbar from '~/components/layout/Navbar.vue'
import Footer from '~/components/layout/Footer.vue'
</script>

<style>
/* استایل‌های کلی */
html {
  direction: rtl;
  scroll-behavior: smooth;
}

body {
  font-family: 'Vazir', 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}
</style>