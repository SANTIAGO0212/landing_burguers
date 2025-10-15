<template>
  <section class="hero-section">
    <!-- Fondo dinámico -->
    <div class="hero-bg" :style="backgroundStyle"></div>

    <div class="hero-inner">
      <div class="hero-left">
        <h1 class="hero-title">{{ activeItem.title }}</h1>
        <p class="hero-sub">{{ activeItem.Subtitle }}</p>

        <!--<div class="ingresients">
          <stron>Descripción: </stron>
          <ul>
            <li v-for="(ing, idx) in activeItem.ingredients" :key="idx">{{ ing }}</li>
          </ul>
        </div>-->

        <div class="hero-actions">
          <button class="btn-primary" @click="viewMore">Ver Ingredientes</button>
          <p class="hero-sub">Pídela por: {{ formatPrice(activeItem.price) }} COP</p>
        </div>
      </div>

      <div class="hero-right">
        <div class="food-card" :key="activeItem.id">
          <img :src="activeItem.image" :alt="activeItem.title" class="food-img" />
        </div>
      </div>
    </div>

    <!-- Thumbnails -->
    <ThumbnalList :items="items" :activeId="activeItem.id" @select="setActivityById" />
  </section>
</template>

<script setup>
import {ref, computed} from 'vue'
import { menuItems } from '../data/menu'
import ThumbnalList from './ThumbnaiList.vue'
import Swal from 'sweetalert2'

const items = menuItems
const activeIndex = ref(0)

function setActivityById(id) {
    const idx = items.findIndex(i => i.id === id)
    if(idx >= 0) activeIndex.value = idx
}

const activeItem = computed(() => items[activeIndex.value])
//Aquí se usará la imagen como fondo difuminado en la parte derecha

const backgroundStyle = computed(() => {
return {
    backgroundImage: `radial-gradient(rgba(0,0,0,0.6), rgba(0,0,0,0.9)), url(${activeItem.value.image})`,
    backgroundSize: 'cover',
    backgroundPosition: 'center right'
}
})

function formatPrice(n) {
    return n.toLocaleString('es-CO')
}

function viewMore() {
  Swal.fire({
    title: `Ingredientes de ${activeItem.value.title}`,
      html: `
    <ul style="text-align: left; list-style-type: disc; margin-left: 20px;">
      ${activeItem.value.ingredients.map(ing => `<li>${ing}</li>`).join('')}
    </ul>`,
    imageUrl: `${activeItem.value.image}`,
    imageWidth: 200,
    imageHeight: 200,
    theme: "dark",
    color: "#FFF",
    confirmButtonColor: "#FF5700",
    imageAlt: "Food"
  });
    //alert()
}
</script>

<style scoped>
.hero-section{
  position: relative;
  min-height: 90vh;
  color: #fff;
  overflow: hidden;
}
.hero-bg{
  position:absolute;inset:0;z-index:0;opacity:0.25;filter:blur(8px);
  transition:background-image .6s ease;
}
.hero-inner{
  position:relative;z-index:1;
  max-width:1200px;margin:115px auto 20px;padding:40px 20px;display:flex;gap:40px;align-items:center;
}
.hero-left{flex:1;max-width:55%}
.hero-title{
  font-size:3.2rem;margin:0 0 12px 0;letter-spacing:1px;text-transform:uppercase;
}
.hero-sub{color:#ccc;margin-bottom:18px;line-height:1.4}
.ingredients{margin-bottom:18px;color:#ddd}
.ingredients ul{margin:8px 0 0 16px}
.hero-actions{display:flex;gap:12px;margin-top:18px}
.btn-primary{
  background:linear-gradient(90deg,#ff8a00,#ff3d00);border:none;padding:12px 18px;border-radius:10px;color:#111;font-weight:700;cursor:pointer;
}
.btn-secondary{
  background:transparent;border:1px solid #fff;padding:10px 16px;border-radius:10px;color:#fff;cursor:pointer;
}

.hero-right{width:420px;display:flex;align-items:center;justify-content:center}
.food-card{position:relative;width:360px;height:360px;border-radius:16px;display:flex;align-items:center;justify-content:center;background:linear-gradient(180deg,rgba(255,255,255,0.04),rgba(0,0,0,0.2));box-shadow:0 10px 30px rgba(0,0,0,0.6)}
.food-img{max-width:85%;max-height:85%;object-fit:contain;transform:translateY(-5px)}
.price-badge{position:absolute;bottom:18px;right:18px;background:rgba(0,0,0,0.6);padding:8px 12px;border-radius:8px;font-weight:700}

@media (max-width: 900px){
  .hero-inner{flex-direction:column;align-items:flex-start;padding-top:90px}
  .hero-right{width:100%;display:flex;justify-content:flex-end}
  .hero-left{max-width:100%}
  .hero-title{font-size:2.2rem}
}
</style>