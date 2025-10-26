<script setup>
import { onMounted, ref } from 'vue'

const isVisible = ref(false)
const currentReviewIndex = ref(0)
const slideDirection = ref('slide-left')

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

let autoSlideInterval = null

const nextReview = () => {
  slideDirection.value = 'slide-left'
  currentReviewIndex.value = (currentReviewIndex.value + 1) % reviews.value.length
  resetAutoSlide()
}

const prevReview = () => {
  slideDirection.value = 'slide-right'
  currentReviewIndex.value =
    currentReviewIndex.value === 0 ? reviews.value.length - 1 : currentReviewIndex.value - 1
  resetAutoSlide()
}

const goToReview = (index) => {
  slideDirection.value = index > currentReviewIndex.value ? 'slide-left' : 'slide-right'
  currentReviewIndex.value = index
  resetAutoSlide()
}

const startAutoSlide = () => {
  autoSlideInterval = setInterval(() => {
    nextReview()
  }, 7000)
}

const resetAutoSlide = () => {
  if (autoSlideInterval) {
    clearInterval(autoSlideInterval)
  }
  startAutoSlide()
}

onMounted(() => {
  setTimeout(() => {
    isVisible.value = true
  }, 300)
  startAutoSlide()
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

        <!-- Gli Spazi - Centered Single Block -->
        <div class="single-story-section">
          <div class="story-block-centered">
            <div class="block-number-centered">◆</div>
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

        <!-- Reviews Carousel -->
        <div class="reviews-wrapper">
          <div class="reviews-intro">
            <div class="intro-ornament">★</div>
            <h3>Parola ai Nostri Ospiti</h3>
            <div class="intro-line"></div>
            <p class="reviews-description">
              Scopri le esperienze autentiche di chi ha scelto il Pesce d'Oro
            </p>
          </div>

          <div class="carousel-main">
            <button class="carousel-nav carousel-prev" @click="prevReview" aria-label="Precedente">
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
                    <p class="author-source">via TripAdvisor</p>
                  </div>
                </div>
              </transition>
            </div>

            <button class="carousel-nav carousel-next" @click="nextReview" aria-label="Successivo">
              <span>›</span>
            </button>
          </div>

          <div class="carousel-pagination">
            <button
              v-for="(review, index) in reviews"
              :key="index"
              :class="['pagination-dot', { active: index === currentReviewIndex }]"
              @click="goToReview(index)"
              :aria-label="`Vai alla recensione ${index + 1}`"
            ></button>
          </div>

          <div class="reviews-footer">
            <div class="tripadvisor-stats">
              <span class="stat-score">4.2/5</span>
              <span class="stat-divider">|</span>
              <span class="stat-reviews">Oltre 2.000 recensioni</span>
            </div>
            <a
              href="https://www.tripadvisor.it/Restaurant_Review-g187880-d1946247-Reviews-Il_Pesce_d_oro-Alghero_Province_of_Sassari_Sardinia.html"
              target="_blank"
              rel="noopener noreferrer"
              class="tripadvisor-cta"
            >
              Leggi tutte le recensioni su TripAdvisor
            </a>
          </div>
        </div>

        <!-- CTA Section -->
        <div class="cta-section">
          <div class="cta-ornament">⚜</div>
          <h3>Vieni a Trovarci</h3>
          <p>Scopri il gusto dell'autentica cucina mediterranea</p>
          <RouterLink to="/contacts" class="cta-button">Prenota un Tavolo</RouterLink>
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
  background:
    linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.7)),
    url('https://images.unsplash.com/photo-1559339352-11d035aa65de?q=80&w=2074') center/cover;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
}

.hero-overlay {
  position: absolute;
  inset: 0;
  background: radial-gradient(circle at center, transparent 0%, rgba(10, 10, 10, 0.6) 100%);
}

.hero-content {
  position: relative;
  text-align: center;
  z-index: 1;
  opacity: 0;
  animation: fadeInUp 1.5s ease-out 0.3s forwards;
}

.ornament {
  color: #d4af37;
  font-size: 3rem;
  margin-bottom: 1rem;
  opacity: 0.8;
  animation: float 3s ease-in-out infinite;
}

.main-title {
  font-family: 'Playfair Display', Georgia, serif;
  font-size: clamp(3rem, 8vw, 5rem);
  font-weight: 400;
  color: #ffffff;
  letter-spacing: 8px;
  margin-bottom: 1rem;
  text-transform: uppercase;
}

.title-divider {
  width: 120px;
  height: 2px;
  background: linear-gradient(90deg, transparent, #d4af37, transparent);
  margin: 1.5rem auto;
}

.subtitle {
  font-size: 1.3rem;
  color: rgba(224, 224, 224, 0.8);
  font-weight: 300;
  letter-spacing: 3px;
  font-style: italic;
}

/* ==================== CONTENT SECTION ==================== */
.content-section {
  padding: 4rem 2rem;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
}

/* ==================== INTRO CARD ==================== */
.intro-card {
  position: relative;
  text-align: center;
  padding: 4rem 3rem;
  background: linear-gradient(135deg, rgba(212, 175, 55, 0.03), rgba(10, 10, 10, 0.5));
  border: 1px solid rgba(212, 175, 55, 0.2);
  margin-bottom: 4rem;
  opacity: 0;
  animation: fadeInUp 1s ease-out 0.5s forwards;
}

.intro-card::before,
.intro-card::after {
  content: '';
  position: absolute;
  width: 60px;
  height: 60px;
  border: 1px solid rgba(212, 175, 55, 0.4);
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
  font-size: 2rem;
  margin-bottom: 1.5rem;
  opacity: 0.6;
}

.intro-card h2 {
  font-family: 'Playfair Display', Georgia, serif;
  font-size: 2.5rem;
  color: #d4af37;
  font-weight: 400;
  margin-bottom: 1.5rem;
  letter-spacing: 2px;
}

.text-divider {
  width: 80px;
  height: 1px;
  background: #d4af37;
  margin: 1.5rem auto;
  opacity: 0.5;
}

.lead-text {
  color: rgba(224, 224, 224, 0.85);
  font-size: 1.15rem;
  line-height: 1.9;
  font-weight: 300;
  max-width: 800px;
  margin: 0 auto;
}

/* ==================== CENTERED SINGLE STORY BLOCK ==================== */
.single-story-section {
  margin-bottom: 4rem;
  display: flex;
  justify-content: center;
  opacity: 0;
  animation: fadeInUp 1s ease-out 1s forwards;
}

.story-block-centered {
  position: relative;
  background: linear-gradient(135deg, rgba(212, 175, 55, 0.05), rgba(10, 10, 10, 0.3));
  padding: 3rem;
  border: 1px solid rgba(212, 175, 55, 0.2);
  max-width: 700px;
  width: 100%;
  text-align: center;
}

.story-block-centered::before {
  content: '';
  position: absolute;
  top: -1px;
  left: -1px;
  width: 80px;
  height: 80px;
  border-top: 2px solid rgba(212, 175, 55, 0.4);
  border-left: 2px solid rgba(212, 175, 55, 0.4);
}

.story-block-centered::after {
  content: '';
  position: absolute;
  bottom: -1px;
  right: -1px;
  width: 80px;
  height: 80px;
  border-bottom: 2px solid rgba(212, 175, 55, 0.4);
  border-right: 2px solid rgba(212, 175, 55, 0.4);
}

.block-number-centered {
  color: #d4af37;
  font-size: 2rem;
  margin-bottom: 1.5rem;
  opacity: 0.5;
}

.story-block-centered h3 {
  font-family: 'Playfair Display', Georgia, serif;
  font-size: 2rem;
  color: #d4af37;
  font-weight: 400;
  margin-bottom: 1.5rem;
  letter-spacing: 1px;
}

.block-divider {
  width: 60px;
  height: 1px;
  background: rgba(212, 175, 55, 0.5);
  margin: 1.5rem auto;
}

.story-block-centered p {
  color: rgba(224, 224, 224, 0.8);
  font-size: 1.05rem;
  line-height: 1.8;
  margin-bottom: 1rem;
  font-weight: 300;
}

.story-block-centered p:last-child {
  margin-bottom: 0;
}

.story-block-centered strong {
  color: #d4af37;
  font-weight: 500;
}

/* ==================== MISSION SECTION ==================== */
.mission-section {
  margin-bottom: 4rem;
  opacity: 0;
  animation: fadeInUp 1s ease-out 1.2s forwards;
}

.mission-content {
  position: relative;
  background: linear-gradient(135deg, rgba(10, 10, 10, 0.8), rgba(212, 175, 55, 0.03));
  padding: 4rem 3rem;
  border: 1px solid rgba(212, 175, 55, 0.15);
  text-align: center;
}

.mission-content::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 2px;
  background: linear-gradient(90deg, transparent, #d4af37, transparent);
}

.mission-icon {
  color: #d4af37;
  font-size: 3rem;
  margin-bottom: 1.5rem;
  opacity: 0.7;
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
  width: 100px;
  height: 1px;
  background: #d4af37;
  margin: 1.5rem auto;
  opacity: 0.5;
}

.mission-text {
  color: rgba(224, 224, 224, 0.85);
  font-size: 1.15rem;
  line-height: 1.9;
  max-width: 900px;
  margin: 0 auto;
  font-weight: 300;
}

/* ==================== FEATURES SECTION ==================== */
.features-section {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
  margin-bottom: 5rem;
  opacity: 0;
  animation: fadeInUp 1s ease-out 1.5s forwards;
}

.feature-item {
  text-align: center;
  padding: 2.5rem 1.5rem;
  background: linear-gradient(135deg, rgba(212, 175, 55, 0.03), rgba(10, 10, 10, 0.5));
  border: 1px solid rgba(212, 175, 55, 0.15);
  transition: all 0.4s ease;
}

.feature-item:hover {
  transform: translateY(-8px);
  border-color: rgba(212, 175, 55, 0.4);
  box-shadow: 0 10px 30px rgba(212, 175, 55, 0.15);
}

.feature-icon {
  font-size: 3rem;
  margin-bottom: 1rem;
  filter: grayscale(0.3);
}

.feature-item h4 {
  font-family: 'Playfair Display', Georgia, serif;
  color: #d4af37;
  font-size: 1.4rem;
  margin-bottom: 0.8rem;
  font-weight: 500;
  letter-spacing: 1px;
}

.feature-item p {
  color: rgba(224, 224, 224, 0.7);
  font-size: 0.95rem;
  line-height: 1.6;
  font-weight: 300;
}

/* ==================== REVIEWS SECTION ==================== */
.reviews-wrapper {
  margin-bottom: 5rem;
  opacity: 0;
  animation: fadeInUp 1s ease-out 1.8s forwards;
}

.reviews-intro {
  text-align: center;
  margin-bottom: 4rem;
}

.intro-ornament {
  color: #d4af37;
  font-size: 3rem;
  margin-bottom: 1rem;
  opacity: 0.6;
}

.reviews-intro h3 {
  font-family: 'Playfair Display', Georgia, serif;
  font-size: 2.5rem;
  color: #d4af37;
  font-weight: 400;
  margin-bottom: 1rem;
  letter-spacing: 2px;
}

.intro-line {
  width: 100px;
  height: 1px;
  background: #d4af37;
  margin: 1.5rem auto;
  opacity: 0.5;
}

.reviews-description {
  color: rgba(224, 224, 224, 0.7);
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
  background: rgba(212, 175, 55, 0.1);
  border: 1px solid rgba(212, 175, 55, 0.3);
  color: #d4af37;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all 0.3s ease;
  flex-shrink: 0;
}

.carousel-nav span {
  font-size: 2rem;
  line-height: 1;
}

.carousel-nav:hover {
  background: rgba(212, 175, 55, 0.2);
  border-color: rgba(212, 175, 55, 0.5);
  transform: scale(1.1);
}

.carousel-stage {
  flex: 1;
  max-width: 800px;
  min-height: 450px;
  position: relative;
}

.review-showcase {
  position: relative;
  background: linear-gradient(135deg, rgba(212, 175, 55, 0.05), rgba(10, 10, 10, 0.6));
  padding: 4rem 3rem;
  border: 1px solid rgba(212, 175, 55, 0.2);
  min-height: 450px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.showcase-border-tl,
.showcase-border-br {
  position: absolute;
  width: 60px;
  height: 60px;
  border: 2px solid rgba(212, 175, 55, 0.4);
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
  color: #d4af37;
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
  color: rgba(212, 175, 55, 0.2);
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
  color: rgba(224, 224, 224, 0.9);
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
  height: 1px;
  background: rgba(212, 175, 55, 0.5);
  margin: 0 auto 1rem;
}

.author-name {
  color: #d4af37;
  font-size: 1.1rem;
  font-weight: 500;
  margin-bottom: 0.3rem;
  letter-spacing: 0.5px;
}

.author-source {
  color: rgba(224, 224, 224, 0.5);
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
  background: rgba(212, 175, 55, 0.3);
  border: 1px solid rgba(212, 175, 55, 0.4);
  cursor: pointer;
  transition: all 0.3s ease;
  padding: 0;
}

.pagination-dot:hover {
  background: rgba(212, 175, 55, 0.5);
  transform: scale(1.2);
}

.pagination-dot.active {
  background: #d4af37;
  border-color: #d4af37;
  transform: scale(1.3);
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
  color: rgba(224, 224, 224, 0.8);
  font-size: 1rem;
}

.stat-score {
  color: #d4af37;
  font-weight: 600;
  font-size: 1.2rem;
}

.stat-divider {
  color: rgba(212, 175, 55, 0.5);
}

.tripadvisor-cta {
  color: #d4af37;
  text-decoration: none;
  font-size: 1rem;
  font-weight: 300;
  letter-spacing: 0.5px;
  padding: 0.5rem 0;
  position: relative;
  transition: opacity 0.3s ease;
}

.tripadvisor-cta::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 0;
  height: 1px;
  background: #d4af37;
  transition: width 0.3s ease;
}

.tripadvisor-cta:hover::after {
  width: 100%;
}

.tripadvisor-cta:hover {
  opacity: 0.8;
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
  padding: 4rem 2rem;
  background: linear-gradient(135deg, rgba(212, 175, 55, 0.05), rgba(218, 165, 32, 0.02));
  border: 1px solid rgba(212, 175, 55, 0.2);
  opacity: 0;
  animation: fadeInUp 1s ease-out 2.2s forwards;
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
    height: 50vh;
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

  .mission-content h3 {
    font-size: 2rem;
  }

  .mission-text {
    font-size: 1rem;
  }

  .features-section {
    grid-template-columns: 1fr;
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
