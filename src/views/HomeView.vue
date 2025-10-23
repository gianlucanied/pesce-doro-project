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
  <main>
    <section class="hero-section" :class="{ visible: isVisible }">
      <!-- Sfondo decorativo -->
      <div class="elegant-bg"></div>

      <!-- Header elegante -->
      <div class="header-container">
        <div class="ornament-top">⚜</div>
        <h1 class="main-title">
          <span class="title-line">Ristorante Pizzeria</span>
          <span class="title-highlight">Il Pesce d'Oro</span>
          <span class="title-location">Alghero</span>
        </h1>
        <div class="ornament-bottom">⚜</div>
      </div>

      <!-- Contenuto principale -->
      <div class="content-wrapper">
        <!-- SEZIONE PRINCIPALE - Storia di Enzo e Debora -->
        <div class="hero-story-section">
          <div class="story-container">
            <div class="story-border-tl"></div>
            <div class="story-border-br"></div>

            <div class="story-ornament-top">◆</div>
            <h2 class="story-title">Un Grande Amore per il Mare</h2>
            <div class="story-divider"></div>

            <div class="story-content">
              <p class="story-main-text">
                Il Pesce d'Oro di <strong>Enzo e Debora</strong>, storia di un grande amore e
                ospitalità che si rinnova quotidianamente portando in tavola il meglio del nostro
                mare.
              </p>
              <p class="story-secondary-text">
                Location perfetta per le specialità ittiche preparate dallo chef Enzo e dai suoi
                collaboratori, veri e propri percorsi attraverso la Sardegna in cui la materia prima
                è la protagonista assoluta.
              </p>
            </div>

            <div class="story-signature">
              <div class="signature-line"></div>
              <span class="signature-text">Enzo & Debora</span>
              <div class="signature-line"></div>
            </div>
          </div>
        </div>

        <!-- Sezione ospitalità -->
        <div class="intro-section">
          <div class="intro-content">
            <h2 class="section-title">Ospitalità e Cortesia</h2>
            <div class="divider"></div>
            <p class="intro-text">
              Un ambiente confortevole per tutti dove potrete trovare ottime pizze, gustosissimi
              piatti del ristorante con pasta e dolci fatti in casa.
            </p>
          </div>
        </div>

        <!-- Grid elegante -->
        <div class="features-grid">
          <!-- Eventi -->
          <div class="feature-box box-1">
            <div class="box-icon">◆</div>
            <h3>Eventi & Cerimonie</h3>
            <p>
              Il locale è ideale anche per compagnie che vogliono festeggiare compleanni, addii al
              celibato, lauree. Puoi festeggiare un evento riservando il ristorante anche a pranzo.
            </p>
            <div class="services-list">
              <span>Compleanni</span>
              <span>Comunioni</span>
              <span>Pranzi di lavoro</span>
            </div>
          </div>

          <!-- Atmosfera -->
          <div class="feature-box box-2">
            <div class="box-icon">◆</div>
            <h3>Atmosfera Mediterranea</h3>
            <p>
              Al Ristorante Pesce d'oro trionfano i sapori mediterranei e l'atmosfera del locale è
              elegante, accogliente e piacevole.
            </p>
          </div>
        </div>

        <!-- Sezione cucina -->
        <div class="cuisine-section">
          <div class="cuisine-content">
            <h2 class="section-title">La Nostra Cucina</h2>
            <div class="divider"></div>
            <p class="cuisine-text">
              Proponiamo piatti molto legati alla tradizione locale con sapori tipicamente
              mediterranei e con una varietà di pietanze che variano: dagli sfiziosi antipasti di
              mare al pesce fresco, alla carne, alle gustosissime zuppe passando alla pizza cotta
              nel forno a legna.
            </p>
            <div class="specialty-badge">
              <span class="badge-icon">★</span>
              Tutto rigorosamente accompagnato da pane preparato quotidianamente nel nostro forno a
              legna
              <span class="badge-icon">★</span>
            </div>
          </div>
        </div>
      </div>

      <!-- Elemento decorativo footer -->
      <div class="footer-ornament">
        <div class="ornament-line"></div>
      </div>
    </section>
  </main>
</template>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.hero-section {
  min-height: 100vh;
  background: #0a0a0a;
  padding: 4rem 2rem;
  position: relative;
  overflow: hidden;
  opacity: 0;
  transition: opacity 1.2s ease-out;
}

.hero-section.visible {
  opacity: 1;
}

/* Sfondo elegante */
.elegant-bg {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background:
    radial-gradient(circle at 20% 30%, rgba(218, 165, 32, 0.05) 0%, transparent 50%),
    radial-gradient(circle at 80% 70%, rgba(218, 165, 32, 0.05) 0%, transparent 50%);
  opacity: 0;
  animation: bgFadeIn 2s ease-out 0.5s forwards;
}

@keyframes bgFadeIn {
  to {
    opacity: 1;
  }
}

.elegant-bg::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-image: repeating-linear-gradient(
    0deg,
    transparent,
    transparent 2px,
    rgba(218, 165, 32, 0.03) 2px,
    rgba(218, 165, 32, 0.03) 4px
  );
}

/* Header */
.header-container {
  text-align: center;
  margin-bottom: 5rem;
  position: relative;
  z-index: 2;
  opacity: 0;
  transform: translateY(-30px);
  animation: headerSlide 1s ease-out 0.3s forwards;
}

@keyframes headerSlide {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.ornament-top,
.ornament-bottom {
  color: #d4af37;
  font-size: 2rem;
  margin: 1rem 0;
  opacity: 0;
  animation: ornamentFade 1s ease-out forwards;
}

.ornament-top {
  animation-delay: 0.6s;
}

.ornament-bottom {
  animation-delay: 1.2s;
}

@keyframes ornamentFade {
  to {
    opacity: 1;
  }
}

.main-title {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  font-family: 'Playfair Display', 'Georgia', serif;
}

.title-line {
  color: #ffffff;
  font-size: clamp(1.5rem, 3vw, 2rem);
  font-weight: 400;
  letter-spacing: 4px;
  text-transform: uppercase;
  opacity: 0;
  animation: titleFadeIn 1s ease-out 0.8s forwards;
}

.title-highlight {
  color: #d4af37;
  font-size: clamp(2.5rem, 5vw, 4.5rem);
  font-weight: 700;
  letter-spacing: 2px;
  text-shadow: 0 0 40px rgba(212, 175, 55, 0.3);
  opacity: 0;
  animation: titleFadeIn 1s ease-out 1s forwards;
}

.title-location {
  color: #c0c0c0;
  font-size: clamp(1.2rem, 2vw, 1.5rem);
  font-weight: 300;
  letter-spacing: 6px;
  text-transform: uppercase;
  opacity: 0;
  animation: titleFadeIn 1s ease-out 1.2s forwards;
}

@keyframes titleFadeIn {
  to {
    opacity: 1;
  }
}

/* Content wrapper */
.content-wrapper {
  max-width: 1200px;
  margin: 0 auto;
  position: relative;
  z-index: 2;
}

/* ==================== SEZIONE PRINCIPALE - STORIA ==================== */
.hero-story-section {
  margin-bottom: 5rem;
  opacity: 0;
  transform: translateY(30px);
  animation: storySlide 1s ease-out 1.4s forwards;
}

@keyframes storySlide {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.story-container {
  max-width: 950px;
  margin: 0 auto;
  padding: 5rem 4rem;
  background: linear-gradient(135deg, rgba(212, 175, 55, 0.08), rgba(218, 165, 32, 0.03));
  border: 1px solid rgba(212, 175, 55, 0.3);
  position: relative;
  text-align: center;
}

.story-border-tl,
.story-border-br {
  position: absolute;
  width: 90px;
  height: 90px;
  border: 2px solid #d4af37;
  opacity: 0.6;
}

.story-border-tl {
  top: -1px;
  left: -1px;
  border-right: none;
  border-bottom: none;
}

.story-border-br {
  bottom: -1px;
  right: -1px;
  border-left: none;
  border-top: none;
}

.story-ornament-top {
  color: #d4af37;
  font-size: 2rem;
  margin-bottom: 1.5rem;
  opacity: 0.9;
}

.story-title {
  color: #d4af37;
  font-size: clamp(2rem, 4vw, 3.2rem);
  font-weight: 400;
  font-family: 'Playfair Display', 'Georgia', serif;
  margin-bottom: 1.5rem;
  letter-spacing: 2px;
}

.story-divider {
  width: 100px;
  height: 2px;
  background: linear-gradient(90deg, transparent, #d4af37, transparent);
  margin: 2rem auto;
}

.story-content {
  margin-bottom: 3rem;
}

.story-main-text {
  color: #e0e0e0;
  font-size: clamp(1.25rem, 2.5vw, 1.5rem);
  line-height: 2;
  font-weight: 300;
  margin-bottom: 2rem;
  font-family: 'Playfair Display', 'Georgia', serif;
}

.story-main-text strong {
  color: #d4af37;
  font-weight: 500;
  font-style: italic;
}

.story-secondary-text {
  color: rgba(224, 224, 224, 0.85);
  font-size: clamp(1.1rem, 2vw, 1.25rem);
  line-height: 1.9;
  font-weight: 300;
}

.story-signature {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1.5rem;
  padding-top: 2.5rem;
  border-top: 1px solid rgba(212, 175, 55, 0.2);
}

.signature-line {
  flex: 1;
  max-width: 100px;
  height: 1px;
  background: linear-gradient(90deg, transparent, #d4af37);
}

.signature-line:last-child {
  background: linear-gradient(90deg, #d4af37, transparent);
}

.signature-text {
  color: #d4af37;
  font-size: 1.3rem;
  font-weight: 400;
  font-family: 'Playfair Display', 'Georgia', serif;
  font-style: italic;
  letter-spacing: 2px;
}

/* Intro section */
.intro-section {
  margin-bottom: 4rem;
  opacity: 0;
  transform: translateY(30px);
  animation: contentSlide 1s ease-out 1.6s forwards;
}

@keyframes contentSlide {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.intro-content {
  text-align: center;
  max-width: 800px;
  margin: 0 auto;
  padding: 3rem;
  background: linear-gradient(135deg, rgba(212, 175, 55, 0.05), rgba(218, 165, 32, 0.02));
  border: 1px solid rgba(212, 175, 55, 0.2);
  border-radius: 2px;
  position: relative;
}

.intro-content::before,
.intro-content::after {
  content: '';
  position: absolute;
  width: 60px;
  height: 60px;
  border: 2px solid #d4af37;
}

.intro-content::before {
  top: -1px;
  left: -1px;
  border-right: none;
  border-bottom: none;
}

.intro-content::after {
  bottom: -1px;
  right: -1px;
  border-left: none;
  border-top: none;
}

.section-title {
  color: #d4af37;
  font-size: clamp(1.8rem, 3vw, 2.5rem);
  font-weight: 400;
  font-family: 'Playfair Display', 'Georgia', serif;
  margin-bottom: 1rem;
}

.divider {
  width: 80px;
  height: 2px;
  background: linear-gradient(90deg, transparent, #d4af37, transparent);
  margin: 1.5rem auto;
}

.intro-text {
  color: #e0e0e0;
  font-size: 1.1rem;
  line-height: 1.8;
  font-weight: 300;
}

/* Features grid */
.features-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 2rem;
  margin-bottom: 4rem;
}

.feature-box {
  background: rgba(212, 175, 55, 0.02);
  border: 1px solid rgba(212, 175, 55, 0.2);
  padding: 2.5rem;
  position: relative;
  transition: all 0.4s ease;
  opacity: 0;
  transform: translateY(30px);
}

.box-1 {
  animation: boxSlide 1s ease-out 1.8s forwards;
}

.box-2 {
  animation: boxSlide 1s ease-out 2s forwards;
}

@keyframes boxSlide {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.feature-box::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(135deg, rgba(212, 175, 55, 0.05), transparent);
  opacity: 0;
  transition: opacity 0.4s ease;
}

.feature-box:hover {
  border-color: rgba(212, 175, 55, 0.4);
  transform: translateY(-5px);
}

.feature-box:hover::before {
  opacity: 1;
}

.box-icon {
  color: #d4af37;
  font-size: 1.5rem;
  margin-bottom: 1.5rem;
}

.feature-box h3 {
  color: #d4af37;
  font-size: 1.5rem;
  font-weight: 400;
  font-family: 'Playfair Display', 'Georgia', serif;
  margin-bottom: 1rem;
}

.feature-box p {
  color: #c0c0c0;
  line-height: 1.8;
  font-weight: 300;
  margin-bottom: 1.5rem;
}

.services-list {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
  padding-top: 1rem;
  border-top: 1px solid rgba(212, 175, 55, 0.2);
}

.services-list span {
  color: #d4af37;
  font-size: 0.9rem;
  font-weight: 300;
  letter-spacing: 1px;
}

/* Cuisine section */
.cuisine-section {
  opacity: 0;
  transform: translateY(30px);
  animation: contentSlide 1s ease-out 2.2s forwards;
}

.cuisine-content {
  text-align: center;
  max-width: 900px;
  margin: 0 auto;
  padding: 3rem;
  background: linear-gradient(135deg, rgba(10, 10, 10, 0.8), rgba(20, 20, 20, 0.6));
  border: 1px solid rgba(212, 175, 55, 0.3);
  position: relative;
}

.cuisine-content::before {
  content: '';
  position: absolute;
  top: 15px;
  left: 15px;
  right: 15px;
  bottom: 15px;
  border: 1px solid rgba(212, 175, 55, 0.1);
  pointer-events: none;
}

.cuisine-text {
  color: #e0e0e0;
  font-size: 1.1rem;
  line-height: 1.9;
  font-weight: 300;
  margin-bottom: 2rem;
}

.specialty-badge {
  background: linear-gradient(135deg, #d4af37, #c9a028);
  color: #0a0a0a;
  padding: 1.5rem 2rem;
  font-weight: 500;
  font-size: 1rem;
  line-height: 1.6;
  position: relative;
  border-radius: 2px;
}

.badge-icon {
  color: #0a0a0a;
  font-size: 1.2rem;
  margin: 0 0.5rem;
}

/* Footer ornament */
.footer-ornament {
  position: absolute;
  bottom: 2rem;
  left: 50%;
  transform: translateX(-50%);
  width: 200px;
}

.ornament-line {
  height: 1px;
  background: linear-gradient(90deg, transparent, #d4af37, transparent);
  opacity: 0;
  animation: ornamentFade 1s ease-out 2.4s forwards;
}

/* Responsive */
@media (max-width: 768px) {
  .hero-section {
    padding: 2rem 1rem;
  }

  .header-container {
    margin-bottom: 3rem;
  }

  .story-container {
    padding: 3rem 2rem;
  }

  .story-border-tl,
  .story-border-br {
    width: 60px;
    height: 60px;
  }

  .story-main-text {
    font-size: 1.15rem;
  }

  .story-secondary-text {
    font-size: 1.05rem;
  }

  .signature-line {
    max-width: 60px;
  }

  .intro-content,
  .cuisine-content {
    padding: 2rem 1.5rem;
  }

  .intro-content::before,
  .intro-content::after {
    width: 40px;
    height: 40px;
  }

  .features-grid {
    grid-template-columns: 1fr;
    gap: 1.5rem;
  }

  .feature-box {
    padding: 2rem;
  }

  .services-list {
    flex-direction: column;
    gap: 0.5rem;
  }
}

@media (max-width: 480px) {
  .story-container {
    padding: 2.5rem 1.5rem;
  }

  .story-border-tl,
  .story-border-br {
    width: 45px;
    height: 45px;
  }

  .story-main-text {
    font-size: 1.1rem;
    line-height: 1.8;
  }

  .story-secondary-text {
    font-size: 1rem;
  }

  .signature-text {
    font-size: 1.1rem;
  }
}
</style>
