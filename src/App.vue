<template>
  <div id="app" class="app-root">
    <HeaderNav />
    <main>
      <HeroCarousel />
    </main>
    <Footer />
  </div>
</template>

<script setup>
import HeaderNav from './components/HeaderNav.vue'
import HeroCarousel from './components/HeroCarousel.vue'
import Footer from './components/Footer.vue'
</script>
