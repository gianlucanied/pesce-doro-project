<script setup>
import { onMounted, ref } from 'vue'
import { useI18n } from 'vue-i18n'

const { t } = useI18n()

const isVisible = ref(false)
const currentSlide = ref(0)
const currentHeaderImage = ref(0)
const totalSlides = 7
const isAutoPlaying = ref(true)
let autoPlayInterval = null
let headerImageInterval = null

// Array di immagini per l'header
const headerImages = [
  new URL('@/assets/1.jpg', import.meta.url).href,
  new URL('@/assets/2.jpg', import.meta.url).href,
  new URL('@/assets/3.jpg', import.meta.url).href,
  new URL('@/assets/4.jpg', import.meta.url).href,
  new URL('@/assets/5.jpg', import.meta.url).href,
  new URL('@/assets/6.jpg', import.meta.url).href,
  new URL('@/assets/7.jpg', import.meta.url).href,
]

// Array di immagini per il jumbotron (stesso array)
const jumbotronImages = [
  new URL('@/assets/1.jpg', import.meta.url).href,
  new URL('@/assets/2.jpg', import.meta.url).href,
  new URL('@/assets/3.jpg', import.meta.url).href,
  new URL('@/assets/4.jpg', import.meta.url).href,
  new URL('@/assets/5.jpg', import.meta.url).href,
  new URL('@/assets/6.jpg', import.meta.url).href,
  new URL('@/assets/7.jpg', import.meta.url).href,
]

onMounted(() => {
  setTimeout(() => {
    isVisible.value = true
  }, 300)

  startAutoPlay()
  startHeaderImageSlide()
})

const startAutoPlay = () => {
  autoPlayInterval = setInterval(() => {
    if (isAutoPlaying.value) {
      nextSlide()
    }
  }, 4000)
}

const startHeaderImageSlide = () => {
  headerImageInterval = setInterval(() => {
    currentHeaderImage.value = (currentHeaderImage.value + 1) % headerImages.length
  }, 5000)
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
        <!-- Background con immagini scorrevoli -->
        <div class="header-background">
          <transition name="header-fade" mode="out-in">
            <div
              :key="currentHeaderImage"
              class="header-bg-image"
              :style="{ backgroundImage: `url(${headerImages[currentHeaderImage]})` }"
            ></div>
          </transition>
          <div class="header-bg-overlay"></div>
        </div>

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
                :src="jumbotronImages[currentSlide]"
                :alt="`Il Pesce d'Oro - ${t('common.image')} ${currentSlide + 1}`"
                class="jumbotron-image"
              />
              <div class="jumbotron-overlay"></div>
            </div>

            <!-- Thumbnails sotto -->
            <div class="jumbotron-thumbnails">
              <button
                v-for="(image, index) in jumbotronImages"
                :key="index"
                class="thumbnail"
                :class="{ active: currentSlide === index }"
                @click="goToSlide(index)"
                :aria-label="`${t('common.goToImage')} ${index + 1}`"
              >
                <img
                  :src="image"
                  :alt="`${t('common.thumbnail')} ${index + 1}`"
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
  background: linear-gradient(135deg, #0a0a0a 0%, #1a1410 50%, #0a0a0a 100%);
  position: relative;
  overflow: hidden;
  opacity: 0;
  transition: opacity 1.2s ease-out;
}

.hero-section.visible {
  opacity: 1;
}

/* Sfondo elegante con più oro */
.elegant-bg {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background:
    radial-gradient(circle at 20% 30%, rgba(218, 165, 32, 0.12) 0%, transparent 50%),
    radial-gradient(circle at 80% 70%, rgba(218, 165, 32, 0.12) 0%, transparent 50%),
    radial-gradient(circle at 50% 50%, rgba(212, 175, 55, 0.08) 0%, transparent 70%);
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
    rgba(218, 165, 32, 0.05) 2px,
    rgba(218, 165, 32, 0.05) 4px
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
  padding: 4rem 2rem;
  border-radius: 4px;
  overflow: hidden;
  border: 2px solid rgba(212, 175, 55, 0.4);
  box-shadow: 0 10px 40px rgba(212, 175, 55, 0.25);
  min-height: 600px;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

/* Background con immagini scorrevoli */
.header-background {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 0;
}

.header-bg-image {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
}

.header-bg-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(
    135deg,
    rgba(10, 10, 10, 0.5) 0%,
    rgba(26, 20, 16, 0.6) 50%,
    rgba(10, 10, 10, 0.5) 100%
  );
  backdrop-filter: blur(1px);
  box-shadow: inset 0 0 100px rgba(212, 175, 55, 0.1);
}

/* Transizione fade per le immagini header */
.header-fade-enter-active,
.header-fade-leave-active {
  transition: opacity 2s ease;
}

.header-fade-enter-from {
  opacity: 0;
}

.header-fade-leave-to {
  opacity: 0;
}

@keyframes headerSlide {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.ornament-top,
.ornament-bottom {
  color: #e19b1d;
  font-size: 2.5rem;
  margin: 1rem 0;
  opacity: 0;
  animation: ornamentFade 1s ease-out forwards;
  text-shadow:
    0 0 20px rgba(212, 175, 55, 0.8),
    0 0 40px rgba(212, 175, 55, 0.5),
    0 2px 4px rgba(0, 0, 0, 0.8);
  position: relative;
  z-index: 1;
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
  position: relative;
  z-index: 1;
}

.title-line {
  color: #ffffff;
  font-size: clamp(1.5rem, 3vw, 2rem);
  font-weight: 400;
  letter-spacing: 4px;
  text-transform: uppercase;
  opacity: 0;
  animation: titleFadeIn 1s ease-out 0.8s forwards;
  text-shadow:
    0 2px 4px rgba(0, 0, 0, 0.8),
    0 0 20px rgba(212, 175, 55, 0.3);
}

.title-highlight {
  color: #e19b1d;
  font-size: clamp(2.5rem, 5vw, 4.5rem);
  font-weight: 700;
  letter-spacing: 2px;
  text-shadow:
    0 0 40px rgba(212, 175, 55, 0.8),
    0 0 60px rgba(212, 175, 55, 0.5),
    0 4px 8px rgba(0, 0, 0, 0.9);
  opacity: 0;
  animation: titleFadeIn 1s ease-out 1s forwards;
}

.title-location {
  color: #ffd700;
  font-size: clamp(1.2rem, 2vw, 1.5rem);
  font-weight: 300;
  letter-spacing: 6px;
  text-transform: uppercase;
  opacity: 0;
  animation: titleFadeIn 1s ease-out 1.2s forwards;
  text-shadow:
    0 2px 4px rgba(0, 0, 0, 0.8),
    0 0 20px rgba(212, 175, 55, 0.4);
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
  background: linear-gradient(135deg, rgba(212, 175, 55, 0.15), rgba(218, 165, 32, 0.08));
  border: 2px solid rgba(212, 175, 55, 0.4);
  position: relative;
  text-align: center;
  box-shadow: 0 10px 40px rgba(212, 175, 55, 0.15);
}

.story-border-tl,
.story-border-br {
  position: absolute;
  width: 90px;
  height: 90px;
  border: 2px solid #e19b1d;
  opacity: 0.8;
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
  color: #e19b1d;
  font-size: 2rem;
  margin-bottom: 1.5rem;
  opacity: 1;
  text-shadow: 0 0 15px rgba(212, 175, 55, 0.6);
}

.story-title {
  color: #e19b1d;
  font-size: clamp(2rem, 4vw, 3.2rem);
  font-weight: 400;
  font-family: 'Playfair Display', 'Georgia', serif;
  margin-bottom: 1.5rem;
  letter-spacing: 2px;
  text-shadow: 0 0 20px rgba(212, 175, 55, 0.3);
}

.story-divider {
  width: 100px;
  height: 2px;
  background: linear-gradient(90deg, transparent, #e19b1d, transparent);
  margin: 2rem auto;
  box-shadow: 0 0 10px rgba(212, 175, 55, 0.5);
}

.story-content {
  margin-bottom: 0;
}

.story-main-text {
  color: #f0f0f0;
  font-size: clamp(1.25rem, 2.5vw, 1.5rem);
  line-height: 2;
  font-weight: 300;
  margin-bottom: 2rem;
  font-family: 'Playfair Display', 'Georgia', serif;
}

.story-main-text :deep(strong) {
  color: #e19b1d;
  font-weight: 500;
  font-style: italic;
  text-shadow: 0 0 10px rgba(212, 175, 55, 0.3);
}

.story-secondary-text {
  color: rgba(240, 240, 240, 0.9);
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
  background: linear-gradient(135deg, rgba(212, 175, 55, 0.1), rgba(218, 165, 32, 0.05));
  border: 2px solid rgba(212, 175, 55, 0.4);
  box-shadow: 0 10px 40px rgba(212, 175, 55, 0.15);
}

.jumbotron-border-tl,
.jumbotron-border-br {
  position: absolute;
  width: 90px;
  height: 90px;
  border: 2px solid #e19b1d;
  opacity: 0.7;
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
  border: 1px solid rgba(212, 175, 55, 0.3);
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
    rgba(212, 175, 55, 0.15) 0%,
    rgba(0, 0, 0, 0.2) 50%,
    rgba(0, 0, 0, 0.6) 100%
  );
  pointer-events: none;
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
  border: 2px solid rgba(212, 175, 55, 0.4);
  cursor: pointer;
  transition: all 0.4s ease;
  background: #000;
  padding: 0;
}

.thumbnail:hover {
  border-color: #e19b1d;
  transform: translateY(-5px);
  box-shadow: 0 8px 20px rgba(212, 175, 55, 0.4);
}

.thumbnail.active {
  border-color: #e19b1d;
  box-shadow: 0 0 30px rgba(212, 175, 55, 0.6);
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
  background: rgba(212, 175, 55, 0.1);
}

.thumbnail.active .thumbnail-overlay {
  background: rgba(212, 175, 55, 0.3);
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
  background: linear-gradient(135deg, rgba(212, 175, 55, 0.12), rgba(218, 165, 32, 0.06));
  border: 2px solid rgba(212, 175, 55, 0.4);
  position: relative;
  box-shadow: 0 10px 40px rgba(212, 175, 55, 0.15);
}

.cuisine-content::before {
  content: '';
  position: absolute;
  top: 15px;
  left: 15px;
  right: 15px;
  bottom: 15px;
  border: 1px solid rgba(212, 175, 55, 0.2);
  pointer-events: none;
}

.section-title {
  color: #e19b1d;
  font-size: clamp(1.8rem, 3vw, 2.5rem);
  font-weight: 400;
  font-family: 'Playfair Display', 'Georgia', serif;
  margin-bottom: 1rem;
  text-shadow: 0 0 15px rgba(212, 175, 55, 0.3);
}

.divider {
  width: 80px;
  height: 2px;
  background: linear-gradient(90deg, transparent, #e19b1d, transparent);
  margin: 1.5rem auto;
  box-shadow: 0 0 10px rgba(212, 175, 55, 0.5);
}

.cuisine-text {
  color: #f0f0f0;
  font-size: 1.1rem;
  line-height: 1.9;
  font-weight: 300;
  margin-bottom: 2rem;
}

.specialty-badge {
  background: linear-gradient(135deg, #e19b1d, #c9a028);
  color: #0a0a0a;
  padding: 1.5rem 2rem;
  font-weight: 600;
  font-size: 1.05rem;
  line-height: 1.6;
  position: relative;
  border-radius: 2px;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 5px 20px rgba(212, 175, 55, 0.3);
}

.specialty-badge:hover {
  transform: translateY(-3px);
  box-shadow: 0 8px 30px rgba(212, 175, 55, 0.5);
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
  background: linear-gradient(135deg, rgba(212, 175, 55, 0.1), rgba(218, 165, 32, 0.05));
  border: 2px solid rgba(212, 175, 55, 0.3);
  border-radius: 2px;
  position: relative;
  box-shadow: 0 8px 30px rgba(212, 175, 55, 0.12);
}

.intro-content::before,
.intro-content::after {
  content: '';
  position: absolute;
  width: 60px;
  height: 60px;
  border: 2px solid #e19b1d;
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
  color: #f0f0f0;
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
  background: linear-gradient(135deg, rgba(212, 175, 55, 0.08), rgba(218, 165, 32, 0.04));
  border: 2px solid rgba(212, 175, 55, 0.3);
  padding: 2.5rem;
  position: relative;
  transition: all 0.4s ease;
  opacity: 0;
  transform: translateY(30px);
  box-shadow: 0 5px 20px rgba(212, 175, 55, 0.1);
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
  background: linear-gradient(135deg, rgba(212, 175, 55, 0.1), transparent);
  opacity: 0;
  transition: opacity 0.4s ease;
}

.feature-box:hover {
  border-color: rgba(212, 175, 55, 0.6);
  transform: translateY(-5px);
  box-shadow: 0 10px 30px rgba(212, 175, 55, 0.25);
}

.feature-box:hover::before {
  opacity: 1;
}

.box-icon {
  color: #e19b1d;
  font-size: 1.5rem;
  margin-bottom: 1.5rem;
  text-shadow: 0 0 10px rgba(212, 175, 55, 0.5);
}

.feature-box h3 {
  color: #e19b1d;
  font-size: 1.5rem;
  font-weight: 400;
  font-family: 'Playfair Display', 'Georgia', serif;
  margin-bottom: 1rem;
  text-shadow: 0 0 10px rgba(212, 175, 55, 0.2);
}

.feature-box p {
  color: #e0e0e0;
  line-height: 1.8;
  font-weight: 300;
  margin-bottom: 1.5rem;
}

.services-list {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
  padding-top: 1rem;
  border-top: 1px solid rgba(212, 175, 55, 0.3);
}

.services-list span {
  color: #e19b1d;
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
  background: linear-gradient(90deg, transparent, #e19b1d, transparent);
  opacity: 0;
  animation: ornamentFade 1s ease-out 2.6s forwards;
  box-shadow: 0 0 10px rgba(212, 175, 55, 0.5);
}

/* Responsive */
@media (max-width: 768px) {
  .hero-section.visible {
    padding: 2rem 1.5rem;
  }
  .header-container {
    margin-bottom: 3rem;
    padding: 3rem 1.5rem;
    min-height: 80vh;
  }

  .story-container {
    padding: 3rem 2rem;
  }

  .story-border-tl,
  .story-border-br {
    width: 60px;
    height: 60px;
  }

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

  .jumbotron-thumbnails {
    grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
    gap: 0.75rem;
    padding: 0;
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
  .header-container {
    padding: 2.5rem 1rem;
    border: 0;
  }

  .story-container {
    padding: 2.5rem 1.5rem;
  }

  .story-border-tl,
  .story-border-br {
    width: 45px;
    height: 45px;
  }

  .jumbotron-main {
    height: 300px;
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

  .story-main-text {
    font-size: 1.1rem;
    line-height: 1.8;
  }

  .story-secondary-text {
    font-size: 1rem;
  }
}
</style>
