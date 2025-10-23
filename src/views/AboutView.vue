<script setup>
import { onMounted, ref } from 'vue'

const isVisible = ref(false)

onMounted(() => {
  setTimeout(() => {
    isVisible.value = true
  }, 300)
})
</script>

<template>
  <div class="about-page" :class="{ visible: isVisible }">
    <!-- Hero Section -->
    <section class="hero-about">
      <div class="hero-overlay"></div>
      <div class="hero-content">
        <div class="ornament">⚜</div>
        <h1 class="main-title">Chi Siamo</h1>
        <div class="title-divider"></div>
        <p class="subtitle">La nostra storia, la nostra passione</p>
      </div>
    </section>

    <!-- Main Content -->
    <section class="content-section">
      <div class="container">
        <!-- Intro Card -->
        <div class="intro-card">
          <div class="card-ornament">◆</div>
          <h2>Un Angolo di Sapori</h2>
          <div class="text-divider"></div>
          <p class="lead-text">
            Il Ristorante Pesce d'Oro è uno fra i locali più antichi di Alghero, ormai sta
            diventando una meta obbligatoria per il turismo e un punto d'incontro per i cittadini di
            Alghero e dintorni.
          </p>
        </div>

        <!-- Story Grid -->
        <div class="story-grid">
          <!-- Left Column -->
          <div class="story-block block-left">
            <div class="block-number">01</div>
            <h3>La Nuova Gestione</h3>
            <div class="block-divider"></div>
            <p>
              Al "Pesce d'oro" c'è stato un cambio di gestione che ha decisamente rivalutato il
              locale. La trasformazione è stata, infatti, opera dello chef algherese e della moglie.
            </p>
            <p>
              Il talento dello chef lascerà soddisfatti i vostri palati grazie ai suoi anni di
              esperienza nel settore.
            </p>
          </div>

          <!-- Right Column -->
          <div class="story-block block-right">
            <div class="block-number">02</div>
            <h3>Gli Spazi</h3>
            <div class="block-divider"></div>
            <p>
              Il locale dispone di <strong>100 posti a sedere</strong> che si dividono in 2 sale
              interne accoglienti e munite di aria condizionata.
            </p>
            <p>
              Altri <strong>20 posti</strong> sono situati nella sala esterna, immersi nel giardino
              dell'isola pedonale.
            </p>
          </div>
        </div>

        <!-- Mission Statement -->
        <div class="mission-section">
          <div class="mission-content">
            <div class="mission-icon">★</div>
            <h3>La Nostra Missione</h3>
            <div class="mission-divider"></div>
            <p class="mission-text">
              Il nostro ristorante, in cui emergono serietà e dedizione per questo tipo di lavoro, è
              un punto di riferimento nella zona di Alghero per gli appassionati del buon cibo e di
              un menù che spazia dal piatto più semplice al più raffinato e per soddisfare ogni tipo
              di occasione… e di palato!
            </p>
          </div>
        </div>

        <!-- Features -->
        <div class="features-section">
          <div class="feature-item">
            <div class="feature-icon">🍽️</div>
            <h4>Tradizione</h4>
            <p>Ricette autentiche tramandate nel tempo</p>
          </div>
          <div class="feature-item">
            <div class="feature-icon">👨‍🍳</div>
            <h4>Esperienza</h4>
            <p>Chef con anni di esperienza nel settore</p>
          </div>
          <div class="feature-item">
            <div class="feature-icon">🌿</div>
            <h4>Qualità</h4>
            <p>Ingredienti freschi e selezionati</p>
          </div>
          <div class="feature-item">
            <div class="feature-icon">❤️</div>
            <h4>Passione</h4>
            <p>Dedizione in ogni piatto servito</p>
          </div>
        </div>

        <!-- CTA Section -->
        <div class="cta-section">
          <div class="cta-ornament">⚜</div>
          <h3>Vieni a Trovarci</h3>
          <p>Scopri il gusto dell'autentica cucina mediterranea</p>
          <a href="#prenota" class="cta-button">Prenota un Tavolo</a>
        </div>
      </div>
    </section>
  </div>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Playfair+Display:wght@300;400;500;600;700&display=swap');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.about-page {
  background: #0a0a0a;
  min-height: 100vh;
  opacity: 0;
  transition: opacity 1s ease-out;
}

.about-page.visible {
  opacity: 1;
}

/* ==================== HERO SECTION ==================== */
.hero-about {
  position: relative;
  height: 60vh;
  min-height: 400px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(135deg, #0a0a0a 0%, #1a1a1a 100%);
  overflow: hidden;
}

.hero-about::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background:
    radial-gradient(circle at 30% 50%, rgba(212, 175, 55, 0.1) 0%, transparent 50%),
    radial-gradient(circle at 70% 50%, rgba(212, 175, 55, 0.1) 0%, transparent 50%);
  animation: heroGlow 8s ease-in-out infinite;
}

@keyframes heroGlow {
  0%,
  100% {
    opacity: 1;
  }
  50% {
    opacity: 0.6;
  }
}

.hero-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: repeating-linear-gradient(
    0deg,
    transparent,
    transparent 2px,
    rgba(212, 175, 55, 0.02) 2px,
    rgba(212, 175, 55, 0.02) 4px
  );
}

.hero-content {
  position: relative;
  z-index: 2;
  text-align: center;
  padding: 2rem;
  animation: heroSlideUp 1s ease-out;
}

@keyframes heroSlideUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.ornament {
  color: #d4af37;
  font-size: 2.5rem;
  margin-bottom: 1rem;
  opacity: 0;
  animation: fadeIn 1s ease-out 0.3s forwards;
}

@keyframes fadeIn {
  to {
    opacity: 1;
  }
}

.main-title {
  font-family: 'Playfair Display', Georgia, serif;
  font-size: clamp(3rem, 6vw, 5rem);
  font-weight: 400;
  color: #d4af37;
  margin-bottom: 1rem;
  letter-spacing: 3px;
  text-shadow: 0 0 40px rgba(212, 175, 55, 0.3);
  opacity: 0;
  animation: fadeIn 1s ease-out 0.5s forwards;
}

.title-divider {
  width: 120px;
  height: 2px;
  background: linear-gradient(90deg, transparent, #d4af37, transparent);
  margin: 1.5rem auto;
  opacity: 0;
  animation: expandLine 1s ease-out 0.7s forwards;
}

@keyframes expandLine {
  from {
    transform: scaleX(0);
  }
  to {
    opacity: 1;
    transform: scaleX(1);
  }
}

.subtitle {
  font-family: 'Playfair Display', Georgia, serif;
  font-size: clamp(1.2rem, 2vw, 1.5rem);
  color: rgba(224, 224, 224, 0.8);
  font-weight: 300;
  font-style: italic;
  letter-spacing: 2px;
  opacity: 0;
  animation: fadeIn 1s ease-out 0.9s forwards;
}

/* ==================== CONTENT SECTION ==================== */
.content-section {
  padding: 5rem 2rem;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
}

/* Intro Card */
.intro-card {
  text-align: center;
  padding: 4rem 3rem;
  background: linear-gradient(135deg, rgba(212, 175, 55, 0.05), rgba(218, 165, 32, 0.02));
  border: 1px solid rgba(212, 175, 55, 0.2);
  position: relative;
  margin-bottom: 5rem;
  opacity: 0;
  animation: fadeInUp 1s ease-out 1.1s forwards;
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.intro-card::before,
.intro-card::after {
  content: '';
  position: absolute;
  width: 80px;
  height: 80px;
  border: 2px solid #d4af37;
}

.intro-card::before {
  top: -1px;
  left: -1px;
  border-right: none;
  border-bottom: none;
}

.intro-card::after {
  bottom: -1px;
  right: -1px;
  border-left: none;
  border-top: none;
}

.card-ornament {
  color: #d4af37;
  font-size: 1.8rem;
  margin-bottom: 1.5rem;
}

.intro-card h2 {
  font-family: 'Playfair Display', Georgia, serif;
  font-size: clamp(2rem, 4vw, 3rem);
  color: #d4af37;
  font-weight: 400;
  margin-bottom: 1.5rem;
  letter-spacing: 2px;
}

.text-divider {
  width: 60px;
  height: 2px;
  background: #d4af37;
  margin: 1.5rem auto;
}

.lead-text {
  font-size: 1.2rem;
  line-height: 2;
  color: rgba(224, 224, 224, 0.8);
  font-weight: 300;
  max-width: 800px;
  margin: 0 auto;
}

/* Story Grid */
.story-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 3rem;
  margin-bottom: 5rem;
}

.story-block {
  background: rgba(212, 175, 55, 0.02);
  border: 1px solid rgba(212, 175, 55, 0.2);
  padding: 3rem;
  position: relative;
  transition: all 0.4s ease;
  opacity: 0;
}

.block-left {
  animation: fadeInLeft 1s ease-out 1.3s forwards;
}

.block-right {
  animation: fadeInRight 1s ease-out 1.5s forwards;
}

@keyframes fadeInLeft {
  from {
    opacity: 0;
    transform: translateX(-30px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

@keyframes fadeInRight {
  from {
    opacity: 0;
    transform: translateX(30px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

.story-block:hover {
  border-color: rgba(212, 175, 55, 0.4);
  transform: translateY(-5px);
}

.block-number {
  position: absolute;
  top: 1.5rem;
  right: 1.5rem;
  font-size: 3rem;
  color: rgba(212, 175, 55, 0.15);
  font-weight: 700;
  font-family: 'Playfair Display', Georgia, serif;
}

.story-block h3 {
  font-family: 'Playfair Display', Georgia, serif;
  font-size: 1.8rem;
  color: #d4af37;
  font-weight: 500;
  margin-bottom: 1rem;
  letter-spacing: 1px;
}

.block-divider {
  width: 40px;
  height: 2px;
  background: #d4af37;
  margin-bottom: 1.5rem;
}

.story-block p {
  color: rgba(224, 224, 224, 0.7);
  line-height: 1.9;
  margin-bottom: 1rem;
  font-size: 1rem;
  font-weight: 300;
}

.story-block p:last-child {
  margin-bottom: 0;
}

.story-block strong {
  color: #d4af37;
  font-weight: 500;
}

/* Mission Section */
.mission-section {
  margin-bottom: 5rem;
  opacity: 0;
  animation: fadeInUp 1s ease-out 1.7s forwards;
}

.mission-content {
  background: linear-gradient(135deg, rgba(10, 10, 10, 0.8), rgba(20, 20, 20, 0.6));
  border: 1px solid rgba(212, 175, 55, 0.3);
  padding: 4rem 3rem;
  text-align: center;
  position: relative;
}

.mission-content::before {
  content: '';
  position: absolute;
  top: 15px;
  left: 15px;
  right: 15px;
  bottom: 15px;
  border: 1px solid rgba(212, 175, 55, 0.1);
  pointer-events: none;
}

.mission-icon {
  font-size: 2.5rem;
  color: #d4af37;
  margin-bottom: 1.5rem;
}

.mission-content h3 {
  font-family: 'Playfair Display', Georgia, serif;
  font-size: 2.5rem;
  color: #d4af37;
  font-weight: 400;
  margin-bottom: 1.5rem;
  letter-spacing: 2px;
}

.mission-divider {
  width: 80px;
  height: 2px;
  background: linear-gradient(90deg, transparent, #d4af37, transparent);
  margin: 1.5rem auto;
}

.mission-text {
  font-size: 1.15rem;
  line-height: 2;
  color: rgba(224, 224, 224, 0.8);
  font-weight: 300;
  max-width: 900px;
  margin: 0 auto;
}

/* Features Section */
.features-section {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
  margin-bottom: 5rem;
}

.feature-item {
  text-align: center;
  padding: 2.5rem 1.5rem;
  border: 1px solid rgba(212, 175, 55, 0.1);
  transition: all 0.4s ease;
  opacity: 0;
  animation: fadeInUp 1s ease-out forwards;
}

.feature-item:nth-child(1) {
  animation-delay: 1.9s;
}
.feature-item:nth-child(2) {
  animation-delay: 2s;
}
.feature-item:nth-child(3) {
  animation-delay: 2.1s;
}
.feature-item:nth-child(4) {
  animation-delay: 2.2s;
}

.feature-item:hover {
  background: rgba(212, 175, 55, 0.03);
  border-color: rgba(212, 175, 55, 0.3);
  transform: translateY(-5px);
}

.feature-icon {
  font-size: 2.5rem;
  margin-bottom: 1rem;
}

.feature-item h4 {
  font-family: 'Playfair Display', Georgia, serif;
  font-size: 1.3rem;
  color: #d4af37;
  font-weight: 500;
  margin-bottom: 0.8rem;
  letter-spacing: 1px;
}

.feature-item p {
  color: rgba(224, 224, 224, 0.65);
  font-size: 0.95rem;
  line-height: 1.6;
  font-weight: 300;
}

/* CTA Section */
.cta-section {
  text-align: center;
  padding: 4rem 2rem;
  background: linear-gradient(135deg, rgba(212, 175, 55, 0.05), rgba(218, 165, 32, 0.02));
  border: 1px solid rgba(212, 175, 55, 0.2);
  opacity: 0;
  animation: fadeInUp 1s ease-out 2.3s forwards;
}

.cta-ornament {
  color: #d4af37;
  font-size: 2rem;
  margin-bottom: 1.5rem;
  opacity: 0.7;
}

.cta-section h3 {
  font-family: 'Playfair Display', Georgia, serif;
  font-size: 2.5rem;
  color: #d4af37;
  font-weight: 400;
  margin-bottom: 1rem;
  letter-spacing: 2px;
}

.cta-section p {
  color: rgba(224, 224, 224, 0.7);
  font-size: 1.1rem;
  margin-bottom: 2.5rem;
  font-weight: 300;
}

.cta-button {
  display: inline-block;
  background: linear-gradient(135deg, #d4af37, #c9a028);
  color: #0a0a0a;
  padding: 1rem 3rem;
  text-decoration: none;
  font-weight: 600;
  font-size: 1rem;
  letter-spacing: 1px;
  transition: all 0.3s ease;
  position: relative;
  overflow: hidden;
}

.cta-button::before {
  content: '';
  position: absolute;
  top: 50%;
  left: 50%;
  width: 0;
  height: 0;
  background: rgba(255, 255, 255, 0.2);
  border-radius: 50%;
  transform: translate(-50%, -50%);
  transition:
    width 0.5s ease,
    height 0.5s ease;
}

.cta-button:hover::before {
  width: 400px;
  height: 400px;
}

.cta-button:hover {
  transform: translateY(-3px);
  box-shadow: 0 8px 25px rgba(212, 175, 55, 0.4);
}

/* ==================== RESPONSIVE ==================== */
@media (max-width: 768px) {
  .content-section {
    padding: 3rem 1.5rem;
  }

  .intro-card {
    padding: 3rem 2rem;
    margin-bottom: 3rem;
  }

  .intro-card::before,
  .intro-card::after {
    width: 50px;
    height: 50px;
  }

  .story-grid {
    grid-template-columns: 1fr;
    gap: 2rem;
    margin-bottom: 3rem;
  }

  .story-block {
    padding: 2rem;
  }

  .mission-content {
    padding: 3rem 2rem;
  }

  .mission-section {
    margin-bottom: 3rem;
  }

  .features-section {
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 1.5rem;
    margin-bottom: 3rem;
  }

  .feature-item {
    padding: 2rem 1rem;
  }

  .cta-section {
    padding: 3rem 1.5rem;
  }
}

@media (max-width: 480px) {
  .hero-about {
    height: 50vh;
  }

  .intro-card h2 {
    font-size: 1.8rem;
  }

  .lead-text {
    font-size: 1rem;
  }

  .story-block h3 {
    font-size: 1.5rem;
  }

  .mission-content h3 {
    font-size: 2rem;
  }

  .mission-text {
    font-size: 1rem;
  }

  .features-section {
    grid-template-columns: 1fr;
  }
}
</style>
