<script setup>
import { RouterLink, useRoute } from 'vue-router'
import { ShoppingCart } from 'lucide-vue-next'

const route = useRoute()
</script>

<template>
  <nav class="w-full bg-white border-b border-gray-100 sticky top-0 z-50">
    <div class="max-w-6xl mx-auto px-6 py-4 flex items-center justify-between">
      <!-- Logo -->
      <RouterLink to="/" class="text-xl font-bold text-green-700">Wlijoku</RouterLink>

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
          class="text-sm font-semibold text-gray-500 hover:text-gray-900 transition-colors"
        >
          Rak Sayur
        </RouterLink>
      </div>

      <!-- Actions -->
      <div class="flex items-center gap-3">
        <button class="p-2 text-gray-500 hover:text-gray-900 transition-colors">
          <ShoppingCart :size="20" />
        </button>
        <button
          class="px-5 py-2 bg-green-900 text-white text-sm font-semibold rounded-full hover:bg-green-800 transition-colors"
        >
          Masuk
        </button>
      </div>
    </div>
  </nav>
</template>
