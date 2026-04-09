<script setup>
import { ref, computed } from 'vue'
import { RouterLink } from 'vue-router'
import { ShoppingBasket } from 'lucide-vue-next'
import TheNavbar from '../components/layout/TheNavbar.vue'
import TheFooter from '../components/layout/TheFooter.vue'
import CategoryFilter from '../components/ui/CategoryFilter.vue'
import ketumbarImg from '../assets/images/ketumbar.jpg'

const categories = ['Semua', 'Daun Hijau', 'Akar & Umbi', 'Buah Sayur', 'Organik']
const activeCategory = ref('Semua')

const products = [
  { id: 1, name: 'Bayam', description: 'Segar, organik, 250gr', price: 'Rp. 12.000', category: 'Daun Hijau' },
  { id: 2, name: 'Dhanikun', description: 'Sayuran hidroponik premium', price: 'Rp. 20.000', category: 'Daun Hijau' },
  { id: 3, name: 'Wortel Organik', description: 'Manis dan renyah, 500gr', price: 'Rp. 15.000', category: 'Akar & Umbi' },
  { id: 4, name: 'Tomat Cherry', description: 'Kualitas grade A, 200gr', price: 'Rp. 18.000', category: 'Buah Sayur' },
  { id: 5, name: 'Brokoli', description: 'Segar tanpa pestisida, per pcs', price: 'Rp. 22.000', category: 'Organik' },
  { id: 6, name: 'Selada Keriting', description: 'Hidroponik bebas hama, per ikat', price: 'Rp. 10.000', category: 'Daun Hijau' },
  { id: 7, name: 'Terong Ungu', description: 'Pilihan kebun lokal, 500gr', price: 'Rp. 14.000', category: 'Buah Sayur' },
  { id: 8, name: 'Paprika Mix', description: 'Warna-warni segar, per pcs', price: 'Rp. 16.000', category: 'Buah Sayur' },
]

const filteredProducts = computed(() => {
  if (activeCategory.value === 'Semua') return products
  return products.filter((p) => p.category === activeCategory.value)
})
</script>

<template>
  <div class="min-h-screen bg-gray-50">
    <TheNavbar />

    <main class="max-w-6xl mx-auto px-6 py-10">
      <!-- Hero -->
      <div class="mb-8">
        <h1 class="text-4xl font-bold text-green-800 mb-2">Rak Sayur</h1>
        <p class="text-sm text-gray-500 max-w-sm leading-relaxed">
          Pilihan sayuran premium yang dipanen pagi ini dari kebun mitra kami. Segar,
          organik, dan penuh nutrisi untuk keluarga Anda.
        </p>
      </div>

      <!-- Category Filter -->
      <div class="mb-8">
        <CategoryFilter
          :categories="categories"
          :activeCategory="activeCategory"
          @update:activeCategory="activeCategory = $event"
        />
      </div>

      <!-- Product Grid -->
      <div class="grid grid-cols-2 md:grid-cols-4 gap-4">
        <RouterLink
          v-for="product in filteredProducts"
          :key="product.id"
          :to="`/rak-sayur/${product.id}`"
          class="bg-white rounded-2xl overflow-hidden border border-gray-100 hover:shadow-md transition-shadow"
        >
          <!-- Image -->
          <div class="relative">
            <img
              :src="ketumbarImg"
              :alt="product.name"
              class="w-full aspect-square object-cover"
            />
            <span
              class="absolute top-3 left-3 bg-green-600 text-white text-[10px] font-semibold px-2.5 py-0.5 rounded"
            >
              Tersedia
            </span>
          </div>

          <!-- Info -->
          <div class="p-4">
            <h3 class="font-bold text-gray-900 text-sm">{{ product.name }}</h3>
            <p class="text-xs text-gray-400 mt-0.5 mb-3">{{ product.description }}</p>
            <div class="flex items-center justify-between">
              <span class="font-bold text-green-800 text-sm">{{ product.price }}</span>
              <button
                class="flex items-center gap-1.5 px-3 py-1.5 bg-green-700 text-white text-xs font-semibold rounded-lg hover:bg-green-600 transition-colors"
              >
                <ShoppingBasket :size="12" />
                Pesan
              </button>
            </div>
          </div>
        </RouterLink>
      </div>
    </main>

    <TheFooter />
  </div>
</template>
