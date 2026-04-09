<script setup>
import { Truck } from 'lucide-vue-next'
</script>

<template>
  <section class="bg-[#EFF7F2] py-16 overflow-hidden">
    <div class="max-w-6xl mx-auto px-6">
      <div class="flex items-center gap-16">
        <!-- Left Content -->
        <div class="flex-1 animate-fade-in-left">
          <!-- Badge -->
          <div
            class="inline-flex items-center gap-2 px-3 py-1.5 bg-green-100 text-green-700 rounded-full text-xs font-bold mb-6 animate-bounce-subtle"
          >
            <span class="w-1.5 h-1.5 rounded-full bg-green-500 animate-pulse"></span>
            100% ORGANIK & SEGAR
          </div>

          <!-- Heading -->
          <h1 class="text-5xl font-extrabold text-gray-900 leading-tight mb-5">
            <span class="block animate-fade-in-up" style="animation-delay: 0.1s">Sayur Segar,</span>
            <span class="block animate-fade-in-up" style="animation-delay: 0.25s">
              <em class="not-italic text-green-600 italic">Langsung</em> ke
            </span>
            <span class="block animate-fade-in-up" style="animation-delay: 0.4s">Rumah Anda.</span>
          </h1>

          <!-- Subtext -->
          <p
            class="text-gray-500 text-sm leading-relaxed mb-8 max-w-sm animate-fade-in-up"
            style="animation-delay: 0.55s"
          >
            Nikmati hasil panen terbaik hari ini. Kami mengantarkan sayuran berkualitas tinggi dari
            petani lokal langsung ke dapur Anda dalam waktu kurang dari 24 jam.
          </p>

          <!-- Buttons -->
          <div
            class="flex items-center gap-4 animate-fade-in-up"
            style="animation-delay: 0.7s"
          >
            <button
              class="px-6 py-3 bg-green-900 text-white text-sm font-semibold rounded-lg hover:bg-green-800 hover:scale-105 active:scale-95 transition-all duration-200"
            >
              Pesan Sekarang
            </button>
            <button
              class="px-6 py-3 border border-gray-800 text-gray-800 text-sm font-semibold rounded-lg hover:bg-gray-50 hover:scale-105 active:scale-95 transition-all duration-200"
            >
              Lihat Katalog
            </button>
          </div>
        </div>

        <!-- Right Image -->
        <div class="flex-1 relative animate-fade-in-right">
          <!-- Decorative blob behind image -->
          <div
            class="absolute inset-0 rounded-2xl bg-green-200/40 scale-105 blur-2xl animate-pulse-slow"
          ></div>

          <img
            src="@/assets/images/hero-vegetables.jpg"
            alt="Sayur Segar dalam Keranjang"
            class="relative w-full aspect-square rounded-2xl object-cover shadow-lg animate-float"
          />

          <!-- Floating delivery badge -->
          <div
            class="absolute bottom-5 left-5 bg-white rounded-2xl px-4 py-3 flex items-center gap-3 shadow-lg animate-slide-up"
            style="animation-delay: 0.8s"
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

<style scoped>
/* Fade in from left */
.animate-fade-in-left {
  animation: fadeInLeft 0.8s ease both;
}
@keyframes fadeInLeft {
  from { opacity: 0; transform: translateX(-40px); }
  to   { opacity: 1; transform: translateX(0); }
}

/* Fade in from right */
.animate-fade-in-right {
  animation: fadeInRight 0.8s ease both;
}
@keyframes fadeInRight {
  from { opacity: 0; transform: translateX(40px); }
  to   { opacity: 1; transform: translateX(0); }
}

/* Fade in upward (staggered via inline delay) */
.animate-fade-in-up {
  opacity: 0;
  animation: fadeInUp 0.65s ease forwards;
}
@keyframes fadeInUp {
  from { opacity: 0; transform: translateY(20px); }
  to   { opacity: 1; transform: translateY(0); }
}

/* Gentle floating for the image */
.animate-float {
  animation: float 4s ease-in-out infinite;
}
@keyframes float {
  0%, 100% { transform: translateY(0); }
  50%       { transform: translateY(-10px); }
}

/* Slow pulsing blob glow */
.animate-pulse-slow {
  animation: pulseSlow 3s ease-in-out infinite;
}
@keyframes pulseSlow {
  0%, 100% { opacity: 0.4; transform: scale(1.05); }
  50%       { opacity: 0.7; transform: scale(1.1); }
}

/* Subtle badge bounce */
.animate-bounce-subtle {
  animation: bounceBadge 2.5s ease-in-out infinite;
}
@keyframes bounceBadge {
  0%, 100% { transform: translateY(0); }
  50%       { transform: translateY(-4px); }
}

/* Slide up for floating card */
.animate-slide-up {
  opacity: 0;
  animation: slideUp 0.6s ease forwards;
}
@keyframes slideUp {
  from { opacity: 0; transform: translateY(16px); }
  to   { opacity: 1; transform: translateY(0); }
}
</style>
