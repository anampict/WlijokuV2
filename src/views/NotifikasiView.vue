<script setup>
import { ref } from 'vue'
import { RouterLink } from 'vue-router'
import { Truck, CreditCard, CheckCircle, Info, Tag } from 'lucide-vue-next'
import TheNavbar from '../components/layout/TheNavbar.vue'
import TheFooter from '../components/layout/TheFooter.vue'

const promoImage = new URL('@/assets/images/sayur-horizontal.jpg', import.meta.url).href

const notifications = ref([
  {
    id: 1,
    type: 'delivery',
    icon: Truck,
    iconBg: 'bg-green-100',
    iconColor: 'text-green-600',
    title: 'Pesanan #WJ-2024001 sedang dalam perjalanan',
    body: 'Kurir kami sedang menuju lokasi Anda. Pastikan ada seseorang untuk menerima sayuran segar Anda!',
    time: 'Baru saja',
    isNew: true,
    actions: [{ label: 'Lacak Pesanan', to: '/keranjang', style: 'link' }],
  },
  {
    id: 2,
    type: 'payment',
    icon: CreditCard,
    iconBg: 'bg-blue-100',
    iconColor: 'text-blue-500',
    title: 'Pembayaran telah diverifikasi',
    body: 'Pembayaran untuk pesanan #WJ-2024002 telah kami terima. Kami segera menyiapkan sayuran terbaik untuk Anda.',
    time: '2 jam yang lalu',
    isNew: false,
    actions: [],
  },
  {
    id: 'promo',
    type: 'promo',
  },
  {
    id: 3,
    type: 'done',
    icon: CheckCircle,
    iconBg: 'bg-cyan-100',
    iconColor: 'text-cyan-500',
    title: 'Pesanan #WJ-2024003 telah selesai',
    body: 'Terima kasih telah berbelanja di Wlijoku! Bagaimana kualitas sayuran kami hari ini?',
    time: 'Kemarin',
    isNew: false,
    actions: [
      { label: 'Beri Ulasan', to: '/testimoni', style: 'outline' },
      { label: 'Pesan Lagi', to: '/rak-sayur', style: 'outline' },
    ],
  },
  {
    id: 4,
    type: 'info',
    icon: Info,
    iconBg: 'bg-gray-100',
    iconColor: 'text-gray-500',
    title: 'Pembaruan Kebijakan Pengiriman',
    body: 'Kami telah memperluas area pengiriman gratis kami. Cek apakah area Anda termasuk!',
    time: '3 hari yang lalu',
    isNew: false,
    actions: [],
  },
])
</script>

<template>
  <div class="min-h-screen bg-gray-50">
    <TheNavbar />

    <main class="max-w-2xl mx-auto px-4 py-10">
      <!-- Page Header -->
      <div class="mb-6">
        <h1 class="text-2xl font-bold text-gray-900">Notifikasi</h1>
        <p class="text-sm text-gray-400 mt-1">Pantau status pesanan dan penawaran terbaru untuk Anda.</p>
      </div>

      <!-- Notification List -->
      <div class="flex flex-col gap-3">
        <template v-for="notif in notifications" :key="notif.id">

          <!-- Promo Banner Card -->
          <div
            v-if="notif.type === 'promo'"
            class="rounded-2xl bg-green-700 p-5 flex items-center gap-5"
          >
            <!-- Text side -->
            <div class="flex-1 min-w-0">
              <span class="inline-block px-2.5 py-0.5 bg-green-600/70 text-white text-[10px] font-bold rounded-full uppercase tracking-wider mb-3">
                PROMO SPESIAL
              </span>
              <h3 class="text-white font-bold text-lg leading-snug">
                Ada promo baru: Diskon 15%<br />untuk sayur organik minggu ini!
              </h3>
              <p class="text-green-200 text-xs mt-2 leading-relaxed">
                Nikmati kesegaran hasil bumi terbaik dengan harga lebih hemat.<br />
                Gunakan kode: <span class="font-semibold text-white">ORGANIKSEGAR</span>
              </p>
              <RouterLink
                to="/rak-sayur"
                class="mt-4 inline-block px-5 py-2.5 bg-white text-green-800 text-sm font-bold rounded-xl hover:bg-green-50 transition-colors"
              >
                Belanja Sekarang
              </RouterLink>
            </div>
            <!-- Image inside card, rounded-xl -->
            <div class="w-44 h-44 shrink-0 rounded-xl overflow-hidden">
              <img
                :src="promoImage"
                alt="Sayur Organik"
                class="w-full h-full object-cover"
              />
            </div>
          </div>

          <!-- Regular Notification Card -->
          <div
            v-else
            class="bg-white rounded-2xl px-5 py-4 border border-gray-100 flex items-start gap-4"
          >
            <!-- Icon -->
            <div
              class="w-10 h-10 rounded-full flex items-center justify-center shrink-0 mt-0.5"
              :class="notif.iconBg"
            >
              <component :is="notif.icon" :size="18" :class="notif.iconColor" />
            </div>

            <!-- Content -->
            <div class="flex-1 min-w-0">
              <div class="flex items-start justify-between gap-2">
                <p class="text-sm font-semibold text-gray-900 leading-snug">{{ notif.title }}</p>
                <div class="flex items-center gap-1.5 shrink-0">
                  <span class="text-xs text-gray-400 whitespace-nowrap">{{ notif.time }}</span>
                  <span
                    v-if="notif.isNew"
                    class="w-2 h-2 rounded-full bg-green-500 shrink-0"
                  ></span>
                </div>
              </div>
              <p class="text-xs text-gray-500 mt-1 leading-relaxed">{{ notif.body }}</p>

              <!-- Action Buttons / Links -->
              <div v-if="notif.actions.length" class="flex items-center gap-2 mt-3">
                <template v-for="action in notif.actions" :key="action.label">
                  <RouterLink
                    v-if="action.style === 'link'"
                    :to="action.to"
                    class="text-xs font-semibold text-green-700 hover:text-green-900 transition-colors"
                  >
                    {{ action.label }}
                  </RouterLink>
                  <RouterLink
                    v-else
                    :to="action.to"
                    class="px-3 py-1 text-xs font-medium border border-gray-200 text-gray-700 rounded-lg hover:bg-gray-50 transition-colors"
                  >
                    {{ action.label }}
                  </RouterLink>
                </template>
              </div>
            </div>
          </div>

        </template>
      </div>

      <!-- Load More -->
      <div class="flex justify-center mt-8">
        <button
          class="px-6 py-2.5 border border-gray-200 text-sm font-medium text-gray-600 rounded-full bg-white hover:bg-gray-50 transition-colors"
        >
          Lihat Notifikasi Lama
        </button>
      </div>
    </main>

    <TheFooter />
  </div>
</template>
