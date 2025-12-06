<script setup>
import { onMounted, ref } from 'vue'
import { useI18n } from 'vue-i18n'

const { t } = useI18n()

const isVisible = ref(false)
const currentSlide = ref(0)
const currentHeaderImage = ref(0)
const showFloatingButton = ref(false)
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

// Logo image
const logoImage = new URL('/imageremove.png', import.meta.url).href

// Gestione scroll per il floating button
const handleScroll = () => {
  // Mostra il pulsante dopo 300px di scroll
  showFloatingButton.value = window.scrollY > 300
}

onMounted(() => {
  setTimeout(() => {
    isVisible.value = true
  }, 300)

  startAutoPlay()
  startHeaderImageSlide()

  // Aggiungi listener per lo scroll
  window.addEventListener('scroll', handleScroll)
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

        <!-- Logo Image invece del testo -->
        <div class="logo-container">
          <img :src="logoImage" alt="Il Pesce d'Oro" class="header-logo" />
        </div>

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

    <!-- Floating Menu Button - Solo Desktop -->
    <transition name="float-fade">
      <a
        v-if="showFloatingButton"
        href="/menu.pdf"
        download
        class="floating-menu-btn"
        :aria-label="t('nav.downloadMenu')"
      >
        <div class="floating-btn-content">
          <svg
            class="floating-btn-icon"
            width="24"
            height="24"
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="2.5"
            stroke-linecap="round"
            stroke-linejoin="round"
          >
            <path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4" />
            <polyline points="7 10 12 15 17 10" />
            <line x1="12" y1="15" x2="12" y2="3" />
          </svg>
          <span class="floating-btn-text">{{ t('nav.downloadMenu') }}</span>
        </div>

        <!-- Pulse ring effect -->
        <div class="floating-btn-ring"></div>
      </a>
    </transition>
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
  background: linear-gradient(135deg, #f8f6f2 0%, #ebe8e1 50%, #f8f6f2 100%);
  position: relative;
  overflow: hidden;
  opacity: 0;
  transition: opacity 1.2s ease-out;
}

.hero-section.visible {
  opacity: 1;
}

/* ==================== FLOATING MENU BUTTON - NUOVO STILE ==================== */
.floating-menu-btn {
  position: fixed;
  bottom: 40px;
  right: 40px;
  z-index: 999;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.98), rgba(248, 246, 242, 0.95));
  color: #8b6914;
  padding: 1.5rem;
  text-decoration: none;
  font-weight: 500;
  font-size: 0.85rem;
  letter-spacing: 1px;
  border-radius: 12px;
  box-shadow:
    0 10px 40px rgba(0, 0, 0, 0.15),
    0 0 0 1px rgba(212, 175, 55, 0.3) inset,
    0 0 0 2px rgba(255, 255, 255, 0.8);
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
  cursor: pointer;
  font-family: 'Lora', 'Georgia', serif;
  border: 2px solid rgba(212, 175, 55, 0.4);
  min-width: 80px;
  backdrop-filter: blur(10px);
}

.floating-btn-content {
  position: relative;
  z-index: 2;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.5rem;
}

.floating-btn-icon {
  color: #c9a028;
  filter: drop-shadow(0 2px 4px rgba(201, 160, 40, 0.2));
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
}

.floating-btn-text {
  font-weight: 500;
  /* text-transform: uppercase; */
  font-size: 0.75rem;
  color: #8b6914;
  text-align: center;
  line-height: 1.3;
  max-width: 70px;
}

/* Pulse ring effect - più sottile */
.floating-btn-ring {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 100%;
  height: 100%;
  border: 2px solid rgba(201, 160, 40, 0.4);
  border-radius: 12px;
  animation: pulse-ring-subtle 3s cubic-bezier(0.4, 0, 0.2, 1) infinite;
}

@keyframes pulse-ring-subtle {
  0% {
    width: 100%;
    height: 100%;
    opacity: 0.6;
  }
  50% {
    width: 110%;
    height: 110%;
    opacity: 0.3;
  }
  100% {
    width: 100%;
    height: 100%;
    opacity: 0.6;
  }
}

.floating-menu-btn::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(135deg, rgba(212, 175, 55, 0.08), rgba(201, 160, 40, 0.12));
  opacity: 0;
  transition: opacity 0.4s ease;
  border-radius: 12px;
}

.floating-menu-btn:hover::before {
  opacity: 1;
}

.floating-menu-btn:hover {
  transform: translateY(-8px);
  box-shadow:
    0 15px 50px rgba(0, 0, 0, 0.2),
    0 0 0 1px rgba(212, 175, 55, 0.5) inset,
    0 0 0 2px rgba(255, 255, 255, 0.9);
  border-color: rgba(212, 175, 55, 0.6);
}

.floating-menu-btn:hover .floating-btn-icon {
  transform: translateY(5px) scale(1.1);
  color: #e19b1d;
  filter: drop-shadow(0 4px 8px rgba(225, 155, 29, 0.4));
}

.floating-menu-btn:hover .floating-btn-text {
  color: #c9a028;
}

.floating-menu-btn:active {
  transform: translateY(-5px) scale(0.98);
  box-shadow:
    0 10px 35px rgba(0, 0, 0, 0.15),
    0 0 0 1px rgba(212, 175, 55, 0.4) inset,
    0 0 0 2px rgba(255, 255, 255, 0.8);
}

/* Decorazione angolare elegante */
.floating-menu-btn::after {
  content: '';
  position: absolute;
  top: 8px;
  left: 8px;
  right: 8px;
  bottom: 8px;
  border: 1px solid rgba(212, 175, 55, 0.15);
  border-radius: 8px;
  pointer-events: none;
  transition: all 0.4s ease;
}

.floating-menu-btn:hover::after {
  border-color: rgba(212, 175, 55, 0.3);
  top: 6px;
  left: 6px;
  right: 6px;
  bottom: 6px;
}

/* Transition for floating button */
.float-fade-enter-active,
.float-fade-leave-active {
  transition: all 0.5s cubic-bezier(0.4, 0, 0.2, 1);
}

.float-fade-enter-from {
  opacity: 0;
  transform: translateY(30px) scale(0.9);
}

.float-fade-leave-to {
  opacity: 0;
  transform: translateY(30px) scale(0.9);
}

/* Nascondi su mobile e tablet */
@media (max-width: 1024px) {
  .floating-menu-btn {
    display: none;
  }
}

/* Responsive per desktop piccoli */
@media (max-width: 1200px) and (min-width: 1025px) {
  .floating-menu-btn {
    bottom: 30px;
    right: 30px;
    padding: 1.2rem;
    min-width: 70px;
  }

  .floating-btn-text {
    font-size: 0.7rem;
    max-width: 60px;
  }

  .floating-btn-icon {
    width: 20px;
    height: 20px;
  }
}

/* Sfondo elegante con texture sottile */
.elegant-bg {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background:
    radial-gradient(circle at 20% 30%, rgba(212, 175, 55, 0.08) 0%, transparent 50%),
    radial-gradient(circle at 80% 70%, rgba(212, 175, 55, 0.08) 0%, transparent 50%),
    radial-gradient(circle at 50% 50%, rgba(218, 165, 32, 0.04) 0%, transparent 70%);
  opacity: 1;
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
    rgba(212, 175, 55, 0.02) 2px,
    rgba(212, 175, 55, 0.02) 4px
  );
}

/* Header */
.header-container {
  text-align: center;
  margin-bottom: 6rem;
  position: relative;
  z-index: 2;
  opacity: 0;
  transform: translateY(-30px);
  animation: headerSlide 1s ease-out 0.3s forwards;
  padding: 4rem 2rem;
  overflow: hidden;
  box-shadow:
    0 10px 40px rgba(0, 0, 0, 0.15),
    0 0 0 1px rgba(212, 175, 55, 0.1) inset;
  min-height: 600px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
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
    rgba(10, 10, 10, 0.65) 0%,
    rgba(26, 20, 16, 0.7) 50%,
    rgba(10, 10, 10, 0.65) 100%
  );
  backdrop-filter: blur(1px);
  box-shadow: inset 0 0 100px rgba(212, 175, 55, 0.15);
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

/* Logo Container */
.logo-container {
  position: relative;
  z-index: 1;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 2rem;
  opacity: 0;
  animation: logoFadeIn 1.5s ease-out 0.8s forwards;
}

.header-logo {
  max-width: 500px;
  width: 100%;
  height: auto;
  filter: drop-shadow(0 0 30px rgba(212, 175, 55, 0.6))
    drop-shadow(0 0 50px rgba(212, 175, 55, 0.4)) drop-shadow(0 4px 8px rgba(0, 0, 0, 0.8));
  transition: all 0.6s ease;
}

.header-logo:hover {
  filter: drop-shadow(0 0 40px rgba(212, 175, 55, 0.8))
    drop-shadow(0 0 60px rgba(212, 175, 55, 0.5)) drop-shadow(0 4px 12px rgba(0, 0, 0, 0.9));
  transform: scale(1.02);
}

@keyframes logoFadeIn {
  from {
    opacity: 0;
    transform: scale(0.95) translateY(20px);
  }
  to {
    opacity: 1;
    transform: scale(1) translateY(0);
  }
}

/* Content wrapper */
.content-wrapper {
  max-width: 1200px;
  margin: 0 auto;
  padding: 3rem 1.5rem;
  position: relative;
  z-index: 2;
}

/* ==================== SEZIONE PRINCIPALE - STORIA ==================== */
.hero-story-section {
  margin-bottom: 6rem;
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
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.95), rgba(248, 246, 242, 0.9));
  border: 2px solid rgba(212, 175, 55, 0.3);
  position: relative;
  text-align: center;
  box-shadow:
    0 10px 40px rgba(0, 0, 0, 0.1),
    0 0 0 1px rgba(212, 175, 55, 0.1) inset;
}

.story-border-tl,
.story-border-br {
  position: absolute;
  width: 90px;
  height: 90px;
  border: 2px solid #c9a028;
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
  color: #c9a028;
  font-size: 2rem;
  margin-bottom: 1.5rem;
  opacity: 1;
}

.story-title {
  color: #8b6914;
  font-size: clamp(2rem, 4vw, 3.2rem);
  font-weight: 400;
  font-family: 'Lora', 'Georgia', serif;
  margin-bottom: 1.5rem;
  letter-spacing: 2px;
}

.story-divider {
  width: 100px;
  height: 2px;
  background: linear-gradient(90deg, transparent, #c9a028, transparent);
  margin: 2rem auto;
}

.story-content {
  margin-bottom: 0;
}

.story-main-text {
  color: #2c2416;
  font-size: clamp(1.25rem, 2.5vw, 1.5rem);
  line-height: 2;
  font-weight: 300;
  margin-bottom: 2rem;
  font-family: 'Lora', 'Georgia', serif;
}

.story-main-text :deep(strong) {
  color: #8b6914;
  font-weight: 500;
  font-style: italic;
}

.story-secondary-text {
  color: #4a4032;
  font-size: clamp(1.1rem, 2vw, 1.25rem);
  line-height: 1.9;
  font-weight: 300;
  margin-bottom: 0;
}

/* ==================== JUMBOTRON ==================== */
.jumbotron-section {
  margin-bottom: 6rem;
  opacity: 0;
  transform: translateY(30px);
  animation: storySlide 1s ease-out 1.6s forwards;
}

.jumbotron-container {
  max-width: 1200px;
  margin: 0 auto;
  position: relative;
  padding: 2rem;
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.9), rgba(248, 246, 242, 0.85));
  border: 2px solid rgba(212, 175, 55, 0.3);
  box-shadow:
    0 10px 40px rgba(0, 0, 0, 0.08),
    0 0 0 1px rgba(212, 175, 55, 0.1) inset;
}

.jumbotron-border-tl,
.jumbotron-border-br {
  position: absolute;
  width: 90px;
  height: 90px;
  border: 2px solid #c9a028;
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
  border: 1px solid rgba(212, 175, 55, 0.3);
  box-shadow: 0 5px 20px rgba(0, 0, 0, 0.1);
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
    rgba(212, 175, 55, 0.1) 0%,
    rgba(0, 0, 0, 0.15) 50%,
    rgba(0, 0, 0, 0.4) 100%
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
  border: 2px solid rgba(212, 175, 55, 0.3);
  cursor: pointer;
  transition: all 0.4s ease;
  background: #000;
  padding: 0;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
}

.thumbnail:hover {
  border-color: #c9a028;
  transform: translateY(-5px);
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.15);
}

.thumbnail.active {
  border-color: #c9a028;
  box-shadow: 0 0 20px rgba(201, 160, 40, 0.4);
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
  background: rgba(0, 0, 0, 0.2);
  transition: background 0.4s ease;
  pointer-events: none;
}

.thumbnail:hover .thumbnail-overlay {
  background: rgba(212, 175, 55, 0.1);
}

.thumbnail.active .thumbnail-overlay {
  background: rgba(212, 175, 55, 0.2);
}

/* Cuisine section */
.cuisine-section {
  margin-bottom: 5rem;
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
  padding: 4rem 3rem;
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.95), rgba(248, 246, 242, 0.9));
  border: 2px solid rgba(212, 175, 55, 0.3);
  position: relative;
  box-shadow:
    0 10px 40px rgba(0, 0, 0, 0.08),
    0 0 0 1px rgba(212, 175, 55, 0.1) inset;
}

.cuisine-content::before {
  content: '';
  position: absolute;
  top: 15px;
  left: 15px;
  right: 15px;
  bottom: 15px;
  border: 1px solid rgba(212, 175, 55, 0.15);
  pointer-events: none;
}

.section-title {
  color: #8b6914;
  font-size: clamp(1.8rem, 3vw, 2.5rem);
  font-weight: 400;
  font-family: 'Lora', 'Georgia', serif;
  margin-bottom: 1rem;
}

.divider {
  width: 80px;
  height: 2px;
  background: linear-gradient(90deg, transparent, #c9a028, transparent);
  margin: 1.5rem auto;
}

.cuisine-text {
  color: #2c2416;
  font-size: 1.1rem;
  line-height: 1.9;
  font-weight: 300;
  margin-bottom: 2rem;
}

.specialty-badge {
  background: linear-gradient(135deg, #e19b1d, #c9a028);
  color: #ffffff;
  padding: 1.5rem 2rem;
  font-weight: 600;
  font-size: 1.05rem;
  line-height: 1.6;
  position: relative;
  border-radius: 2px;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 5px 20px rgba(201, 160, 40, 0.3);
}

.specialty-badge:hover {
  transform: translateY(-3px);
  box-shadow: 0 8px 30px rgba(201, 160, 40, 0.4);
}

/* Intro section */
.intro-section {
  margin-bottom: 5rem;
  opacity: 0;
  transform: translateY(30px);
  animation: contentSlide 1s ease-out 2s forwards;
}

.intro-content {
  text-align: center;
  margin: 0 auto;
  padding: 4rem 3rem;
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.9), rgba(248, 246, 242, 0.85));
  border: 2px solid rgba(212, 175, 55, 0.25);
  border-radius: 2px;
  position: relative;
  box-shadow:
    0 8px 30px rgba(0, 0, 0, 0.06),
    0 0 0 1px rgba(212, 175, 55, 0.08) inset;
}

.intro-content::before,
.intro-content::after {
  content: '';
  position: absolute;
  width: 60px;
  height: 60px;
  border: 2px solid #c9a028;
  opacity: 0.5;
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
  color: #2c2416;
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
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.85), rgba(248, 246, 242, 0.8));
  border: 2px solid rgba(212, 175, 55, 0.25);
  padding: 3rem 2.5rem;
  position: relative;
  transition: all 0.4s ease;
  opacity: 0;
  transform: translateY(30px);
  box-shadow:
    0 5px 20px rgba(0, 0, 0, 0.05),
    0 0 0 1px rgba(212, 175, 55, 0.08) inset;
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
  border-color: rgba(212, 175, 55, 0.5);
  transform: translateY(-5px);
  box-shadow:
    0 10px 30px rgba(0, 0, 0, 0.1),
    0 0 0 1px rgba(212, 175, 55, 0.15) inset;
}

.feature-box:hover::before {
  opacity: 1;
}

.box-icon {
  color: #c9a028;
  font-size: 1.5rem;
  margin-bottom: 1.5rem;
}

.feature-box h3 {
  color: #8b6914;
  font-size: 1.5rem;
  font-weight: 400;
  font-family: 'Lora', 'Georgia', serif;
  margin-bottom: 1rem;
}

.feature-box p {
  color: #4a4032;
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
  color: #8b6914;
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
  background: linear-gradient(90deg, transparent, #c9a028, transparent);
  opacity: 0;
  animation: ornamentFade 1s ease-out 2.6s forwards;
}

/* Responsive */
@media (max-width: 768px) {
  .header-container {
    margin-bottom: 1rem;
    padding: 3rem 1.5rem;
    min-height: 500px;
  }

  .header-logo {
    max-width: 450px;
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
    padding: 2.5rem 1.5rem;
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
    min-height: 400px;
  }

  .header-logo {
    max-width: 300px;
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
