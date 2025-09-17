<template>
    <header
      class="navbar-wrapper"
      :class="{ 'is-hidden': !visible }"
      aria-label="Main navigation"
    >
      <!-- Top thin bar -->
      <div class="topbar">
        <div class="topbar-inner">
          <div class="left">
            <span class="pin">📍</span>
            <span class="text">MAJALENGKA, JAWA BARAT</span>
          </div>
          <div class="right">
            <a class="help">HELP</a>
            <a class="support">SUPPORT</a>
            <a class="contact">CONTACT</a>
          </div>
        </div>
      </div>
  
      <!-- Main nav (floating white rounded box) -->
      <div class="nav-main">
        <div class="nav-inner">
          <div class="logo">
            <!-- slot untuk logo sehingga bisa diganti -->
            <slot name="logo">
              <div class="logo-placeholder">PELGONE STEMANIKA</div>
            </slot>
          </div>
  
          <nav class="nav-links">
            <a href="#">HOME</a>
            <a href="#">CONTENT</a>
            <a href="#">TEAM</a>
            <a href="#">BLOG</a>
            <a href="#">SHOP</a>
            <a href="#">TOPUP</a>
          </nav>
  
          <div class="nav-actions">
            <button class="cart"><a href="https://www.instagram.com/software.e_one/" style="text-decoration: none; color: black;"><i class="ri-instagram-line"/></a></button>
          </div>
        </div>
      </div>
    </header>
  </template>
  
  <script setup>
  import { ref, onMounted, onBeforeUnmount } from 'vue'
  
  // props untuk kustomisasi (opsional)
  const props = defineProps({
    hideThreshold: { type: Number, default: 10 }, // pixel threshold untuk show/hide
    topAlwaysVisibleAt: { type: Number, default: 10 } // nilai scrollY di bawah ini selalu tampil
  })
  
  const visible = ref(true)
  let lastScrollY = window.scrollY || 0
  let ticking = false
  
  function handleScroll() {
    if (!ticking) {
      window.requestAnimationFrame(processScroll)
      ticking = true
    }
  }
  
  function processScroll() {
    const currentY = window.scrollY || 0
    const delta = currentY - lastScrollY
  
    // jika di paling atas -> selalu tampil
    if (currentY <= props.topAlwaysVisibleAt) {
      visible.value = true
    } else {
      // scroll turun cukup jauh -> sembunyikan
      if (delta > props.hideThreshold) {
        visible.value = false
      }
      // scroll naik cukup jauh -> tampilkan
      else if (delta < -props.hideThreshold) {
        visible.value = true
      }
      // jika perubahan kecil, jangan ubah status
    }
  
    lastScrollY = currentY
    ticking = false
  }
  
  onMounted(() => {
    lastScrollY = window.scrollY || 0
    window.addEventListener('scroll', handleScroll, { passive: true })
  })
  
  onBeforeUnmount(() => {
    window.removeEventListener('scroll', handleScroll)
  })
  </script>
  
  <style scoped>
  /* Wrapper fixed di atas supaya nav mengambang di layar */
  .navbar-wrapper {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    z-index: 9999;
    transform: translateY(0);
    transition: transform 300ms ease, opacity 300ms ease;
    will-change: transform, opacity;
    pointer-events: auto;
  }
  
  /* class ketika disembunyikan */
  .navbar-wrapper.is-hidden {
    transform: translateY(-120%); /* sembunyikan dengan slide up */
    opacity: 0;
    pointer-events: none;
  }
  
  /* Top small bar */
  .topbar {
    background: #cf7d4b; /* warna mirip gambar */
    color: #fff;
    font-size: 13px;
    padding: 6px 0;
  }
  .topbar-inner {
    max-width: 1100px;
    margin: 0 auto;
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 12px;
    padding: 0 16px;
  }
  .topbar .left { display:flex; align-items:center; gap:8px; font-weight:700;}
  .topbar .center { color: rgba(255,255,255,0.95); }
  .topbar .right { display:flex; gap:12px; align-items:center; font-weight:600; }
  
  /* Nav main: white rounded box shadow, positioned overlapping the topbar */
  .nav-main {
    display: flex;
    justify-content: center;
    padding: 10px 16px 18px; /* memberi jarak */
  }
  .nav-inner {
    width: 100%;
    max-width: 1100px;
    background: #fff;
    border-radius: 8px;
    box-shadow: 0 6px 18px rgba(15,23,42,.12);
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 12px 18px;
    gap: 12px;
  }
  
  /* Logo */
  .logo { display:flex; align-items:center; }
  .logo-placeholder {
    font-weight: 800;
    font-size: 20px;
    letter-spacing: 1px;
    color: #f59e0b;
    padding-right: 8px;
  }
  
  /* Links */
  .nav-links {
    display:flex;
    gap: 18px;
    align-items:center;
    justify-content:center;
    flex: 1;
  }
  .nav-links a {
    text-decoration: none;
    color: #111827;
    font-weight: 700;
    font-size: 14px;
  }
  
  /* Actions (right) */
  .nav-actions {
    display:flex;
    gap: 10px;
    align-items:center;
  }
  .nav-actions button {
    background: transparent;
    border: none;
    cursor: pointer;
    font-size: 14px;
    font-weight: 700;
  }
  .cart { position: relative; }
  .badge {
    position: absolute;
    top: -6px;
    right: -8px;
    background: #111827;
    color: #fff;
    font-size: 11px;
    padding: 2px 6px;
    border-radius: 999px;
  }
  
  /* Responsive adjustments */
  @media (max-width: 880px) {
    .nav-links { display: none; } /* hide big links on small screen (you can replace with hamburger) */
    .topbar .center { display:none; }
  }
  </style>
  