<!-- src/components/About.vue -->
<template>
  <section class="about-section">
    <!-- Background Image -->
    <div class="background-image"></div>
    
    <!-- Content -->
    <div class="about-content">
      <!-- Unique ABOUT Title -->
      <h1 class="unique-title">
        <span class="char-a">A</span>
        <span class="char-b">B</span>
        <span class="char-o">O</span>
        <span class="char-u">U</span>
        <span class="char-t">T</span>
      </h1>
      
      <!-- About Card -->
      <div class="about-card">
        <p class="lead">
          Kami adalah tim pengembang web yang fokus pada pembuatan solusi digital yang
          menarik, cepat, dan mudah digunakan. Misi kami adalah membantu bisnis dan
          individu mewujudkan ide menjadi kenyataan melalui teknologi.
        </p>

        <div class="features">
          <div class="feature">
            <h3>Visi</h3>
            <p>Menciptakan pengalaman digital yang bermakna dan berdampak.</p>
          </div>
          <div class="feature">
            <h3>Misi</h3>
            <p>Mendesain & membangun produk berkualitas dengan praktik terbaik.</p>
          </div>
          <div class="feature">
            <h3>Nilai</h3>
            <p>Kolaborasi, kecepatan, dan tanggung jawab terhadap hasil.</p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
// fungsi scroll ke bagian kontak
const scrollToContact = () => {
  const el = document.getElementById('contact') || document.querySelector('.contact')
  if (el) el.scrollIntoView({ behavior: 'smooth', block: 'start' })
}
</script>

<style scoped>
/* Section utama */
.about-section {
  min-height: 100vh;
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 3rem 1rem;
  box-sizing: border-box;
  overflow: hidden;
}

/* Background image */
.background-image {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: url('../assets/BGabout.png') center/cover no-repeat;
  z-index: -1;
}

/* Content container */
.about-content {
  width: 100%;
  max-width: 1000px;
  text-align: center;
  position: relative;
  z-index: 1;
}

/* Unique ABOUT title dengan font berbeda untuk setiap karakter */
.unique-title {
  margin: 0 0 2rem 0;
  font-size: 4rem;
  line-height: 1;
  display: flex;
  justify-content: center;
  align-items: baseline;
  gap: 0.2rem;
  text-shadow: 2px 2px 4px rgba(0,0,0,0.1);
}

.char-a {
  font-family: 'Georgia', serif;
  color: #ff6b6b;
  font-weight: bold;
  transform: rotate(-5deg);
  display: inline-block;
}

.char-b {
  font-family: 'Arial Black', sans-serif;
  color: #4ecdc4;
  font-weight: 900;
  transform: rotate(3deg);
  display: inline-block;
}

.char-o {
  font-family: 'Times New Roman', serif;
  color: #ffe66d;
  font-weight: bold;
  font-style: italic;
  transform: rotate(-2deg) scale(1.1);
  display: inline-block;
}

.char-u {
  font-family: 'Verdana', sans-serif;
  color: #ff8e53;
  font-weight: bold;
  transform: rotate(4deg);
  display: inline-block;
}

.char-t {
  font-family: 'Trebuchet MS', sans-serif;
  color: #a8e6cf;
  font-weight: bold;
  transform: rotate(-3deg);
  display: inline-block;
}

/* About card */
.about-card {
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);
  padding: 2.5rem;
  border-radius: 20px;
  box-shadow: 0 15px 35px rgba(0, 0, 0, 0.1);
  border: 1px solid rgba(255, 255, 255, 0.2);
}

/* Lead text */
.lead {
  font-size: 1.1rem;
  line-height: 1.6;
  color: #333;
  margin: 0 0 2rem 0;
  max-width: 700px;
  margin-left: auto;
  margin-right: auto;
}

/* Features grid */
.features {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 2rem;
  margin: 2rem 0;
}

.feature {
  text-align: center;
  padding: 1rem;
}

.feature h3 {
  margin: 0 0 0.5rem 0;
  font-size: 1.2rem;
  color: #151e27;
  font-weight: 600;
}

.feature p {
  margin: 0;
  font-size: 0.95rem;
  color: #e0e0e0;
  line-height: 1.4;
}

.btn-primary:hover {
  transform: translateY(-2px);
  box-shadow: 0 12px 35px rgba(102, 126, 234, 0.4);
}

.btn-primary:active {
  transform: translateY(0);
}

/* Responsive design */
@media (max-width: 768px) {
  .unique-title {
    font-size: 3rem;
  }
  
  .features {
    grid-template-columns: 1fr;
    gap: 1.5rem;
  }
  
  .about-card {
    padding: 1.5rem;
    border-radius: 15px;
  }
  
  .lead {
    font-size: 1rem;
  }
}

@media (max-width: 480px) {
  .unique-title {
    font-size: 2.5rem;
    gap: 0.1rem;
  }
  
  .about-section {
    padding: 2rem 1rem;
  }
  
  .about-card {
    padding: 1.2rem;
  }
}

/* Hover effects untuk karakter ABOUT */
.unique-title span {
  transition: all 0.3s ease;
  cursor: pointer;
}

.unique-title span:hover {
  transform: rotate(0deg) scale(1.2);
  filter: brightness(1.2);
}
</style>