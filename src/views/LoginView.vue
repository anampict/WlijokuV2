<script setup>
import { ref } from 'vue'
import { RouterLink, useRouter } from 'vue-router'
import { User, Lock, Eye, EyeOff, ArrowRight, Leaf, Truck } from 'lucide-vue-next'

const router = useRouter()

const heroImage = new URL('@/assets/images/sayur-horizontal.jpg', import.meta.url).href

const email = ref('')
const password = ref('')
const rememberMe = ref(false)
const showPassword = ref(false)
const isLoading = ref(false)
const errorMsg = ref('')

async function handleLogin() {
  if (!email.value.trim()) {
    errorMsg.value = 'Email atau username wajib diisi.'
    return
  }
  if (!password.value) {
    errorMsg.value = 'Kata sandi wajib diisi.'
    return
  }
  errorMsg.value = ''
  isLoading.value = true
  await new Promise((r) => setTimeout(r, 1000))
  isLoading.value = false
  router.push({ name: 'home' })
}
</script>

<template>
  <div class="min-h-screen bg-gradient-to-br from-green-50 via-white to-emerald-50 flex flex-col items-center justify-center px-4 py-10">
    <div class="w-full max-w-3xl bg-white rounded-3xl shadow-xl overflow-hidden flex flex-col md:flex-row">

      <!-- Left: Brand Panel -->
      <div class="relative md:w-5/12 min-h-[260px] md:min-h-0 flex flex-col justify-between p-8 overflow-hidden">
        <!-- Background image -->
        <img
          :src="heroImage"
          alt="Sayur Segar"
          class="absolute inset-0 w-full h-full object-cover"
        />
        <!-- Dark overlay -->
        <div class="absolute inset-0 bg-green-900/70"></div>

        <!-- Content -->
        <div class="relative z-10">
          <p class="text-white font-bold text-lg mb-1">Wlijoku</p>
          <div class="w-8 h-0.5 bg-white/60 mb-5 rounded-full"></div>
          <h2 class="text-white text-2xl md:text-3xl font-extrabold leading-snug">
            Segar dari Kebun Ke<br />Rumah Anda.
          </h2>
          <p class="text-white/70 text-sm mt-3 leading-relaxed">
            Nikmati kemudahan berbelanja sayur organik berkualitas tinggi langsung dari genggaman Anda.
          </p>
        </div>

        <!-- Trust icons -->
        <div class="relative z-10 flex items-center gap-3 mt-6">
          <div class="w-8 h-8 rounded-full bg-white/20 flex items-center justify-center">
            <Leaf :size="15" class="text-white" />
          </div>
          <div class="w-8 h-8 rounded-full bg-white/20 flex items-center justify-center">
            <Truck :size="15" class="text-white" />
          </div>
        </div>
      </div>

      <!-- Right: Form -->
      <div class="flex-1 p-8 md:p-10 flex flex-col justify-center">
        <h1 class="text-2xl font-extrabold text-gray-900 mb-1">Selamat Datang</h1>
        <p class="text-sm text-gray-400 mb-7">Silakan masuk ke akun Wlijoku Anda</p>

        <div class="space-y-4">
          <!-- Email -->
          <div>
            <label class="block text-[10px] font-bold text-gray-500 uppercase tracking-widest mb-1.5">
              Email atau Username
            </label>
            <div class="relative">
              <User :size="15" class="absolute left-3.5 top-1/2 -translate-y-1/2 text-gray-400" />
              <input
                v-model="email"
                type="text"
                placeholder="nama@email.com"
                autocomplete="email"
                class="w-full pl-10 pr-4 py-2.5 rounded-xl border border-gray-200 text-sm bg-gray-50 focus:bg-white focus:outline-none focus:border-green-400 transition"
                @keyup.enter="handleLogin"
              />
            </div>
          </div>

          <!-- Password -->
          <div>
            <div class="flex items-center justify-between mb-1.5">
              <label class="block text-[10px] font-bold text-gray-500 uppercase tracking-widest">
                Kata Sandi
              </label>
              <a href="#" class="text-xs text-green-600 font-semibold hover:underline">Lupa Kata Sandi?</a>
            </div>
            <div class="relative">
              <Lock :size="15" class="absolute left-3.5 top-1/2 -translate-y-1/2 text-gray-400" />
              <input
                v-model="password"
                :type="showPassword ? 'text' : 'password'"
                placeholder="••••••••"
                autocomplete="current-password"
                class="w-full pl-10 pr-10 py-2.5 rounded-xl border border-gray-200 text-sm bg-gray-50 focus:bg-white focus:outline-none focus:border-green-400 transition"
                @keyup.enter="handleLogin"
              />
              <button
                type="button"
                class="absolute right-3.5 top-1/2 -translate-y-1/2 text-gray-400 hover:text-gray-600 transition"
                @click="showPassword = !showPassword"
              >
                <EyeOff v-if="showPassword" :size="15" />
                <Eye v-else :size="15" />
              </button>
            </div>
          </div>

          <!-- Remember me -->
          <label class="flex items-center gap-2 cursor-pointer select-none">
            <input
              v-model="rememberMe"
              type="checkbox"
              class="w-4 h-4 rounded border-gray-300 accent-green-700"
            />
            <span class="text-sm text-gray-500">Ingat saya</span>
          </label>

          <!-- Error -->
          <p v-if="errorMsg" class="text-xs text-red-500">{{ errorMsg }}</p>

          <!-- Submit -->
          <button
            @click="handleLogin"
            :disabled="isLoading"
            class="w-full py-3 bg-green-800 text-white text-sm font-semibold rounded-full flex items-center justify-center gap-2 hover:bg-green-700 transition-colors disabled:opacity-60 disabled:cursor-not-allowed mt-1"
          >
            <span v-if="isLoading">Memproses...</span>
            <template v-else>
              Masuk
              <ArrowRight :size="15" />
            </template>
          </button>
        </div>

        <!-- Register link -->
        <p class="text-sm text-center text-gray-400 mt-6">
          Belum punya akun?
          <RouterLink to="/daftar" class="text-green-700 font-bold hover:underline ml-1">Daftar Sekarang</RouterLink>
        </p>
      </div>
    </div>

    <!-- Footer note -->
    <p class="text-xs text-gray-400 mt-6 uppercase tracking-widest">© 2024 Wlijoku. Segar dari Kebun Ke Rumah Anda.</p>
  </div>
</template>
