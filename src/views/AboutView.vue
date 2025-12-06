<script setup>
import { onMounted, ref } from 'vue'
import { useI18n } from 'vue-i18n'

const { t } = useI18n()

const isVisible = ref(false)
const currentReviewIndex = ref(0)
const slideDirection = ref('slide-left')
const currentHeroImage = ref(0)
const isHoveringReview = ref(false)

const heroImages = [
  new URL('@/assets/8.jpg', import.meta.url).href,
  new URL('@/assets/9.jpg', import.meta.url).href,
  new URL('@/assets/10.jpg', import.meta.url).href,
  new URL('@/assets/11.jpg', import.meta.url).href,
  new URL('@/assets/12.jpg', import.meta.url).href,
  new URL('@/assets/13.jpg', import.meta.url).href,
  new URL('@/assets/14.jpg', import.meta.url).href,
]

const reviews = ref([
  {
    text: "L'antipasto della casa è pazzesco: si compone di 10 piccoli assaggi, un connubio di sapori. Come primo abbiamo mangiato spaghetti con vongole perfettamente al dente con vongole grandissime. Il branzino al sale, cotto divinamente e servito magistralmente. Ottimo rapporto qualità/prezzo!",
    author: 'Marco T.',
    rating: 5,
  },
  {
    text: "Ogni estate vado ad Alghero e non posso farmi mancare una cena al Ristorante Pesce d'Oro. Qualità ottima, servizio ottimo, tavolini all'aperto e prezzo giusto. Una garanzia che rinnovo ogni anno!",
    author: 'Giulia S.',
    rating: 5,
  },
  {
    text: 'Siamo stati in tre persone più la nostra barboncina e siamo rimasti entusiasti! Il pesce è freschissimo, cucinato in maniera sublime e servito con grande cura. Ogni piatto ci ha davvero conquistati per qualità e sapore.',
    author: 'Andrea P.',
    rating: 5,
  },
  {
    text: "Una cena a base di pesce eccezionale: una zuppetta di frutti di mare buonissima e abbondante, un'orata fresca da 750gr sotto sale cotta alla perfezione, gamberoni al mirto gustosissimi. Un prezzo che abbiamo pagato con vero piacere. Lo consiglio vivamente!",
    author: 'Roberto L.',
    rating: 5,
  },
  {
    text: 'Il talento dello chef lascia soddisfatti i palati. Abbiamo ordinato un antipasto misto di pesce con sei portate diverse ed un gusto veramente squisito. Il filetto di branzino allo zafferano e la pasta al ragù di polpo e mirto sono stati apprezzatissimi!',
    author: 'Francesca M.',
    rating: 5,
  },
  {
    text: "Superbo ristorante di pesce a prezzi ragionevoli e gestito molto professionalmente. L'antipasto consigliato dagli chef con 6 assaggiatori e il tonno con salse di frutti di bossi e barbabietole è stato fantastico. Piatti creativi altamente consigliati!",
    author: 'Thomas K.',
    rating: 5,
  },
  {
    text: 'Questo ristorante ci è stato consigliato da un residente di Alghero. Locale ben arredato e curato, cibo freschissimo e ben cucinato. Ottima la tartare di tonno e la fregola ai frutti di mare. Durante questa vacanza ci siamo stati per 3 volte!',
    author: 'Laura B.',
    rating: 5,
  },
  {
    text: 'La gestione di questo ristorante è vincente: cibo ottimo, ambiente semplice e accogliente, staff cordiale e professionale. Un posto dove torno sempre volentieri! Frequentato quasi esclusivamente dai locals.',
    author: 'Alessandro V.',
    rating: 5,
  },
])

let heroSlideInterval = null

const nextReview = () => {
  slideDirection.value = 'slide-left'
  currentReviewIndex.value = (currentReviewIndex.value + 1) % reviews.value.length
}

const prevReview = () => {
  slideDirection.value = 'slide-right'
  currentReviewIndex.value =
    currentReviewIndex.value === 0 ? reviews.value.length - 1 : currentReviewIndex.value - 1
}

const goToReview = (index) => {
  slideDirection.value = index > currentReviewIndex.value ? 'slide-left' : 'slide-right'
  currentReviewIndex.value = index
}

const startHeroSlide = () => {
  heroSlideInterval = setInterval(() => {
    currentHeroImage.value = (currentHeroImage.value + 1) % heroImages.length
  }, 2000)
}

onMounted(() => {
  setTimeout(() => {
    isVisible.value = true
  }, 150)
  startHeroSlide()
})
</script>

<template>
  <div class="about-page" :class="{ visible: isVisible }">
    <!-- Hero Section with Image Carousel -->
    <section class="hero-about">
      <div class="hero-images-container">
        <transition name="hero-fade" mode="out-in">
          <div
            :key="currentHeroImage"
            class="hero-image"
            :style="{ backgroundImage: `url(${heroImages[currentHeroImage]})` }"
          ></div>
        </transition>
      </div>
      <div class="hero-overlay"></div>
      <div class="hero-content">
        <div class="ornament"></div>
        <h1 class="main-title">{{ t('about.title') }}</h1>
        <div class="title-divider"></div>
        <p class="subtitle">{{ t('about.subtitle') }}</p>
      </div>
    </section>

    <!-- Main Content -->
    <section class="content-section">
      <div class="container">
        <!-- Intro Card -->
        <div class="intro-card">
          <div class="card-ornament">◆</div>
          <h2>{{ t('about.introTitle') }}</h2>
          <div class="text-divider"></div>
          <p class="lead-text">{{ t('about.introText') }}</p>
        </div>

        <!-- Gli Spazi - With Image -->
        <div class="single-story-section">
          <div class="story-grid">
            <!-- Text Block -->
            <div class="story-block-centered">
              <div class="block-number-centered">◆</div>
              <h3>{{ t('about.spacesTitle') }}</h3>
              <div class="block-divider"></div>
              <p v-html="t('about.spacesText1')"></p>
              <p v-html="t('about.spacesText2')"></p>
            </div>

            <!-- Image Block -->
            <div class="story-image-block">
              <div class="image-border-tl"></div>
              <div class="image-border-br"></div>
              <img :src="heroImages[0]" alt="Il Pesce d'Oro - Gli Spazi" class="story-image" />
              <div class="image-overlay"></div>
            </div>
          </div>
        </div>

        <!-- Mission Statement -->
        <div class="mission-section">
          <div class="mission-content">
            <div class="mission-icon">★</div>
            <h3>{{ t('about.missionTitle') }}</h3>
            <div class="mission-divider"></div>
            <p class="mission-text">{{ t('about.missionText') }}</p>
          </div>
        </div>

        <!-- Reviews Carousel -->
        <div class="reviews-wrapper">
          <div class="reviews-intro">
            <!-- <div class="intro-ornament">★</div> -->
            <h3>{{ t('about.reviewsTitle') }}</h3>
            <div class="intro-line"></div>
            <p class="reviews-description">{{ t('about.reviewsDescription') }}</p>
          </div>

          <div class="carousel-main">
            <button
              class="carousel-nav carousel-prev"
              @click="prevReview"
              :aria-label="t('common.previous')"
            >
              <span>‹</span>
            </button>

            <div class="carousel-stage">
              <transition :name="slideDirection" mode="out-in">
                <div :key="currentReviewIndex" class="review-showcase">
                  <div class="showcase-border-tl"></div>
                  <div class="showcase-border-br"></div>

                  <div class="review-header">
                    <div class="stars-display">
                      <span
                        v-for="star in reviews[currentReviewIndex].rating"
                        :key="star"
                        class="star-icon"
                        >★</span
                      >
                    </div>
                  </div>

                  <div class="review-body">
                    <div class="quotation-left">"</div>
                    <p class="review-quote">{{ reviews[currentReviewIndex].text }}</p>
                    <div class="quotation-right">"</div>
                  </div>

                  <div class="review-author-section">
                    <div class="author-line"></div>
                    <p class="author-name">{{ reviews[currentReviewIndex].author }}</p>
                    <p class="author-source">{{ t('about.viaTripAdvisor') }}</p>
                  </div>
                </div>
              </transition>
            </div>

            <button
              class="carousel-nav carousel-next"
              @click="nextReview"
              :aria-label="t('common.next')"
            >
              <span>›</span>
            </button>
          </div>

          <div class="carousel-pagination">
            <button
              v-for="(review, index) in reviews"
              :key="index"
              :class="['pagination-dot', { active: index === currentReviewIndex }]"
              @click="goToReview(index)"
              :aria-label="`${t('common.goToReview')} ${index + 1}`"
            ></button>
          </div>

          <div class="reviews-footer">
            <div class="tripadvisor-stats">
              <span class="stat-score">{{ t('about.rating') }}</span>
              <span class="stat-divider">|</span>
              <span class="stat-reviews">{{ t('about.reviewsCount') }}</span>
            </div>

            <a
              href="https://www.tripadvisor.it/Restaurant_Review-g187880-d1946247-Reviews-Il_Pesce_d_oro-Alghero_Province_of_Sassari_Sardinia.html"
              target="_blank"
              rel="noopener noreferrer"
              class="tripadvisor-cta"
            >
              {{ t('about.readAllReviews') }}
            </a>
          </div>
        </div>

        <!-- CTA Section -->
        <div class="cta-section">
          <div class="cta-ornament"></div>
          <h3>{{ t('about.ctaTitle') }}</h3>
          <p>{{ t('about.ctaText') }}</p>
          <RouterLink to="/contacts" class="cta-button">{{ t('about.bookTable') }}</RouterLink>
        </div>
      </div>
    </section>
  </div>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Lora:wght@400;500;600;700&display=swap');
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.about-page {
  background: linear-gradient(135deg, #f8f6f2 0%, #ebe8e1 50%, #f8f6f2 100%);
  min-height: 100vh;
  opacity: 0;
  transition: opacity 1s ease-out;
}

.about-page.visible {
  opacity: 1;
}

/* ==================== HERO SECTION WITH IMAGE CAROUSEL ==================== */
.hero-about {
  position: relative;
  height: 80vh;
  min-height: 400px;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
}

.hero-images-container {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
}

.hero-image {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
}

.hero-fade-enter-active,
.hero-fade-leave-active {
  transition: opacity 2s ease;
}

.hero-fade-enter-from {
  opacity: 0;
}

.hero-fade-leave-to {
  opacity: 0;
}

.hero-overlay {
  position: absolute;
  inset: 0;
  background: linear-gradient(rgba(212, 175, 55, 0.1), rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.7));
  z-index: 1;
}

.hero-content {
  position: relative;
  text-align: center;
  z-index: 2;
  opacity: 0;
  animation: fadeInUp 1.5s ease-out 0.3s forwards;
  padding: 3rem;
  border-radius: 4px;
}

.ornament {
  color: #e19b1d;
  font-size: 3rem;
  margin-bottom: 1rem;
  opacity: 1;
  animation: float 3s ease-in-out infinite;
  text-shadow: 0 0 30px rgba(212, 175, 55, 0.6);
}

.main-title {
  font-family: 'Lora', Georgia, serif;
  font-size: clamp(3rem, 8vw, 5rem);
  font-weight: 400;
  color: #ffffff;
  letter-spacing: 8px;
  margin-bottom: 1rem;
  text-shadow: 0 0 40px rgba(212, 175, 55, 0.3);
}

.title-divider {
  width: 120px;
  height: 2px;
  background: linear-gradient(90deg, transparent, #e19b1d, transparent);
  margin: 1.5rem auto;
  box-shadow: 0 0 15px rgba(212, 175, 55, 0.6);
}

.subtitle {
  font-size: 1.3rem;
  color: #e6c77f;
  font-weight: 300;
  letter-spacing: 3px;
  font-style: italic;
}

/* ==================== CONTENT SECTION ==================== */
.content-section {
  padding: 4rem 2rem;
  position: relative;
}

.content-section::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background:
    radial-gradient(circle at 30% 20%, rgba(212, 175, 55, 0.05) 0%, transparent 50%),
    radial-gradient(circle at 70% 80%, rgba(212, 175, 55, 0.05) 0%, transparent 50%);
  pointer-events: none;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  position: relative;
  z-index: 1;
}

/* ==================== INTRO CARD ==================== */
.intro-card {
  position: relative;
  text-align: center;
  padding: 5rem 4rem;
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.95), rgba(248, 246, 242, 0.9));
  border: 2px solid rgba(212, 175, 55, 0.3);
  margin-bottom: 6rem;
  opacity: 0;
  animation: fadeInUp 1s ease-out 0.5s forwards;
  box-shadow:
    0 10px 40px rgba(0, 0, 0, 0.08),
    0 0 0 1px rgba(212, 175, 55, 0.1) inset;
}

.intro-card::before,
.intro-card::after {
  content: '';
  position: absolute;
  width: 60px;
  height: 60px;
  border: 2px solid #c9a028;
  opacity: 0.5;
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
  color: #c9a028;
  font-size: 2rem;
  margin-bottom: 1.5rem;
  opacity: 1;
}

.intro-card h2 {
  font-family: 'Lora', Georgia, serif;
  font-size: 2.5rem;
  color: #8b6914;
  font-weight: 400;
  margin-bottom: 1.5rem;
  letter-spacing: 2px;
}

.text-divider {
  width: 80px;
  height: 2px;
  background: linear-gradient(90deg, transparent, #c9a028, transparent);
  margin: 1.5rem auto;
}

.lead-text {
  color: #2c2416;
  font-size: 1.15rem;
  line-height: 1.9;
  font-weight: 300;
  max-width: 800px;
  margin: 0 auto;
}

/* ==================== CENTERED SINGLE STORY BLOCK WITH IMAGE ==================== */
.single-story-section {
  margin-bottom: 6rem;
  opacity: 0;
  animation: fadeInUp 1s ease-out 1s forwards;
}

.story-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 2rem;
  align-items: stretch;
}

.story-block-centered {
  position: relative;
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.9), rgba(248, 246, 242, 0.85));
  padding: 4rem 3rem;
  border: 2px solid rgba(212, 175, 55, 0.3);
  text-align: center;
  box-shadow:
    0 10px 40px rgba(0, 0, 0, 0.08),
    0 0 0 1px rgba(212, 175, 55, 0.1) inset;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.story-block-centered::before {
  content: '';
  position: absolute;
  top: -1px;
  left: -1px;
  width: 80px;
  height: 80px;
  border-top: 2px solid #c9a028;
  border-left: 2px solid #c9a028;
  opacity: 0.5;
}

.story-block-centered::after {
  content: '';
  position: absolute;
  bottom: -1px;
  right: -1px;
  width: 80px;
  height: 80px;
  border-bottom: 2px solid #c9a028;
  border-right: 2px solid #c9a028;
  opacity: 0.5;
}

.block-number-centered {
  color: #c9a028;
  font-size: 2rem;
  margin-bottom: 1.5rem;
  opacity: 1;
}

.story-block-centered h3 {
  font-family: 'Lora', Georgia, serif;
  font-size: 2rem;
  color: #8b6914;
  font-weight: 400;
  margin-bottom: 1.5rem;
  letter-spacing: 1px;
}

.block-divider {
  width: 60px;
  height: 2px;
  background: linear-gradient(90deg, transparent, #c9a028, transparent);
  margin: 1.5rem auto;
}

.story-block-centered p {
  color: #2c2416;
  font-size: 1.05rem;
  line-height: 1.8;
  margin-bottom: 1rem;
  font-weight: 300;
}

.story-block-centered p:last-child {
  margin-bottom: 0;
}

.story-block-centered :deep(strong) {
  color: #8b6914;
  font-weight: 500;
}

/* Image Block */
.story-image-block {
  position: relative;
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.9), rgba(248, 246, 242, 0.85));
  border: 2px solid rgba(212, 175, 55, 0.3);
  overflow: hidden;
  box-shadow:
    0 10px 40px rgba(0, 0, 0, 0.08),
    0 0 0 1px rgba(212, 175, 55, 0.1) inset;
}

.image-border-tl,
.image-border-br {
  position: absolute;
  width: 80px;
  height: 80px;
  border: 2px solid #c9a028;
  opacity: 0.5;
  z-index: 2;
}

.image-border-tl {
  top: -1px;
  left: -1px;
  border-right: none;
  border-bottom: none;
}

.image-border-br {
  bottom: -1px;
  right: -1px;
  border-left: none;
  border-top: none;
}

.story-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
  transition: transform 0.6s ease;
}

.story-image-block:hover .story-image {
  transform: scale(1.05);
}

.image-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(
    to bottom,
    rgba(212, 175, 55, 0.08) 0%,
    rgba(0, 0, 0, 0.1) 50%,
    rgba(0, 0, 0, 0.25) 100%
  );
  pointer-events: none;
  z-index: 1;
}

/* ==================== MISSION SECTION ==================== */
.mission-section {
  margin-bottom: 6rem;
  opacity: 0;
  animation: fadeInUp 1s ease-out 1.2s forwards;
}

.mission-content {
  position: relative;
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.95), rgba(248, 246, 242, 0.9));
  padding: 5rem 4rem;
  border: 2px solid rgba(212, 175, 55, 0.3);
  text-align: center;
  box-shadow:
    0 10px 40px rgba(0, 0, 0, 0.08),
    0 0 0 1px rgba(212, 175, 55, 0.1) inset;
}

.mission-content::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 3px;
  background: linear-gradient(90deg, transparent, #c9a028, transparent);
}

.mission-icon {
  color: #c9a028;
  font-size: 3rem;
  margin-bottom: 1.5rem;
  opacity: 1;
}

.mission-content h3 {
  font-family: 'Lora', Georgia, serif;
  font-size: 2.5rem;
  color: #8b6914;
  font-weight: 400;
  margin-bottom: 1.5rem;
  letter-spacing: 2px;
}

.mission-divider {
  width: 100px;
  height: 2px;
  background: linear-gradient(90deg, transparent, #c9a028, transparent);
  margin: 1.5rem auto;
}

.mission-text {
  color: #2c2416;
  font-size: 1.15rem;
  line-height: 1.9;
  max-width: 900px;
  margin: 0 auto;
  font-weight: 300;
}

/* ==================== REVIEWS SECTION ==================== */
.reviews-wrapper {
  margin-bottom: 6rem;
  opacity: 0;
  animation: fadeInUp 1s ease-out 1.8s forwards;
}

.reviews-intro {
  text-align: center;
  margin-bottom: 4rem;
}

.intro-ornament {
  color: #c9a028;
  font-size: 3rem;
  margin-bottom: 1rem;
  opacity: 1;
}

.reviews-intro h3 {
  font-family: 'Lora', Georgia, serif;
  font-size: 2.5rem;
  color: #8b6914;
  font-weight: 400;
  margin-bottom: 1rem;
  letter-spacing: 2px;
}

.intro-line {
  width: 100px;
  height: 2px;
  background: linear-gradient(90deg, transparent, #c9a028, transparent);
  margin: 1.5rem auto;
}

.reviews-description {
  color: #8b6914;
  font-size: 1.1rem;
  font-weight: 300;
  font-style: italic;
}

.carousel-main {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 2rem;
  margin-bottom: 2rem;
}

.carousel-nav {
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.9), rgba(248, 246, 242, 0.85));
  border: 2px solid rgba(212, 175, 55, 0.3);
  color: #8b6914;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all 0.3s ease;
  flex-shrink: 0;
  box-shadow: 0 3px 15px rgba(0, 0, 0, 0.08);
}

.carousel-nav span {
  font-size: 2rem;
  line-height: 1;
}

.carousel-nav:hover {
  background: linear-gradient(135deg, rgba(255, 255, 255, 1), rgba(248, 246, 242, 0.95));
  border-color: #c9a028;
  transform: scale(1.1);
  box-shadow: 0 5px 20px rgba(0, 0, 0, 0.12);
}

.carousel-stage {
  flex: 1;
  max-width: 800px;
  min-height: 450px;
  position: relative;
}

.review-showcase {
  position: relative;
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.95), rgba(248, 246, 242, 0.9));
  padding: 4rem 3rem;
  border: 2px solid rgba(212, 175, 55, 0.3);
  min-height: 450px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  box-shadow:
    0 10px 40px rgba(0, 0, 0, 0.08),
    0 0 0 1px rgba(212, 175, 55, 0.1) inset;
}

.showcase-border-tl,
.showcase-border-br {
  position: absolute;
  width: 60px;
  height: 60px;
  border: 2px solid #c9a028;
  opacity: 0.5;
}

.showcase-border-tl {
  top: -1px;
  left: -1px;
  border-right: none;
  border-bottom: none;
}

.showcase-border-br {
  bottom: -1px;
  right: -1px;
  border-left: none;
  border-top: none;
}

.review-header {
  display: flex;
  justify-content: center;
  margin-bottom: 2rem;
}

.stars-display {
  display: flex;
  gap: 0.3rem;
}

.star-icon {
  color: #c9a028;
  font-size: 1.5rem;
}

.review-body {
  position: relative;
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 2rem 1rem;
}

.quotation-left,
.quotation-right {
  position: absolute;
  font-family: Georgia, serif;
  font-size: 5rem;
  color: rgba(201, 160, 40, 0.15);
  line-height: 1;
}

.quotation-left {
  top: -1rem;
  left: 0;
}

.quotation-right {
  bottom: -2rem;
  right: 0;
}

.review-quote {
  color: #2c2416;
  font-size: 1.1rem;
  line-height: 1.9;
  text-align: center;
  font-weight: 300;
  font-style: italic;
  position: relative;
  z-index: 1;
}

.review-author-section {
  text-align: center;
  margin-top: 2rem;
}

.author-line {
  width: 60px;
  height: 2px;
  background: linear-gradient(90deg, transparent, #c9a028, transparent);
  margin: 0 auto 1rem;
}

.author-name {
  color: #8b6914;
  font-size: 1.1rem;
  font-weight: 500;
  margin-bottom: 0.3rem;
  letter-spacing: 0.5px;
}

.author-source {
  color: #8b6914;
  font-size: 0.9rem;
  font-weight: 300;
}

.carousel-pagination {
  display: flex;
  justify-content: center;
  gap: 0.8rem;
  margin-bottom: 2.5rem;
}

.pagination-dot {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background: rgba(201, 160, 40, 0.2);
  border: 2px solid rgba(201, 160, 40, 0.4);
  cursor: pointer;
  transition: all 0.3s ease;
  padding: 0;
}

.pagination-dot:hover {
  background: rgba(201, 160, 40, 0.5);
  transform: scale(1.2);
  box-shadow: 0 0 10px rgba(201, 160, 40, 0.3);
}

.pagination-dot.active {
  background: #c9a028;
  border-color: #c9a028;
  transform: scale(1.3);
  box-shadow: 0 0 15px rgba(201, 160, 40, 0.4);
}

.reviews-footer {
  text-align: center;
}

.tripadvisor-stats {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1rem;
  margin-bottom: 1.5rem;
  color: #4a4032;
  font-size: 1rem;
}

.stat-score {
  color: #8b6914;
  font-weight: 600;
  font-size: 1.2rem;
}

.stat-divider {
  color: rgba(139, 105, 20, 0.4);
}

.tripadvisor-cta {
  color: #8b6914;
  text-decoration: none;
  font-size: 1rem;
  font-weight: 300;
  letter-spacing: 0.5px;
  padding: 0.5rem 0;
  position: relative;
  transition: all 0.3s ease;
}

.tripadvisor-cta::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 0;
  height: 1px;
  background: #8b6914;
  transition: width 0.3s ease;
}

.tripadvisor-cta:hover::after {
  width: 100%;
}

/* Carousel Transitions */
.slide-left-enter-active,
.slide-left-leave-active,
.slide-right-enter-active,
.slide-right-leave-active {
  transition: all 0.6s ease;
}

.slide-left-enter-from {
  opacity: 0;
  transform: translateX(40px);
}

.slide-left-leave-to {
  opacity: 0;
  transform: translateX(-40px);
}

.slide-right-enter-from {
  opacity: 0;
  transform: translateX(-40px);
}

.slide-right-leave-to {
  opacity: 0;
  transform: translateX(40px);
}

/* CTA Section */
.cta-section {
  text-align: center;
  padding: 5rem 3rem;
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.95), rgba(248, 246, 242, 0.9));
  border: 2px solid rgba(212, 175, 55, 0.3);
  opacity: 0;
  animation: fadeInUp 1s ease-out 2.2s forwards;
  box-shadow:
    0 10px 40px rgba(0, 0, 0, 0.08),
    0 0 0 1px rgba(212, 175, 55, 0.1) inset;
}

.cta-ornament {
  color: #c9a028;
  font-size: 2rem;
  margin-bottom: 1.5rem;
  opacity: 1;
}

.cta-section h3 {
  font-family: 'Lora', Georgia, serif;
  font-size: 2.5rem;
  color: #8b6914;
  font-weight: 400;
  margin-bottom: 1rem;
  letter-spacing: 2px;
}

.cta-section p {
  color: #4a4032;
  font-size: 1.1rem;
  margin-bottom: 2.5rem;
  font-weight: 300;
}

.cta-button {
  display: inline-block;
  background: linear-gradient(135deg, #e19b1d, #c9a028);
  color: #ffffff;
  padding: 1rem 3rem;
  text-decoration: none;
  font-weight: 600;
  font-size: 1rem;
  letter-spacing: 1px;
  transition: all 0.3s ease;
  position: relative;
  overflow: hidden;
  box-shadow: 0 5px 20px rgba(201, 160, 40, 0.3);
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
  box-shadow: 0 10px 35px rgba(201, 160, 40, 0.4);
}

/* ==================== ANIMATIONS ==================== */
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

@keyframes float {
  0%,
  100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-10px);
  }
}

/* ==================== RESPONSIVE ==================== */
@media (max-width: 968px) {
  .story-grid {
    grid-template-columns: 1fr;
    gap: 2rem;
  }

  .story-image-block {
    min-height: 400px;
  }
}

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

  .single-story-section {
    margin-bottom: 3rem;
  }

  .story-block-centered {
    padding: 3rem 2rem;
  }

  .story-image-block {
    min-height: 350px;
  }

  .mission-content {
    padding: 3rem 2rem;
  }

  .mission-section {
    margin-bottom: 3rem;
  }

  .reviews-wrapper {
    margin-bottom: 3rem;
  }

  .reviews-intro {
    margin-bottom: 3rem;
  }

  .carousel-main {
    gap: 1rem;
  }

  .carousel-nav {
    width: 45px;
    height: 45px;
  }

  .carousel-nav span {
    font-size: 1.8rem;
  }

  .review-showcase {
    padding: 3rem 2rem;
    min-height: 400px;
  }

  .showcase-border-tl,
  .showcase-border-br {
    width: 50px;
    height: 50px;
  }

  .quotation-left,
  .quotation-right {
    font-size: 4rem;
  }

  .review-quote {
    font-size: 1.05rem;
  }

  .cta-section {
    padding: 3rem 1.5rem;
  }
}

@media (max-width: 480px) {
  .hero-about {
    height: 70vh;
  }

  .intro-card h2 {
    font-size: 1.8rem;
  }

  .lead-text {
    font-size: 1rem;
  }

  .story-block-centered h3 {
    font-size: 1.5rem;
  }

  .story-image-block {
    min-height: 300px;
  }

  .image-border-tl,
  .image-border-br {
    width: 60px;
    height: 60px;
  }

  .mission-content h3 {
    font-size: 2rem;
  }

  .mission-text {
    font-size: 1rem;
  }

  .reviews-intro h3 {
    font-size: 1.8rem;
  }

  .carousel-main {
    gap: 0.5rem;
  }

  .carousel-nav {
    width: 40px;
    height: 40px;
  }

  .carousel-nav span {
    font-size: 1.5rem;
  }

  .review-showcase {
    padding: 2.5rem 1.5rem;
    min-height: 420px;
  }

  .showcase-border-tl,
  .showcase-border-br {
    width: 40px;
    height: 40px;
  }

  .quotation-left {
    font-size: 3.5rem;
    top: -0.5rem;
    left: -0.5rem;
  }

  .quotation-right {
    font-size: 3.5rem;
    bottom: -1.5rem;
    right: -0.5rem;
  }

  .review-quote {
    font-size: 0.98rem;
    line-height: 1.8;
  }

  .pagination-dot {
    width: 7px;
    height: 7px;
  }

  .tripadvisor-stats {
    flex-direction: column;
    gap: 0.3rem;
  }

  .stat-divider {
    display: none;
  }
}
</style>
