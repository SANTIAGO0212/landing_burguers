<template>
  <div class="thumbs-wrap" id="menu">
    <div class="thumbs-inner">
      <div
        v-for="item in items"
        :key="item.id"
        class="thumb"
        :class="{ active: item.id === activeId }"
        @click="$emit('select', item.id)"
      >
        <img :src="item.image" :alt="item.title" />
      </div>
    </div>
  </div>
</template>

<script setup>
defineProps({
  items: Array,
  activeId: { type: [Number, String], required: true }
})
</script>

<style scoped>
.thumbs-wrap{max-width:1200px;margin:20px auto 80px;padding:0 20px;z-index:3;position:relative}
.thumbs-inner{display:flex;gap:12px;align-items:center;overflow:auto;padding:10px 4px}
.thumb{min-width:88px;height:88px;border:2px solid rgba(255,255,255,0.12);border-radius:8px;padding:6px;display:flex;align-items:center;justify-content:center;cursor:pointer;background:rgba(255,255,255,0.02);transition:transform .18s, border-color .18s}
.thumb img{width:100%;height:100%;object-fit:cover;border-radius:4px}
.thumb.active{transform:scale(1.06);border-color: rgba(255, 138, 0, 0.95);box-shadow:0 8px 22px rgba(255,138,0,0.12)}
</style>
