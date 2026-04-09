<script setup>
import { ref, computed } from 'vue'
import CategoryFilter from '../ui/CategoryFilter.vue'
import ProductCard from '../ui/ProductCard.vue'

const categories = ['Semua', 'Daun Hijau', 'Umbi-umbian', 'Buah Sayur']
const activeCategory = ref('Semua')

const products = [
  {
    id: 1,
    name: 'Dhanikun',
    description: 'Ketumbar segar per 250gr',
    price: 'Rp 8.500',
    badge: 'ORGANIK',
    category: 'Daun Hijau',
    inCart: false,
    image: new URL('@/assets/images/ketumbar.jpg', import.meta.url).href,
  },
  {
    id: 2,
    name: 'Bayam',
    description: 'Bayam hijau segar per ikat',
    price: 'Rp 5.000',
    badge: 'HIDROPONIK',
    category: 'Daun Hijau',
    inCart: true,
    image: new URL('@/assets/images/ketumbar.jpg', import.meta.url).href,
  },
  {
    id: 3,
    name: 'Wortel Lokal',
    description: 'Wortel manis per 500gr',
    price: 'Rp 12.000',
    badge: null,
    category: 'Umbi-umbian',
    inCart: false,
    image: new URL('@/assets/images/ketumbar.jpg', import.meta.url).href,
  },
  {
    id: 4,
    name: 'Tomat Cherry',
    description: 'Tomat segar manis per pack',
    price: 'Rp 15.000',
    badge: null,
    category: 'Buah Sayur',
    inCart: false,
    image: new URL('@/assets/images/ketumbar.jpg', import.meta.url).href,
  },
]

const filteredProducts = computed(() =>
  activeCategory.value === 'Semua'
    ? products
    : products.filter((p) => p.category === activeCategory.value),
)
</script>

<template>
  <section class="py-16">
    <div class="max-w-6xl mx-auto px-6">
      <!-- Header -->
      <div class="flex items-end justify-between mb-8">
        <div>
          <h2 class="text-3xl font-extrabold text-gray-900">
            Pilihan Sayur <span class="text-green-600">Minggu Ini</span>
          </h2>
          <p class="text-sm text-gray-400 mt-1">
            Produk pilihan terbaik yang baru saja dipanen pagi ini.
          </p>
        </div>
        <CategoryFilter
          :categories="categories"
          :active-category="activeCategory"
          @update:active-category="activeCategory = $event"
        />
      </div>

      <!-- Product Grid -->
      <div class="grid grid-cols-4 gap-5">
        <ProductCard v-for="product in filteredProducts" :key="product.id" :product="product" />
      </div>
    </div>
  </section>
</template>
