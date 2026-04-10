<script setup>
import { RouterLink, useRoute } from 'vue-router'
import { ShoppingCart, Search } from 'lucide-vue-next'

const route = useRoute()
</script>

<template>
  <nav class="w-full bg-white border-b border-gray-100 sticky top-0 z-50">
    <div class="max-w-6xl mx-auto px-6 py-4 flex items-center gap-6 justify-between">
      <!-- Logo -->
      <RouterLink to="/" class="text-xl font-bold text-green-700 shrink-0">Wlijoku</RouterLink>

      <!-- Nav Links -->
      <div class="flex items-center gap-8">
        <RouterLink
          to="/"
          class="text-sm font-semibold transition-colors"
          :class="route.name === 'home' ? 'text-gray-900' : 'text-gray-500 hover:text-gray-900'"
        >
          Home
        </RouterLink>
        <RouterLink
          to="/rak-sayur"
          class="text-sm font-semibold transition-colors"
          :class="
            route.name === 'rak-sayur'
              ? 'text-gray-900 underline underline-offset-4'
              : 'text-gray-500 hover:text-gray-900'
          "
        >
          Rak Sayur
        </RouterLink>
      </div>

      <!-- Search -->
      <div class="flex-1 max-w-md">
        <div class="relative">
          <Search class="absolute left-3 top-1/2 -translate-y-1/2 text-gray-400" :size="16" />
          <input
            type="text"
            placeholder="Cari Sayuran Anda"
            class="w-full pl-9 pr-4 py-2 rounded-full border border-gray-200 text-sm focus:outline-none focus:border-green-400"
          />
        </div>
      </div>

      <!-- Actions -->
      <div class="flex items-center gap-3">
        <RouterLink
          to="/keranjang"
          class="relative p-2 text-gray-500 hover:text-gray-900 transition-colors"
        >
          <ShoppingCart :size="20" />
          <span class="absolute -top-0.5 -right-0.5 w-4 h-4 bg-green-600 text-white text-[9px] font-bold rounded-full flex items-center justify-center">
            2
          </span>
        </RouterLink>
        <button
          class="px-5 py-2 bg-green-900 text-white text-sm font-semibold rounded-full hover:bg-green-800 transition-colors"
        >
          Masuk
        </button>
      </div>
    </div>
  </nav>
</template>
