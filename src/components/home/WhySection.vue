<script setup>
import { Bike, ShieldCheck, Recycle } from 'lucide-vue-next'

const features = [
  {
    icon: Bike,
    title: 'Petani Lokal',
    description:
      'Semua sayur kami bersumber dari petani lokal terpilih yang menerapkan metode tani berkelanjutan.',
  },
  {
    icon: ShieldCheck,
    title: 'Kualitas Terjamin',
    description:
      'Proses quality control ketat untuk memastikan tidak ada sayur yang cacat atau layu sampai di tangan Anda.',
  },
  {
    icon: Recycle,
    title: 'Ramah Lingkungan',
    description:
      'Menggunakan kemasan yang dapat didaur ulang dan mengurangi jejak karbon melalui rute pengantaran efisien.',
  },
]
</script>

<template>
  <section class="py-20">
    <div class="max-w-6xl mx-auto px-6">
      <!-- Heading -->
      <div class="text-center mb-16">
        <h2 class="text-3xl font-extrabold text-gray-900">Mengapa Wlijoku?</h2>
        <p class="text-gray-400 text-sm mt-2">
          Kami berkomitmen untuk mendukung petani lokal dan memberikan Anda nutrisi terbaik.
        </p>
      </div>

      <!-- Features Grid -->
      <div class="grid grid-cols-3 gap-16">
        <div v-for="feature in features" :key="feature.title">
          <div
            class="w-12 h-12 bg-gray-100 rounded-xl flex items-center justify-center mb-5"
          >
            <component :is="feature.icon" :size="22" class="text-gray-600" />
          </div>
          <h3 class="font-bold text-gray-900 mb-2">{{ feature.title }}</h3>
          <p class="text-sm text-gray-400 leading-relaxed">{{ feature.description }}</p>
        </div>
      </div>
    </div>
  </section>
</template>
