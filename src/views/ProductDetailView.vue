<script setup>
import { ref, computed } from 'vue'
import { useRoute, RouterLink } from 'vue-router'
import { ShoppingCart, Minus, Plus, Truck, ShieldCheck, Leaf, Flame, Archive } from 'lucide-vue-next'
import TheNavbar from '../components/layout/TheNavbar.vue'
import TheFooter from '../components/layout/TheFooter.vue'
import ketumbarImg from '../assets/images/ketumbar.jpg'

const route = useRoute()

const allProducts = [
  {
    id: 1,
    name: 'Bayam',
    badge: 'ORGANIK PILIHAN',
    description: 'Segar, organik, 250gr',
    price: 'Rp. 12.000',
    priceNum: 12000,
    category: 'Daun Hijau',
    rating: 4.5,
    reviews: 48,
    longDescription:
      'Bayam hijau segar yang dipanen langsung dari kebun hidroponik kami setiap pagi. Kaya akan zat besi dan vitamin, sangat cocok untuk berbagai hidangan sayur bening maupun tumisan sehat untuk keluarga.',
    gizi: 'Tinggi Vitamin A, C, dan K serta sumber zat besi yang sangat baik untuk pembentukan sel darah merah.',
    tips: 'Jangan memasak bayam terlalu lama. Masukkan bayam saat air sudah mendidih dan masak maksimal 1–2 menit saja.',
    simpan: 'Simpan dalam wadah tertutup di lemari es tanpa dicuci terlebih dahulu untuk menjaga kesegaran hingga 3 hari.',
    unit: 'ikat',
  },
  {
    id: 2,
    name: 'Dhanikun',
    badge: 'HIDROPONIK',
    description: 'Sayuran hidroponik premium',
    price: 'Rp. 20.000',
    priceNum: 20000,
    category: 'Daun Hijau',
    rating: 4.0,
    reviews: 31,
    longDescription:
      'Dhanikun segar hasil budidaya hidroponik tanpa tanah. Bebas pestisida dan dipanen pada tingkat kematangan optimal untuk rasa terbaik.',
    gizi: 'Kaya serat, Vitamin C, dan antioksidan yang mendukung sistem imun tubuh.',
    tips: 'Cuci bersih sebelum dikonsumsi. Cocok dimakan segar sebagai lalapan atau ditumis sebentar.',
    simpan: 'Bungkus dengan tisu lembab dan simpan di kulkas, tahan hingga 4 hari.',
    unit: 'ikat',
  },
  {
    id: 3,
    name: 'Wortel Organik',
    badge: 'ORGANIK PILIHAN',
    description: 'Manis dan renyah, 500gr',
    price: 'Rp. 15.000',
    priceNum: 15000,
    category: 'Akar & Umbi',
    rating: 4.8,
    reviews: 62,
    longDescription:
      'Wortel organik manis dengan tekstur renyah yang sempurna. Ditanam tanpa pupuk kimia di lahan organik bersertifikat.',
    gizi: 'Sumber beta-karoten dan Vitamin A yang sangat tinggi, baik untuk kesehatan mata dan kulit.',
    tips: 'Kukus atau rebus sebentar untuk mempertahankan nutrisinya. Bisa juga dimakan mentah sebagai camilan.',
    simpan: 'Simpan di tempat sejuk dan kering, atau di kulkas hingga 2 minggu.',
    unit: 'pack',
  },
  {
    id: 4,
    name: 'Tomat Cherry',
    badge: 'ORGANIK PILIHAN',
    description: 'Kualitas grade A, 200gr',
    price: 'Rp. 18.000',
    priceNum: 18000,
    category: 'Buah Sayur',
    rating: 4.6,
    reviews: 55,
    longDescription:
      'Tomat cherry grade A dengan rasa manis dan asam yang seimbang. Dipetik saat matang sempurna di kebun mitra kami.',
    gizi: 'Kaya likopen, Vitamin C, dan antioksidan yang membantu melindungi tubuh dari radikal bebas.',
    tips: 'Simpan di suhu ruangan untuk rasa terbaik. Hindari kulkas agar rasa tidak berubah.',
    simpan: 'Simpan di suhu ruangan selama 3–4 hari, atau di kulkas hingga seminggu.',
    unit: 'pack',
  },
  {
    id: 5,
    name: 'Brokoli',
    badge: 'ORGANIK PILIHAN',
    description: 'Segar tanpa pestisida, per pcs',
    price: 'Rp. 22.000',
    priceNum: 22000,
    category: 'Organik',
    rating: 4.7,
    reviews: 39,
    longDescription:
      'Brokoli segar organik berukuran besar tanpa penggunaan pestisida. Dipanen pagi hari untuk memastikan kesegaran maksimal.',
    gizi: 'Tinggi serat, Vitamin C, K, dan senyawa sulforafan yang dikenal memiliki sifat anti-kanker.',
    tips: 'Kukus selama 5–7 menit untuk tekstur terbaik. Hindari merebus terlalu lama agar nutrisi tidak hilang.',
    simpan: 'Simpan tanpa dicuci di kulkas dalam kantong plastik berlubang, tahan hingga 5 hari.',
    unit: 'pcs',
  },
  {
    id: 6,
    name: 'Selada Keriting',
    badge: 'HIDROPONIK',
    description: 'Hidroponik bebas hama, per ikat',
    price: 'Rp. 10.000',
    priceNum: 10000,
    category: 'Daun Hijau',
    rating: 4.3,
    reviews: 27,
    longDescription:
      'Selada keriting hidroponik segar bebas hama dan pestisida. Tekstur renyah dengan rasa sedikit pahit yang menyegarkan.',
    gizi: 'Sumber Vitamin A, K, dan folat. Rendah kalori, cocok untuk diet sehat.',
    tips: 'Cuci dengan air mengalir, tiriskan, dan langsung sajikan segar sebagai salad atau pelengkap.',
    simpan: 'Bungkus dengan kertas tisu lembab, simpan di kulkas, tahan hingga 3 hari.',
    unit: 'ikat',
  },
  {
    id: 7,
    name: 'Terong Ungu',
    badge: 'ORGANIK PILIHAN',
    description: 'Pilihan kebun lokal, 500gr',
    price: 'Rp. 14.000',
    priceNum: 14000,
    category: 'Buah Sayur',
    rating: 4.2,
    reviews: 22,
    longDescription:
      'Terong ungu lokal segar pilihan petani mitra kami. Daging buah lembut dengan rasa gurih yang khas.',
    gizi: 'Mengandung antosianin (nasunin) yang berperan sebagai antioksidan kuat pelindung sel otak.',
    tips: 'Rendam irisan terong dalam air garam selama 10 menit sebelum dimasak untuk mengurangi rasa pahit.',
    simpan: 'Simpan di suhu ruangan hingga 2 hari, atau di kulkas dalam kantong kertas hingga 5 hari.',
    unit: 'pack',
  },
  {
    id: 8,
    name: 'Paprika Mix',
    badge: 'ORGANIK PILIHAN',
    description: 'Warna-warni segar, per pcs',
    price: 'Rp. 16.000',
    priceNum: 16000,
    category: 'Buah Sayur',
    rating: 4.4,
    reviews: 34,
    longDescription:
      'Paprika mix tiga warna (merah, kuning, hijau) segar organik. Manis renyah dan kaya warna untuk hidangan yang menggugah selera.',
    gizi: 'Sangat tinggi Vitamin C (3× lebih tinggi dari jeruk), dan kaya antioksidan karotenoid.',
    tips: 'Enak dimakan mentah sebagai salad atau ditumis cepat agar tetap renyah dan nutrisinya terjaga.',
    simpan: 'Simpan di kulkas dalam kantong plastik, tahan hingga 1 minggu.',
    unit: 'pcs',
  },
]

const product = computed(() => allProducts.find((p) => p.id === Number(route.params.id)))

const qty = ref(1)
const address = ref('')

function decrement() {
  if (qty.value > 1) qty.value--
}
function increment() {
  qty.value++
}

const fullStars = computed(() => Math.floor(product.value?.rating ?? 0))
const hasHalf = computed(() => (product.value?.rating ?? 0) % 1 >= 0.5)
</script>

<template>
  <div class="min-h-screen bg-gray-50">
    <TheNavbar />

    <main v-if="product" class="max-w-5xl mx-auto px-6 py-8">
      <!-- Breadcrumb -->
      <nav class="flex items-center gap-2 text-xs text-gray-400 mb-8">
        <RouterLink to="/" class="hover:text-gray-700 transition-colors">Beranda</RouterLink>
        <span>›</span>
        <RouterLink to="/rak-sayur" class="hover:text-gray-700 transition-colors">Rak Sayur</RouterLink>
        <span>›</span>
        <span class="text-gray-700 font-medium">{{ product.name }}</span>
      </nav>

      <!-- Main Content -->
      <div class="flex flex-col md:flex-row gap-10">
        <!-- Left: Image -->
        <div class="md:w-[45%] shrink-0">
          <div class="relative rounded-2xl overflow-hidden">
            <img
              :src="ketumbarImg"
              :alt="product.name"
              class="w-full aspect-square object-cover"
            />
            <span
              class="absolute top-4 left-4 flex items-center gap-1.5 bg-white/90 backdrop-blur-sm text-green-700 text-xs font-bold px-3 py-1.5 rounded-full shadow-sm"
            >
              <Leaf :size="12" />
              {{ product.badge }}
            </span>
          </div>
        </div>

        <!-- Right: Detail -->
        <div class="flex-1">
          <h1 class="text-4xl font-bold text-gray-900 mb-1">{{ product.name }}</h1>
          <p class="text-lg font-semibold text-gray-700 mb-3">Harga : {{ product.price }}</p>

          <!-- Rating -->
          <div class="flex items-center gap-2 mb-5">
            <div class="flex items-center gap-0.5">
              <span
                v-for="i in 5"
                :key="i"
                class="text-lg"
                :class="
                  i <= fullStars
                    ? 'text-yellow-400'
                    : i === fullStars + 1 && hasHalf
                      ? 'text-yellow-400'
                      : 'text-gray-300'
                "
              >
                {{ i <= fullStars ? '★' : i === fullStars + 1 && hasHalf ? '½' : '☆' }}
              </span>
            </div>
            <span class="text-sm text-gray-500">({{ product.reviews }} ulasan)</span>
          </div>

          <!-- Description -->
          <p class="text-sm text-gray-600 leading-relaxed mb-6">{{ product.longDescription }}</p>

          <!-- Qty -->
          <div class="mb-4">
            <label class="block text-sm font-semibold text-gray-700 mb-2">
              Jumlah pesan ({{ product.unit }})
            </label>
            <div class="flex items-center border border-gray-200 rounded-xl overflow-hidden w-full bg-white">
              <span class="flex-1 px-4 py-2.5 text-sm text-gray-800">{{ qty }}</span>
              <button
                @click="decrement"
                class="px-4 py-2.5 text-gray-500 hover:bg-gray-50 transition-colors border-l border-gray-200"
              >
                <Minus :size="14" />
              </button>
              <button
                @click="increment"
                class="px-4 py-2.5 text-gray-500 hover:bg-gray-50 transition-colors border-l border-gray-200"
              >
                <Plus :size="14" />
              </button>
            </div>
          </div>

          <!-- Address -->
          <div class="mb-5">
            <label class="block text-sm font-semibold text-gray-700 mb-2">
              Nama dan Alamat Lengkap
            </label>
            <textarea
              v-model="address"
              rows="3"
              placeholder="Contoh: Budi Santoso, Jl. Kebun Hijau No. 12, Jakarta"
              class="w-full px-4 py-3 text-sm border border-gray-200 rounded-xl resize-none focus:outline-none focus:border-green-400 bg-white"
            />
          </div>

          <!-- CTA -->
          <button
            class="w-full flex items-center justify-center gap-2 bg-green-700 hover:bg-green-600 text-white font-semibold py-3.5 rounded-xl transition-colors mb-4"
          >
            <ShoppingCart :size="18" />
            Pesan Sekarang
          </button>

          <!-- Badges -->
          <div class="flex items-center gap-4">
            <div class="flex items-center gap-2 text-xs text-gray-500">
              <Truck :size="16" class="text-green-600" />
              Pengiriman Kilat
            </div>
            <div class="flex items-center gap-2 text-xs text-gray-500">
              <ShieldCheck :size="16" class="text-green-600" />
              Garansi Segar
            </div>
          </div>
        </div>
      </div>

      <!-- Info Cards -->
      <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mt-14">
        <div class="bg-white rounded-2xl p-6 border border-gray-100">
          <Leaf :size="22" class="text-green-600 mb-3" />
          <h3 class="font-bold text-gray-800 mb-2">Kandungan Gizi</h3>
          <p class="text-xs text-gray-500 leading-relaxed">{{ product.gizi }}</p>
        </div>
        <div class="bg-white rounded-2xl p-6 border border-gray-100">
          <Flame :size="22" class="text-orange-500 mb-3" />
          <h3 class="font-bold text-gray-800 mb-2">Tips Memasak</h3>
          <p class="text-xs text-gray-500 leading-relaxed">{{ product.tips }}</p>
        </div>
        <div class="bg-white rounded-2xl p-6 border border-gray-100">
          <Archive :size="22" class="text-blue-500 mb-3" />
          <h3 class="font-bold text-gray-800 mb-2">Penyimpanan</h3>
          <p class="text-xs text-gray-500 leading-relaxed">{{ product.simpan }}</p>
        </div>
      </div>
    </main>

    <!-- 404 state -->
    <main v-else class="max-w-5xl mx-auto px-6 py-20 text-center">
      <p class="text-gray-400 text-sm">Produk tidak ditemukan.</p>
      <RouterLink to="/rak-sayur" class="text-green-700 text-sm font-semibold mt-2 inline-block">
        ← Kembali ke Rak Sayur
      </RouterLink>
    </main>

    <TheFooter />
  </div>
</template>
