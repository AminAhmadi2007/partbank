<template>
  <div class="min-h-screen bg-gray-50 flex items-center justify-center p-4">
    <div class="w-full sm:w-3/4 md:w-2/4 lg:w-full max-w-4xl">
      <!-- Auth Card - ارتفاع ثابت -->
      <div class="bg-white rounded-2xl shadow-xl overflow-hidden border border-gray-200 h-[620px]">
        <!-- تغییر اصلی: اضافه کردن h-[620px] و overflow-hidden -->
        <div class="flex flex-col lg:flex-row h-full">
          <!-- Left Side - Form -->
          <div class="lg:w-1/2 p-8 lg:p-12 overflow-y-auto">
            <!-- تغییر: اضافه کردن overflow-y-auto برای اسکرول داخل فرم -->
            
            <!-- Toggle Buttons -->
            <div class="flex border-b border-gray-200 mb-6">
              <!-- کاهش margin-bottom برای فشرده‌تر شدن -->
              <button @click="setMode('login')" 
                      :class="[
                        'flex-1 py-3 font-semibold text-lg transition-all duration-300',
                        mode === 'login' 
                          ? 'text-blue-600 border-b-2 border-blue-600' 
                          : 'text-gray-500 hover:text-gray-700'
                      ]">
                ورود
              </button>
              <button @click="setMode('register')" 
                      :class="[
                        'flex-1 py-3 font-semibold text-lg transition-all duration-300',
                        mode === 'register' 
                          ? 'text-blue-600 border-b-2 border-blue-600' 
                          : 'text-gray-500 hover:text-gray-700'
                      ]">
                ثبت‌نام
              </button>
            </div>

            <!-- Form Container با ارتفاع ثابت -->
            <div class="h-[calc(100%-60px)]">
              <!-- Validation Messages -->
              <div v-if="validationErrors.length" class="mb-4 p-3 bg-red-50 border border-red-200 rounded-lg">
                <ul class="list-disc list-inside space-y-1">
                  <li v-for="error in validationErrors" :key="error" class="text-red-600 text-sm">
                    {{ error }}
                  </li>
                </ul>
              </div>

              <!-- Form با spacing فشرده‌تر -->
              <form @submit.prevent="handleSubmit" class="space-y-4">
                <!-- کاهش space-y از 6 به 4 -->

                <!-- Full Name (Register only) -->
                <div v-if="mode === 'register'" class="space-y-2">
                  <label class="block text-gray-700 font-medium text-sm">
                    نام و نام خانوادگی
                  </label>
                  <input v-model="form.fullName" type="text" required
                         placeholder="علی محمدی" 
                         :class="[
                           'w-full px-4 py-2.5 border rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 outline-none transition text-sm',
                           errors.fullName ? 'border-red-500' : 'border-gray-300'
                         ]">
                  <span v-if="errors.fullName" class="text-red-500 text-xs">{{ errors.fullName }}</span>
                </div>

                <!-- Phone Number -->
                <div class="space-y-2">
                  <label class="block text-gray-700 font-medium text-sm">
                    شماره موبایل
                  </label>
                  <input v-model="form.phone" type="tel" required
                         placeholder="09123456789" 
                         :class="[
                           'w-full px-4 py-2.5 border rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 outline-none transition text-sm text-left',
                           errors.phone ? 'border-red-500' : 'border-gray-300'
                         ]"
                         dir="ltr">
                  <span v-if="errors.phone" class="text-red-500 text-xs">{{ errors.phone }}</span>
                </div>

                <!-- Password -->
                <div class="space-y-2">
                  <label class="block text-gray-700 font-medium text-sm">
                    رمز عبور
                  </label>
                  <div class="relative">
                    <input v-model="form.password" :type="showPassword ? 'text' : 'password'" required
                           :placeholder="mode === 'login' ? 'رمز عبور' : 'حداقل ۶ کاراکتر'" 
                           :class="[
                             'w-full px-4 py-2.5 border rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 outline-none transition text-sm pr-12',
                             errors.password ? 'border-red-500' : 'border-gray-300'
                           ]">
                    <button type="button" @click="showPassword = !showPassword" 
                            class="absolute left-3 top-1/2 -translate-y-1/2 text-gray-400 hover:text-blue-500">
                      <svg v-if="showPassword" class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13.875 18.825A10.05 10.05 0 0112 19c-4.478 0-8.268-2.943-9.543-7a9.97 9.97 0 011.563-3.029m5.858.908a3 3 0 114.243 4.243M9.878 9.878l4.242 4.242M9.878 9.878L6.59 6.59m7.532 7.532l3.29 3.29M3 3l3.59 3.59m0 0A9.953 9.953 0 0112 5c4.478 0 8.268 2.943 9.543 7a10.025 10.025 0 01-4.132 5.411m0 0L21 21" />
                      </svg>
                      <svg v-else class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z" />
                      </svg>
                    </button>
                  </div>
                  <span v-if="errors.password" class="text-red-500 text-xs">{{ errors.password }}</span>
                </div>

                <!-- Confirm Password (Register only) -->
                <div v-if="mode === 'register'" class="space-y-2">
                  <label class="block text-gray-700 font-medium text-sm">
                    تکرار رمز عبور
                  </label>
                  <input v-model="form.confirmPassword" :type="showPassword ? 'text' : 'password'" required
                         placeholder="تکرار رمز عبور" 
                         :class="[
                           'w-full px-4 py-2.5 border rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 outline-none transition text-sm',
                           errors.confirmPassword ? 'border-red-500' : 'border-gray-300'
                         ]">
                  <span v-if="errors.confirmPassword" class="text-red-500 text-xs">{{ errors.confirmPassword }}</span>
                </div>

                <!-- Remember Me & Terms -->
                <div class="pt-2">
                  <div v-if="mode === 'login'" class="flex items-center justify-between mb-4">
                    <label class="flex items-center gap-2 cursor-pointer">
                      <input v-model="form.remember" type="checkbox" class="w-4 h-4 text-blue-600 rounded border-gray-300">
                      <span class="text-gray-600 text-sm">مرا به خاطر بسپار</span>
                    </label>
                    
                    <a href="/forgot-password" class="text-blue-600 hover:text-blue-700 text-sm">
                      فراموشی رمز؟
                    </a>
                  </div>

                  <div v-if="mode === 'register'" class="flex items-start gap-3 mb-4">
                    <input v-model="form.acceptTerms" type="checkbox" required
                           class="w-4 h-4 mt-0.5 text-blue-600 rounded border-gray-300">
                    <label class="text-gray-600 text-sm leading-relaxed">
                      با 
                      <a href="/terms" class="text-blue-600 hover:text-blue-700">قوانین</a>
                      موافقم
                    </label>
                  </div>

                  <!-- Submit Button -->
                  <button type="submit" 
                          :disabled="isSubmitting"
                          :class="[
                            'w-full py-2.5 rounded-lg font-semibold transition shadow-sm hover:shadow mt-2',
                            isSubmitting 
                              ? 'bg-blue-400 cursor-not-allowed' 
                              : 'bg-blue-600 hover:bg-blue-700 text-white'
                          ]">
                    <span v-if="isSubmitting">در حال پردازش...</span>
                    <span v-else>{{ mode === 'login' ? 'ورود به حساب' : 'ثبت‌نام' }}</span>
                  </button>
                </div>

                <!-- Alternative Login -->
                <div v-if="mode === 'login'" class="relative my-4">
                  <!-- کاهش my-6 به my-4 -->
                  <div class="absolute inset-0 flex items-center">
                    <div class="w-full border-t border-gray-200"></div>
                  </div>
                  <div class="relative flex justify-center text-sm">
                    <span class="px-4 bg-white text-gray-500">یا ورود با</span>
                  </div>
                </div>

                <!-- Social Buttons (Login only) -->
                <div v-if="mode === 'login'" class="grid grid-cols-2 gap-3 pt-2">
                  <button type="button" 
                          class="flex items-center justify-center gap-2 py-2.5 bg-gray-50 hover:bg-gray-100 rounded-lg border border-gray-200 transition text-sm">
                    <span class="text-lg">G</span>
                    <span>گوگل</span>
                  </button>
                  <button type="button" 
                          class="flex items-center justify-center gap-2 py-2.5 bg-blue-50 hover:bg-blue-100 rounded-lg border border-blue-200 transition text-sm">
                    <span class="text-lg">ت</span>
                    <span>تیکت</span>
                  </button>
                </div>
              </form>

              <!-- Bottom Link -->
              <div class="mt-6 pt-4 border-t border-gray-200 text-center">
                <!-- کاهش margin و padding -->
                <p class="text-gray-600 text-sm">
                  {{ mode === 'login' ? 'حساب کاربری ندارید؟' : 'قبلاً حساب دارید؟' }}
                  <button type="button" @click="toggleMode" 
                          class="text-blue-600 hover:text-blue-700 font-semibold mr-1">
                    {{ mode === 'login' ? 'ثبت‌نام کنید' : 'وارد شوید' }}
                  </button>
                </p>
              </div>
            </div>
          </div>

          <!-- Right Side - Image/Content (ارتفاع ثابت) -->
          <div class="hidden lg:block lg:w-1/2 bg-gradient-to-br from-blue-600 to-blue-800 p-8 lg:p-12 text-white h-full">
            <!-- اضافه کردن h-full -->
            <div class="h-full flex flex-col">
              <!-- Logo -->
              <div class="mb-6">
                <!-- کاهش margin-bottom -->
                <div class="flex items-center gap-3">
                  <div class="w-10 h-10 bg-white/20 rounded-xl flex items-center justify-center">
                    <span class="text-xl">🔧</span>
                  </div>
                  <div>
                    <h2 class="text-xl font-bold">آرا سرویس</h2>
                    <p class="text-blue-200 text-xs">مرجع تخصصی قطعات</p>
                  </div>
                </div>
              </div>

              <!-- Content -->
              <div class="flex-1">
                <!-- Title -->
                <div class="mb-6">
                  <h3 class="text-xl font-bold mb-3">
                    {{ mode === 'login' ? 'خوش آمدید' : 'به جمع ما بپیوندید' }}
                  </h3>
                  <p class="text-blue-100 leading-relaxed text-sm">
                    {{ mode === 'login' 
                      ? 'به بزرگترین مرجع قطعات لوازم خانگی خوش آمدید. با ورود به حساب کاربری خود، از تمامی امکانات ویژه سایت بهره‌مند شوید.' 
                      : 'با ثبت‌نام در قطعه بازار، علاوه بر دسترسی به بیش از ۵۰۰۰ قطعه اورجینال، از مزایای ویژه‌ای نیز برخوردار خواهید شد.' 
                    }}
                  </p>
                </div>

                <!-- Features - فشرده‌تر -->
                <div class="space-y-4 mb-6">
                  <div class="flex items-start gap-3">
                    <div class="w-8 h-8 bg-white/20 rounded-lg flex items-center justify-center flex-shrink-0">
                      <span class="text-sm">🚚</span>
                    </div>
                    <div>
                      <h4 class="font-semibold text-sm mb-1">ارسال سریع</h4>
                      <p class="text-blue-100 text-xs">تهران ۳ ساعته - شهرستان ۲۴ ساعته</p>
                    </div>
                  </div>

                  <div class="flex items-start gap-3">
                    <div class="w-8 h-8 bg-white/20 rounded-lg flex items-center justify-center flex-shrink-0">
                      <span class="text-sm">🛡️</span>
                    </div>
                    <div>
                      <h4 class="font-semibold text-sm mb-1">گارانتی معتبر</h4>
                      <p class="text-blue-100 text-xs">۱۲ تا ۲۴ ماه گارانتی تمام قطعات</p>
                    </div>
                  </div>

                  <div class="flex items-start gap-3">
                    <div class="w-8 h-8 bg-white/20 rounded-lg flex items-center justify-center flex-shrink-0">
                      <span class="text-sm">💯</span>
                    </div>
                    <div>
                      <h4 class="font-semibold text-sm mb-1">ضمانت کیفیت</h4>
                      <p class="text-blue-100 text-xs">قطعات اورجینال با تضمین اصالت</p>
                    </div>
                  </div>

                  <div v-if="mode === 'register'" class="flex items-start gap-3">
                    <div class="w-8 h-8 bg-white/20 rounded-lg flex items-center justify-center flex-shrink-0">
                      <span class="text-sm">🎁</span>
                    </div>
                    <div>
                      <h4 class="font-semibold text-sm mb-1">تخفیف ویژه</h4>
                      <p class="text-blue-100 text-xs">۱۵٪ تخفیف برای اولین خرید از سایت</p>
                    </div>
                  </div>

                  <div v-if="mode === 'login'" class="flex items-start gap-3">
                    <div class="w-8 h-8 bg-white/20 rounded-lg flex items-center justify-center flex-shrink-0">
                      <span class="text-sm">📦</span>
                    </div>
                    <div>
                      <h4 class="font-semibold text-sm mb-1">پیگیری سفارش</h4>
                      <p class="text-blue-100 text-xs">پیگیری لحظه‌ای سفارش‌های خود</p>
                    </div>
                  </div>
                </div>

                <!-- Quote -->
                <div class="pt-4 border-t border-white/20">
                  <p class="italic text-blue-100 text-xs">
                    {{ mode === 'login' 
                      ? '"همراه شما در مسیر نگهداری و تعمیر لوازم خانگی با ارائه قطعات اورجینال و مشاوره تخصصی"' 
                      : '"با اطمینان خرید کنید، با آرامش استفاده نمایید. کیفیت محصولات ما، آرامش خاطر شماست"' 
                    }}
                  </p>
                </div>
              </div>

              <!-- Back to Home -->
              <div class="pt-4 border-t border-white/20 mt-4">
                <a href="/" class="inline-flex items-center gap-2 text-blue-200 hover:text-white transition text-xs">
                  <svg class="w-3 h-3" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 19l-7-7m0 0l7-7m-7 7h18" />
                  </svg>
                  بازگشت به صفحه اصلی
                </a>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Footer Note -->
      <div class="text-center mt-4">
        <!-- کاهش margin-top -->
        <p class="text-gray-500 text-xs">
          برای پشتیبانی با شماره 
          <a href="tel:+982112345678" class="text-blue-600 hover:text-blue-700">۰۲۱۱۲۳۴۵۶۷۸</a> 
          تماس بگیرید
        </p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()
const mode = ref('login')
const showPassword = ref(false)
const isSubmitting = ref(false)
const validationErrors = ref([])

const form = reactive({
  fullName: '',
  phone: '',
  password: '',
  confirmPassword: '',
  remember: false,
  acceptTerms: false
})

const errors = reactive({
  fullName: '',
  phone: '',
  password: '',
  confirmPassword: ''
})

const validateForm = () => {
  validationErrors.value = []
  Object.keys(errors).forEach(key => errors[key] = '')

  const phoneRegex = /^09[0-9]{9}$/
  if (!phoneRegex.test(form.phone)) {
    errors.phone = 'شماره موبایل معتبر نیست'
    validationErrors.value.push('شماره موبایل معتبر نیست')
  }

  if (mode.value === 'register') {
    if (form.fullName.trim().length < 3) {
      errors.fullName = 'نام باید حداقل ۳ کاراکتر باشد'
      validationErrors.value.push('نام باید حداقل ۳ کاراکتر باشد')
    }

    if (form.password.length < 6) {
      errors.password = 'رمز عبور باید حداقل ۶ کاراکتر باشد'
      validationErrors.value.push('رمز عبور باید حداقل ۶ کاراکتر باشد')
    }

    if (form.password !== form.confirmPassword) {
      errors.confirmPassword = 'رمز عبور و تکرار آن مطابقت ندارند'
      validationErrors.value.push('رمز عبور و تکرار آن مطابقت ندارند')
    }

    if (!form.acceptTerms) {
      validationErrors.value.push('لطفاً با قوانین موافقت کنید')
    }
  }

  return validationErrors.value.length === 0
}

const setMode = (newMode) => {
  mode.value = newMode
  Object.keys(form).forEach(key => {
    if (typeof form[key] === 'boolean') {
      form[key] = false
    } else {
      form[key] = ''
    }
  })
  Object.keys(errors).forEach(key => errors[key] = '')
  validationErrors.value = []
}

const toggleMode = () => {
  setMode(mode.value === 'login' ? 'register' : 'login')
}

const handleSubmit = async () => {
  if (!validateForm()) {
    return
  }

  isSubmitting.value = true

  try {
    await new Promise(resolve => setTimeout(resolve, 1500))
    
    if (mode.value === 'register') {
      console.log('Registering:', form)
      alert('ثبت‌نام با موفقیت انجام شد')
    } else {
      console.log('Logging in:', form)
      alert('ورود با موفقیت انجام شد')
    }
    router.push('/')
  } catch (error) {
    console.error('Auth error:', error)
    validationErrors.value.push('خطا در انجام عملیات')
  } finally {
    isSubmitting.value = false
  }
}
</script>

<style scoped>
/* استایل‌های خاص برای ثابت نگه داشتن ارتفاع */
.h-\[620px\] {
  height: 620px;
}

/* اسکرول نرم داخل فرم */
.overflow-y-auto {
  scrollbar-width: thin;
  scrollbar-color: #cbd5e1 transparent;
}

.overflow-y-auto::-webkit-scrollbar {
  width: 6px;
}

.overflow-y-auto::-webkit-scrollbar-track {
  background: transparent;
}

.overflow-y-auto::-webkit-scrollbar-thumb {
  background-color: #cbd5e1;
  border-radius: 3px;
}

/* انیمیشن برای تغییر حالت */
form > * {
  animation: slideDown 0.3s ease-out;
}

@keyframes slideDown {
  from {
    opacity: 0;
    transform: translateY(-10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* ترنزیشن برای دکمه‌های سوییچ */
button[type="button"] {
  transition: all 0.2s ease;
}

/* سایز فونت‌های متغیر برای ثابت ماندن ارتفاع */
.text-sm {
  font-size: 0.875rem;
  line-height: 1.25rem;
}

.text-xs {
  font-size: 0.75rem;
  line-height: 1rem;
}
</style>