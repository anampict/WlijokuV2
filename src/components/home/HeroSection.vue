<script setup>
import { Truck } from 'lucide-vue-next'
</script>

<template>
  <section class="bg-[#EFF7F2] py-16">
    <div class="max-w-6xl mx-auto px-6">
      <div class="flex items-center gap-16">
        <!-- Left Content -->
        <div class="flex-1">
          <!-- Badge -->
          <div
            class="inline-flex items-center gap-2 px-3 py-1.5 bg-green-100 text-green-700 rounded-full text-xs font-bold mb-6"
          >
            <span class="w-1.5 h-1.5 rounded-full bg-green-500"></span>
            100% ORGANIK & SEGAR
          </div>

          <!-- Heading -->
          <h1 class="text-5xl font-extrabold text-gray-900 leading-tight mb-5">
            Sayur Segar,<br />
            <em class="not-italic text-green-600 italic">Langsung</em> ke<br />
            Rumah Anda.
          </h1>

          <!-- Subtext -->
          <p class="text-gray-500 text-sm leading-relaxed mb-8 max-w-sm">
            Nikmati hasil panen terbaik hari ini. Kami mengantarkan sayuran berkualitas tinggi dari
            petani lokal langsung ke dapur Anda dalam waktu kurang dari 24 jam.
          </p>

          <!-- Buttons -->
          <div class="flex items-center gap-4">
            <button
              class="px-6 py-3 bg-green-900 text-white text-sm font-semibold rounded-lg hover:bg-green-800 transition-colors"
            >
              Pesan Sekarang
            </button>
            <button
              class="px-6 py-3 border border-gray-800 text-gray-800 text-sm font-semibold rounded-lg hover:bg-gray-50 transition-colors"
            >
              Lihat Katalog
            </button>
          </div>
        </div>

        <!-- Right Image -->
        <div class="flex-1 relative">
          <!--
            TODO: Ganti div placeholder di bawah dengan tag img setelah import gambar:
            <img
              src="@/assets/images/hero-vegetables.jpg"
              alt="Sayur Segar dalam Keranjang"
              class="w-full aspect-square rounded-2xl object-cover"
            />
          -->
          <div
            class="w-full aspect-square bg-gray-200 rounded-2xl flex items-center justify-center text-gray-400 text-sm"
          >
            [Gambar Hero – Sayur dalam Keranjang]
          </div>

          <!-- Floating delivery badge -->
          <div
            class="absolute bottom-5 left-5 bg-white rounded-2xl px-4 py-3 flex items-center gap-3 shadow-lg"
          >
            <div class="w-9 h-9 bg-green-100 rounded-full flex items-center justify-center shrink-0">
              <Truck :size="16" class="text-green-700" />
            </div>
            <div>
              <p class="text-xs font-bold text-gray-800">Pengiriman Cepat</p>
              <p class="text-xs text-gray-400">Kurang dari 24 jam</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
