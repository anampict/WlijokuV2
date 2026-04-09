<script setup>
import TheNavbar from '../components/layout/TheNavbar.vue'
import TheFooter from '../components/layout/TheFooter.vue'
import HeroSection from '../components/home/HeroSection.vue'
import ProductSection from '../components/home/ProductSection.vue'
import SubscriptionBanner from '../components/home/SubscriptionBanner.vue'
import WhySection from '../components/home/WhySection.vue'
</script>

<template>
  <div class="min-h-screen bg-white">
    <TheNavbar />
    <main>
      <HeroSection />
      <ProductSection />
      <SubscriptionBanner />
      <WhySection />
    </main>
    <TheFooter />
  </div>
</template>
