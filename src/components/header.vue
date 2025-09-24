<template>
  <div class="hero-wrapper">
    <img :src="Fotokita" alt="Foto Pelgone" class="hero-img" />
    <!-- konten lain di atas foto, jika perlu -->
  </div>
</template>

<script setup>
import Fotokita from '../assets/usXIrpl1.png';
</script>

<style scoped>
.hero-wrapper {
  width: 100%; 
  box-sizing: border-box;
  height: 100%;      /* penuh layar */
  overflow: hidden;   /* potongan yang melampaui disembunyikan */
  display: block;
}

/* Foto sebagai elemen, bukan background */
.hero-img {
  width: 100%;
  height: 100%;
  object-fit: cover;    /* isi area, crop bila perlu */
  object-position: center;
  display: block;
}
</style>
