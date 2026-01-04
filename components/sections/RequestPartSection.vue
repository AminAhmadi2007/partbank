<template>
  <section class="py-16 bg-gradient-to-r from-blue-600 to-blue-700">
    <div class="container mx-auto px-4">
      <div class="max-w-4xl mx-auto">
        <div class="text-center text-white mb-12">
          <h2 class="text-3xl md:text-4xl font-bold mb-4">قطعه مورد نظرتان را پیدا نکردید؟</h2>
          <p class="text-xl text-blue-100">قطعه مورد نیاز خود را ثبت کنید تا در کوتاه‌ترین زمان برایتان تأمین کنیم</p>
        </div>
        
        <div class="bg-white rounded-2xl shadow-2xl p-8">
          <form @submit.prevent="submitRequest" class="space-y-6">
            <!-- دستگاه مورد نظر -->
            <div>
              <label class="block text-gray-700 font-semibold mb-3">دستگاه مورد نظر</label>
              <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 gap-3">
                <div v-for="device in devices" :key="device.id"
                     @click="selectedDevice = device.id"
                     :class="['p-4 border-2 rounded-xl text-center cursor-pointer transition-all duration-200',
                              selectedDevice === device.id 
                                ? 'border-blue-600 bg-blue-50 text-blue-700' 
                                : 'border-gray-200 hover:border-gray-300 hover:bg-gray-50']">
                  <span class="text-2xl block mb-2">{{ device.icon }}</span>
                  <span class="text-sm font-medium">{{ device.name }}</span>
                </div>
              </div>
            </div>
            
            <!-- برند دستگاه -->
            <div>
              <label class="block text-gray-700 font-semibold mb-2">برند دستگاه</label>
              <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-5 gap-3">
                <div v-for="brand in brandOptions" :key="brand.id"
                     @click="selectedBrand = brand.id"
                     :class="['p-3 border rounded-lg text-center cursor-pointer transition',
                              selectedBrand === brand.id 
                                ? 'border-blue-600 bg-blue-50 text-blue-700' 
                                : 'border-gray-200 hover:border-gray-300']">
                  <span class="text-sm font-medium">{{ brand.name }}</span>
                </div>
              </div>
            </div>
            
            <!-- اطلاعات قطعه -->
            <div class="grid md:grid-cols-2 gap-6">
              <div>
                <label for="partName" class="block text-gray-700 font-semibold mb-2">نام قطعه</label>
                <input id="partName" v-model="form.partName" type="text" 
                       placeholder="مثال: کمپرسور، ترموستات، موتور و ..." 
                       class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 outline-none transition">
              </div>
              
              <div>
                <label for="modelNumber" class="block text-gray-700 font-semibold mb-2">مدل دستگاه</label>
                <input id="modelNumber" v-model="form.modelNumber" type="text" 
                       placeholder="مثال: RS50, F4-123, SMS46" 
                       class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 outline-none transition">
              </div>
            </div>
            
            <!-- توضیحات -->
            <div>
              <label for="description" class="block text-gray-700 font-semibold mb-2">توضیحات بیشتر</label>
              <textarea id="description" v-model="form.description" rows="4"
                        placeholder="در صورت داشتن تصویر یا شماره قطعه، اینجا وارد کنید. همچنین علائم خرابی دستگاه را شرح دهید."
                        class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 outline-none transition resize-none"></textarea>
            </div>
            
            <!-- اطلاعات تماس -->
            <div class="grid md:grid-cols-2 gap-6">
              <div>
                <label for="phone" class="block text-gray-700 font-semibold mb-2">شماره تماس</label>
                <input id="phone" v-model="form.phone" type="tel" 
                       placeholder="09xxxxxxxxx" 
                       class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 outline-none transition">
              </div>
              
              <div>
                <label for="city" class="block text-gray-700 font-semibold mb-2">شهر</label>
                <select id="city" v-model="form.city" 
                        class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 outline-none transition bg-white">
                  <option value="">انتخاب شهر</option>
                  <option value="tehran">تهران</option>
                  <option value="mashhad">مشهد</option>
                  <option value="isfahan">اصفهان</option>
                  <option value="shiraz">شیراز</option>
                  <option value="tabriz">تبریز</option>
                </select>
              </div>
            </div>
            
            <!-- دکمه‌های ارسال -->
            <div class="flex flex-col sm:flex-row gap-4">
              <button type="submit" 
                      class="flex-1 bg-blue-600 hover:bg-blue-700 text-white py-4 rounded-lg font-semibold text-lg transition shadow-lg hover:shadow-xl flex items-center justify-center gap-3">
                <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 19l9 2-9-18-9 18 9-2zm0 0v-8" />
                </svg>
                ارسال درخواست
              </button>
              
              <button type="button" @click="callSupport"
                      class="flex-1 bg-white border-2 border-blue-600 text-blue-600 hover:bg-blue-50 py-4 rounded-lg font-semibold text-lg transition flex items-center justify-center gap-3">
                <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z" />
                </svg>
                تماس با پشتیبانی
              </button>
            </div>
            
            <!-- نکات -->
            <div class="bg-blue-50 border border-blue-200 rounded-xl p-4 mt-6">
              <div class="flex items-start gap-3">
                <span class="text-blue-600">💡</span>
                <div class="text-sm text-blue-800">
                  <p class="font-semibold mb-2">نکات مهم:</p>
                  <ul class="list-disc pr-4 space-y-1">
                    <li>پس از ثبت درخواست، کارشناسان ما در اسرع وقت با شما تماس خواهند گرفت</li>
                    <li>حداکثر زمان پاسخگویی: 2 ساعت کاری</li>
                    <li>در صورت موجود بودن قطعه در انبار، ارسال در همان روز انجام می‌شود</li>
                    <li>برای قطعات نایاب، زمان تأمین حداکثر 72 ساعت کاری می‌باشد</li>
                  </ul>
                </div>
              </div>
            </div>
          </form>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'

const selectedDevice = ref(1)
const selectedBrand = ref(1)
const form = ref({
  partName: '',
  modelNumber: '',
  description: '',
  phone: '',
  city: ''
})

const devices = [
  { id: 1, name: 'یخچال', icon: '❄️' },
  { id: 2, name: 'لباسشویی', icon: '🧺' },
  { id: 3, name: 'ظرفشویی', icon: '🍽️' },
  { id: 4, name: 'اجاق گاز', icon: '🔥' },
  { id: 5, name: 'کولر', icon: '💨' },
  { id: 6, name: 'آبگرمکن', icon: '🚿' },
  { id: 7, name: 'جاروبرقی', icon: '🧹' },
  { id: 8, name: 'سایر', icon: '🔌' }
]

const brandOptions = [
  { id: 1, name: 'سامسونگ' },
  { id: 2, name: 'ال جی' },
  { id: 3, name: 'بوش' },
  { id: 4, name: 'اسنوا' },
  { id: 5, name: 'پارس خزر' },
  { id: 6, name: 'دوو' },
  { id: 7, name: 'جنرال' },
  { id: 8, name: 'ایندیزیت' },
  { id: 9, name: 'سایر' }
]

const submitRequest = () => {
  console.log('Form submitted:', form.value)
  // Submit form logic
  alert('درخواست شما با موفقیت ثبت شد. کارشناسان ما به زودی با شما تماس خواهند گرفت.')
  
  // Reset form
  form.value = {
    partName: '',
    modelNumber: '',
    description: '',
    phone: '',
    city: ''
  }
}

const callSupport = () => {
  window.location.href = 'tel:+982112345678'
}
</script>