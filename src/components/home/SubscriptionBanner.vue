<script setup>
import { Leaf } from 'lucide-vue-next'
</script>

<template>
  <section class="py-6">
    <div class="max-w-6xl mx-auto px-6">
      <div
        class="bg-[#C8EDCD] rounded-3xl px-14 py-12 flex items-center justify-between relative overflow-hidden"
      >
        <!-- Left Content -->
        <div class="max-w-md z-10">
          <h2 class="text-3xl font-extrabold text-gray-900 mb-3">Berlangganan Box Mingguan</h2>
          <p class="text-gray-600 text-sm leading-relaxed mb-7">
            Dapatkan kurasi sayur terbaik setiap Senin pagi dengan diskon 15% untuk pelanggan tetap.
          </p>
          <button
            class="px-6 py-3 bg-green-900 text-white text-sm font-semibold rounded-lg hover:bg-green-800 transition-colors"
          >
            Pelajari Langganan
          </button>
        </div>

        <!-- DISKON badge -->
        <div
          class="absolute top-7 right-40 bg-green-800 text-white text-xs font-bold px-3 py-1.5 rounded-full rotate-12 z-10"
        >
          DISKON 15%
        </div>

        <!-- Leaf circle decoration -->
        <div class="flex items-center justify-center z-10">
          <div class="w-40 h-40 bg-[#a8dbb0] rounded-full flex items-center justify-center">
            <div class="w-28 h-28 bg-[#b8e5c0] rounded-full flex items-center justify-center">
              <Leaf :size="70" class="text-green-800" />
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
