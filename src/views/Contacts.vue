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
  <div class="contacts-page" :class="{ visible: isVisible }">
    <!-- Hero Section -->
    <section class="hero-contacts">
      <div class="hero-overlay"></div>
      <div class="hero-content">
        <div class="ornament">⚜</div>
        <h1 class="main-title">Contatti</h1>
        <div class="title-divider"></div>
        <p class="subtitle">Siamo qui per voi</p>
      </div>
    </section>

    <!-- Main Content -->
    <section class="content-section">
      <div class="container">
        <!-- Info Cards Grid -->
        <div class="info-grid">
          <!-- Contact Info Card -->
          <div class="info-card contact-card">
            <h2>Info & Contatti</h2>
            <div class="card-divider"></div>

            <div class="contact-item">
              <h4>Telefono</h4>
              <a href="tel:+39079952602" class="contact-link">+39 079 952 602</a>
            </div>

            <div class="contact-item">
              <h4>Email</h4>
              <a href="mailto:info@pescedoroalghero.it" class="contact-link"
                >info@pescedoroalghero.it</a
              >
            </div>

            <div class="contact-item">
              <h4>Giorni di Chiusura</h4>
              <p class="closure-info">
                <span class="closure-day">Mercoledì</span> tutto il giorno<br />
                <span class="closure-day">Giovedì</span> la mattina
              </p>
            </div>
          </div>

          <!-- Hours Card -->
          <div class="info-card hours-card">
            <h2>Orari di Apertura</h2>
            <div class="card-divider"></div>

            <div class="hours-item">
              <div class="day-label">Martedì - Domenica</div>
              <div class="time-slots">
                <div class="time-slot">
                  <span class="slot-label">Pranzo</span>
                  <span class="slot-time">12:00 - 15:00</span>
                </div>
                <div class="time-slot">
                  <span class="slot-label">Cena</span>
                  <span class="slot-time">19:00 - 23:00</span>
                </div>
              </div>
            </div>

            <div class="closed-notice">◆ Lunedì chiuso</div>
          </div>
        </div>

        <!-- Location Section -->
        <div class="location-section">
          <div class="location-header">
            <div class="header-ornament">◆</div>
            <h2>Dove Siamo</h2>
            <div class="header-divider"></div>
          </div>

          <div class="location-grid">
            <!-- Location Info -->
            <div class="location-info">
              <div class="location-text">
                <p class="intro-text">
                  La posizione del nostro Ristorante è ideale per chi vuole cercare un tranquillo
                  punto di ristoro all'insegna della genuinità e della cucina casereccia.
                </p>

                <div class="address-box">
                  <div class="address-content">
                    <h3>Indirizzo</h3>
                    <p class="address">Via Catalogna n°12</p>
                    <p class="city">07041 Alghero (SS)</p>
                    <p class="note">A soli 2 passi dal porto</p>
                  </div>
                </div>
              </div>
            </div>

            <!-- Map -->
            <div class="map-container">
              <iframe
                src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d2992.3622847654586!2d8.31622!3d40.55823!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x12da3425c9f3e9e9%3A0x9e6e8e9f3e9e9e9e!2sVia%20Catalogna%2C%2007041%20Alghero%20SS!5e0!3m2!1sit!2sit!4v1234567890"
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

        <!-- Tradition Section -->
        <div class="tradition-section">
          <div class="tradition-content">
            <div class="tradition-icon">★</div>
            <h3>Itinerari del Gusto</h3>
            <div class="tradition-divider"></div>
            <p class="tradition-text">
              Al Pesce d'oro è facile lasciarsi incantare dai sapori della Terra di Sardegna
              mediante degustazioni guidate e selezionate, alla scoperta dei prodotti tipici locali
              e di produzione; insomma dei veri e propri "Itinerari del Gusto", per richiamare
              suggestioni, profumi antichi e far rivivere la tradizione.
            </p>
          </div>
        </div>

        <!-- CTA Section -->
        <div class="cta-section">
          <div class="cta-ornament">⚜</div>
          <h3>Prenota il Tuo Tavolo</h3>
          <p>Vivi un'esperienza culinaria indimenticabile</p>
          <div class="cta-buttons">
            <a href="tel:+39079952602" class="cta-button primary">Chiama Ora</a>
            <a href="mailto:info@pescedoroalghero.it" class="cta-button secondary">Invia Email</a>
          </div>
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

.contacts-page {
  background: #0a0a0a;
  min-height: 100vh;
  opacity: 0;
  transition: opacity 1s ease-out;
}

.contacts-page.visible {
  opacity: 1;
}

/* ==================== HERO SECTION ==================== */
.hero-contacts {
  position: relative;
  height: 50vh;
  min-height: 350px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(135deg, #0a0a0a 0%, #1a1a1a 100%);
  overflow: hidden;
}

.hero-contacts::before {
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

/* Info Grid */
.info-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 2.5rem;
  margin-bottom: 5rem;
}

.info-card {
  background: rgba(212, 175, 55, 0.02);
  border: 1px solid rgba(212, 175, 55, 0.2);
  padding: 3rem;
  transition: all 0.4s ease;
  opacity: 0;
  animation: fadeInUp 1s ease-out forwards;
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
  border-color: rgba(212, 175, 55, 0.4);
  transform: translateY(-5px);
}

.card-icon {
  font-size: 2.5rem;
  margin-bottom: 1.5rem;
}

.info-card h2 {
  font-family: 'Playfair Display', Georgia, serif;
  font-size: 2rem;
  color: #d4af37;
  font-weight: 500;
  margin-bottom: 1rem;
  letter-spacing: 1px;
}

.card-divider {
  width: 50px;
  height: 2px;
  background: #d4af37;
  margin-bottom: 2rem;
}

.contact-item {
  margin-bottom: 2rem;
}

.contact-item:last-child {
  margin-bottom: 0;
}

.contact-item h4 {
  color: rgba(224, 224, 224, 0.6);
  font-size: 0.85rem;
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 2px;
  margin-bottom: 0.5rem;
}

.contact-link {
  color: #d4af37;
  text-decoration: none;
  font-size: 1.3rem;
  font-weight: 400;
  transition: all 0.3s ease;
  display: inline-block;
}

.contact-link:hover {
  color: #ffa500;
  transform: translateX(5px);
}

.closure-info {
  color: rgba(224, 224, 224, 0.7);
  font-size: 1.05rem;
  line-height: 1.8;
  font-weight: 300;
}

.closure-day {
  color: #d4af37;
  font-weight: 500;
}

/* Hours Card */
.hours-item {
  margin-bottom: 2rem;
}

.day-label {
  color: rgba(224, 224, 224, 0.8);
  font-size: 1.1rem;
  font-weight: 400;
  margin-bottom: 1rem;
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
  background: rgba(212, 175, 55, 0.05);
  border-left: 2px solid #d4af37;
}

.slot-label {
  color: rgba(224, 224, 224, 0.7);
  font-size: 0.95rem;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.slot-time {
  color: #d4af37;
  font-size: 1.1rem;
  font-weight: 500;
  font-family: 'Courier New', monospace;
}

.closed-notice {
  color: #d4af37;
  font-size: 0.95rem;
  font-style: italic;
  text-align: center;
  padding-top: 1rem;
  border-top: 1px solid rgba(212, 175, 55, 0.2);
}

/* Location Section */
.location-section {
  margin-bottom: 5rem;
  opacity: 0;
  animation: fadeInUp 1s ease-out 1.5s forwards;
}

.location-header {
  text-align: center;
  margin-bottom: 3rem;
}

.header-ornament {
  color: #d4af37;
  font-size: 1.8rem;
  margin-bottom: 1rem;
}

.location-header h2 {
  font-family: 'Playfair Display', Georgia, serif;
  font-size: 2.5rem;
  color: #d4af37;
  font-weight: 400;
  margin-bottom: 1rem;
  letter-spacing: 2px;
}

.header-divider {
  width: 80px;
  height: 2px;
  background: linear-gradient(90deg, transparent, #d4af37, transparent);
  margin: 0 auto;
}

.location-grid {
  display: grid;
  grid-template-columns: 1fr 1.2fr;
  gap: 3rem;
  align-items: stretch;
}

.location-info {
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.intro-text {
  color: rgba(224, 224, 224, 0.75);
  font-size: 1.05rem;
  line-height: 1.9;
  font-weight: 300;
  margin-bottom: 2rem;
}

.address-box {
  background: linear-gradient(135deg, rgba(212, 175, 55, 0.08), rgba(218, 165, 32, 0.03));
  border: 1px solid rgba(212, 175, 55, 0.3);
  padding: 2rem;
  display: flex;
  gap: 1.5rem;
  margin-bottom: 2rem;
}

.address-icon {
  font-size: 2.5rem;
  flex-shrink: 0;
}

.address-content h3 {
  font-family: 'Playfair Display', Georgia, serif;
  color: #d4af37;
  font-size: 1.3rem;
  font-weight: 500;
  margin-bottom: 0.8rem;
  letter-spacing: 1px;
}

.address-content p {
  color: rgba(224, 224, 224, 0.8);
  font-size: 1.05rem;
  line-height: 1.6;
  font-weight: 300;
}

.address {
  font-size: 1.2rem;
  color: #d4af37;
  font-weight: 400;
}

.note {
  font-style: italic;
  color: rgba(224, 224, 224, 0.65);
  margin-top: 0.5rem;
}

.accessibility {
  color: rgba(224, 224, 224, 0.7);
  font-size: 0.95rem;
  line-height: 1.6;
  font-weight: 300;
  font-style: italic;
}

/* Map */
.map-container {
  min-height: 400px;
  border: 2px solid rgba(212, 175, 55, 0.3);
  overflow: hidden;
  position: relative;
}

.map-container::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  border: 10px solid rgba(10, 10, 10, 0.2);
  pointer-events: none;
  z-index: 1;
}

/* Tradition Section */
.tradition-section {
  margin-bottom: 5rem;
  opacity: 0;
  animation: fadeInUp 1s ease-out 1.7s forwards;
}

.tradition-content {
  background: linear-gradient(135deg, rgba(10, 10, 10, 0.8), rgba(20, 20, 20, 0.6));
  border: 1px solid rgba(212, 175, 55, 0.3);
  padding: 4rem 3rem;
  text-align: center;
  position: relative;
}

.tradition-content::before {
  content: '';
  position: absolute;
  top: 15px;
  left: 15px;
  right: 15px;
  bottom: 15px;
  border: 1px solid rgba(212, 175, 55, 0.1);
  pointer-events: none;
}

.tradition-icon {
  font-size: 2.5rem;
  color: #d4af37;
  margin-bottom: 1.5rem;
}

.tradition-content h3 {
  font-family: 'Playfair Display', Georgia, serif;
  font-size: 2.5rem;
  color: #d4af37;
  font-weight: 400;
  margin-bottom: 1.5rem;
  letter-spacing: 2px;
}

.tradition-divider {
  width: 80px;
  height: 2px;
  background: linear-gradient(90deg, transparent, #d4af37, transparent);
  margin: 1.5rem auto;
}

.tradition-text {
  font-size: 1.15rem;
  line-height: 2;
  color: rgba(224, 224, 224, 0.8);
  font-weight: 300;
  max-width: 900px;
  margin: 0 auto;
}

/* CTA Section */
.cta-section {
  text-align: center;
  padding: 4rem 2rem;
  background: linear-gradient(135deg, rgba(212, 175, 55, 0.05), rgba(218, 165, 32, 0.02));
  border: 1px solid rgba(212, 175, 55, 0.2);
  opacity: 0;
  animation: fadeInUp 1s ease-out 1.9s forwards;
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
  background: linear-gradient(135deg, #d4af37, #c9a028);
  color: #0a0a0a;
}

.cta-button.secondary {
  background: transparent;
  color: #d4af37;
  border: 2px solid #d4af37;
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
  box-shadow: 0 8px 25px rgba(212, 175, 55, 0.4);
}

.cta-button.secondary:hover {
  background: rgba(212, 175, 55, 0.1);
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
  }

  .map-container {
    min-height: 350px;
  }

  .tradition-content {
    padding: 3rem 2rem;
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
    height: 40vh;
  }

  .info-card {
    padding: 2rem;
  }

  .contact-link {
    font-size: 1.1rem;
  }

  .address-box {
    padding: 1.5rem;
    flex-direction: column;
    text-align: center;
  }

  .map-container {
    min-height: 300px;
  }

  .tradition-content {
    padding: 2.5rem 1.5rem;
  }

  .tradition-content h3 {
    font-size: 2rem;
  }

  .tradition-text {
    font-size: 1rem;
  }

  .cta-section {
    padding: 3rem 1.5rem;
  }

  .cta-section h3 {
    font-size: 2rem;
  }
}
</style>
