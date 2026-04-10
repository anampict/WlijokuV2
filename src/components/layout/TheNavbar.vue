<script setup>
import { ref } from 'vue'
import { RouterLink, useRoute } from 'vue-router'
import { ShoppingCart, Search, Menu, X } from 'lucide-vue-next'

const route = useRoute()
const menuOpen = ref(false)
</script>

<template>
  <nav class="w-full bg-white border-b border-gray-100 sticky top-0 z-50">
    <!-- Main Bar -->
    <div class="max-w-6xl mx-auto px-4 md:px-6 py-3 md:py-4 flex items-center gap-4 justify-between">
      <!-- Logo -->
      <RouterLink to="/" class="text-xl font-bold text-green-700 shrink-0">Wlijoku</RouterLink>

      <!-- Nav Links (desktop) -->
      <div class="hidden md:flex items-center gap-8">
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

      <!-- Search (desktop) -->
      <div class="hidden md:flex flex-1 max-w-md">
        <div class="relative w-full">
          <Search class="absolute left-3 top-1/2 -translate-y-1/2 text-gray-400" :size="16" />
          <input
            type="text"
            placeholder="Cari Sayuran Anda"
            class="w-full pl-9 pr-4 py-2 rounded-full border border-gray-200 text-sm focus:outline-none focus:border-green-400"
          />
        </div>
      </div>

      <!-- Right Actions -->
      <div class="flex items-center gap-2">
        <!-- Cart -->
        <RouterLink
          to="/keranjang"
          class="relative p-2 text-gray-500 hover:text-gray-900 transition-colors"
        >
          <ShoppingCart :size="20" />
          <span class="absolute -top-0.5 -right-0.5 w-4 h-4 bg-green-600 text-white text-[9px] font-bold rounded-full flex items-center justify-center">
            2
          </span>
        </RouterLink>

        <!-- Masuk button (desktop) -->
        <RouterLink
          to="/login"
          class="hidden md:inline-flex px-5 py-2 bg-green-900 text-white text-sm font-semibold rounded-full hover:bg-green-800 transition-colors"
        >
          Masuk
        </RouterLink>

        <!-- Hamburger (mobile) -->
        <button
          class="md:hidden p-2 text-gray-500 hover:text-gray-900 transition-colors"
          @click="menuOpen = !menuOpen"
        >
          <X v-if="menuOpen" :size="22" />
          <Menu v-else :size="22" />
        </button>
      </div>
    </div>

    <!-- Mobile Menu -->
    <div v-if="menuOpen" class="md:hidden border-t border-gray-100 bg-white px-4 pb-4 space-y-4">
      <!-- Search -->
      <div class="relative mt-3">
        <Search class="absolute left-3 top-1/2 -translate-y-1/2 text-gray-400" :size="16" />
        <input
          type="text"
          placeholder="Cari Sayuran Anda"
          class="w-full pl-9 pr-4 py-2 rounded-full border border-gray-200 text-sm focus:outline-none focus:border-green-400"
        />
      </div>

      <!-- Nav Links -->
      <div class="flex flex-col gap-1">
        <RouterLink
          to="/"
          class="py-2 px-3 rounded-xl text-sm font-semibold transition-colors"
          :class="route.name === 'home' ? 'bg-green-50 text-green-700' : 'text-gray-600 hover:bg-gray-50'"
          @click="menuOpen = false"
        >
          Home
        </RouterLink>
        <RouterLink
          to="/rak-sayur"
          class="py-2 px-3 rounded-xl text-sm font-semibold transition-colors"
          :class="route.name === 'rak-sayur' ? 'bg-green-50 text-green-700' : 'text-gray-600 hover:bg-gray-50'"
          @click="menuOpen = false"
        >
          Rak Sayur
        </RouterLink>
      </div>

      <!-- Masuk button -->
      <RouterLink
        to="/login"
        class="w-full py-2.5 bg-green-900 text-white text-sm font-semibold rounded-full hover:bg-green-800 transition-colors text-center block"
        @click="menuOpen = false"
      >
        Masuk
      </RouterLink>
    </div>
  </nav>
</template>
