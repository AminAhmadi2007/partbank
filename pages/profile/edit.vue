<template>
  <div class="min-h-screen bg-gradient-to-br from-gray-50 to-blue-50/30 py-6 md:py-10">
    <div class="container mx-auto px-4 max-w-7xl">
      <!-- Header with Breadcrumb -->
      <div class="mb-8">
        <nav class="flex items-center gap-2 text-sm text-gray-500 mb-4">
          <router-link to="/" class="hover:text-blue-600 transition">خانه</router-link>
          <span class="text-gray-400">/</span>
          <router-link to="/profile" class="hover:text-blue-600 transition">حساب کاربری</router-link>
          <span class="text-gray-400">/</span>
          <span class="text-gray-900 font-medium">ویرایش حساب</span>
        </nav>
        
        <div class="flex items-center justify-between gap-4">
          <div>
            <h1 class="text-3xl font-bold text-gray-900 mb-2 bg-gradient-to-l from-blue-600 to-blue-800 bg-clip-text text-transparent">
              ویرایش حساب کاربری
            </h1>
            <p class="text-gray-600">
              اطلاعات شخصی و حساب کاربری خود را به روز کنید
            </p>
          </div>
          
          <router-link to="/profile"
                       class="px-4 py-2.5 border border-gray-300 hover:border-gray-400 rounded-xl text-gray-700 hover:text-gray-900 text-sm font-medium transition-all flex items-center gap-2 hover:shadow-sm">
            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 19l-7-7m0 0l7-7m-7 7h18" />
            </svg>
            بازگشت
          </router-link>
        </div>
      </div>

      <div class="grid grid-cols-1 lg:grid-cols-4 gap-6">
        <!-- Sidebar -->
        <div class="lg:col-span-1">
          <div class="sticky top-6 space-y-6">
            <!-- Profile Preview Card -->
            <div class="bg-gradient-to-br from-white to-blue-50 rounded-2xl shadow-lg border border-blue-100 overflow-hidden">
              <div class="p-6 border-b border-blue-100">
                <div class="flex flex-col items-center text-center">
                  <div class="relative mb-4">
                    <div class="w-32 h-32 rounded-full bg-gradient-to-br from-blue-100 to-blue-200 border-4 border-white shadow-lg flex items-center justify-center overflow-hidden">
                      <img v-if="formData.avatar" :src="formData.avatar" alt="Avatar" class="w-full h-full object-cover">
                      <span v-else class="text-5xl text-blue-700 font-bold">{{ user?.initials || '?' }}</span>
                    </div>
                    <button @click="openAvatarUpload"
                            class="absolute bottom-2 left-2 w-10 h-10 bg-white rounded-full shadow-md flex items-center justify-center hover:bg-blue-50 transition group">
                      <svg class="w-5 h-5 text-blue-600 group-hover:scale-110 transition" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 9a2 2 0 012-2h.93a2 2 0 001.664-.89l.812-1.22A2 2 0 0110.07 4h3.86a2 2 0 011.664.89l.812 1.22A2 2 0 0018.07 7H19a2 2 0 012 2v9a2 2 0 01-2 2H5a2 2 0 01-2-2V9z" />
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 13a3 3 0 11-6 0 3 3 0 016 0z" />
                      </svg>
                    </button>
                  </div>
                  <h3 class="text-xl font-bold text-gray-900 mb-1">{{ formData.fullName || 'کاربر' }}</h3>
                  <p class="text-gray-600 text-sm">{{ formData.email || 'ایمیل ثبت نشده' }}</p>
                  <div class="mt-2 px-3 py-1 bg-gradient-to-r from-yellow-50 to-amber-50 border border-yellow-200 rounded-full text-xs text-yellow-700">
                    سطح {{ user?.membershipLevel || 'عادی' }}
                  </div>
                </div>
              </div>
              
              <div class="p-4 bg-blue-50/50">
                <div class="text-center">
                  <div class="text-sm font-medium text-gray-900 mb-1">تکمیل پروفایل</div>
                  <div class="w-full bg-gray-200 rounded-full h-2 mb-2">
                    <div class="bg-gradient-to-r from-blue-500 to-blue-600 h-2 rounded-full transition-all duration-500" 
                         :style="{ width: `${profileCompletion}%` }"></div>
                  </div>
                  <div class="text-xs text-gray-500">{{ profileCompletion }}% تکمیل شده</div>
                </div>
              </div>
            </div>

            <!-- Edit Navigation -->
            <div class="bg-white rounded-2xl shadow-lg border border-gray-200 overflow-hidden">
              <div class="p-4 border-b border-gray-200">
                <h4 class="font-bold text-gray-900 flex items-center gap-2">
                  <svg class="w-5 h-5 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10.325 4.317c.426-1.756 2.924-1.756 3.35 0a1.724 1.724 0 002.573 1.066c1.543-.94 3.31.826 2.37 2.37a1.724 1.724 0 001.065 2.572c1.756.426 1.756 2.924 0 3.35a1.724 1.724 0 00-1.066 2.573c.94 1.543-.826 3.31-2.37 2.37a1.724 1.724 0 00-2.572 1.065c-.426 1.756-2.924 1.756-3.35 0a1.724 1.724 0 00-2.573-1.066c-1.543.94-3.31-.826-2.37-2.37a1.724 1.724 0 00-1.065-2.572c-1.756-.426-1.756-2.924 0-3.35a1.724 1.724 0 001.066-2.573c-.94-1.543.826-3.31 2.37-2.37.996.608 2.296.07 2.572-1.065z" />
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
                  </svg>
                  تنظیمات
                </h4>
              </div>
              
              <nav class="p-2">
                <button v-for="tab in formTabs" 
                        :key="tab.id"
                        @click="activeFormTab = tab.id"
                        :class="[
                          'w-full text-right px-4 py-4 rounded-xl mb-1 transition-all duration-300 flex items-center justify-between group',
                          activeFormTab === tab.id
                            ? 'bg-gradient-to-l from-blue-600 to-blue-700 text-white shadow-md transform scale-[1.02]'
                            : 'text-gray-700 hover:bg-gray-50 hover:pr-6'
                        ]">
                  <div class="flex items-center gap-3">
                    <span :class="[
                      'text-lg transition-transform',
                      activeFormTab === tab.id ? 'scale-110' : 'group-hover:scale-110'
                    ]">
                      {{ tab.icon }}
                    </span>
                    <span class="font-medium">{{ tab.title }}</span>
                  </div>
                  <svg class="w-5 h-5 transition-transform" 
                       :class="{ 'rotate-180': activeFormTab === tab.id }"
                       fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
                  </svg>
                </button>
              </nav>
            </div>
          </div>
        </div>

        <!-- Main Content Area -->
        <div class="lg:col-span-3">
          <transition name="fade" mode="out-in">
            <!-- Personal Info Tab -->
            <div v-if="activeFormTab === 'personal'" 
                 class="bg-white rounded-2xl shadow-lg border border-gray-200 overflow-hidden">
              <div class="p-6 border-b border-gray-200 flex items-center justify-between">
                <h2 class="text-lg font-bold text-gray-900 flex items-center gap-2">
                  <span class="w-2 h-2 bg-blue-600 rounded-full"></span>
                  اطلاعات شخصی
                </h2>
                <span class="text-sm text-gray-500">همه فیلدهای ضروری را پر کنید</span>
              </div>
              
              <form @submit.prevent="saveProfile" class="p-6">
                <div class="space-y-8">
                  <!-- Basic Info Section -->
                  <div>
                    <h3 class="text-lg font-bold text-gray-900 mb-6 pb-3 border-b border-gray-200">اطلاعات اصلی</h3>
                    
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                      <!-- First Name -->
                      <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">
                          نام
                          <span class="text-red-500">*</span>
                        </label>
                        <div class="relative">
                          <input v-model="formData.firstName"
                                 type="text"
                                 required
                                 class="w-full px-4 py-3.5 border border-gray-300 rounded-xl focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition-all"
                                 placeholder="نام خود را وارد کنید">
                          <div class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400">
                            👤
                          </div>
                        </div>
                      </div>

                      <!-- Last Name -->
                      <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">
                          نام خانوادگی
                          <span class="text-red-500">*</span>
                        </label>
                        <input v-model="formData.lastName"
                               type="text"
                               required
                               class="w-full px-4 py-3.5 border border-gray-300 rounded-xl focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition-all"
                               placeholder="نام خانوادگی خود را وارد کنید">
                      </div>
                    </div>
                  </div>

                  <!-- Contact Info Section -->
                  <div>
                    <h3 class="text-lg font-bold text-gray-900 mb-6 pb-3 border-b border-gray-200">اطلاعات تماس</h3>
                    
                    <div class="space-y-6">
                      <!-- Email -->
                      <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">
                          ایمیل
                          <span class="text-red-500">*</span>
                        </label>
                        <div class="relative">
                          <input v-model="formData.email"
                                 type="email"
                                 required
                                 class="w-full px-4 py-3.5 border border-gray-300 rounded-xl focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition-all direction-ltr text-left pr-10"
                                 placeholder="example@domain.com">
                          <div class="absolute left-3 top-1/2 transform -translate-y-1/2">
                            <span v-if="user?.emailVerified" class="text-green-600 text-sm">✓ تایید شده</span>
                            <button v-else type="button"
                                    @click="verifyEmail"
                                    class="text-blue-600 hover:text-blue-700 text-sm">
                              تایید ایمیل
                            </button>
                          </div>
                        </div>
                      </div>

                      <!-- Phone -->
                      <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">
                          شماره تماس
                          <span class="text-red-500">*</span>
                        </label>
                        <div class="relative">
                          <input v-model="formData.phone"
                                 type="tel"
                                 required
                                 class="w-full px-4 py-3.5 border border-gray-300 rounded-xl focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition-all direction-ltr text-left"
                                 placeholder="09123456789">
                          <div class="absolute left-3 top-1/2 transform -translate-y-1/2">
                            <span v-if="user?.phoneVerified" class="text-green-600 text-sm">✓ تایید شده</span>
                            <button v-else type="button"
                                    @click="verifyPhone"
                                    class="text-blue-600 hover:text-blue-700 text-sm">
                              ارسال کد تایید
                            </button>
                          </div>
                        </div>
                      </div>
                    </div>
                  </div>

                  <!-- Additional Info Section -->
                  <div>
                    <h3 class="text-lg font-bold text-gray-900 mb-6 pb-3 border-b border-gray-200">اطلاعات تکمیلی</h3>
                    
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                      <!-- Birth Date -->
                      <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">
                          تاریخ تولد
                        </label>
                        <div class="relative">
                          <input v-model="formData.birthDate"
                                 type="text"
                                 class="w-full px-4 py-3.5 border border-gray-300 rounded-xl focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition-all"
                                 placeholder="۱۳۷۰/۰۱/۰۱">
                          <div class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400">
                            🎂
                          </div>
                        </div>
                      </div>

                      <!-- Gender -->
                      <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">
                          جنسیت
                        </label>
                        <div class="flex gap-4">
                          <label class="flex items-center gap-2 cursor-pointer p-3 border border-gray-300 rounded-xl hover:border-blue-400 transition flex-1 text-center">
                            <input v-model="formData.gender" type="radio" value="male" class="text-blue-600">
                            <span class="text-gray-700">آقا</span>
                          </label>
                          <label class="flex items-center gap-2 cursor-pointer p-3 border border-gray-300 rounded-xl hover:border-blue-400 transition flex-1 text-center">
                            <input v-model="formData.gender" type="radio" value="female" class="text-blue-600">
                            <span class="text-gray-700">خانم</span>
                          </label>
                        </div>
                      </div>

                      <!-- National ID -->
                      <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">
                          کد ملی
                        </label>
                        <input v-model="formData.nationalId"
                               type="text"
                               class="w-full px-4 py-3.5 border border-gray-300 rounded-xl focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition-all direction-ltr text-left"
                               placeholder="۰۰۰۰۰۰۰۰۰۰">
                      </div>
                    </div>

                    <!-- Bio -->
                    <div class="mt-6">
                      <label class="block text-sm font-medium text-gray-700 mb-2">
                        بیوگرافی
                      </label>
                      <textarea v-model="formData.bio"
                                rows="3"
                                class="w-full px-4 py-3.5 border border-gray-300 rounded-xl focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition-all resize-none"
                                placeholder="درباره خودتان بنویسید..."></textarea>
                      <div class="text-xs text-gray-500 mt-2">
                        {{ formData.bio?.length || 0 }}/200 کاراکتر
                      </div>
                    </div>
                  </div>

                  <!-- Form Actions -->
                  <div class="flex gap-4 pt-6 border-t border-gray-200">
                    <button type="submit"
                            :disabled="loading"
                            class="px-8 py-3.5 bg-gradient-to-r from-blue-600 to-blue-700 hover:from-blue-700 hover:to-blue-800 text-white rounded-xl font-medium transition-all flex-1 flex items-center justify-center gap-2 disabled:opacity-50 disabled:cursor-not-allowed shadow-md hover:shadow-lg">
                      <svg v-if="loading" class="w-5 h-5 animate-spin" fill="none" viewBox="0 0 24 24">
                        <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
                        <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
                      </svg>
                      <span v-else>ذخیره تغییرات</span>
                    </button>
                    <button type="button"
                            @click="resetForm"
                            class="px-6 py-3.5 border border-gray-300 hover:border-gray-400 text-gray-700 hover:text-gray-900 rounded-xl font-medium transition hover:shadow-sm">
                      بازنشانی
                    </button>
                  </div>
                </div>
              </form>
            </div>

            <!-- Preferences Tab -->
            

            <!-- Security Tab -->
            <div v-else-if="activeFormTab === 'security'" 
                 class="bg-white rounded-2xl shadow-lg border border-gray-200 overflow-hidden">
              <div class="p-6 border-b border-gray-200">
                <h2 class="text-lg font-bold text-gray-900 flex items-center gap-2">
                  <span class="w-2 h-2 bg-green-600 rounded-full"></span>
                  امنیت و رمز عبور
                </h2>
              </div>
              
              <form @submit.prevent="changePassword" class="p-6">
                <div class="space-y-8">
                  <!-- Change Password -->
                  <div>
                    <h3 class="text-lg font-bold text-gray-900 mb-6 pb-3 border-b border-gray-200">تغییر رمز عبور</h3>
                    
                    <div class="space-y-6">
                      <!-- Current Password -->
                      <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">
                          رمز عبور فعلی
                        </label>
                        <div class="relative">
                          <input v-model="passwordData.currentPassword"
                                 :type="showCurrentPassword ? 'text' : 'password'"
                                 required
                                 class="w-full px-4 py-3.5 border border-gray-300 rounded-xl focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition-all pr-10">
                          <button type="button"
                                  @click="showCurrentPassword = !showCurrentPassword"
                                  class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-500 hover:text-gray-700">
                            {{ showCurrentPassword ? '🙈' : '👁️' }}
                          </button>
                        </div>
                      </div>

                      <!-- New Password -->
                      <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">
                          رمز عبور جدید
                        </label>
                        <div class="relative">
                          <input v-model="passwordData.newPassword"
                                 :type="showNewPassword ? 'text' : 'password'"
                                 required
                                 class="w-full px-4 py-3.5 border border-gray-300 rounded-xl focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition-all pr-10"
                                 placeholder="حداقل ۸ کاراکتر">
                          <button type="button"
                                  @click="showNewPassword = !showNewPassword"
                                  class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-500 hover:text-gray-700">
                            {{ showNewPassword ? '🙈' : '👁️' }}
                          </button>
                        </div>
                        
                        <!-- Password Strength -->
                        <div v-if="passwordData.newPassword" class="mt-4">
                          <div class="flex items-center justify-between mb-2">
                            <div class="text-sm font-medium text-gray-700">قدرت رمز عبور:</div>
                            <div class="text-sm" :class="passwordStrengthColor">
                              {{ passwordStrengthText }}
                            </div>
                          </div>
                          <div class="h-2 bg-gray-200 rounded-full overflow-hidden">
                            <div :class="[
                              'h-full transition-all duration-500 rounded-full',
                              passwordStrength === 'weak' ? 'bg-red-500 w-1/3' : '',
                              passwordStrength === 'medium' ? 'bg-yellow-500 w-2/3' : '',
                              passwordStrength === 'strong' ? 'bg-green-500 w-full' : ''
                            ]"></div>
                          </div>
                          <div class="text-xs text-gray-500 mt-2">
                            رمز عبور باید شامل حروف بزرگ و کوچک انگلیسی و اعداد باشد
                          </div>
                        </div>
                      </div>

                      <!-- Confirm Password -->
                      <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">
                          تکرار رمز عبور جدید
                        </label>
                        <input v-model="passwordData.confirmPassword"
                               type="password"
                               required
                               class="w-full px-4 py-3.5 border border-gray-300 rounded-xl focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition-all">
                        <div v-if="passwordData.confirmPassword && !passwordsMatch" 
                             class="text-red-600 text-sm mt-2">
                          رمز عبور و تکرار آن مطابقت ندارند
                        </div>
                      </div>
                    </div>
                  </div>

                  <!-- Two-Factor Authentication -->
                  <div class="border-t border-gray-200 pt-6">
                    <div class="flex items-center justify-between p-4 border border-gray-200 rounded-xl hover:bg-gray-50 transition-all">
                      <div class="flex items-center gap-4">
                        <div class="w-12 h-12 bg-blue-100 rounded-xl flex items-center justify-center">
                          <span class="text-blue-600 text-xl">🔐</span>
                        </div>
                        <div>
                          <div class="font-medium text-gray-900">احراز هویت دو مرحله‌ای</div>
                          <div class="text-sm text-gray-500">افزایش امنیت حساب کاربری</div>
                        </div>
                      </div>
                      <button type="button"
                              @click="toggleTwoFactor"
                              :class="[
                                'relative inline-flex h-7 w-12 items-center rounded-full transition-all',
                                twoFactorEnabled ? 'bg-green-500' : 'bg-gray-300'
                              ]">
                        <span :class="[
                          'inline-block h-5 w-5 transform rounded-full bg-white transition-all shadow-md',
                          twoFactorEnabled ? 'translate-x-6' : 'translate-x-1'
                        ]"></span>
                      </button>
                    </div>
                  </div>

                  <!-- Recent Logins -->
                  <div v-if="recentLogins && recentLogins.length > 0" class="border-t border-gray-200 pt-6">
                    <h3 class="text-lg font-bold text-gray-900 mb-4">ورودهای اخیر</h3>
                    <div class="space-y-3">
                      <div v-for="login in recentLogins" :key="login.id"
                           class="flex items-center justify-between p-4 border border-gray-200 rounded-xl hover:bg-gray-50 transition-all">
                        <div class="flex items-center gap-4">
                          <div class="w-10 h-10 bg-gray-100 rounded-lg flex items-center justify-center">
                            <span class="text-gray-600">{{ login.icon }}</span>
                          </div>
                          <div>
                            <div class="font-medium text-gray-900">{{ login.device }}</div>
                            <div class="text-sm text-gray-500">{{ login.location }} • {{ login.time }}</div>
                          </div>
                        </div>
                        <div>
                          <span v-if="login.current" class="text-green-600 text-sm">در حال استفاده</span>
                          <button v-else
                                  @click="logoutDevice(login.id)"
                                  class="text-red-600 hover:text-red-700 text-sm">
                            خروج از دستگاه
                          </button>
                        </div>
                      </div>
                    </div>
                  </div>

                  <!-- Form Actions -->
                  <div class="flex gap-4 pt-6 border-t border-gray-200">
                    <button type="submit"
                            :disabled="!passwordsMatch || loading || passwordData.newPassword.length < 8"
                            class="px-8 py-3.5 bg-gradient-to-r from-blue-600 to-blue-700 hover:from-blue-700 hover:to-blue-800 text-white rounded-xl font-medium transition-all flex-1 disabled:opacity-50 disabled:cursor-not-allowed shadow-md hover:shadow-lg">
                      <svg v-if="loading" class="w-5 h-5 animate-spin" fill="none" viewBox="0 0 24 24">
                        <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
                        <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
                      </svg>
                      <span v-else>تغییر رمز عبور</span>
                    </button>
                  </div>
                </div>
              </form>
            </div>
          </transition>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, reactive, onMounted } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()

// State
const activeFormTab = ref('personal')
const loading = ref(false)
const showCurrentPassword = ref(false)
const showNewPassword = ref(false)
const twoFactorEnabled = ref(false)

// User Data with safe defaults
const user = ref({
  fullName: '',
  email: '',
  phone: '',
  initials: '',
  emailVerified: false,
  phoneVerified: false,
  membershipLevel: 'عادی'
})

// Form Tabs
const formTabs = [
  { id: 'personal', title: 'اطلاعات شخصی', icon: '👤' },
  { id: 'security', title: 'امنیت', icon: '🔒' }
]

// Progress Steps
const progressSteps = ref([
  { id: 1, title: 'اطلاعات شخصی', description: 'تکمیل اطلاعات اصلی', icon: '👤', completed: true },
  { id: 2, title: 'تایید ایمیل', description: 'تایید آدرس ایمیل', icon: '📧', completed: false },
  { id: 3, title: 'تایید شماره', description: 'تایید شماره تماس', icon: '📱', completed: false },
  { id: 4, title: 'افزودن آدرس', description: 'ثبت آدرس تحویل', icon: '🏠', completed: false }
])

// Form Data with safe defaults
const formData = reactive({
  firstName: '',
  lastName: '',
  email: '',
  phone: '',
  birthDate: '',
  gender: 'male',
  nationalId: '',
  bio: '',
  avatar: null,
  fullName: computed(() => `${formData.firstName} ${formData.lastName}`.trim()),
  initials: computed(() => formData.firstName?.[0] || '?')
})

// Preferences
const preferences = reactive({
  language: 'fa',
  theme: 'light',
  emailNotifications: true,
  smsNotifications: true,
  pushNotifications: true,
  newsletter: true
})

// Password Data
const passwordData = reactive({
  currentPassword: '',
  newPassword: '',
  confirmPassword: ''
})

// Recent Logins with safe defaults
const recentLogins = ref([
  { id: 1, device: 'Chrome on Windows', location: 'تهران، ایران', time: '۲ ساعت پیش', current: true, icon: '💻' },
  { id: 2, device: 'Safari on iPhone', location: 'تهران، ایران', time: '۳ روز پیش', current: false, icon: '📱' },
  { id: 3, device: 'Firefox on Mac', location: 'تهران، ایران', time: '۱ هفته پیش', current: false, icon: '🖥️' }
])

// Computed
const profileCompletion = computed(() => {
  let completed = 0
  const total = 6
  
  if (formData.firstName) completed++
  if (formData.lastName) completed++
  if (formData.email) completed++
  if (formData.phone) completed++
  if (formData.birthDate) completed++
  if (formData.gender) completed++
  
  return Math.round((completed / total) * 100)
})

const passwordsMatch = computed(() => {
  return passwordData.newPassword === passwordData.confirmPassword
})

const passwordStrength = computed(() => {
  const password = passwordData.newPassword
  if (!password) return ''
  
  const hasLower = /[a-z]/.test(password)
  const hasUpper = /[A-Z]/.test(password)
  const hasNumber = /\d/.test(password)
  const hasSpecial = /[!@#$%^&*]/.test(password)
  
  const score = [hasLower, hasUpper, hasNumber, hasSpecial].filter(Boolean).length
  
  if (password.length < 8) return 'weak'
  if (score >= 3 && password.length >= 10) return 'strong'
  if (score >= 2) return 'medium'
  return 'weak'
})

const passwordStrengthText = computed(() => {
  switch (passwordStrength.value) {
    case 'weak': return 'ضعیف'
    case 'medium': return 'متوسط'
    case 'strong': return 'قوی'
    default: return ''
  }
})

const passwordStrengthColor = computed(() => {
  switch (passwordStrength.value) {
    case 'weak': return 'text-red-600'
    case 'medium': return 'text-yellow-600'
    case 'strong': return 'text-green-600'
    default: return 'text-gray-600'
  }
})

// Methods
const openAvatarUpload = () => {
  const input = document.createElement('input')
  input.type = 'file'
  input.accept = 'image/*'
  input.onchange = (e) => {
    const file = e.target.files[0]
    if (file) {
      const reader = new FileReader()
      reader.onload = (e) => {
        formData.avatar = e.target.result
        // Save to localStorage
        localStorage.setItem('userAvatar', formData.avatar)
      }
      reader.readAsDataURL(file)
    }
  }
  input.click()
}

const verifyEmail = () => {
  if (!user.value.emailVerified) {
    const code = prompt('کد تایید ارسال شده به ایمیل شما را وارد کنید:')
    if (code === '123456') {
      user.value.emailVerified = true
      progressSteps.value[1].completed = true
      localStorage.setItem('userEmailVerified', 'true')
      alert('ایمیل با موفقیت تایید شد')
    } else {
      alert('کد تایید نادرست است')
    }
  }
}

const verifyPhone = () => {
  if (!user.value.phoneVerified) {
    const code = prompt('کد تایید ارسال شده به شماره شما را وارد کنید:')
    if (code === '123456') {
      user.value.phoneVerified = true
      progressSteps.value[2].completed = true
      localStorage.setItem('userPhoneVerified', 'true')
      alert('شماره تماس با موفقیت تایید شد')
    } else {
      alert('کد تایید نادرست است')
    }
  }
}

const saveProfile = async () => {
  loading.value = true
  try {
    // Simulate API call
    await new Promise(resolve => setTimeout(resolve, 1500))
    
    // Update user data
    user.value.fullName = formData.fullName
    user.value.email = formData.email
    user.value.phone = formData.phone
    user.value.initials = formData.initials
    
    // Save to localStorage
    localStorage.setItem('user', JSON.stringify(user.value))
    localStorage.setItem('userProfile', JSON.stringify(formData))
    
    alert('تغییرات با موفقیت ذخیره شد')
    router.push('/profile')
  } catch (error) {
    console.error('Error saving profile:', error)
    alert('خطا در ذخیره تغییرات')
  } finally {
    loading.value = false
  }
}

const savePreferences = async () => {
  try {
    localStorage.setItem('userPreferences', JSON.stringify(preferences))
    alert('تنظیمات با موفقیت ذخیره شد')
  } catch (error) {
    console.error('Error saving preferences:', error)
    alert('خطا در ذخیره تنظیمات')
  }
}

const changePassword = async () => {
  if (!passwordsMatch.value) {
    alert('رمز عبور جدید و تکرار آن مطابقت ندارند')
    return
  }
  
  if (passwordData.newPassword.length < 8) {
    alert('رمز عبور باید حداقل ۸ کاراکتر باشد')
    return
  }
  
  loading.value = true
  try {
    // Simulate API call
    await new Promise(resolve => setTimeout(resolve, 2000))
    
    // Reset password fields
    passwordData.currentPassword = ''
    passwordData.newPassword = ''
    passwordData.confirmPassword = ''
    
    alert('رمز عبور با موفقیت تغییر کرد')
  } catch (error) {
    console.error('Error changing password:', error)
    alert('خطا در تغییر رمز عبور')
  } finally {
    loading.value = false
  }
}

const toggleTwoFactor = () => {
  twoFactorEnabled.value = !twoFactorEnabled.value
  localStorage.setItem('twoFactorEnabled', twoFactorEnabled.value.toString())
  alert(twoFactorEnabled.value ? 'احراز هویت دو مرحله‌ای فعال شد' : 'احراز هویت دو مرحله‌ای غیرفعال شد')
}

const logoutDevice = (deviceId) => {
  if (confirm('آیا از خروج از این دستگاه مطمئن هستید؟')) {
    recentLogins.value = recentLogins.value.filter(login => login.id !== deviceId)
    localStorage.setItem('userRecentLogins', JSON.stringify(recentLogins.value))
    alert('دستگاه با موفقیت از حساب خارج شد')
  }
}

const deleteAccount = () => {
  if (confirm('⚠️ آیا مطمئن هستید که می‌خواهید حساب کاربری خود را حذف کنید؟ این عمل غیرقابل بازگشت است.')) {
    if (prompt('برای تایید، لطفا کلمه "حذف" را وارد کنید:') === 'حذف') {
      // Clear all user data
      localStorage.removeItem('authToken')
      localStorage.removeItem('user')
      localStorage.removeItem('userProfile')
      localStorage.removeItem('userPreferences')
      localStorage.removeItem('userAvatar')
      
      router.push('/')
    }
  }
}

const deactivateAccount = () => {
  if (confirm('آیا می‌خواهید حساب کاربری خود را موقتاً غیرفعال کنید؟')) {
    // Deactivate logic
    localStorage.setItem('accountDeactivated', 'true')
    alert('حساب کاربری شما با موفقیت غیرفعال شد')
    router.push('/')
  }
}

const resetForm = () => {
  if (confirm('آیا می‌خواهید تمام تغییرات را بازنشانی کنید؟')) {
    const savedData = JSON.parse(localStorage.getItem('userProfile') || '{}')
    Object.assign(formData, savedData)
  }
}

// Initialize with safe data loading
const initializeData = async () => {
  try {
    // Load user data
    const savedUser = localStorage.getItem('user')
    if (savedUser) {
      const parsedUser = JSON.parse(savedUser)
      user.value = {
        fullName: parsedUser.fullName || '',
        email: parsedUser.email || '',
        phone: parsedUser.phone || '',
        initials: parsedUser.initials || '?',
        emailVerified: parsedUser.emailVerified || false,
        phoneVerified: parsedUser.phoneVerified || false,
        membershipLevel: parsedUser.membershipLevel || 'عادی'
      }
    }

    // Load profile data
    const savedProfile = localStorage.getItem('userProfile')
    if (savedProfile) {
      const parsedProfile = JSON.parse(savedProfile)
      Object.assign(formData, parsedProfile)
    }

    // Load preferences
    const savedPreferences = localStorage.getItem('userPreferences')
    if (savedPreferences) {
      Object.assign(preferences, JSON.parse(savedPreferences))
    }

    // Load avatar
    const savedAvatar = localStorage.getItem('userAvatar')
    if (savedAvatar) {
      formData.avatar = savedAvatar
    }

    // Load two-factor setting
    const savedTwoFactor = localStorage.getItem('twoFactorEnabled')
    if (savedTwoFactor) {
      twoFactorEnabled.value = savedTwoFactor === 'true'
    }

    // Load recent logins
    const savedLogins = localStorage.getItem('userRecentLogins')
    if (savedLogins) {
      recentLogins.value = JSON.parse(savedLogins)
    }

    // Update progress steps based on data
    if (user.value.emailVerified) progressSteps.value[1].completed = true
    if (user.value.phoneVerified) progressSteps.value[2].completed = true

  } catch (error) {
    console.error('Error loading user data:', error)
    // Set fallback data
    user.value = {
      fullName: 'کاربر مهمان',
      email: 'guest@example.com',
      phone: '',
      initials: 'گ',
      emailVerified: false,
      phoneVerified: false,
      membershipLevel: 'عادی'
    }
    
    // Set default form data
    formData.firstName = 'کاربر'
    formData.lastName = 'مهمان'
    formData.email = 'guest@example.com'
    formData.gender = 'male'
  }
}

// Initialize
onMounted(() => {
  initializeData()
})
</script>

<style scoped>
/* Smooth transitions */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease, transform 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  transform: translateY(10px);
}

.direction-ltr {
  direction: ltr;
}

/* Custom scrollbar */
::-webkit-scrollbar {
  width: 8px;
}

::-webkit-scrollbar-track {
  background: #f1f1f1;
  border-radius: 4px;
}

::-webkit-scrollbar-thumb {
  background: #888;
  border-radius: 4px;
}

::-webkit-scrollbar-thumb:hover {
  background: #555;
}

/* Animation for password strength */
@keyframes pulse {
  0%, 100% { opacity: 1; }
  50% { opacity: 0.7; }
}

.animate-pulse {
  animation: pulse 2s cubic-bezier(0.4, 0, 0.6, 1) infinite;
}
</style>