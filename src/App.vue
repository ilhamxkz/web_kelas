<script setup>
import Footer from './components/footer.vue';
import Backgroundfixed from './components/backgroundfixed.vue';
import Navbar from './components/navbar.vue';
import Body from './components/header.vue';
import Bayangan from './components/bayangan.vue';
import About from './components/about.vue';
</script>

<template>
  <Backgroundfixed src="src/assets/schoolbackground_.png">
    <Bayangan>
      <Navbar />
      <Body />
      <About />
      <Footer />
    </Bayangan>
  </Backgroundfixed>
</template>

<style>
html,
body {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  background: transparent;
}
*,
*::before,
*::after {
  box-sizing: inherit;
}
</style>
