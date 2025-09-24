<template>
  <div class="bg-wrap">
    <!-- background utama fixed (opsional) -->
    <div
      v-if="src"
      class="bg-fixed"
      :style="fixedStyle"
      aria-hidden="true"
    ></div>

    <!-- decorative shadows (fixed, di atas semua komponen) -->
    <div
      class="dec-shade dec-shade--top"
      :style="topStyle"
      aria-hidden="true"
    ></div>

    <div
      class="dec-shade dec-shade--bottom"
      :style="bottomStyle"
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
import bayangAtas from '@/assets/decoration/bayang-atas.png'
import bayangBawah from '@/assets/decoration/bayang-bawah.png'

const props = defineProps({
  // optional main background image (kalau nggak pakai biarkan kosong)
  src: { type: String, default: '' },

  topShadow: { type: String, default: bayangAtas },
  bottomShadow: { type: String, default: bayangBawah },

  // posisi/bg utama
  position: { type: String, default: 'center center' },
  overlay: { type: String, default: '' },

  // z-index untuk shadows supaya mudah atur (pastikan lebih tinggi dari elemen lain)
  shadeZ: { type: [String, Number], default: 9999 },

  // ukuran default bayangan (bisa override saat pakai komponen)
  topWidth: { type: String, default: '30vw' },
  topHeight: { type: String, default: '30vh' },
  bottomWidth: { type: String, default: '30vw' },
  bottomHeight: { type: String, default: '30vh' }
})

const fixedStyle = computed(() => {
  const base = {
    backgroundSize: 'cover',
    backgroundRepeat: 'no-repeat',
    backgroundPosition: props.position,
    top: '0',
    left: '0',
    right: '0',
    bottom: '0',
    zIndex: 0,
    position: 'fixed',
    pointerEvents: 'none',
    transform: 'translateZ(0)'
  }
  if (props.src) {
    base.backgroundImage = `url('${props.src}')`
    if (props.overlay) {
      base.backgroundColor = props.overlay
      base.backgroundBlendMode = 'overlay'
    }
  }
  return base
})

const topStyle = computed(() => ({
  backgroundImage: `url('${props.topShadow}')`,
  backgroundRepeat: 'no-repeat',
  backgroundPosition: 'right top',
  backgroundSize: 'contain',
  position: 'fixed',
  top: '0',
  right: '0',
  width: props.topWidth,
  height: props.topHeight,
  pointerEvents: 'none',
  zIndex: String(props.shadeZ),
  transform: 'translateZ(0)',
  mixBlendMode: 'multiply',
  opacity: 0.95
}))

const bottomStyle = computed(() => ({
  backgroundImage: `url('${props.bottomShadow}')`,
  backgroundRepeat: 'no-repeat',
  backgroundPosition: 'left bottom',
  backgroundSize: 'contain',
  position: 'fixed',
  left: '0',
  bottom: '0',
  width: props.bottomWidth,
  height: props.bottomHeight,
  pointerEvents: 'none',
  zIndex: String(props.shadeZ),
  transform: 'translateZ(0)',
  mixBlendMode: 'multiply',
  opacity: 0.95
}))
</script>

<style scoped>
.bg-wrap {
  position: relative;
  min-height: 300vh;
  width: 100%;
}

/* bg-fixed hanya muncul jika props.src diisi */
.bg-fixed {
  /* style di-set via computed style */
}

/* decorative shadow base */
.dec-shade {
  pointer-events: none; /* jangan ganggu klik atau hover */
  background-repeat: no-repeat;
  background-position: center;
  background-size: contain;
  will-change: transform;
}

/* jika ingin override/efek tambahan, bisa di sini */
.dec-shade--top { /* tambahan gaya jika perlu */ }
.dec-shade--bottom { /* tambahan gaya jika perlu */ }

.bg-content {
  position: relative;
  z-index: 1; /* konten tetap di bawah dekorasi yang punya shadeZ tinggi */
}

/* Responsive adjustments supaya bayangan tidak terlalu besar di mobile */
@media (max-width: 600px) {
  .dec-shade--top {
    width: 45vw !important;
    height: 35vh !important;
  }
  .dec-shade--bottom {
    width: 45vw !important;
    height: 35vh !important;
  }
}
</style>
