<template>
  <nav class="sticky top-0 z-50 bg-white shadow-md">
    <!-- ==================== موبایل ==================== -->
    <div class="lg:hidden bg-white border-b">
      <div class="flex items-center justify-between px-4 py-3">
        <button @click="toggleMobileSidebar" class="p-2">
          <svg
            class="w-6 h-6 text-gray-700"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M4 6h16M4 12h16M4 18h16"
            />
          </svg>
        </button>

        <!-- لوگو آرا سرویس موبایل -->
        <div class="flex items-center">
          <nuxt-link to="/">
            <div class="text-xl font-bold">
              <span class="text-blue-600">آرا</span>
              <span class="text-gray-800">سرویس</span>
            </div>
          </nuxt-link>
        </div>
        <nuxt-link to="/cart">
          <button class="relative p-2">
          <svg
            class="w-6 h-6 text-gray-700"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M3 3h2l.4 2M7 13h10l4-8H5.4M7 13L5.4 5M7 13l-2.293 2.293c-.63.63-.184 1.707.707 1.707H17m0 0a2 2 0 100 4 2 2 0 000-4zm-8 2a2 2 0 11-4 0 2 2 0 014 0z"
            />
          </svg>
          <span
            class="absolute -top-1 -right-1 bg-red-500 text-white text-xs rounded-full w-4 h-4 flex items-center justify-center"
            >۳</span
          >
        </button>
        </nuxt-link>
      </div>
    </div>

    <!-- سایدبار موبایل -->
    <div
      :class="[
        'fixed inset-0 z-50 lg:hidden transition-all duration-300',
        mobileSidebarOpen ? 'visible' : 'invisible',
      ]"
    >
      <div
        :class="[
          'absolute inset-0 bg-black transition-opacity duration-300',
          mobileSidebarOpen ? 'opacity-50' : 'opacity-0',
        ]"
        @click="toggleMobileSidebar"
      ></div>

      <div
        :class="[
          'absolute right-0 top-0 h-full w-80 bg-white shadow-xl transform transition-transform duration-300 overflow-y-auto',
          mobileSidebarOpen ? 'translate-x-0' : 'translate-x-full',
        ]"
      >
        <!-- هدر سایدبار -->
        <div
          class="flex items-center justify-between p-4 border-b bg-gradient-to-r from-blue-50 to-gray-50"
        >
          <nuxt-link to="/">
            <div class="flex items-center">
            <div class="text-xl font-bold">
              <span class="text-blue-600">آرا</span>
              <span class="text-gray-800">سرویس</span>
            </div>
            <span
              class="text-xs bg-gradient-to-r from-blue-500 to-blue-600 text-white px-2 py-1 rounded-full mr-2"
              >قطعات</span
            >
          </div>
          </nuxt-link>
          <button @click="toggleMobileSidebar" class="p-2">
            <svg
              class="w-6 h-6 text-gray-500"
              fill="none"
              stroke="currentColor"
              viewBox="0 0 24 24"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M6 18L18 6M6 6l12 12"
              />
            </svg>
          </button>
        </div>

        <div class="p-4">
          <!-- جستجو -->
          <div class="mb-6">
            <div class="relative">
              <input
                type="text"
                placeholder="جستجوی قطعه در آرا سرویس..."
                class="w-full px-4 py-3 border-2 border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 outline-none bg-gray-50"
              />
              <button
                class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-500"
              >
                <svg
                  class="w-5 h-5"
                  fill="none"
                  stroke="currentColor"
                  viewBox="0 0 24 24"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"
                  />
                </svg>
              </button>
            </div>
          </div>

          <!-- دسته‌بندی‌های موبایل -->
          <div class="mb-6">
            <h3 class="text-sm font-semibold text-gray-700 mb-3 pb-2 border-b">
              دسته‌بندی قطعات آرا سرویس
            </h3>
            <div class="space-y-1">
              <div
                v-for="category in categoriesData"
                :key="category.id"
                class="border-b border-gray-100 last:border-b-0"
              >
                <button
                  @click="toggleMobileSubmenu(category.id)"
                  class="w-full flex items-center justify-between px-3 py-4 text-right text-gray-700 hover:bg-blue-50 rounded-lg transition-all duration-200"
                >
                  <span class="text-sm font-medium">{{ category.name }}</span>
                  <svg
                    class="w-4 h-4 text-gray-400 transition-transform duration-200"
                    :class="{ 'rotate-90': openMobileSubmenu === category.id }"
                    fill="none"
                    stroke="currentColor"
                    viewBox="0 0 24 24"
                  >
                    <path
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      stroke-width="2"
                      d="M9 5l7 7-7 7"
                    />
                  </svg>
                </button>

                <div
                  v-if="openMobileSubmenu === category.id"
                  class="overflow-hidden transition-all duration-300"
                  :class="
                    openMobileSubmenu === category.id
                      ? 'max-h-96 opacity-100'
                      : 'max-h-0 opacity-0'
                  "
                >
                  <div class="pr-4 pb-3 space-y-2">
                    <a
                      v-for="sub in category.subcategories"
                      :key="sub.slug"
                      href="#"
                      class="block py-2 px-4 text-sm text-gray-600 hover:text-blue-600 hover:bg-blue-50 rounded-lg"
                    >
                      • {{ sub.name }}
                    </a>

                    <div class="pt-2 border-t border-gray-100 mt-2">
                      <nuxt-link to="/category"
                        class="block py-2 px-4 text-xs text-blue-600 hover:text-blue-700 hover:bg-blue-50 rounded-lg font-medium"
                      >
                        مشاهده در آرا سرویس →
                      </nuxt-link>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <!-- خدمات موبایل -->
          <div class="mb-6">
            <h3 class="text-sm font-semibold text-gray-700 mb-3">
              خدمات آرا سرویس
            </h3>
            <div class="space-y-2">
              <a
                href="https://araservice.co/services/repair"
                target="_blank"
                class="flex items-center px-3 py-2 text-sm text-gray-700 hover:bg-blue-50 rounded-lg"
              >
                <div class="w-2 h-2 bg-blue-500 rounded-full ml-3"></div>
                تعمیرات تخصصی لوازم خانگی
              </a>
              <a
                href="https://araservice.co/services/installation"
                target="_blank"
                class="flex items-center px-3 py-2 text-sm text-gray-700 hover:bg-blue-50 rounded-lg"
              >
                <div class="w-2 h-2 bg-blue-500 rounded-full ml-3"></div>
                نصب و راه‌اندازی حرفه‌ای
              </a>
              <a
                href="https://araservice.co/services/maintenance"
                target="_blank"
                class="flex items-center px-3 py-2 text-sm text-gray-700 hover:bg-blue-50 rounded-lg"
              >
                <div class="w-2 h-2 bg-blue-500 rounded-full ml-3"></div>
                سرویس دوره‌ای و نگهداری
              </a>
            </div>
          </div>

          <!-- حساب کاربری موبایل -->
          <div class="border-t pt-6">
            <div class="space-y-2">
              <a
                href="https://araservice.co/profile"
                target="_blank"
                class="flex items-center space-x-3 px-3 py-3 text-gray-700 hover:bg-gray-100 rounded-lg"
              >
                <svg
                  class="w-5 h-5 text-gray-500"
                  fill="none"
                  stroke="currentColor"
                  viewBox="0 0 24 24"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z"
                  />
                </svg>
                <span>حساب کاربری</span>
              </a>

              <a
                href="https://araservice.co/orders"
                target="_blank"
                class="flex items-center space-x-3 px-3 py-3 text-gray-700 hover:bg-gray-100 rounded-lg"
              >
                <svg
                  class="w-5 h-5 text-gray-500"
                  fill="none"
                  stroke="currentColor"
                  viewBox="0 0 24 24"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2"
                  />
                </svg>
                <span>سفارش‌های من</span>
              </a>

              <a
                href="https://araservice.co/logout"
                target="_blank"
                class="flex items-center space-x-3 px-3 py-3 text-gray-700 hover:bg-gray-100 rounded-lg"
              >
                <svg
                  class="w-5 h-5 text-gray-500"
                  fill="none"
                  stroke="currentColor"
                  viewBox="0 0 24 24"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M17 16l4-4m0 0l-4-4m4 4H7m6 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h4a3 3 0 013 3v1"
                  />
                </svg>
                <span>خروج</span>
              </a>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- ==================== دسکتاپ ==================== -->
    <div class="hidden lg:block shadow-s">
      <!-- هدر بالایی دسکتاپ -->
      <div
        class="bg-gradient-to-r from-blue-50 to-gray-50 border-b border-gray-200"
      >
        <div class="container mx-auto px-6 py-2">
          <div class="flex items-center justify-between">
            <!-- خدمات دسکتاپ -->
            <div class="flex items-center space-x-6">
              <div class="flex items-center space-x-2 text-sm text-gray-700">
                <svg
                  class="w-5 h-5 text-green-600"
                  fill="none"
                  stroke="currentColor"
                  viewBox="0 0 24 24"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"
                  />
                </svg>
                <span class="font-medium">ضمانت ۱۸ ماهه آرا سرویس</span>
              </div>

              <div class="flex items-center space-x-2 text-sm text-gray-700">
                <svg
                  class="w-5 h-5 text-blue-600"
                  fill="none"
                  stroke="currentColor"
                  viewBox="0 0 24 24"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"
                  />
                </svg>
                <span class="font-medium">ارسال سریع ۲۴ ساعته</span>
              </div>

              <div class="flex items-center space-x-2 text-sm text-gray-700">
                <svg
                  class="w-5 h-5 text-red-500"
                  fill="none"
                  stroke="currentColor"
                  viewBox="0 0 24 24"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z"
                  />
                </svg>
                <span class="font-medium">پرداخت امن بانکی</span>
              </div>
            </div>

            <!-- تماس دسکتاپ -->
            <div class="flex items-center space-x-4">
              <div class="text-gray-700 text-sm">
                <span class="text-gray-600">پشتیبانی:</span>
                <a
                  href="tel:02188888888"
                  class="font-bold text-blue-600 hover:text-blue-800 mr-1"
                  >۰۲۱-۸۸۸۸۸۸۸۸</a
                >
              </div>
              <a
                href="https://araservice.co/login"
                target="_blank"
                class="text-sm text-blue-600 hover:text-blue-800 font-medium"
              >
                ورود | ثبت‌نام
              </a>
            </div>
          </div>
        </div>
      </div>

      <!-- بخش اصلی دسکتاپ -->
      <div class="container mx-auto px-6 py-4">
        <div class="flex items-center justify-between mb-4">
          <!-- لوگو و دسته‌بندی‌ها -->
          <div class="flex items-center space-x-8">
            <!-- لوگو آرا سرویس -->
            <div class="flex items-center space-x-3">
              <nuxt-link to="/">
                <div class="flex items-center">
                  <div class="text-3xl font-bold">
                    <span class="text-blue-600">آرا</span>
                    <span class="text-gray-900">سرویس</span>
                  </div>
                  <span
                    class="text-xs bg-gradient-to-r from-blue-500 to-blue-600 text-white px-3 py-1 rounded-full mr-3 font-medium"
                  >
                    فروشگاه قطعات
                  </span>
                </div>
              </nuxt-link>
            </div>
          </div>

          <!-- جستجو -->
          <div class="relative w-1/3">
            <input
              type="text"
              placeholder="جستجوی قطعه، مدل دستگاه یا شماره قطعه..."
              class="w-full px-5 py-3 pr-12 border-2 border-gray-300 rounded-full focus:ring-2 focus:ring-blue-500 focus:border-blue-500 outline-none shadow-sm"
            />
            <button
              class="absolute left-4 top-1/2 transform -translate-y-1/2 text-gray-500 hover:text-blue-600 transition-colors"
            >
              <svg
                class="w-5 h-5"
                fill="none"
                stroke="currentColor"
                viewBox="0 0 24 24"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"
                />
              </svg>
            </button>
          </div>

          <!-- آیکون‌های کاربر -->
          <div class="flex items-center space-x-6 gap-2">
            <nuxt-link to="/cart">
              <button class="relative group">
              <div
                class="flex items-center space-x-2 text-gray-700 hover:text-blue-700 transition-colors"
              >
                <div class="relative">
                  <svg
                    class="w-7 h-7"
                    fill="none"
                    stroke="currentColor"
                    viewBox="0 0 24 24"
                  >
                    <path
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      stroke-width="2"
                      d="M16 11V7a4 4 0 00-8 0v4M5 9h14l1 12H4L5 9z"
                    />
                  </svg>
                  <span
                    class="absolute -top-2 -right-2 bg-red-500 text-white text-xs rounded-full w-5 h-5 flex items-center justify-center font-bold"
                    >۳</span
                  >
                </div>
                <div class="text-right">
                  <div class="text-sm font-medium">سبد خرید</div>
                </div>
              </div>
            </button>
            </nuxt-link>

            <div class="relative">
              <button
                @click="toggleUserMenu"
                class="flex items-center space-x-2 text-gray-700 hover:text-blue-700 group transition-colors gap-2"
              >
                <div
                  class="w-10 h-10 bg-blue-100 rounded-full flex items-center justify-center group-hover:bg-blue-200 transition-colors"
                >
                  <svg
                    class="w-5 h-5 text-blue-600"
                    fill="none"
                    stroke="currentColor"
                    viewBox="0 0 24 24"
                  >
                    <path
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      stroke-width="2"
                      d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z"
                    />
                  </svg>
                </div>
                <div class="text-right">
                  <div class="text-sm font-medium">حساب کاربری</div>
                </div>
              </button>

              <!-- منوی کاربر -->
              <div
                v-if="userMenuOpen"
                class="absolute left-0 mt-3 w-56 bg-white rounded-xl shadow-2xl border z-50 overflow-hidden"
              >
                <div
                  class="p-4 border-b bg-gradient-to-r from-blue-50 to-gray-50"
                >
                  <div class="font-medium text-gray-900">
                    حساب کاربری آرا سرویس
                  </div>
                  <div class="text-xs text-gray-500">
                    برای دسترسی به همه خدمات
                  </div>
                </div>
                <div class="py-2">
                  <a
                    href="https://araservice.co/profile"
                    target="_blank"
                    class="flex items-center px-4 py-3 text-sm text-gray-700 hover:bg-blue-50 hover:text-blue-700 transition-colors"
                  >
                    <svg
                      class="w-5 h-5 ml-3 text-gray-500"
                      fill="none"
                      stroke="currentColor"
                      viewBox="0 0 24 24"
                    >
                      <path
                        stroke-linecap="round"
                        stroke-linejoin="round"
                        stroke-width="2"
                        d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z"
                      />
                    </svg>
                    پروفایل کاربری
                  </a>
                  <a
                    href="https://araservice.co/orders"
                    target="_blank"
                    class="flex items-center px-4 py-3 text-sm text-gray-700 hover:bg-blue-50 hover:text-blue-700 transition-colors"
                  >
                    <svg
                      class="w-5 h-5 ml-3 text-gray-500"
                      fill="none"
                      stroke="currentColor"
                      viewBox="0 0 24 24"
                    >
                      <path
                        stroke-linecap="round"
                        stroke-linejoin="round"
                        stroke-width="2"
                        d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2"
                      />
                    </svg>
                    سفارش‌های من
                  </a>
                  <a
                    href="https://araservice.co/logout"
                    target="_blank"
                    class="flex items-center px-4 py-3 text-sm text-red-600 hover:bg-red-50 transition-colors"
                  >
                    <svg
                      class="w-5 h-5 ml-3"
                      fill="none"
                      stroke="currentColor"
                      viewBox="0 0 24 24"
                    >
                      <path
                        stroke-linecap="round"
                        stroke-linejoin="round"
                        stroke-width="2"
                        d="M17 16l4-4m0 0l-4-4m4 4H7m6 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h4a3 3 0 013 3v1"
                      />
                    </svg>
                    خروج از حساب
                  </a>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- ردیف دوم: منوی دسته‌بندی‌ها -->
        <div class="border-t border-gray-200 pt-3">
          <div class="flex items-center space-x-8 space-x-reverse">
            <!-- دکمه اصلی دسته‌بندی‌ها -->
            <div
              class="relative group"
              @mouseenter="showAllCategories = true"
              @mouseleave="hideAllCategories"
            >
              <button
                class="flex items-center px-5 py-3 bg-gradient-to-r from-blue-600 to-blue-700 text-white rounded-xl hover:from-blue-700 hover:to-blue-800 transition-all duration-300 shadow-lg hover:shadow-xl"
              >
                <svg
                  class="w-5 h-5 ml-2"
                  fill="none"
                  stroke="currentColor"
                  viewBox="0 0 24 24"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M4 6h16M4 12h16M4 18h16"
                  />
                </svg>
                دسته‌بندی قطعات
                <svg
                  class="w-4 h-4 mr-2 transition-transform duration-300"
                  :class="{ 'rotate-180': showAllCategories }"
                  fill="none"
                  stroke="currentColor"
                  viewBox="0 0 24 24"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M19 9l-7 7-7-7"
                  />
                </svg>
              </button>

              <!-- منوی کشویی دسکتاپ -->
              <div
                v-if="showAllCategories"
                class="absolute right-0 mt-3 w-[900px] bg-white rounded-xl shadow-2xl border z-50 overflow-hidden"
              >
                <div class="grid grid-cols-4 gap-10 p-6">
                  <div
                    v-for="(category, index) in categoriesData.slice(0, 5)"
                    :key="category.id"
                    :class="{ ' border-gray-200 pl-5': index > 0 }"
                  >
                    <h3
                      class="text-blue-600 text-sm font-semibold mb-4 pb-2 border-b"
                    >
                      {{ category.icon }}
                      {{ category.name.replace("قطعات ", "") }}
                    </h3>
                    <div>
                      <a
                        v-for="sub in category.subcategories.slice(0, 5)"
                        :key="sub.slug"
                        href="#"
                        class="flex items-center py-2 text-sm text-gray-700 hover:text-blue-600 transition-colors group/subitem"
                      >
                        <div
                          class="w-1.5 h-1.5 bg-blue-200 rounded-full ml-3 group-hover/subitem:bg-blue-500 transition-colors"
                        ></div>
                        <span>{{ sub.name }}</span>
                      </a>
                    </div>
                  </div>
                </div>

                <div
                  class="mt-6 pt-6 border-t p-6 bg-gradient-to-r from-blue-50 to-gray-50"
                >
                  <div class="flex items-center justify-between">
                    <nuxt-link to="/category"
                      href="https://araservice.co/categories"
                      target="_blank"
                      class="inline-flex items-center text-blue-600 hover:text-blue-700 font-medium text-sm"
                    >
                      <svg
                        class="w-4 h-4 ml-2"
                        fill="none"
                        stroke="currentColor"
                        viewBox="0 0 24 24"
                      >
                        <path
                          stroke-linecap="round"
                          stroke-linejoin="round"
                          stroke-width="2"
                          d="M14 5l7 7m0 0l-7 7m7-7H3"
                        />
                      </svg>
                      مشاهده همه دسته‌بندی‌ها در آرا سرویس
                    </nuxt-link>
                    <div class="text-xs text-gray-500">
                      بیش از ۱۰,۰۰۰ قطعه اورجینال
                    </div>
                  </div>
                </div>
              </div>
            </div>

            <!-- زیرمنوهای اصلی -->
            <div class="flex items-center space-x-6 space-x-reverse flex-1">
              <a
                href="https://araservice.co/new-arrivals"
                target="_blank"
                class="text-sm text-gray-700 hover:text-blue-700 font-medium rounded-lg hover:bg-blue-50 px-3 py-2 transition-colors"
              >
                جدیدترین قطعات
              </a>
               <a
                href="https://araservice.co/discounts"
                target="_blank"
                class="text-sm text-gray-700 hover:text-blue-700 font-medium rounded-lg hover:bg-blue-50 px-3 py-2 transition-colors"
              >
                قطعات پرفروش
              </a>
              <a
                href="https://araservice.co/discounts"
                target="_blank"
                class="text-sm text-gray-700 hover:text-blue-700 font-medium rounded-lg hover:bg-blue-50 px-3 py-2 transition-colors"
              >
                تخفیف‌های ویژه
              </a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from "vue";

// داده‌های مشترک با فوتر
const categoriesData = [
  {
    id: 1,
    name: "❄️ قطعات یخچال و فریزر",
    subcategories: [
      { name: "کمپرسور", slug: "compressor" },
      { name: "ترموستات", slug: "thermostat" },
      { name: "فن اواپراتور", slug: "evaporator-fan" },
      { name: "برد کنترل", slug: "control-board" },
      { name: "لاستیک درب", slug: "door-gasket" },
      { name: "شیر آب سردکن", slug: "water-dispenser" },
      { name: "فیلتر تصفیه آب", slug: "water-filter" },
    ],
  },
  {
    id: 2,
    name: "🧺 قطعات ماشین لباسشویی",
    subcategories: [
      { name: "موتور (پمپ)", slug: "motor-pump" },
      { name: "تسمه", slug: "belt" },
      { name: "المنت", slug: "heating-element" },
      { name: "سنسور سطح آب", slug: "water-level-sensor" },
      { name: "درب و قفل", slug: "door-lock" },
      { name: "شیر آب ورودی", slug: "inlet-valve" },
      { name: "دمپر ارتعاش", slug: "shock-absorber" },
    ],
  },
  {
    id: 3,
    name: "🍽️ قطعات ماشین ظرفشویی",
    subcategories: [
      { name: "پمپ تخلیه", slug: "drain-pump" },
      { name: "بازوی اسپری", slug: "spray-arm" },
      { name: "المنت خشک کن", slug: "heating-element" },
      { name: "سنسور کثیفی", slug: "turbidity-sensor" },
      { name: "صافی آشغال‌گیر", slug: "filter" },
      { name: "سطل نمک", slug: "salt-container" },
      { name: "جک درب", slug: "door-hinge" },
    ],
  },
  {
    id: 4,
    name: "🔥 قطعات اجاق گاز",
    subcategories: [
      { name: "شیر گاز ۴ شعله", slug: "gas-valve" },
      { name: "ترموکوپل ایمنی", slug: "thermocouple" },
      { name: "شعله‌پخش کن", slug: "burner" },
      { name: "ترانس جرقه‌زن", slug: "ignition-transformer" },
      { name: "شیشه فر", slug: "oven-glass" },
      { name: "گرماتور", slug: "heater" },
      { name: "رگلاتور فشار", slug: "pressure-regulator" },
    ],
  },
  {
    id: 5,
    name: "💨 قطعات کولر و تهویه",
    subcategories: [
      { name: "کمپرسور کولر گازی", slug: "ac-compressor" },
      { name: "فن کندانسور", slug: "condenser-fan" },
      { name: "برد اینورتر", slug: "inverter-board" },
      { name: "سروو موتور", slug: "servo-motor" },
      { name: "سنسور دما", slug: "temperature-sensor" },
      { name: "لوله مسی", slug: "copper-tube" },
      { name: "فیلتر کربنی", slug: "carbon-filter" },
    ],
  },
];

const popularBrands = [
  { name: "سامسونگ", slug: "samsung" },
  { name: "ال جی", slug: "lg" },
  { name: "بوش", slug: "bosch" },
  { name: "اسنوا", slug: "snova" },
  { name: "پارس خزر", slug: "pars-khazar" },
  { name: "دوو", slug: "daewoo" },
  { name: "هیتاچی", slug: "hitachi" },
];

const topSellingParts = [
  "کمپرسور یخچال",
  "موتور لباسشویی",
  "برد کنترل",
  "المنت آبگرمکن",
  "ترموستات",
  "فن کولر",
];

const subMenus = [
  {
    name: "قطعات پرفروش",
    items: topSellingParts,
  },
  {
    name: "برندهای معروف",
    items: popularBrands.map((brand) => brand.name),
  },
  {
    name: "تخفیف‌های ویژه",
    items: ["تخفیف ۲۰٪", "تخفیف ۳۰٪", "تخفیف ۴۵٪"],
  },
];

// State
const mobileSidebarOpen = ref(false);
const showAllCategories = ref(false);
const userMenuOpen = ref(false);
const openMobileSubmenu = ref(null);

// Functions
const toggleMobileSidebar = () => {
  mobileSidebarOpen.value = !mobileSidebarOpen.value;
  if (mobileSidebarOpen.value) {
    document.body.style.overflow = "hidden";
  } else {
    document.body.style.overflow = "auto";
    openMobileSubmenu.value = null;
  }
};

const toggleUserMenu = () => {
  userMenuOpen.value = !userMenuOpen.value;
};

const toggleMobileSubmenu = (categoryId) => {
  openMobileSubmenu.value =
    openMobileSubmenu.value === categoryId ? null : categoryId;
};

const hideAllCategories = () => {
  setTimeout(() => {
    showAllCategories.value = false;
  }, 300);
};

const handleClickOutside = (event) => {
  if (
    !event.target.closest(".fixed") &&
    !event.target.closest(".lg\\:hidden")
  ) {
    mobileSidebarOpen.value = false;
    document.body.style.overflow = "auto";
    openMobileSubmenu.value = null;
  }

  if (!event.target.closest(".relative")) {
    userMenuOpen.value = false;
  }

  if (
    !event.target.closest(".relative") &&
    !event.target.closest(".absolute")
  ) {
    showAllCategories.value = false;
  }
};

onMounted(() => {
  document.addEventListener("click", handleClickOutside);
});

onUnmounted(() => {
  document.removeEventListener("click", handleClickOutside);
  document.body.style.overflow = "auto";
});
</script>

<style scoped>
body {
  overflow-x: hidden;
}

.transition-all {
  transition-property: all;
}

.transition-transform {
  transition-property: transform;
}

.transition-colors {
  transition-property: background-color, border-color, color, fill, stroke;
}

.duration-200 {
  transition-duration: 200ms;
}

.duration-300 {
  transition-duration: 300ms;
}

.max-h-0 {
  max-height: 0;
}

.max-h-96 {
  max-height: 24rem;
}

.shadow-2xl {
  box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25);
}

.h-full {
  height: 100vh;
}

.rotate-90 {
  transform: rotate(90deg);
}

.rotate-180 {
  transform: rotate(180deg);
}

.bg-gradient-to-r {
  background-image: linear-gradient(to right, var(--tw-gradient-stops));
}
</style>
