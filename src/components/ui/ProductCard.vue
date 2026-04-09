<script setup>
import { ShoppingBasket, Plus } from 'lucide-vue-next'

defineProps({
  product: {
    type: Object,
    required: true,
  },
})
</script>

<template>
  <div
    class="bg-white rounded-2xl overflow-hidden border border-gray-100 hover:shadow-md transition-shadow"
  >
    <!-- Image -->
    <div class="relative">
      <!--
        TODO: Ganti div placeholder dengan tag img setelah import gambar:
        <img
          :src="product.image"
          :alt="product.name"
          class="w-full aspect-square object-cover"
        />
      -->
      <div class="w-full aspect-square bg-gray-100 flex items-center justify-center text-gray-400 text-xs">
        [{{ product.name }}]
      </div>

      <!-- Badge (ORGANIK / HIDROPONIK) -->
      <span
        v-if="product.badge"
        class="absolute top-3 left-3 px-2 py-0.5 text-[10px] font-bold rounded uppercase tracking-wide"
        :class="
          product.badge === 'ORGANIK'
            ? 'bg-yellow-100 text-yellow-700'
            : 'bg-blue-100 text-blue-700'
        "
      >
        {{ product.badge }}
      </span>
    </div>

    <!-- Info -->
    <div class="p-4">
      <h3 class="font-bold text-gray-900 text-sm">{{ product.name }}</h3>
      <p class="text-xs text-gray-400 mt-0.5 mb-3">{{ product.description }}</p>
      <div class="flex items-center justify-between">
        <span class="font-bold text-gray-900 text-sm">{{ product.price }}</span>
        <button
          class="w-7 h-7 rounded-lg flex items-center justify-center transition-colors bg-green-800 text-white hover:bg-green-700"
        >
          <ShoppingBasket v-if="product.inCart" :size="14" />
          <Plus v-else :size="14" />
        </button>
      </div>
    </div>
  </div>
</template>
