<script setup>
import { ref, computed } from 'vue'
import { RouterLink } from 'vue-router'
import { Trash2, Minus, Plus, ShieldCheck, Truck, Leaf } from 'lucide-vue-next'
import TheNavbar from '../components/layout/TheNavbar.vue'
import TheFooter from '../components/layout/TheFooter.vue'

const cartItems = ref([
  {
    id: 'WJ-001',
    name: 'Bayam',
    badge: 'Organik',
    image: new URL('@/assets/images/ketumbar.jpg', import.meta.url).href,
    customerName: 'Budi Santoso',
    address: 'Jl. Kebun Raya No. 42, Bogor Tengah',
    qty: 10,
    price: 5000,
  },
  {
    id: 'WJ-002',
    name: 'Ketumbar',
    badge: 'Organik',
    image: new URL('@/assets/images/ketumbar.jpg', import.meta.url).href,
    customerName: 'Budi Santoso',
    address: 'Jl. Kebun Raya No. 42, Bogor Tengah',
    qty: 3,
    price: 8500,
  },
])

function increment(item) {
  item.qty++
}

function decrement(item) {
  if (item.qty > 1) item.qty--
}

function removeItem(index) {
  cartItems.value.splice(index, 1)
}

const subtotal = computed(() => cartItems.value.reduce((sum, item) => sum + item.price * item.qty, 0))
const shipping = 15000
const discount = 5000
const total = computed(() => subtotal.value + shipping - discount)

function formatRp(value) {
  return 'Rp. ' + value.toLocaleString('id-ID')
}
</script>

<template>
  <div class="min-h-screen bg-gray-50">
    <TheNavbar />

    <main class="max-w-6xl mx-auto px-6 py-10">
      <!-- Page Header -->
      <div class="mb-8">
        <h1 class="text-3xl font-extrabold text-gray-900">Keranjang Belanja</h1>
        <p class="text-sm text-gray-400 mt-1">
          Pastikan pesanan sayur segar Anda sudah sesuai sebelum melakukan pembayaran.
        </p>
      </div>

      <div class="flex gap-6 items-start">
        <!-- Left: Cart Table -->
        <div class="flex-1 min-w-0">
          <!-- Table Header -->
          <div class="grid grid-cols-[60px_80px_1fr_1.4fr_120px_100px_60px] gap-3 px-4 py-3 text-xs font-semibold text-gray-500 uppercase tracking-wide">
            <span>ID</span>
            <span>Gambar</span>
            <span>Nama Sayur</span>
            <span>Nama Dan Alamat</span>
            <span class="text-center">Jumlah</span>
            <span class="text-right">Harga Satuan</span>
            <span class="text-center">Aksi</span>
          </div>

          <!-- Cart Items -->
          <div class="space-y-3">
            <div
              v-for="(item, index) in cartItems"
              :key="item.id"
              class="bg-white rounded-2xl border border-gray-100 grid grid-cols-[60px_80px_1fr_1.4fr_120px_100px_60px] gap-3 items-center px-4 py-4"
            >
              <!-- ID -->
              <span class="text-xs font-semibold text-gray-500">#{{ item.id }}</span>

              <!-- Image -->
              <img
                :src="item.image"
                :alt="item.name"
                class="w-14 h-14 rounded-xl object-cover"
              />

              <!-- Name + Badge -->
              <div>
                <p class="text-sm font-bold text-gray-900">{{ item.name }}</p>
                <span class="text-[11px] font-semibold text-green-600">{{ item.badge }}</span>
              </div>

              <!-- Customer Name + Address -->
              <div>
                <p class="text-sm font-semibold text-gray-800">{{ item.customerName }}</p>
                <p class="text-xs text-gray-400 leading-snug mt-0.5">{{ item.address }}</p>
              </div>

              <!-- Qty Controls -->
              <div class="flex items-center justify-center gap-2">
                <button
                  @click="decrement(item)"
                  class="w-6 h-6 rounded-full border border-gray-200 flex items-center justify-center text-gray-600 hover:bg-gray-100 transition"
                >
                  <Minus :size="12" />
                </button>
                <span class="text-sm font-semibold w-5 text-center">{{ item.qty }}</span>
                <button
                  @click="increment(item)"
                  class="w-6 h-6 rounded-full border border-gray-200 flex items-center justify-center text-gray-600 hover:bg-gray-100 transition"
                >
                  <Plus :size="12" />
                </button>
              </div>

              <!-- Price -->
              <p class="text-sm font-bold text-gray-900 text-right">{{ formatRp(item.price) }}</p>

              <!-- Delete -->
              <div class="flex justify-center">
                <button
                  @click="removeItem(index)"
                  class="w-8 h-8 rounded-lg flex items-center justify-center text-red-400 hover:bg-red-50 transition"
                >
                  <Trash2 :size="16" />
                </button>
              </div>
            </div>
          </div>

          <!-- Empty state -->
          <div v-if="cartItems.length === 0" class="bg-white rounded-2xl border border-gray-100 py-16 text-center text-gray-400">
            <p class="text-sm">Keranjang belanja Anda kosong.</p>
            <RouterLink to="/rak-sayur" class="text-green-600 text-sm font-semibold mt-2 inline-block">Mulai Belanja</RouterLink>
          </div>

          <!-- Upsell Banner -->
          <div class="mt-4 bg-green-50 border border-green-100 rounded-2xl px-5 py-3 flex items-center justify-between">
            <div class="flex items-center gap-2 text-sm text-green-700">
              <Leaf :size="15" class="shrink-0" />
              <span>Tambah Wortel untuk mendapatkan gratis ongkir hari ini!</span>
            </div>
            <RouterLink
              to="/rak-sayur"
              class="text-sm font-semibold text-green-700 underline underline-offset-2 hover:text-green-800 shrink-0 ml-4"
            >
              Lihat Rak Sayur
            </RouterLink>
          </div>
        </div>

        <!-- Right: Order Summary -->
        <div class="w-72 shrink-0 bg-white rounded-2xl border border-gray-100 p-6">
          <h2 class="text-base font-bold text-gray-900 mb-5">Ringkasan Pesanan</h2>

          <div class="space-y-3 text-sm">
            <div class="flex justify-between text-gray-600">
              <span>Subtotal ({{ cartItems.reduce((s, i) => s + i.qty, 0) }} item)</span>
              <span class="font-semibold text-gray-900">{{ formatRp(subtotal) }}</span>
            </div>
            <div class="flex justify-between text-gray-600">
              <span>Biaya Pengiriman</span>
              <span class="font-semibold text-gray-900">{{ formatRp(shipping) }}</span>
            </div>
            <div class="flex justify-between text-gray-600">
              <span>Diskon Member</span>
              <span class="font-semibold text-green-600">- {{ formatRp(discount) }}</span>
            </div>
          </div>

          <div class="border-t border-gray-100 mt-4 pt-4 flex justify-between items-center">
            <span class="text-sm text-gray-600">Total Harga</span>
            <span class="text-2xl font-extrabold text-gray-900">{{ formatRp(total) }}</span>
          </div>

          <button
            class="mt-5 w-full py-3 bg-green-800 text-white font-semibold text-sm rounded-full hover:bg-green-700 transition"
          >
            Pesan Sekarang
          </button>

          <RouterLink
            to="/"
            class="mt-3 w-full py-3 border border-gray-200 text-gray-600 font-semibold text-sm rounded-full hover:bg-gray-50 transition flex items-center justify-center gap-2"
          >
        Lanjut Belanja
          </RouterLink>

          <!-- Trust badges -->
          <div class="mt-6 flex items-center justify-center gap-3 text-gray-400">
            <ShieldCheck :size="18" />
            <Truck :size="18" />
            <Leaf :size="18" />
          </div>
          <p class="text-[10px] text-gray-400 text-center mt-1 tracking-widest uppercase">
            Pembayaran Aman &amp; Sayur Segar Terjamin
          </p>
        </div>
      </div>
    </main>

    <TheFooter />
  </div>
</template>
