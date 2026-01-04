<template>
  <section class="py-16 bg-gradient-to-b from-gray-50 to-white">
    <div class="container mx-auto px-4">
      <div class="text-center mb-12">
        <div
          class="inline-flex items-center gap-2 bg-gradient-to-r from-blue-50 to-blue-100 text-blue-700 px-6 py-2 rounded-full mb-4"
        >
          <span class="text-xl">⭐</span>
          <span class="font-semibold">محصولات ویژه</span>
        </div>
        <h2 class="text-3xl md:text-4xl font-bold text-gray-900 mb-4">
          قطعات منتخب
        </h2>
        <p class="text-lg text-gray-600 max-w-2xl mx-auto">
          قطعات با کیفیت با گارانتی معتبر
        </p>
      </div>

      <!-- Grid of Products -->
      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
        <div
          v-for="product in featuredProducts"
          :key="product.id"
          class="bg-white rounded-xl shadow-md hover:shadow-xl transition-all duration-300 border border-gray-200 overflow-hidden group"
        >
          <!-- Product Image/Icon -->
          <div class="relative h-48 overflow-hidden">
            <div
              :class="[
                'w-full h-full flex items-center justify-center transition-transform duration-500 group-hover:scale-105',
                product.category === 'یخچال'
                  ? 'bg-gradient-to-br from-blue-50 to-blue-100'
                  : product.category === 'لباسشویی'
                  ? 'bg-gradient-to-br from-purple-50 to-purple-100'
                  : product.category === 'ظرفشویی'
                  ? 'bg-gradient-to-br from-green-50 to-green-100'
                  : product.category === 'اجاق گاز'
                  ? 'bg-gradient-to-br from-red-50 to-red-100'
                  : 'bg-gradient-to-br from-gray-50 to-gray-100',
              ]"
            >
              <div
                class="w-24 h-24 bg-white rounded-2xl flex items-center justify-center shadow-lg"
              >
                <img :src="product.image" alt="">
              </div>
            </div>

            <!-- Badges -->
            <div class="absolute top-3 left-3 flex flex-col gap-2">
              <span
                v-if="product.discount"
                class="bg-red-500 text-white text-xs font-bold px-3 py-1 rounded-full"
              >
                {{ product.discount }}% تخفیف
              </span>
              <span
                v-if="product.isNew"
                class="bg-green-500 text-white text-xs font-bold px-3 py-1 rounded-full"
              >
                جدید
              </span>
            </div>
          </div>

          <!-- Product Info -->
          <div class="p-5">
            <!-- Category & Brand -->
            <div class="flex items-center gap-2 mb-3">
              <span
                class="text-xs bg-blue-50 text-blue-600 px-2 py-1 rounded"
                >{{ product.category }}</span
              >
              <span
                class="text-xs bg-gray-100 text-gray-600 px-2 py-1 rounded"
                >{{ product.brand }}</span
              >
            </div>

            <!-- Product Name -->
            <h3
              class="font-bold text-gray-900 mb-3 line-clamp-2 text-base h-12"
            >
              {{ product.name }}
            </h3>

            <!-- Compatibility -->
            <p class="text-sm text-gray-500 mb-4 line-clamp-2 h-10">
              {{ product.compatibility }}
            </p>

            <!-- Price & Rating -->
            <div class="flex items-center justify-between mb-4">
              <div>
                <div class="flex items-center gap-2">
                  <span class="text-xl font-bold text-gray-900">{{
                    formatPrice(product.price)
                  }}</span>
                  <span
                    v-if="product.originalPrice"
                    class="text-sm text-gray-400 line-through"
                  >
                    {{ formatPrice(product.originalPrice) }}
                  </span>
                </div>
                <div class="text-xs text-gray-500 mt-1">تومان</div>
              </div>

              <div class="flex items-center gap-1">
                <div class="flex items-center">
                  <span
                    v-for="i in 5"
                    :key="i"
                    :class="[
                      'text-sm',
                      i <= Math.floor(product.rating)
                        ? 'text-yellow-400'
                        : 'text-gray-300',
                    ]"
                  >
                    ★
                  </span>
                </div>
                <span class="text-xs text-gray-500"
                  >({{ product.reviews }})</span
                >
              </div>
            </div>

            <!-- Add to Cart Button -->
            <button
              @click="addToCart(product)"
              class="w-full bg-blue-600 hover:bg-blue-700 text-white py-3 rounded-lg font-medium transition flex items-center justify-center gap-2"
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
                  d="M12 6v6m0 0v6m0-6h6m-6 0H6"
                />
              </svg>
              افزودن به سبد خرید
            </button>
          </div>
        </div>
      </div>

      <!-- View All Button -->
      <div class="text-center mt-12">
        <a
          href="/products"
          class="inline-flex items-center gap-2 text-blue-600 hover:text-blue-700 font-medium text-lg"
        >
          مشاهده همه محصولات
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
              d="M14 5l7 7m0 0l-7 7m7-7H3"
            />
          </svg>
        </a>
      </div>
    </div>
  </section>
</template>

<script setup>
const featuredProducts = [
  {
    id: 1,
    name: "کمپرسور یخچال سامسونگ مدل DA97-12606A",
    icon: "❄️",
    image: "/cool.webp",
    price: 1850000,
    originalPrice: 2200000,
    discount: 15,
    category: "یخچال",
    brand: "سامسونگ",
    compatibility: "مناسب برای مدل‌های RS50, RS55, RS60",
    rating: 4.8,
    reviews: 42,
    isNew: true,
  },
  {
    id: 2,
    name: "موتور ماشین لباسشویی ال جی مدل 4681EA2001T",
    icon: "🧺",
    image: "/machin-leb.jpg",
    price: 1250000,
    originalPrice: 1450000,
    discount: 14,
    category: "لباسشویی",
    brand: "ال جی",
    compatibility: "مناسب برای سری F4",
    rating: 4.6,
    reviews: 38,
    isNew: false,
  },
  {
    id: 3,
    name: "برد کنترل ماشین ظرفشویی بوش مدل SGV46A33",
    icon: "🍽️",
    image: "/machin-zarf.jpg",
    price: 980000,
    originalPrice: null,
    discount: null,
    category: "ظرفشویی",
    brand: "بوش",
    compatibility: "سری SMS46, SMS48",
    rating: 4.9,
    reviews: 51,
    isNew: true,
  },
  {
    id: 4,
    name: "ترموکوپل اجاق گاز اسنوا مدل TC-105",
    icon: "🔥",
    image: "/ojagh.jpg",
    price: 85000,
    originalPrice: 120000,
    discount: 29,
    category: "اجاق گاز",
    brand: "اسنوا",
    compatibility: "تمام مدل‌های اسنوا",
    rating: 4.4,
    reviews: 29,
    isNew: false,
  },
  {
    id: 5,
    name: "کمپرسور کولر گازی جنرال مدل R410A",
    icon: "💨",
    image: "/hood.jpg",
    price: 2150000,
    originalPrice: null,
    discount: null,
    category: "کولر",
    brand: "جنرال",
    compatibility: "مدل‌های 18000 و 24000 BTU",
    rating: 4.7,
    reviews: 47,
    isNew: true,
  },
  {
    id: 6,
    name: "المنت ماشین لباسشویی پارس خزر مدل PH-HEAT-01",
    icon: "⚡",
    image: "/macro.jpg",
    price: 145000,
    originalPrice: 180000,
    discount: 19,
    category: "لباسشویی",
    brand: "پارس خزر",
    compatibility: "مدل‌های PHW-8000",
    rating: 4.5,
    reviews: 33,
    isNew: false,
  },
  {
    id: 7,
    name: "فن کولر گازی ال جی مدل FAN-LG-2023",
    icon: "🌀",
    image: "/coffe.jpg",
    price: 420000,
    originalPrice: null,
    discount: null,
    category: "کولر",
    brand: "ال جی",
    compatibility: "سری QM, QP",
    rating: 4.6,
    reviews: 41,
    isNew: true,
  },
  {
    id: 8,
    name: "ترموستات یخچال دوو مدل TSTAT-88",
    icon: "🌡️",
    image: "/cooler.png",
    price: 75000,
    originalPrice: 95000,
    discount: 21,
    category: "یخچال",
    brand: "دوو",
    compatibility: "مدل‌های DFR, DFRX",
    rating: 4.3,
    reviews: 27,
    isNew: false,
  },
];

const formatPrice = (price) => {
  return price.toLocaleString("fa-IR");
};

const addToCart = (product) => {
  console.log("Added to cart:", product.name);
  // Emit event or call store action
  alert(`محصول "${product.name}" به سبد خرید اضافه شد`);
};
</script>

<style scoped>
/* Simple styling */
.line-clamp-2 {
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.line-clamp-3 {
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.transition-all {
  transition-property: all;
}

.duration-300 {
  transition-duration: 300ms;
}

.duration-500 {
  transition-duration: 500ms;
}
</style>
