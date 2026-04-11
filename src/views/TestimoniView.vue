<script setup>
import TheNavbar from '../components/layout/TheNavbar.vue'
import TheFooter from '../components/layout/TheFooter.vue'
import { RouterLink } from 'vue-router'
import { Star } from 'lucide-vue-next'
import ibuSarahImg from '../assets/images/ibusarah.png'
import sayurHorizontalImg from '../assets/images/sayur-horizontal.jpg'
</script>

<template>
  <div class="min-h-screen bg-white">
    <TheNavbar />

    <main class="max-w-6xl mx-auto px-6 py-14">

      <!-- Hero Header -->
      <div class="flex flex-col md:flex-row md:items-start md:justify-between mb-14 gap-8">
        <div class="max-w-lg">
          <span class="inline-block px-3 py-1 bg-green-100 text-green-700 text-xs font-semibold rounded-full mb-4">
            Kisah dari Dapur
          </span>
          <h1 class="text-4xl md:text-5xl font-extrabold text-gray-900 leading-tight">
            Apa Kata Mereka<br />
            Tentang <span class="text-green-600">Kesegaran</span><br />
            Kami?
          </h1>
        </div>

        <!-- Avatars + count -->
        <div class="flex flex-col items-center gap-2 md:mt-4">
          <div class="flex items-center">
            <img
              :src="ibuSarahImg"
              alt="User"
              class="w-10 h-10 rounded-full object-cover border-2 border-white ring-2 ring-green-100 -ml-0 z-30"
            />
            <div class="w-10 h-10 rounded-full bg-green-200 border-2 border-white flex items-center justify-center -ml-3 z-20">
              <span class="text-green-800 text-xs font-bold">A</span>
            </div>
            <div class="w-10 h-10 rounded-full bg-green-300 border-2 border-white flex items-center justify-center -ml-3 z-10">
              <span class="text-green-900 text-xs font-bold">M</span>
            </div>
            <div class="w-10 h-10 rounded-full bg-green-600 border-2 border-white flex items-center justify-center -ml-3 z-0">
              <span class="text-white text-xs font-bold">+1k</span>
            </div>
          </div>
          <p class="text-sm text-gray-500 font-medium">1,200+ Keluarga Puas</p>
        </div>
      </div>

      <!-- Testimonial Grid -->
      <div class="grid grid-cols-1 md:grid-cols-2 gap-5">

        <!-- Row 1 Left – Large white card (Ibu Sarah) -->
        <div class="relative bg-white border border-gray-100 rounded-2xl p-7 shadow-sm overflow-hidden">
          <!-- Stars -->
          <div class="flex gap-0.5 mb-4">
            <Star v-for="i in 5" :key="i" :size="18" class="fill-yellow-400 text-yellow-400" />
          </div>
          <p class="text-gray-800 text-lg font-medium leading-relaxed mb-6">
            "Sayurannya benar-benar terasa berbeda. Begitu sampai masih ada embun paginya!
            Anak-anak saya yang biasanya susah makan sayur sekarang jadi lahap karena
            rasanya yang manis dan renyah."
          </p>
          <!-- Author -->
          <div class="flex items-center gap-3">
            <img
              :src="ibuSarahImg"
              alt="Ibu Sarah Wijaya"
              class="w-10 h-10 rounded-full object-cover"
            />
            <div>
              <p class="text-sm font-bold text-gray-900">Ibu Sarah Wijaya</p>
              <p class="text-xs text-gray-400">Ibu Rumah Tangga, Jakarta</p>
            </div>
          </div>
          <!-- Watermark leaf -->
          <div class="absolute -right-6 -bottom-6 w-32 h-32 bg-green-50 rounded-full opacity-60"></div>
          <div class="absolute -right-2 -bottom-2 w-20 h-20 bg-green-100 rounded-full opacity-50"></div>
        </div>

        <!-- Row 1 Right – Green card (Andi Pratama) -->
        <div class="bg-green-500 rounded-2xl p-7 text-white flex flex-col justify-between">
          <div>
            <p class="text-5xl font-black text-white/90 mb-3">99</p>
            <p class="text-sm leading-relaxed text-white/90">
              "Sangat praktis untuk saya yang sibuk. Kualitas sayur hidroponiknya juara,
              packing sangat aman dan ramah lingkungan."
            </p>
          </div>
          <div class="flex items-center gap-3 mt-6">
            <div class="w-9 h-9 rounded-full bg-white/30 flex items-center justify-center shrink-0">
              <span class="text-white text-sm font-bold">A</span>
            </div>
            <div>
              <p class="text-sm font-bold">Andi Pratama</p>
              <p class="text-xs text-white/70">Software Engineer</p>
            </div>
          </div>
        </div>

        <!-- Row 2 Left – Small muted card (Maya Lestari) -->
        <div class="bg-gray-50 border border-gray-100 rounded-2xl p-7 flex flex-col justify-between">
          <p class="text-gray-500 text-sm italic leading-relaxed">
            "Belanja di Wlijoku membantu saya mendapatkan sayur organik yang sulit dicari di
            pasar tradisional. Pengirimannya selalu tepat waktu!"
          </p>
          <div class="flex items-center gap-3 mt-5">
            <div class="w-9 h-9 rounded-full bg-green-200 flex items-center justify-center shrink-0">
              <span class="text-green-800 text-sm font-bold">M</span>
            </div>
            <div>
              <p class="text-sm font-bold text-gray-900">Maya Lestari</p>
              <p class="text-xs text-gray-400">Pecinta Organik</p>
            </div>
          </div>
        </div>

        <!-- Row 2 Right – Image card (Chef Budi Santoso) -->
        <div class="bg-white border border-gray-100 rounded-2xl overflow-hidden shadow-sm">
          <img
            :src="sayurHorizontalImg"
            alt="Sayuran Segar"
            class="w-full h-44 object-cover"
          />
          <div class="p-7">
            <div class="flex gap-0.5 mb-3">
              <Star v-for="i in 5" :key="i" :size="16" class="fill-yellow-400 text-yellow-400" />
            </div>
            <p class="text-base font-bold text-gray-900 mb-2">Kualitas Restoran Bintang Lima</p>
            <p class="text-sm text-gray-500 leading-relaxed mb-4">
              "Sebagai pemilik catering, kualitas bahan baku adalah segalanya. Wlijoku
              memberikan standar kesegaran yang konsisten setiap harinya."
            </p>
            <p class="text-sm">
              <span class="font-bold text-gray-800">Chef Budi Santoso</span>
              <span class="text-gray-400 mx-1">•</span>
              <span class="text-gray-400 text-xs">Owner Rasa Nusantara</span>
            </p>
          </div>
        </div>

      </div>
    </main>

    <!-- CTA Banner -->
    <section class="max-w-6xl mx-auto px-6 pb-14">
      <div class="bg-green-800 rounded-3xl px-10 py-16 text-center relative overflow-hidden">
        <!-- Decorative circles -->
        <div class="absolute top-0 left-1/4 w-64 h-64 bg-green-700/40 rounded-full -translate-y-1/2 -translate-x-1/2"></div>
        <div class="absolute bottom-0 right-1/4 w-64 h-64 bg-green-700/40 rounded-full translate-y-1/2 translate-x-1/2"></div>
        <div class="relative z-10">
          <h2 class="text-3xl md:text-4xl font-extrabold text-white mb-4">
            Siap Merasakan Kesegarannya<br />Sendiri?
          </h2>
          <p class="text-green-200 text-sm mb-8 max-w-md mx-auto leading-relaxed">
            Dapatkan diskon 20% untuk pesanan pertama Anda hari ini. Segar dari kebun,
            langsung ke pintu Anda.
          </p>
          <div class="flex items-center justify-center gap-4 flex-wrap">
            <RouterLink
              to="/rak-sayur"
              class="px-7 py-3 bg-white text-green-900 text-sm font-bold rounded-full hover:bg-gray-100 transition-colors"
            >
              Belanja Sekarang
            </RouterLink>
            <RouterLink
              to="/rak-sayur"
              class="px-7 py-3 border border-white text-white text-sm font-bold rounded-full hover:bg-white/10 transition-colors"
            >
              Lihat Katalog
            </RouterLink>
          </div>
        </div>
      </div>
    </section>

    <TheFooter />
  </div>
</template>
