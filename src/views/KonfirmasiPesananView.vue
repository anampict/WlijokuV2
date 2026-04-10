<script setup>
import { ref, onMounted } from 'vue'
import { RouterLink } from 'vue-router'
import { Check, Copy, Truck, ShoppingBasket, Landmark } from 'lucide-vue-next'
import TheFooter from '../components/layout/TheFooter.vue'

const productImage = new URL('@/assets/images/ketumbar.jpg', import.meta.url).href

const orderNumber = '#WJ-2024001'
const bankNumber = '123-456-7890'
const copied = ref(false)

function copyBank() {
  navigator.clipboard.writeText(bankNumber.replace(/-/g, ''))
  copied.value = true
  setTimeout(() => (copied.value = false), 2000)
}

// Animation states
const showCheck = ref(false)
const showContent = ref(false)

onMounted(() => {
  setTimeout(() => (showCheck.value = true), 100)
  setTimeout(() => (showContent.value = true), 600)
})
</script>

<template>
  <div class="min-h-screen bg-gray-100 flex flex-col">
    <!-- Minimal Top Bar -->
    <header class="bg-gray-100 py-5 text-center">
      <RouterLink to="/" class="text-base font-bold text-green-700">Wlijoku</RouterLink>
    </header>

    <main class="flex-1 flex flex-col items-center px-4 py-6 pb-16">
      <!-- Success Badge -->
      <div
        class="transition-all duration-500 ease-out"
        :class="showCheck ? 'opacity-100 scale-100' : 'opacity-0 scale-50'"
      >
        <div class="w-16 h-16 rounded-full bg-green-500 flex items-center justify-center shadow-lg shadow-green-200 mb-5">
          <Check :size="32" class="text-white" stroke-width="3" />
        </div>
      </div>

      <!-- Title -->
      <div
        class="text-center mb-8 transition-all duration-500 ease-out"
        :class="showContent ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-4'"
      >
        <h1 class="text-3xl md:text-4xl font-extrabold text-green-700">Pesanan Berhasil Dibuat!</h1>
        <p class="text-sm text-gray-500 mt-2">
          Terima kasih atas kepercayaan Anda. Sayur segar Anda akan segera kami siapkan.
        </p>
      </div>

      <!-- Cards -->
      <div
        class="w-full max-w-3xl grid grid-cols-1 md:grid-cols-2 gap-5 transition-all duration-700 ease-out"
        :class="showContent ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-6'"
      >
        <!-- Left: Order Summary -->
        <div class="bg-white rounded-2xl border border-gray-100 p-6 space-y-4">
          <!-- Order number -->
          <div>
            <p class="text-[10px] font-bold text-gray-400 uppercase tracking-widest mb-1">Nomor Pesanan</p>
            <p class="text-2xl font-extrabold text-gray-900">{{ orderNumber }}</p>
          </div>

          <hr class="border-gray-100" />

          <!-- Ringkasan Pesanan -->
          <div>
            <div class="flex items-center gap-2 mb-4">
              <ShoppingBasket :size="18" class="text-gray-700" />
              <p class="text-sm font-bold text-gray-800">Ringkasan Pesanan</p>
            </div>

            <!-- Product row -->
            <div class="flex items-center gap-3 mb-5">
              <img
                :src="productImage"
                alt="Bayam"
                class="w-14 h-14 rounded-xl object-cover shrink-0"
              />
              <div class="flex-1 min-w-0">
                <p class="text-sm font-bold text-gray-900">Bayam</p>
                <p class="text-xs text-gray-400">10 ikat x Rp 21</p>
              </div>
              <p class="text-sm font-bold text-gray-900 shrink-0">Rp 210</p>
            </div>

            <!-- Price breakdown -->
            <div class="space-y-2 text-sm">
              <div class="flex justify-between text-gray-500">
                <span>Subtotal</span>
                <span class="font-semibold text-gray-800">Rp 210</span>
              </div>
              <div class="flex justify-between text-gray-500">
                <span>Biaya Pengiriman</span>
                <span class="font-semibold text-green-600">Gratis</span>
              </div>
              <hr class="border-gray-100 my-2" />
              <div class="flex justify-between font-extrabold text-gray-900 text-base">
                <span>Total Pembayaran</span>
                <span class="text-green-700">Rp 210</span>
              </div>
            </div>
          </div>
        </div>

        <!-- Right: Payment + Delivery -->
        <div class="space-y-4">
          <!-- Payment Instructions -->
          <div class="bg-white rounded-2xl border border-gray-100 p-6">
            <div class="flex items-center gap-2 mb-4">
              <Landmark :size="18" class="text-gray-700" />
              <p class="text-sm font-bold text-gray-800">Instruksi Pembayaran</p>
            </div>

            <!-- Bank transfer box -->
            <div class="bg-gray-50 rounded-xl px-4 py-3 mb-4">
              <p class="text-[10px] font-bold text-gray-400 uppercase tracking-widest mb-1">Transfer ke Bank Mandiri</p>
              <div class="flex items-center justify-between">
                <p class="text-xl font-extrabold text-gray-900 tracking-wider">{{ bankNumber }}</p>
                <button
                  @click="copyBank"
                  class="text-gray-600 hover:text-green-800 transition-colors"
                  :title="copied ? 'Tersalin!' : 'Salin nomor rekening'"
                >
                  <Copy :size="16" />
                </button>
              </div>
              <p class="text-xs text-gray-400 mt-0.5">a/n Wlijoku Segar</p>
              <p
                v-if="copied"
                class="text-xs text-green-600 font-semibold mt-1 transition-opacity"
              >
                Nomor rekening tersalin!
              </p>
            </div>

            <!-- Steps -->
            <ol class="space-y-2.5">
              <li class="flex gap-3 text-xs text-gray-500">
                <span class="w-5 h-5 rounded-full bg-green-100 text-green-700 text-[10px] font-bold flex items-center justify-center shrink-0 mt-0.5">1</span>
                <span>Lakukan transfer sesuai nominal total hingga ke 3 digit terakhir.</span>
              </li>
              <li class="flex gap-3 text-xs text-gray-500">
                <span class="w-5 h-5 rounded-full bg-green-100 text-green-700 text-[10px] font-bold flex items-center justify-center shrink-0 mt-0.5">2</span>
                <span>Simpan bukti transfer dalam format JPG atau PDF.</span>
              </li>
              <li class="flex gap-3 text-xs text-gray-500">
                <span class="w-5 h-5 rounded-full bg-green-100 text-green-700 text-[10px] font-bold flex items-center justify-center shrink-0 mt-0.5">3</span>
                <span>Klik tombol konfirmasi di bawah untuk mengugugah bukti bayar.</span>
              </li>
            </ol>

            <!-- Confirm button -->
            <button
              class="mt-5 w-full py-3 bg-green-800 text-white text-sm font-semibold rounded-full hover:bg-green-700 transition-colors"
            >
              Konfirmasi Pembayaran
            </button>
            <p class="text-center text-xs text-gray-400 mt-3">
              Punya pertanyaan?
              <a href="#" class="text-green-600 font-semibold hover:underline">Hubungi Kami</a>
            </p>
          </div>

          <!-- Delivery estimate -->
          <div class="bg-white rounded-2xl border border-gray-100 px-5 py-4 flex items-center gap-4">
            <Truck :size="22" class="text-gray-400 shrink-0" />
            <div>
              <p class="text-[10px] font-bold text-gray-400 uppercase tracking-widest">Estimasi Tiba</p>
              <p class="text-sm font-bold text-gray-900">Besok, Pukul 07:00 – 09:00 WIB</p>
            </div>
          </div>
        </div>
      </div>
    </main>

    <!-- Footer with expanded columns (matching screenshot) -->
    <footer class="bg-white border-t border-gray-100 py-10">
      <div class="max-w-3xl mx-auto px-6">
        <div class="grid grid-cols-2 md:grid-cols-4 gap-8 mb-8">
          <!-- Brand -->
          <div class="col-span-2 md:col-span-1">
            <p class="text-base font-bold text-green-700 mb-2">Wlijoku</p>
            <p class="text-xs text-gray-400 leading-relaxed">
              Menghubungkan Anda langsung dengan kebun terbaik untuk sayuran yang lebih segar dan hidup yang lebih sehat.
            </p>
          </div>
          <!-- Layanan -->
          <div>
            <p class="text-[10px] font-bold text-gray-500 uppercase tracking-widest mb-3">Layanan</p>
            <ul class="space-y-2 text-xs text-gray-500">
              <li><a href="#" class="hover:text-gray-800">Tentang Wlijoku</a></li>
              <li><a href="#" class="hover:text-gray-800">Hubungi Kami</a></li>
            </ul>
          </div>
          <!-- Legal -->
          <div>
            <p class="text-[10px] font-bold text-gray-500 uppercase tracking-widest mb-3">Legal</p>
            <ul class="space-y-2 text-xs text-gray-500">
              <li><a href="#" class="hover:text-gray-800">Kebijakan Privasi</a></li>
              <li><a href="#" class="hover:text-gray-800">Syarat &amp; Ketentuan</a></li>
            </ul>
          </div>
          <!-- Bantuan -->
          <div>
            <p class="text-[10px] font-bold text-gray-500 uppercase tracking-widest mb-3">Bantuan</p>
            <ul class="space-y-2 text-xs text-gray-500">
              <li><a href="#" class="hover:text-gray-800">FAQ</a></li>
              <li><a href="#" class="hover:text-gray-800">Pusat Bantuan</a></li>
            </ul>
          </div>
        </div>
        <div class="border-t border-gray-100 pt-6 text-center">
          <p class="text-xs text-gray-400">© 2024 Wlijoku. Segar dari Kebun Ke Rumah Anda.</p>
        </div>
      </div>
    </footer>
  </div>
</template>
