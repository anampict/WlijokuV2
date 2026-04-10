<script setup>
import { ref } from 'vue'
import { RouterLink, useRouter } from 'vue-router'
import { User, Mail, Phone, Lock, Eye, EyeOff, ArrowRight } from 'lucide-vue-next'

const router = useRouter()

const heroImage = new URL('@/assets/images/daftar-hero.jpg', import.meta.url).href

const fullName = ref('')
const email = ref('')
const phone = ref('')
const password = ref('')
const confirmPassword = ref('')
const showPassword = ref(false)
const showConfirm = ref(false)
const agreeTerms = ref(false)
const isLoading = ref(false)
const errorMsg = ref('')

async function handleRegister() {
  if (!fullName.value.trim()) {
    errorMsg.value = 'Nama lengkap wajib diisi.'
    return
  }
  if (!email.value.trim()) {
    errorMsg.value = 'Email wajib diisi.'
    return
  }
  if (!phone.value.trim()) {
    errorMsg.value = 'Nomor telepon wajib diisi.'
    return
  }
  if (!password.value) {
    errorMsg.value = 'Kata sandi wajib diisi.'
    return
  }
  if (password.value.length < 8) {
    errorMsg.value = 'Kata sandi minimal 8 karakter.'
    return
  }
  if (password.value !== confirmPassword.value) {
    errorMsg.value = 'Konfirmasi kata sandi tidak cocok.'
    return
  }
  if (!agreeTerms.value) {
    errorMsg.value = 'Anda harus menyetujui syarat & ketentuan.'
    return
  }
  errorMsg.value = ''
  isLoading.value = true
  await new Promise((r) => setTimeout(r, 1200))
  isLoading.value = false
  router.push({ name: 'login' })
}
</script>

<template>
  <div class="min-h-screen bg-gradient-to-br from-green-50 via-white to-emerald-50 flex flex-col items-center justify-center px-4 py-10">
    <div class="w-full max-w-3xl bg-white rounded-3xl shadow-xl overflow-hidden flex flex-col md:flex-row">

      <!-- Left: Hero Image -->
      <div class="relative md:w-5/12 min-h-[260px] md:min-h-0 flex flex-col justify-end overflow-hidden">
        <img
          :src="heroImage"
          alt="Sayur Segar"
          class="absolute inset-0 w-full h-full object-cover"
        />
        <!-- Gradient overlay bottom -->
        <div class="absolute inset-0 bg-gradient-to-t from-black/70 via-black/20 to-transparent"></div>

        <!-- Content -->
        <div class="relative z-10 p-8 pb-10">
          <h2 class="text-white text-2xl md:text-3xl font-extrabold leading-snug mb-2">
            Segar dari Kebun Ke<br />Rumah Anda.
          </h2>
          <p class="text-white/70 text-sm leading-relaxed">
            Bergabunglah dengan Wlijoku untuk mendapatkan akses ke sayuran organik terbaik setiap hari.
          </p>
        </div>
      </div>

      <!-- Right: Form -->
      <div class="flex-1 p-8 md:p-10 flex flex-col justify-center">
        <div class="mb-6">
          <p class="text-green-700 text-lg font-bold mb-1">Wlijoku</p>
          <h1 class="text-xl font-extrabold text-gray-900">Buat Akun Baru</h1>
          <p class="text-sm text-gray-400 mt-1">Buat akun baru untuk mulai belanja segar.</p>
        </div>

        <div class="space-y-4">
          <!-- Nama Lengkap -->
          <div>
            <label class="block text-[10px] font-bold text-gray-500 uppercase tracking-widest mb-1.5">Nama Lengkap</label>
            <div class="relative">
              <User :size="15" class="absolute left-3.5 top-1/2 -translate-y-1/2 text-gray-400" />
              <input
                v-model="fullName"
                type="text"
                placeholder="Budi Santoso"
                autocomplete="name"
                class="w-full pl-10 pr-4 py-2.5 rounded-xl border border-gray-200 text-sm bg-gray-50 focus:bg-white focus:outline-none focus:border-green-400 transition"
              />
            </div>
          </div>

          <!-- Email -->
          <div>
            <label class="block text-[10px] font-bold text-gray-500 uppercase tracking-widest mb-1.5">Email</label>
            <div class="relative">
              <Mail :size="15" class="absolute left-3.5 top-1/2 -translate-y-1/2 text-gray-400" />
              <input
                v-model="email"
                type="email"
                placeholder="budi@email.com"
                autocomplete="email"
                class="w-full pl-10 pr-4 py-2.5 rounded-xl border border-gray-200 text-sm bg-gray-50 focus:bg-white focus:outline-none focus:border-green-400 transition"
              />
            </div>
          </div>

          <!-- Nomor Telepon -->
          <div>
            <label class="block text-[10px] font-bold text-gray-500 uppercase tracking-widest mb-1.5">Nomor Telepon</label>
            <div class="relative">
              <Phone :size="15" class="absolute left-3.5 top-1/2 -translate-y-1/2 text-gray-400" />
              <input
                v-model="phone"
                type="tel"
                placeholder="0812 3456 7890"
                autocomplete="tel"
                class="w-full pl-10 pr-4 py-2.5 rounded-xl border border-gray-200 text-sm bg-gray-50 focus:bg-white focus:outline-none focus:border-green-400 transition"
              />
            </div>
          </div>

          <!-- Password row -->
          <div class="grid grid-cols-2 gap-3">
            <!-- Kata Sandi -->
            <div>
              <label class="block text-[10px] font-bold text-gray-500 uppercase tracking-widest mb-1.5">Kata Sandi</label>
              <div class="relative">
                <Lock :size="15" class="absolute left-3.5 top-1/2 -translate-y-1/2 text-gray-400" />
                <input
                  v-model="password"
                  :type="showPassword ? 'text' : 'password'"
                  placeholder="••••••••"
                  autocomplete="new-password"
                  class="w-full pl-10 pr-9 py-2.5 rounded-xl border border-gray-200 text-sm bg-gray-50 focus:bg-white focus:outline-none focus:border-green-400 transition"
                />
                <button
                  type="button"
                  class="absolute right-3 top-1/2 -translate-y-1/2 text-gray-400 hover:text-gray-600 transition"
                  @click="showPassword = !showPassword"
                >
                  <EyeOff v-if="showPassword" :size="14" />
                  <Eye v-else :size="14" />
                </button>
              </div>
            </div>

            <!-- Konfirmasi Kata Sandi -->
            <div>
              <label class="block text-[10px] font-bold text-gray-500 uppercase tracking-widest mb-1.5">Konfirmasi Kata Sandi</label>
              <div class="relative">
                <Lock :size="15" class="absolute left-3.5 top-1/2 -translate-y-1/2 text-gray-400" />
                <input
                  v-model="confirmPassword"
                  :type="showConfirm ? 'text' : 'password'"
                  placeholder="••••••••"
                  autocomplete="new-password"
                  class="w-full pl-10 pr-9 py-2.5 rounded-xl border border-gray-200 text-sm bg-gray-50 focus:bg-white focus:outline-none focus:border-green-400 transition"
                />
                <button
                  type="button"
                  class="absolute right-3 top-1/2 -translate-y-1/2 text-gray-400 hover:text-gray-600 transition"
                  @click="showConfirm = !showConfirm"
                >
                  <EyeOff v-if="showConfirm" :size="14" />
                  <Eye v-else :size="14" />
                </button>
              </div>
            </div>
          </div>

          <!-- Terms -->
          <label class="flex items-start gap-2 cursor-pointer select-none">
            <input
              v-model="agreeTerms"
              type="checkbox"
              class="w-4 h-4 mt-0.5 rounded border-gray-300 accent-green-700 shrink-0"
            />
            <span class="text-sm text-gray-500 leading-snug">
              Saya menyetujui
              <a href="#" class="text-green-600 font-semibold hover:underline">Syarat &amp; Ketentuan</a>
              serta
              <a href="#" class="text-green-600 font-semibold hover:underline">Kebijakan Privasi</a>
              Wlijoku.
            </span>
          </label>

          <!-- Error -->
          <p v-if="errorMsg" class="text-xs text-red-500 -mt-1">{{ errorMsg }}</p>

          <!-- Submit -->
          <button
            @click="handleRegister"
            :disabled="isLoading"
            class="w-full py-3 bg-green-800 text-white text-sm font-semibold rounded-full flex items-center justify-center gap-2 hover:bg-green-700 transition-colors disabled:opacity-60 disabled:cursor-not-allowed"
          >
            <span v-if="isLoading">Mendaftarkan...</span>
            <template v-else>
              Daftar Sekarang
              <ArrowRight :size="15" />
            </template>
          </button>
        </div>

        <!-- Login link -->
        <p class="text-sm text-center text-gray-400 mt-5">
          Sudah punya akun?
          <RouterLink to="/login" class="text-green-700 font-bold hover:underline ml-1">Masuk</RouterLink>
        </p>
      </div>
    </div>

    <!-- Footer -->
    <footer class="w-full max-w-3xl mt-10">
      <div class="flex flex-col md:flex-row items-start md:items-center justify-between gap-4">
        <div>
          <p class="text-sm font-bold text-green-700">Wlijoku</p>
          <p class="text-xs text-gray-400 mt-0.5">© 2024 Wlijoku. Segar dari Kebun Ke Rumah Anda.</p>
        </div>
        <div class="flex gap-5 text-xs text-gray-400">
          <a href="#" class="hover:text-gray-700 transition">Tentang Kami</a>
          <a href="#" class="hover:text-gray-700 transition">Kebijakan Privasi</a>
          <a href="#" class="hover:text-gray-700 transition">Syarat &amp; Ketentuan</a>
          <a href="#" class="hover:text-gray-700 transition">Hubungi Kami</a>
        </div>
      </div>
    </footer>
  </div>
</template>
