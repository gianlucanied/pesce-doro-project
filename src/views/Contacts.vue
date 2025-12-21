<script setup>
import { onMounted, ref } from 'vue'
import { useI18n } from 'vue-i18n'

const { t } = useI18n()

const isVisible = ref(false)
const currentHeroImage = ref(0)
let heroImageInterval = null

// Array di immagini per l'hero - USA NEW URL INVECE DI PERCORSI RELATIVI
const heroImages = [
  new URL('@/assets/8.jpg', import.meta.url).href,
  new URL('@/assets/9.jpg', import.meta.url).href,
  new URL('@/assets/10.jpg', import.meta.url).href,
  new URL('@/assets/11.jpg', import.meta.url).href,
  new URL('@/assets/12.jpg', import.meta.url).href,
  new URL('@/assets/13.jpg', import.meta.url).href,
  new URL('@/assets/14.jpg', import.meta.url).href,
]

onMounted(() => {
  setTimeout(() => {
    isVisible.value = true
  }, 300)
  startHeroImageSlide()
})

const startHeroImageSlide = () => {
  heroImageInterval = setInterval(() => {
    currentHeroImage.value = (currentHeroImage.value + 1) % heroImages.length
  }, 5000) // Cambia immagine ogni 5 secondi
}
</script>

<template>
  <div class="contacts-page" :class="{ visible: isVisible }">
    <!-- Hero Section -->
    <section class="hero-contacts">
      <!-- Background con immagini scorrevoli -->
      <div class="hero-background">
        <transition name="hero-fade" mode="out-in">
          <div
            :key="currentHeroImage"
            class="hero-bg-image"
            :style="{ backgroundImage: `url(${heroImages[currentHeroImage]})` }"
          ></div>
        </transition>
        <div class="hero-bg-overlay"></div>
      </div>

      <div class="hero-overlay"></div>
      <div class="hero-content">
        <div class="ornament"></div>
        <h1 class="main-title">{{ t('contacts.title') }}</h1>
        <div class="title-divider"></div>
      </div>
    </section>

    <!-- Main Content -->
    <section class="content-section">
      <div class="container">
        <!-- Info Cards Grid -->
        <div class="info-grid">
          <!-- Contact Info Card -->
          <div class="info-card contact-card">
            <div class="card-icon">
              <svg
                width="40"
                height="40"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="1.5"
                stroke-linecap="round"
                stroke-linejoin="round"
              >
                <path
                  d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07 19.5 19.5 0 0 1-6-6 19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 4.11 2h3a2 2 0 0 1 2 1.72 12.84 12.84 0 0 0 .7 2.81 2 2 0 0 1-.45 2.11L8.09 9.91a16 16 0 0 0 6 6l1.27-1.27a2 2 0 0 1 2.11-.45 12.84 12.84 0 0 0 2.81.7A2 2 0 0 1 22 16.92z"
                />
              </svg>
            </div>
            <h2>{{ t('contacts.infoContactsTitle') }}</h2>
            <div class="card-divider"></div>

            <div class="contact-item">
              <h4>{{ t('contacts.phone') }}</h4>
              <a href="tel:+39079952602" class="contact-link">+39 079 952 602</a>
            </div>

            <div class="contact-item">
              <h4>{{ t('contacts.email') }}</h4>
              <a href="mailto:info@pescedoroalghero.it" class="contact-link"
                >info@pescedoroalghero.it</a
              >
            </div>

            <div class="card-divider"></div>

            <div class="contact-link">
              <h4 id="prenotation">{{ t('contacts.prenotation') }}</h4>
            </div>
          </div>

          <!-- Hours Card -->
          <div class="info-card hours-card">
            <div class="card-icon">
              <svg
                width="40"
                height="40"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="1.5"
                stroke-linecap="round"
                stroke-linejoin="round"
              >
                <circle cx="12" cy="12" r="10" />
                <polyline points="12 6 12 12 16 14" />
              </svg>
            </div>
            <h2>{{ t('contacts.openingHoursTitle') }}</h2>
            <div class="card-divider"></div>

            <div class="hours-item">
              <div class="time-slots">
                <div class="time-slot">
                  <span class="slot-label">{{ t('contacts.lunch') }}</span>
                  <span class="slot-time">12:30 - 14:30</span>
                </div>
                <div class="time-slot">
                  <span class="slot-label">{{ t('contacts.dinner') }}</span>
                  <span class="slot-time">19:30 - 23:00</span>
                </div>
              </div>
            </div>

            <div class="contact-item">
              <h4>{{ t('contacts.closureDays') }}</h4>
              <p class="closure-info">
                <span class="closure-day">{{ t('contacts.wednesday') }}</span>
                {{ t('contacts.allDay') }}<br />
                <span class="closure-day">{{ t('contacts.thursday') }}</span>
                {{ t('contacts.morning') }}
              </p>
            </div>
          </div>
        </div>

        <!-- Location Section -->
        <div class="location-section">
          <div class="location-header">
            <div class="header-ornament">◆</div>
            <h2>{{ t('contacts.whereWeAre') }}</h2>
            <div class="header-divider"></div>
          </div>

          <div class="location-grid">
            <!-- Location Info -->
            <div class="location-info">
              <div class="address-box">
                <div class="address-icon">
                  <svg
                    width="48"
                    height="48"
                    viewBox="0 0 24 24"
                    fill="none"
                    stroke="currentColor"
                    stroke-width="1.5"
                    stroke-linecap="round"
                    stroke-linejoin="round"
                  >
                    <path d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0 1 18 0z" />
                    <circle cx="12" cy="10" r="3" />
                  </svg>
                </div>
                <div class="address-content">
                  <h3>{{ t('contacts.addressTitle') }}</h3>
                  <p class="address">{{ t('contacts.address') }}</p>
                  <p class="city">{{ t('contacts.city') }}</p>
                  <p class="note">{{ t('contacts.nearPort') }}</p>
                </div>
              </div>
            </div>

            <!-- Map -->
            <div class="map-container">
              <iframe
                src="https://www.google.com/maps?q=Via+Catalogna+12,+Alghero&output=embed"
                width="100%"
                height="100%"
                style="border: 0"
                allowfullscreen=""
                loading="lazy"
                referrerpolicy="no-referrer-when-downgrade"
              ></iframe>
            </div>
          </div>
        </div>

        <!-- CTA Section -->
        <div class="cta-section">
          <div class="cta-ornament"></div>
          <h3>{{ t('contacts.bookTableTitle') }}</h3>
          <p>{{ t('contacts.bookTableText') }}</p>
          <div class="cta-buttons">
            <a href="tel:+39079952602" class="cta-button primary">{{ t('contacts.callNow') }}</a>
          </div>
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

.contacts-page {
  background: linear-gradient(135deg, #f8f6f2 0%, #ebe8e1 50%, #f8f6f2 100%);
  min-height: 100vh;
  opacity: 0;
  transition: opacity 1s ease-out;
  position: relative;
}

.contacts-page::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background:
    radial-gradient(circle at 25% 30%, rgba(212, 175, 55, 0.05) 0%, transparent 50%),
    radial-gradient(circle at 75% 70%, rgba(212, 175, 55, 0.05) 0%, transparent 50%);
  pointer-events: none;
}

.contacts-page.visible {
  opacity: 1;
}

/* ==================== HERO SECTION ==================== */
.hero-contacts {
  position: relative;
  height: 80vh;
  min-height: 350px;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
}

/* Background con immagini scorrevoli */
.hero-background {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 0;
}

.hero-bg-image {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
}

.hero-bg-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(
    135deg,
    rgba(212, 175, 55, 0.1) 0%,
    rgba(0, 0, 0, 0.5) 50%,
    rgba(0, 0, 0, 0.7) 100%
  );
  backdrop-filter: blur(1px);
}

/* Transizione fade per le immagini hero */
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
  z-index: 1;
  pointer-events: none;
}

.hero-content {
  position: relative;
  z-index: 2;
  text-align: center;
  padding: 3rem;
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
  color: #e19b1d;
  font-size: 2.5rem;
  margin-bottom: 1rem;
  opacity: 0;
  animation: fadeIn 1s ease-out 0.3s forwards;
  text-shadow:
    0 0 30px rgba(212, 175, 55, 0.6),
    0 2px 4px rgba(0, 0, 0, 0.5);
}

@keyframes fadeIn {
  to {
    opacity: 1;
  }
}

.main-title {
  font-family: 'Lora', Georgia, serif;
  font-size: clamp(3rem, 6vw, 5rem);
  font-weight: 400;
  color: #ffffff;
  margin-bottom: 1rem;
  letter-spacing: 3px;
  text-shadow:
    0 0 40px rgba(212, 175, 55, 0.5),
    0 4px 8px rgba(0, 0, 0, 0.6);
  opacity: 0;
  animation: fadeIn 1s ease-out 0.5s forwards;
}

.title-divider {
  width: 120px;
  height: 2px;
  background: linear-gradient(90deg, transparent, #e19b1d, transparent);
  margin: 1.5rem auto;
  opacity: 0;
  animation: expandLine 1s ease-out 0.7s forwards;
  box-shadow: 0 0 15px rgba(212, 175, 55, 0.6);
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

/* ==================== CONTENT SECTION ==================== */
.content-section {
  padding: 6rem 2rem;
  position: relative;
  z-index: 1;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
}

/* Info Grid */
.info-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 2.5rem;
  margin-bottom: 6rem;
}

.info-card {
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.95), rgba(248, 246, 242, 0.9));
  border: 2px solid rgba(212, 175, 55, 0.3);
  padding: 4rem 3rem;
  transition: all 0.4s ease;
  opacity: 0;
  animation: fadeInUp 1s ease-out forwards;
  box-shadow:
    0 10px 40px rgba(0, 0, 0, 0.08),
    0 0 0 1px rgba(212, 175, 55, 0.1) inset;
  text-align: center;
}

.contact-card {
  animation-delay: 1.1s;
}

.hours-card {
  animation-delay: 1.3s;
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

.info-card:hover {
  border-color: #c9a028;
  transform: translateY(-5px);
  box-shadow:
    0 15px 50px rgba(0, 0, 0, 0.12),
    0 0 0 1px rgba(212, 175, 55, 0.15) inset;
}

.card-icon {
  color: #c9a028;
  margin-bottom: 1.5rem;
  display: flex;
  justify-content: center;
}

.card-icon svg {
  color: #c9a028;
}

.info-card h2 {
  font-family: 'Lora', Georgia, serif;
  font-size: 2rem;
  color: #8b6914;
  font-weight: 500;
  margin-bottom: 1rem;
  letter-spacing: 1px;
}

.card-divider {
  width: 100%;
  height: 2px;
  background: linear-gradient(90deg, transparent, #c9a028, transparent);
  margin-bottom: 2rem;
}

.contact-item {
  margin-bottom: 2rem;
}

.contact-item:last-child {
  margin-bottom: 0;
}

.contact-item h4 {
  color: #8b6914;
  font-size: 0.85rem;
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 2px;
  margin-bottom: 0.5rem;
}

.contact-link {
  color: #8b6914;
  text-decoration: none;
  font-size: 1.3rem;
  font-weight: 400;
  transition: all 0.3s ease;
  display: inline-block;
}

#prenotation {
  font-size: 1.05rem;
}

.contact-link:hover {
  color: #c9a028;
  transform: translateX(5px);
}

.closure-info {
  color: #2c2416;
  font-size: 1.05rem;
  line-height: 1.8;
  font-weight: 300;
}

.closure-day {
  color: #8b6914;
  font-weight: 500;
}

/* Hours Card */
.hours-item {
  margin-bottom: 2rem;
}

.time-slots {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.time-slot {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem;
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.9), rgba(248, 246, 242, 0.85));
  border-left: 3px solid #c9a028;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
  transition: all 0.3s ease;
}

.time-slot:hover {
  background: linear-gradient(135deg, rgba(255, 255, 255, 1), rgba(248, 246, 242, 0.95));
  transform: translateX(5px);
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.08);
}

.slot-label {
  color: #8b6914;
  font-size: 0.95rem;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.slot-time {
  color: #8b6914;
  font-size: 1.1rem;
  font-weight: 500;
  font-family: 'Courier New', monospace;
}

/* Location Section */
.location-section {
  margin-bottom: 6rem;
  opacity: 0;
  animation: fadeInUp 1s ease-out 1.5s forwards;
}

.location-header {
  text-align: center;
  margin-bottom: 3rem;
}

.header-ornament {
  color: #c9a028;
  font-size: 1.8rem;
  margin-bottom: 1rem;
}

.location-header h2 {
  font-family: 'Lora', Georgia, serif;
  font-size: 2.5rem;
  color: #8b6914;
  font-weight: 400;
  margin-bottom: 1rem;
  letter-spacing: 2px;
}

.header-divider {
  width: 80px;
  height: 2px;
  background: linear-gradient(90deg, transparent, #c9a028, transparent);
  margin: 0 auto;
}

.location-grid {
  display: grid;
  grid-template-columns: 1fr 1.5fr;
  /* gap: 2rem; */
  align-items: stretch;
}

.location-info {
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.address-box {
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.95), rgba(248, 246, 242, 0.9));
  /* border: 2px solid rgba(212, 175, 55, 0.3); */
  padding: 3rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  gap: 2rem;
  box-shadow:
    0 10px 40px rgba(0, 0, 0, 0.08),
    0 0 0 1px rgba(212, 175, 55, 0.1) inset;
  height: 100%;
  justify-content: center;
}

.address-icon {
  color: #c9a028;
  flex-shrink: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 1rem;
}

.address-icon svg {
  color: #c9a028;
  width: 48px;
  height: 48px;
}

.address-content {
  width: 100%;
}

.address-content h3 {
  font-family: 'Lora', Georgia, serif;
  color: #8b6914;
  font-size: 1.8rem;
  font-weight: 500;
  margin-bottom: 1.5rem;
  letter-spacing: 1px;
}

.address-content p {
  color: #2c2416;
  font-size: 1.1rem;
  line-height: 1.8;
  font-weight: 300;
  margin-bottom: 0.5rem;
}

.address {
  font-size: 1.3rem;
  color: #8b6914;
  font-weight: 500;
  margin-bottom: 0.8rem;
}

.city {
  font-size: 1.15rem;
  color: #4a4032;
  margin-bottom: 1rem;
}

.note {
  font-style: italic;
  color: #8b6914;
  margin-top: 1rem;
  padding-top: 1rem;
  border-top: 1px solid rgba(212, 175, 55, 0.2);
}

/* Map */
.map-container {
  min-height: 450px;
  /* border: 3px solid rgba(212, 175, 55, 0.3); */
  overflow: hidden;
  position: relative;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.1);
}

.map-container::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  border: 10px solid rgba(212, 175, 55, 0.03);
  pointer-events: none;
  z-index: 1;
}

/* CTA Section */
.cta-section {
  text-align: center;
  padding: 5rem 3rem;
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.95), rgba(248, 246, 242, 0.9));
  border: 2px solid rgba(212, 175, 55, 0.3);
  opacity: 0;
  animation: fadeInUp 1s ease-out 1.9s forwards;
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

.cta-buttons {
  display: flex;
  gap: 1.5rem;
  justify-content: center;
  flex-wrap: wrap;
}

.cta-button {
  display: inline-block;
  padding: 1rem 3rem;
  text-decoration: none;
  font-weight: 600;
  font-size: 1rem;
  letter-spacing: 1px;
  transition: all 0.3s ease;
  position: relative;
  overflow: hidden;
}

.cta-button.primary {
  background: linear-gradient(135deg, #e19b1d, #c9a028);
  color: #ffffff;
  box-shadow: 0 5px 20px rgba(201, 160, 40, 0.3);
}

.cta-button.secondary {
  background: transparent;
  color: #8b6914;
  border: 2px solid #c9a028;
  box-shadow: 0 3px 15px rgba(0, 0, 0, 0.05);
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
}

.cta-button.primary:hover {
  box-shadow: 0 10px 35px rgba(201, 160, 40, 0.4);
}

.cta-button.secondary:hover {
  background: rgba(201, 160, 40, 0.1);
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.08);
}

/* ==================== RESPONSIVE ==================== */
@media (max-width: 968px) {
  .content-section {
    padding: 3rem 1.5rem;
  }

  .info-grid {
    grid-template-columns: 1fr;
    gap: 2rem;
    margin-bottom: 3rem;
  }

  .location-grid {
    grid-template-columns: 1fr;
    gap: 2rem;
    /* border: 3px solid rgba(212, 175, 55, 0.3); */
  }

  .map-container {
    min-height: 350px;
  }

  .cta-buttons {
    flex-direction: column;
    align-items: stretch;
  }

  .cta-button {
    width: 100%;
    max-width: 400px;
    margin: 0 auto;
  }
}

@media (max-width: 640px) {
  .hero-contacts {
    height: 100vh;
  }

  .hero-content {
    padding: 2rem 1.5rem;
  }

  .info-card {
    padding: 3rem 2rem;
  }

  .contact-link {
    font-size: 1.1rem;
  }

  .address-box {
    padding: 2rem 1.5rem;
  }

  .address-icon svg {
    width: 40px;
    height: 40px;
  }

  .address-content h3 {
    font-size: 1.5rem;
  }

  .address {
    font-size: 1.1rem;
  }

  .city {
    font-size: 1rem;
  }

  .map-container {
    min-height: 300px;
  }

  .cta-section {
    padding: 3rem 1.5rem;
  }

  .cta-section h3 {
    font-size: 2rem;
  }
}
</style>
