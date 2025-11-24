<script setup>
import { onMounted, ref } from 'vue'
import { useI18n } from 'vue-i18n'

const { t } = useI18n()

const isVisible = ref(false)
const currentSlide = ref(0)
const totalSlides = 7
const isAutoPlaying = ref(true)
let autoPlayInterval = null

onMounted(() => {
  setTimeout(() => {
    isVisible.value = true
  }, 300)

  // Avvia autoplay
  startAutoPlay()
})

const startAutoPlay = () => {
  autoPlayInterval = setInterval(() => {
    if (isAutoPlaying.value) {
      nextSlide()
    }
  }, 4000) // Cambia slide ogni 4 secondi
}

const stopAutoPlay = () => {
  isAutoPlaying.value = false
  if (autoPlayInterval) {
    clearInterval(autoPlayInterval)
  }
}

const nextSlide = () => {
  currentSlide.value = (currentSlide.value + 1) % totalSlides
}

const prevSlide = () => {
  currentSlide.value = (currentSlide.value - 1 + totalSlides) % totalSlides
}

const handlePrevClick = () => {
  prevSlide()
  stopAutoPlay()
}

const handleNextClick = () => {
  nextSlide()
  stopAutoPlay()
}

const goToSlide = (index) => {
  currentSlide.value = index
  stopAutoPlay()
}
</script>

<template>
  <main>
    <section class="hero-section" :class="{ visible: isVisible }">
      <!-- Sfondo decorativo -->
      <div class="elegant-bg"></div>

      <!-- Header elegante -->
      <div class="header-container">
        <div class="ornament-top"></div>
        <h1 class="main-title">
          <span class="title-line">{{ t('home.mainTitle') }}</span>
          <span class="title-highlight">{{ t('home.restaurantName') }}</span>
          <span class="title-location">{{ t('home.location') }}</span>
        </h1>
        <div class="ornament-bottom"></div>
      </div>

      <!-- Contenuto principale -->
      <div class="content-wrapper">
        <!-- SEZIONE PRINCIPALE - Storia di Enzo e Debora -->
        <div class="hero-story-section">
          <div class="story-container">
            <div class="story-border-tl"></div>
            <div class="story-border-br"></div>

            <div class="story-ornament-top">◆</div>
            <h2 class="story-title">{{ t('home.storyTitle') }}</h2>
            <div class="story-divider"></div>

            <div class="story-content">
              <p class="story-main-text" v-html="t('home.storyMain')"></p>
              <p class="story-secondary-text">{{ t('home.storySecondary') }}</p>
            </div>
          </div>
        </div>

        <!-- JUMBOTRON FOTO -->
        <div class="jumbotron-section">
          <div class="jumbotron-container">
            <div class="jumbotron-border-tl"></div>
            <div class="jumbotron-border-br"></div>

            <!-- Immagine principale grande -->
            <div class="jumbotron-main">
              <img
                :src="`src/assets/${currentSlide + 1}.jpg`"
                :alt="`Il Pesce d'Oro - ${t('common.image')} ${currentSlide + 1}`"
                class="jumbotron-image"
              />
              <div class="jumbotron-overlay"></div>
            </div>

            <!-- Thumbnails sotto -->
            <div class="jumbotron-thumbnails">
              <button
                v-for="i in totalSlides"
                :key="i"
                class="thumbnail"
                :class="{ active: currentSlide === i - 1 }"
                @click="goToSlide(i - 1)"
                :aria-label="`${t('common.goToImage')} ${i}`"
              >
                <img
                  :src="`src/assets/${i}.jpg`"
                  :alt="`${t('common.thumbnail')} ${i}`"
                  class="thumbnail-image"
                />
                <div class="thumbnail-overlay"></div>
              </button>
            </div>
          </div>
        </div>

        <!-- Sezione cucina -->
        <div class="cuisine-section">
          <div class="cuisine-content">
            <h2 class="section-title">{{ t('home.cuisineTitle') }}</h2>
            <div class="divider"></div>
            <p class="cuisine-text">{{ t('home.cuisineText') }}</p>
            <div class="specialty-badge">{{ t('home.downloadMenu') }}</div>
          </div>
        </div>

        <!-- Sezione ospitalità -->
        <div class="intro-section">
          <div class="intro-content">
            <h2 class="section-title">{{ t('home.hospitalityTitle') }}</h2>
            <div class="divider"></div>
            <p class="intro-text">{{ t('home.hospitalityText') }}</p>
          </div>
        </div>

        <!-- Grid elegante -->
        <div class="features-grid">
          <!-- Eventi -->
          <div class="feature-box box-1">
            <div class="box-icon">◆</div>
            <h3>{{ t('home.eventsTitle') }}</h3>
            <p>{{ t('home.eventsText') }}</p>
            <div class="services-list">
              <span>{{ t('home.birthdays') }}</span>
              <span>{{ t('home.communions') }}</span>
              <span>{{ t('home.businessLunches') }}</span>
            </div>
          </div>

          <!-- Atmosfera -->
          <div class="feature-box box-2">
            <div class="box-icon">◆</div>
            <h3>{{ t('home.atmosphereTitle') }}</h3>
            <p>{{ t('home.atmosphereText') }}</p>
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
  margin-bottom: 0;
}

.story-main-text {
  color: #e0e0e0;
  font-size: clamp(1.25rem, 2.5vw, 1.5rem);
  line-height: 2;
  font-weight: 300;
  margin-bottom: 2rem;
  font-family: 'Playfair Display', 'Georgia', serif;
}

.story-main-text :deep(strong) {
  color: #d4af37;
  font-weight: 500;
  font-style: italic;
}

.story-secondary-text {
  color: rgba(224, 224, 224, 0.85);
  font-size: clamp(1.1rem, 2vw, 1.25rem);
  line-height: 1.9;
  font-weight: 300;
  margin-bottom: 0;
}

/* ==================== JUMBOTRON ==================== */
.jumbotron-section {
  margin-bottom: 5rem;
  opacity: 0;
  transform: translateY(30px);
  animation: storySlide 1s ease-out 1.6s forwards;
}

.jumbotron-container {
  max-width: 1200px;
  margin: 0 auto;
  position: relative;
  padding: 2rem;
  background: linear-gradient(135deg, rgba(212, 175, 55, 0.05), rgba(218, 165, 32, 0.02));
  border: 1px solid rgba(212, 175, 55, 0.3);
}

.jumbotron-border-tl,
.jumbotron-border-br {
  position: absolute;
  width: 90px;
  height: 90px;
  border: 2px solid #d4af37;
  opacity: 0.5;
  z-index: 2;
}

.jumbotron-border-tl {
  top: -1px;
  left: -1px;
  border-right: none;
  border-bottom: none;
}

.jumbotron-border-br {
  bottom: -1px;
  right: -1px;
  border-left: none;
  border-top: none;
}

.jumbotron-main {
  position: relative;
  width: 100%;
  height: 600px;
  overflow: hidden;
  margin-bottom: 2rem;
  background: #000;
}

.jumbotron-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
  transition: transform 0.6s ease;
}

.jumbotron-main:hover .jumbotron-image {
  transform: scale(1.05);
}

.jumbotron-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(
    to bottom,
    rgba(0, 0, 0, 0.4) 0%,
    rgba(0, 0, 0, 0.2) 50%,
    rgba(0, 0, 0, 0.6) 100%
  );
  pointer-events: none;
}

.jumbotron-content {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  padding: 3rem;
  text-align: center;
  z-index: 3;
}

.jumbotron-ornament {
  color: #d4af37;
  font-size: 2rem;
  margin-bottom: 1rem;
  opacity: 0.9;
  text-shadow: 0 2px 10px rgba(0, 0, 0, 0.5);
}

.jumbotron-title {
  color: #ffffff;
  font-size: clamp(2.5rem, 5vw, 4rem);
  font-weight: 400;
  font-family: 'Playfair Display', 'Georgia', serif;
  margin-bottom: 1rem;
  letter-spacing: 3px;
  text-shadow: 0 2px 20px rgba(0, 0, 0, 0.7);
}

.jumbotron-divider {
  width: 120px;
  height: 2px;
  background: linear-gradient(90deg, transparent, #d4af37, transparent);
  margin: 1.5rem auto;
}

.jumbotron-text {
  color: rgba(255, 255, 255, 0.9);
  font-size: clamp(1.1rem, 2vw, 1.4rem);
  font-weight: 300;
  letter-spacing: 1px;
  text-shadow: 0 2px 10px rgba(0, 0, 0, 0.5);
}

/* Thumbnails */
.jumbotron-thumbnails {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(140px, 1fr));
  gap: 1rem;
  padding: 0 1rem;
}

.thumbnail {
  position: relative;
  aspect-ratio: 16 / 10;
  overflow: hidden;
  border: 2px solid rgba(212, 175, 55, 0.3);
  cursor: pointer;
  transition: all 0.4s ease;
  background: #000;
  padding: 0;
}

.thumbnail:hover {
  border-color: #d4af37;
  transform: translateY(-5px);
  box-shadow: 0 8px 20px rgba(212, 175, 55, 0.3);
}

.thumbnail.active {
  border-color: #d4af37;
  box-shadow: 0 0 25px rgba(212, 175, 55, 0.5);
}

.thumbnail-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
  transition: transform 0.4s ease;
}

.thumbnail:hover .thumbnail-image {
  transform: scale(1.1);
}

.thumbnail-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.3);
  transition: background 0.4s ease;
  pointer-events: none;
}

.thumbnail:hover .thumbnail-overlay {
  background: rgba(0, 0, 0, 0.1);
}

.thumbnail.active .thumbnail-overlay {
  background: rgba(212, 175, 55, 0.2);
}

/* Responsive Jumbotron */
@media (max-width: 768px) {
  .jumbotron-container {
    padding: 1rem;
  }

  .jumbotron-border-tl,
  .jumbotron-border-br {
    width: 60px;
    height: 60px;
  }

  .jumbotron-main {
    height: 400px;
  }

  .jumbotron-content {
    padding: 2rem 1.5rem;
  }

  .jumbotron-thumbnails {
    grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
    gap: 0.75rem;
    padding: 0;
  }
}

@media (max-width: 480px) {
  .jumbotron-main {
    height: 300px;
  }

  .jumbotron-content {
    padding: 1.5rem 1rem;
  }

  .jumbotron-title {
    font-size: 2rem;
  }

  .jumbotron-thumbnails {
    grid-template-columns: repeat(auto-fit, minmax(80px, 1fr));
    gap: 0.5rem;
  }

  .jumbotron-border-tl,
  .jumbotron-border-br {
    width: 45px;
    height: 45px;
  }
}

/* Cuisine section */
.cuisine-section {
  margin-bottom: 4rem;
  opacity: 0;
  transform: translateY(30px);
  animation: contentSlide 1s ease-out 1.8s forwards;
}

@keyframes contentSlide {
  to {
    opacity: 1;
    transform: translateY(0);
  }
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
  font-weight: 600;
  font-size: 1.05rem;
  line-height: 1.6;
  position: relative;
  border-radius: 2px;
  cursor: pointer;
  transition: all 0.3s ease;
}

.specialty-badge:hover {
  transform: translateY(-3px);
  box-shadow: 0 8px 25px rgba(212, 175, 55, 0.4);
}

/* Intro section */
.intro-section {
  margin-bottom: 4rem;
  opacity: 0;
  transform: translateY(30px);
  animation: contentSlide 1s ease-out 2s forwards;
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
  animation: boxSlide 1s ease-out 2.2s forwards;
}

.box-2 {
  animation: boxSlide 1s ease-out 2.4s forwards;
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

/* Footer ornament */
.footer-ornament {
  position: absolute;
  bottom: 2rem;
  left: 50%;
  transform: translateX(-50%);
  width: 200px;
  z-index: 1;
}

.ornament-line {
  height: 1px;
  background: linear-gradient(90deg, transparent, #d4af37, transparent);
  opacity: 0;
  animation: ornamentFade 1s ease-out 2.6s forwards;
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

  .carousel-container {
    padding: 1rem;
  }

  .carousel-border-tl,
  .carousel-border-br {
    width: 50px;
    height: 50px;
  }

  .carousel-btn {
    width: 40px;
    height: 40px;
  }

  .carousel-btn span {
    font-size: 1.5rem;
  }

  .carousel-btn-prev {
    left: 0.5rem;
  }

  .carousel-btn-next {
    right: 0.5rem;
  }

  .carousel-indicators {
    bottom: 1rem;
    gap: 0.6rem;
  }

  .indicator {
    width: 10px;
    height: 10px;
  }

  .story-main-text {
    font-size: 1.15rem;
  }

  .story-secondary-text {
    font-size: 1.05rem;
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

  .carousel-wrapper {
    aspect-ratio: 4 / 3;
  }

  .story-main-text {
    font-size: 1.1rem;
    line-height: 1.8;
  }

  .story-secondary-text {
    font-size: 1rem;
  }
}
</style>
