<script setup>
import { ref, nextTick } from 'vue'
import { useRouter } from 'vue-router'
import { RouterLink } from 'vue-router'
import { UploadCloud, Send, ShieldCheck, ChevronDown, Landmark, CheckCircle2, ShoppingBag } from 'lucide-vue-next'

const router = useRouter()

const heroImage = new URL('@/assets/images/sayur-horizontal.jpg', import.meta.url).href

const orderNumber = ref('')
const selectedBank = ref('')
const uploadedFile = ref(null)
const uploadedPreview = ref(null)
const isDragging = ref(false)
const isSubmitting = ref(false)
const errorMsg = ref('')
const showPopup = ref(false)
const popupVisible = ref(false)

const banks = ['Bank Mandiri', 'Bank BCA', 'Bank BNI', 'Bank BRI', 'Bank BSI']

function handleFileChange(e) {
  const file = e.target.files[0]
  setFile(file)
}

function handleDrop(e) {
  isDragging.value = false
  const file = e.dataTransfer.files[0]
  setFile(file)
}

function setFile(file) {
  if (!file) return
  const allowed = ['image/jpeg', 'image/png', 'application/pdf']
  if (!allowed.includes(file.type)) {
    errorMsg.value = 'Format file tidak didukung. Gunakan PNG, JPG, atau PDF.'
    return
  }
  if (file.size > 5 * 1024 * 1024) {
    errorMsg.value = 'Ukuran file maksimal 5MB.'
    return
  }
  errorMsg.value = ''
  uploadedFile.value = file
  if (file.type !== 'application/pdf') {
    const reader = new FileReader()
    reader.onload = (ev) => (uploadedPreview.value = ev.target.result)
    reader.readAsDataURL(file)
  } else {
    uploadedPreview.value = null
  }
}

function removeFile() {
  uploadedFile.value = null
  uploadedPreview.value = null
}

async function submit() {
  if (!orderNumber.value.trim()) {
    errorMsg.value = 'Nomor pesanan wajib diisi.'
    return
  }
  if (!selectedBank.value) {
    errorMsg.value = 'Pilih bank pengirim terlebih dahulu.'
    return
  }
  if (!uploadedFile.value) {
    errorMsg.value = 'Bukti pembayaran wajib diunggah.'
    return
  }
  errorMsg.value = ''
  isSubmitting.value = true
  // Simulate async submit
  await new Promise((r) => setTimeout(r, 1200))
  isSubmitting.value = false
  showPopup.value = true
  await nextTick()
  setTimeout(() => (popupVisible.value = true), 30)
}

function closePopup() {
  popupVisible.value = false
  setTimeout(() => (showPopup.value = false), 300)
}
</script>

<template>
  <div class="min-h-screen bg-gray-50 flex flex-col">
    <!-- Navbar minimal -->
    <header class="bg-white border-b border-gray-100 sticky top-0 z-50">
      <div class="max-w-5xl mx-auto px-6 py-4 flex items-center justify-between">
        <RouterLink to="/" class="text-base font-bold text-green-700">Wlijoku</RouterLink>
        <div class="flex items-center gap-2 text-xs text-gray-400">
          <span class="w-5 h-5 rounded-full bg-green-600 text-white flex items-center justify-center text-[10px] font-bold">✓</span>
          <span class="text-gray-500 font-medium">Pesanan Dibuat</span>
          <span class="mx-1 text-gray-300">›</span>
          <span class="w-5 h-5 rounded-full bg-green-800 text-white flex items-center justify-center text-[10px] font-bold">2</span>
          <span class="text-green-800 font-semibold">Verifikasi Pembayaran</span>
        </div>
      </div>
    </header>

    <main class="flex-1 max-w-5xl mx-auto w-full px-4 md:px-6 py-10 grid grid-cols-1 md:grid-cols-2 gap-10 items-start">
      <!-- Left: Info -->
      <div>
        <span class="inline-block px-3 py-1 bg-green-100 text-green-700 text-[10px] font-bold uppercase tracking-widest rounded-full mb-4">
          Langkah Terakhir
        </span>
        <h1 class="text-4xl font-extrabold text-green-700 leading-tight mb-4">
          Verifikasi<br />Pembayaran
        </h1>
        <p class="text-sm text-gray-500 leading-relaxed mb-6">
          Bantu kami memproses pesanan Anda lebih cepat.<br />
          Silakan unggah bukti transfer Anda untuk verifikasi instan oleh tim kami.
        </p>

        <!-- Hero image -->
        <div class="rounded-2xl overflow-hidden">
          <img
            :src="heroImage"
            alt="Sayur Segar"
            class="w-full h-56 object-cover"
          />
        </div>
      </div>

      <!-- Right: Form -->
      <div class="bg-white rounded-2xl border border-gray-100 p-6 shadow-sm">
        <!-- Nomor Pesanan -->
        <div class="mb-4">
          <label class="block text-xs font-semibold text-gray-600 mb-1.5">Nomor Pesanan</label>
          <div class="relative">
            <Landmark :size="15" class="absolute left-3 top-1/2 -translate-y-1/2 text-gray-400" />
            <input
              v-model="orderNumber"
              type="text"
              placeholder="Contoh: WLJ-88291"
              class="w-full pl-9 pr-4 py-2.5 rounded-xl border border-gray-200 text-sm focus:outline-none focus:border-green-400 transition"
            />
          </div>
        </div>

        <!-- Bank Pengirim -->
        <div class="mb-5">
          <label class="block text-xs font-semibold text-gray-600 mb-1.5">Bank Pengirim</label>
          <div class="relative">
            <ChevronDown :size="15" class="absolute right-3 top-1/2 -translate-y-1/2 text-gray-400 pointer-events-none" />
            <select
              v-model="selectedBank"
              class="w-full appearance-none pl-4 pr-9 py-2.5 rounded-xl border border-gray-200 text-sm focus:outline-none focus:border-green-400 transition bg-white text-gray-700"
            >
              <option value="" disabled>Pilih Bank</option>
              <option v-for="bank in banks" :key="bank" :value="bank">{{ bank }}</option>
            </select>
          </div>
        </div>

        <!-- Upload Area -->
        <div class="mb-5">
          <label class="block text-xs font-semibold text-gray-600 mb-1.5">Bukti Pembayaran</label>

          <!-- Preview -->
          <div v-if="uploadedFile" class="relative rounded-xl border border-gray-200 overflow-hidden">
            <img
              v-if="uploadedPreview"
              :src="uploadedPreview"
              alt="Preview"
              class="w-full max-h-48 object-contain bg-gray-50"
            />
            <div
              v-else
              class="flex items-center gap-3 px-4 py-4 bg-gray-50"
            >
              <UploadCloud :size="20" class="text-green-600" />
              <span class="text-sm text-gray-700 font-medium truncate">{{ uploadedFile.name }}</span>
            </div>
            <button
              @click="removeFile"
              class="absolute top-2 right-2 w-6 h-6 rounded-full bg-white border border-gray-200 text-gray-500 hover:text-red-500 flex items-center justify-center text-xs shadow-sm"
            >✕</button>
          </div>

          <!-- Drop zone -->
          <label
            v-else
            class="flex flex-col items-center justify-center gap-2 border-2 border-dashed rounded-xl py-10 cursor-pointer transition-colors"
            :class="isDragging ? 'border-green-400 bg-green-50' : 'border-gray-200 bg-gray-50 hover:border-green-300'"
            @dragover.prevent="isDragging = true"
            @dragleave.prevent="isDragging = false"
            @drop.prevent="handleDrop"
          >
            <div class="w-12 h-12 rounded-full bg-green-100 flex items-center justify-center">
              <UploadCloud :size="22" class="text-green-600" />
            </div>
            <p class="text-sm font-semibold text-gray-700">Upload Foto Bukti Transfer atau Invoice Anda</p>
            <p class="text-xs text-gray-400">PNG, JPG atau PDF (Maks. 5MB)</p>
            <input
              type="file"
              accept=".png,.jpg,.jpeg,.pdf"
              class="hidden"
              @change="handleFileChange"
            />
          </label>
        </div>

        <!-- Error -->
        <p v-if="errorMsg" class="text-xs text-red-500 mb-3 -mt-2">{{ errorMsg }}</p>

        <!-- Submit -->
        <button
          @click="submit"
          :disabled="isSubmitting"
          class="w-full py-3 bg-green-800 text-white text-sm font-semibold rounded-full flex items-center justify-center gap-2 hover:bg-green-700 transition-colors disabled:opacity-60 disabled:cursor-not-allowed"
        >
          <span v-if="isSubmitting">Mengirim...</span>
          <template v-else>
            Kirim Verifikasi
            <Send :size="15" />
          </template>
        </button>

        <!-- Trust note -->
        <div class="flex items-center justify-center gap-1.5 mt-3 text-xs text-gray-400">
          <ShieldCheck :size="13" />
          <span>Data Anda dienkripsi dan aman bersama kami.</span>
        </div>
      </div>
    </main>

    <!-- Footer -->
    <footer class="bg-white border-t border-gray-100 py-10">
      <div class="max-w-5xl mx-auto px-6">
        <div class="grid grid-cols-2 md:grid-cols-4 gap-8 mb-8">
          <div class="col-span-2 md:col-span-1">
            <p class="text-base font-bold text-green-700 mb-2">Wlijoku</p>
            <p class="text-xs text-gray-400 leading-relaxed">
              Menghadirkan keajaiban alam langsung ke dapur Anda. Segar, organik, dan penuh nutrisi.
            </p>
          </div>
          <div>
            <p class="text-[10px] font-bold text-gray-500 uppercase tracking-widest mb-3">Perusahaan</p>
            <ul class="space-y-2 text-xs text-gray-500">
              <li><a href="#" class="hover:text-gray-800">Tentang Wlijoku</a></li>
              <li><a href="#" class="hover:text-gray-800">Hubungi Kami</a></li>
            </ul>
          </div>
          <div>
            <p class="text-[10px] font-bold text-gray-500 uppercase tracking-widest mb-3">Bantuan</p>
            <ul class="space-y-2 text-xs text-gray-500">
              <li><a href="#" class="hover:text-gray-800">FAQ</a></li>
              <li><a href="#" class="hover:text-gray-800">Syarat &amp; Ketentuan</a></li>
            </ul>
          </div>
          <div>
            <p class="text-[10px] font-bold text-gray-500 uppercase tracking-widest mb-3">Legal</p>
            <ul class="space-y-2 text-xs text-gray-500">
              <li><a href="#" class="hover:text-gray-800">Kebijakan Privasi</a></li>
            </ul>
          </div>
        </div>
        <div class="border-t border-gray-100 pt-6 text-center">
          <p class="text-xs text-gray-400">© 2024 Wlijoku. Segar dari Kebun Ke Rumah Anda.</p>
        </div>
      </div>
    </footer>

    <!-- Success Popup Overlay -->
    <Teleport to="body">
      <div
        v-if="showPopup"
        class="fixed inset-0 z-50 flex items-center justify-center px-4 transition-all duration-300"
        :class="popupVisible ? 'bg-black/40 backdrop-blur-sm' : 'bg-transparent'"
        @click.self="closePopup"
      >
        <div
          class="bg-white rounded-3xl shadow-2xl max-w-sm w-full p-8 flex flex-col items-center text-center transition-all duration-300"
          :class="popupVisible ? 'opacity-100 scale-100 translate-y-0' : 'opacity-0 scale-90 translate-y-6'"
        >
          <!-- Animated check icon -->
          <div class="w-20 h-20 rounded-full bg-green-100 flex items-center justify-center mb-5 animate-bounce-once">
            <CheckCircle2 :size="44" class="text-green-600" stroke-width="1.5" />
          </div>

          <!-- Text -->
          <h2 class="text-xl font-extrabold text-gray-900 mb-2">Pesanan Akan Segera Diproses!</h2>
          <p class="text-sm text-gray-500 leading-relaxed mb-6">
            Terima kasih telah berbelanja di toko kami.<br />
            Tim kami akan memverifikasi pembayaran Anda dan mempersiapkan sayuran segar pilihan Anda.
          </p>

          <!-- Order badge -->
          <div class="flex items-center gap-2 bg-green-50 border border-green-100 rounded-xl px-4 py-2.5 mb-6 w-full justify-center">
            <ShoppingBag :size="15" class="text-green-600" />
            <span class="text-sm font-semibold text-green-700">{{ orderNumber || '#WJ-2024001' }}</span>
          </div>

          <!-- CTA -->
          <button
            @click="() => { closePopup(); router.push({ name: 'home' }) }"
            class="w-full py-3 bg-green-800 text-white text-sm font-semibold rounded-full hover:bg-green-700 transition-colors mb-3"
          >
            Kembali ke Beranda
          </button>
          <RouterLink
            to="/keranjang"
            class="text-xs text-gray-400 hover:text-gray-600 transition-colors"
            @click="closePopup"
          >
            Lihat status pesanan saya
          </RouterLink>
        </div>
      </div>
    </Teleport>
  </div>
</template>

<style scoped>
@keyframes bounce-once {
  0%, 100% { transform: translateY(0); }
  30% { transform: translateY(-12px); }
  60% { transform: translateY(-5px); }
}
.animate-bounce-once {
  animation: bounce-once 0.7s ease 0.2s both;
}
</style>
