<!-- src/components/About.vue -->
<template>
  <!-- pakai komponen bayangan (pastikan path import benar) -->
  <Bayangan :src="bgImage">
    <!-- slot -> isi konten About, kita bungkus di section yang centered -->
    <section class="about-section" role="region" aria-labelledby="about-title">
      <div class="about-card">
        <h1 id="about-title">Tentang Kami</h1>
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

        <div class="actions">
          <button class="btn-primary" @click="scrollToContact">Hubungi Kami</button>
        </div>
      </div>
    </section>
  </Bayangan>
</template>

<script setup>
import bgImage from '@/assets/BGabout.png' // ganti dengan path background-mu

// fungsi kecil: contoh scroll ke bagian kontak jika ada
const scrollToContact = () => {
  const el = document.getElementById('contact') || document.querySelector('.contact')
  if (el) el.scrollIntoView({ behavior: 'smooth', block: 'start' })
}
</script>

<style scoped>
/* section yg menengahkan konten */
.about-section{
  min-height: 100vh;           /* pusatkan di viewport */
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 3rem 1rem;
  box-sizing: border-box;
}

/* kartu konten */
.about-card{
  width: 100%;
  max-width: 980px;
  padding: 2rem;
  border-radius: 16px;
  box-shadow: 0 10px 30px rgba(2,6,23,0.35);
  background: rgba(255,255,255,0.75);   /* terang di atas background */
  backdrop-filter: blur(6px);
  -webkit-backdrop-filter: blur(6px);
  color: #0b1220;
}

/* judul */
.about-card h1{
  margin: 0 0 0.5rem 0;
  font-size: 2rem;
  line-height: 1.1;
}

/* ringkasan */
.about-card .lead{
  margin: 0 0 1.25rem 0;
  font-size: 1.05rem;
  color: rgba(11,18,32,0.85);
}

/* tiga fitur di bawah */
.features{
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1rem;
  margin-top: 1rem;
}

.feature h3{
  margin: 0 0 0.4rem 0;
  font-size: 1rem;
}
.feature p{
  margin: 0;
  font-size: 0.95rem;
  color: rgba(11,18,32,0.85);
}

/* aksi / tombol */
.actions{
  margin-top: 1.25rem;
  display: flex;
  gap: 0.75rem;
}

/* simple button */
.btn-primary{
  background: linear-gradient(180deg,#0b63ff,#0a4fe0);
  color: white;
  border: none;
  padding: 0.6rem 1rem;
  border-radius: 8px;
  cursor: pointer;
  font-weight: 600;
  box-shadow: 0 6px 18px rgba(10,79,224,0.28);
}
.btn-primary:active{ transform: translateY(1px); }

/* responsive: ubah layout fitur jadi 1 kolom di mobile */
@media (max-width: 880px){
  .features{ grid-template-columns: 1fr; }
  .about-card{ padding: 1.25rem; border-radius: 12px; }
  .about-card h1{ font-size: 1.6rem; }
}

/* jika kamu pake bayangan dengan shadeZ sangat tinggi, konten tetap terlihat
   karena .about-card memiliki background semi-opaque dan z-index default.
   Jika terjadi tumpang tindih z-index, tambahkan z-index di sini: */
.about-card{ position: relative; z-index: 2; }
</style>
