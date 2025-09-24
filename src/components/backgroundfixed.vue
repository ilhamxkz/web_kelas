<template>
    <div class="bg-wrap">
      <!-- elemen fixed di belakang -->
      <div
        class="bg-fixed"
        :style="fixedStyle"
        aria-hidden="true"
      ></div>
  
      <!-- konten -->
      <div class="bg-content">
        <slot />
      </div>
    </div>
  </template>
  
  <script setup>
  import { computed } from 'vue'
  
  const props = defineProps({
    src: { type: String, required: true },
    position: { type: String, default: 'center center' },
    overlay: { type: String, default: '' } // contoh: 'rgba(0,0,0,0.3)'
  })
  
  const fixedStyle = computed(() => ({
    backgroundImage: `url('${props.src}')`,
    backgroundSize: 'cover',
    backgroundRepeat: 'no-repeat',
    backgroundPosition: props.position,
    top: '0',
    left: '0',
    width: '100%',
    height: '100%',
    zIndex: '-1',
    position: 'fixed',
    transform: 'translateZ(0)', /* membantu rendering */
    // overlay dengan gradient jika diberi props.overlay
    ...(props.overlay ? { backgroundColor: props.overlay, backgroundBlendMode: 'overlay' } : {})
  }))
  </script>
  
  <style scoped>
  .bg-wrap {
    position: relative;
    min-height: 300vh;
    width: 100%;
    /* jika mau area lebih panjang, min-height bisa diubah */
  }
  
  /* elemen gambar fixed di belakang layar */
  .bg-fixed {
    pointer-events: none;
    /* sudah di-set position:fixed dari computed style */
    background-attachment: initial; /* neutral */
  }
  
  /* konten yang di atas background */
  .bg-content {
    position: relative;
    /* beri padding supaya konten terlihat */

  }
  </style>
  