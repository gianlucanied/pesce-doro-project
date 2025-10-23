<script setup>
import { ref } from 'vue'
import { RouterLink, RouterView } from 'vue-router'

const mobileMenuOpen = ref(false)

const toggleMobileMenu = () => {
  mobileMenuOpen.value = !mobileMenuOpen.value
}
</script>

<template>
  <div class="page-wrapper">
    <header>
      <div class="header-ornament-top"></div>
      <div class="header-content">
        <div class="logo">
          <RouterLink to="/" @click="mobileMenuOpen = false">
            <img src="/public/images.png" alt="Il Pesce d'Oro" class="logo-img" />
          </RouterLink>
        </div>

        <nav class="desktop-nav">
          <RouterLink to="/" class="nav-link">Home</RouterLink>
          <RouterLink to="/about" class="nav-link">Chi Siamo</RouterLink>
          <RouterLink to="/contacts" class="nav-link">Contatti</RouterLink>
          <a href="#prenota" class="btn-prenota">Prenota Ora</a>
        </nav>

        <button class="mobile-menu-btn" @click="toggleMobileMenu" aria-label="Menu">
          <span :class="{ open: mobileMenuOpen }"></span>
          <span :class="{ open: mobileMenuOpen }"></span>
          <span :class="{ open: mobileMenuOpen }"></span>
        </button>
      </div>

      <div class="mobile-nav" :class="{ open: mobileMenuOpen }">
        <RouterLink to="/" class="mobile-nav-link" @click="toggleMobileMenu">Home</RouterLink>
        <RouterLink to="/about" class="mobile-nav-link" @click="toggleMobileMenu"
          >Chi Siamo</RouterLink
        >
        <RouterLink to="/contacts" class="mobile-nav-link" @click="toggleMobileMenu"
          >Contatti</RouterLink
        >
        <a href="#prenota" class="mobile-nav-link" @click="toggleMobileMenu">Prenota Ora</a>
      </div>
    </header>

    <main>
      <RouterView />
    </main>

    <footer>
      <div class="footer-ornament">⚜</div>

      <div class="footer-content">
        <div class="footer-section footer-brand">
          <img src="/public/images.png" alt="Il Pesce d'Oro" class="footer-logo" />
          <p class="footer-tagline">Tradizione e sapori mediterranei dal 1985</p>
          <div class="footer-divider"></div>
        </div>

        <div class="footer-grid">
          <div class="footer-column">
            <h4>Navigazione</h4>
            <div class="column-divider"></div>
            <RouterLink to="/">Home</RouterLink>
            <RouterLink to="/about">Chi Siamo</RouterLink>
            <RouterLink to="/contacts">Contatti</RouterLink>
          </div>

          <div class="footer-column">
            <h4>Orari di Apertura</h4>
            <div class="column-divider"></div>
            <p class="day-range">Martedì - Domenica</p>
            <p class="hours">12:00 - 15:00</p>
            <p class="hours">19:00 - 23:00</p>
            <p class="closed">◆ Lunedì chiuso</p>
          </div>

          <div class="footer-column">
            <h4>Dove Trovarci</h4>
            <div class="column-divider"></div>
            <p>Via Roma, 123</p>
            <p>07041 Alghero (SS)</p>
            <p class="contact-info">☎ +39 079 123 4567</p>
            <p class="contact-info">✉ info@pescedoro.it</p>
          </div>

          <div class="footer-column">
            <h4>Seguici</h4>
            <div class="column-divider"></div>
            <div class="social-links">
              <a href="#" aria-label="Facebook" class="social-link">
                <svg
                  width="18"
                  height="18"
                  viewBox="0 0 24 24"
                  fill="none"
                  stroke="currentColor"
                  stroke-width="2"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                >
                  <path d="M18 2h-3a5 5 0 0 0-5 5v3H7v4h3v8h4v-8h3l1-4h-4V7a1 1 0 0 1 1-1h3z" />
                </svg>
              </a>
              <a href="#" aria-label="Instagram" class="social-link">
                <svg
                  width="18"
                  height="18"
                  viewBox="0 0 24 24"
                  fill="none"
                  stroke="currentColor"
                  stroke-width="2"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                >
                  <rect x="2" y="2" width="20" height="20" rx="5" ry="5" />
                  <path d="M16 11.37A4 4 0 1 1 12.63 8 4 4 0 0 1 16 11.37z" />
                  <line x1="17.5" y1="6.5" x2="17.51" y2="6.5" />
                </svg>
              </a>
              <a href="#" aria-label="TripAdvisor" class="social-link">
                <svg
                  width="18"
                  height="18"
                  viewBox="0 0 24 24"
                  fill="none"
                  stroke="currentColor"
                  stroke-width="2"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                >
                  <circle cx="12" cy="12" r="10" />
                  <circle cx="12" cy="12" r="3" />
                </svg>
              </a>
            </div>
            <p class="social-text">Condividi la tua esperienza</p>
          </div>
        </div>
      </div>

      <div class="footer-bottom">
        <div class="footer-bottom-divider"></div>
        <p>&copy; 2025 Il Pesce d'Oro - Ristorante Pizzeria Alghero</p>
        <p class="legal">Tutti i diritti riservati | P.IVA 12345678901</p>
      </div>
    </footer>
  </div>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Playfair+Display:wght@300;400;500;600;700&display=swap');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.page-wrapper {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  background-color: #0a0a0a;
  color: #fff;
  font-family: 'Playfair Display', 'Georgia', serif;
}

/* ==================== HEADER ==================== */
header {
  background: #0a0a0a;
  position: sticky;
  top: 0;
  z-index: 1000;
  border-bottom: 1px solid rgba(212, 175, 55, 0.2);
}

.header-ornament-top {
  height: 2px;
  background: linear-gradient(90deg, transparent, #d4af37, transparent);
}

.header-content {
  max-width: 1400px;
  margin: 0 auto;
  padding: 1.5rem 3rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo a {
  display: block;
  transition: opacity 0.3s ease;
}

.logo a:hover {
  opacity: 0.85;
}

.logo-img {
  height: 65px;
  width: auto;
  display: block;
  filter: drop-shadow(0 0 10px rgba(212, 175, 55, 0.2));
}

.desktop-nav {
  display: flex;
  gap: 3rem;
  align-items: center;
}

.nav-link {
  color: #e0e0e0;
  text-decoration: none;
  font-size: 1rem;
  font-weight: 400;
  letter-spacing: 1px;
  position: relative;
  padding: 0.5rem 0;
  transition: color 0.3s ease;
}

.nav-link::before {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 0;
  height: 1px;
  background: #d4af37;
  transition: width 0.3s ease;
}

.nav-link:hover {
  color: #d4af37;
}

.nav-link:hover::before {
  width: 100%;
}

.nav-link.router-link-active {
  color: #d4af37;
}

.nav-link.router-link-active::before {
  width: 100%;
}

.btn-prenota {
  background: linear-gradient(135deg, #d4af37, #c9a028);
  color: #0a0a0a;
  padding: 0.8rem 2rem;
  border: none;
  text-decoration: none;
  font-weight: 600;
  font-size: 0.9rem;
  letter-spacing: 1px;
  transition: all 0.3s ease;
  position: relative;
  overflow: hidden;
}

.btn-prenota::before {
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

.btn-prenota:hover::before {
  width: 300px;
  height: 300px;
}

.btn-prenota:hover {
  transform: translateY(-2px);
  box-shadow: 0 5px 20px rgba(212, 175, 55, 0.4);
}

/* Mobile Menu Button */
.mobile-menu-btn {
  display: none;
  flex-direction: column;
  gap: 5px;
  background: none;
  border: none;
  cursor: pointer;
  padding: 0.5rem;
}

.mobile-menu-btn span {
  width: 28px;
  height: 2px;
  background: #d4af37;
  transition: all 0.3s ease;
}

.mobile-menu-btn span.open:nth-child(1) {
  transform: rotate(45deg) translate(6px, 6px);
}

.mobile-menu-btn span.open:nth-child(2) {
  opacity: 0;
}

.mobile-menu-btn span.open:nth-child(3) {
  transform: rotate(-45deg) translate(7px, -7px);
}

/* Mobile Navigation */
.mobile-nav {
  max-height: 0;
  overflow: hidden;
  transition: max-height 0.4s cubic-bezier(0.4, 0, 0.2, 1);
  background: #0a0a0a;
  border-top: 1px solid rgba(212, 175, 55, 0.1);
}

.mobile-nav.open {
  max-height: 500px;
}

.mobile-nav-link {
  display: block;
  color: #e0e0e0;
  text-decoration: none;
  padding: 1.2rem 3rem;
  font-size: 1rem;
  font-weight: 400;
  letter-spacing: 1px;
  transition: all 0.3s ease;
  border-bottom: 1px solid rgba(212, 175, 55, 0.05);
}

.mobile-nav-link:hover {
  background: rgba(212, 175, 55, 0.05);
  color: #d4af37;
  padding-left: 3.5rem;
}

.mobile-nav-link.router-link-active {
  background: rgba(212, 175, 55, 0.08);
  color: #d4af37;
}

/* ==================== MAIN ==================== */
main {
  flex: 1;
  width: 100%;
}

/* ==================== FOOTER ==================== */
footer {
  background: #0a0a0a;
  margin-top: auto;
  border-top: 1px solid rgba(212, 175, 55, 0.2);
  position: relative;
}

.footer-ornament {
  text-align: center;
  color: #d4af37;
  font-size: 2rem;
  padding: 2rem 0 1rem;
  opacity: 0.6;
}

.footer-content {
  max-width: 1400px;
  margin: 0 auto;
  padding: 2rem 3rem 3rem;
}

.footer-section {
  margin-bottom: 3rem;
}

.footer-brand {
  text-align: center;
}

.footer-logo {
  height: 90px;
  width: auto;
  margin: 0 auto 1.5rem;
  display: block;
  filter: drop-shadow(0 0 15px rgba(212, 175, 55, 0.2));
}

.footer-tagline {
  color: rgba(224, 224, 224, 0.7);
  font-size: 1rem;
  font-weight: 300;
  letter-spacing: 0.5px;
  line-height: 1.6;
  font-style: italic;
}

.footer-divider {
  width: 100px;
  height: 1px;
  background: linear-gradient(90deg, transparent, #d4af37, transparent);
  margin: 2rem auto 3rem;
}

.footer-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 3rem;
}

.footer-column {
  text-align: left;
}

.footer-column h4 {
  color: #d4af37;
  font-size: 0.95rem;
  margin-bottom: 1rem;
  font-weight: 600;
  letter-spacing: 1px;
}

.column-divider {
  width: 40px;
  height: 1px;
  background: #d4af37;
  margin-bottom: 1.2rem;
}

.footer-column a,
.footer-column p {
  color: rgba(224, 224, 224, 0.65);
  text-decoration: none;
  font-size: 0.9rem;
  line-height: 2;
  font-weight: 300;
  transition: all 0.3s ease;
  display: block;
}

.footer-column a:hover {
  color: #d4af37;
  padding-left: 8px;
}

.day-range {
  color: rgba(224, 224, 224, 0.8);
  font-weight: 400;
  margin-bottom: 0.5rem;
}

.footer-column .hours {
  color: rgba(224, 224, 224, 0.7);
  font-weight: 300;
  line-height: 1.8;
}

.footer-column .closed {
  color: #d4af37;
  font-style: italic;
  margin-top: 0.8rem;
  font-size: 0.85rem;
}

.footer-column .contact-info {
  color: rgba(224, 224, 224, 0.75);
  font-weight: 400;
}

.social-links {
  display: flex;
  gap: 0.8rem;
  margin-bottom: 1rem;
}

.social-link {
  color: #d4af37;
  width: 38px;
  height: 38px;
  display: flex;
  align-items: center;
  justify-content: center;
  border: 1px solid rgba(212, 175, 55, 0.3);
  transition: all 0.3s ease;
  position: relative;
}

.social-link::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: #d4af37;
  transform: scale(0);
  transition: transform 0.3s ease;
}

.social-link:hover {
  border-color: #d4af37;
}

.social-link:hover::before {
  transform: scale(1);
}

.social-link:hover svg {
  position: relative;
  z-index: 1;
  color: #0a0a0a;
}

.social-text {
  font-size: 0.8rem;
  color: rgba(224, 224, 224, 0.5);
  font-style: italic;
}

/* Footer Bottom */
.footer-bottom {
  padding: 2rem 3rem;
  text-align: center;
}

.footer-bottom-divider {
  width: 200px;
  height: 1px;
  background: linear-gradient(90deg, transparent, rgba(212, 175, 55, 0.3), transparent);
  margin: 0 auto 2rem;
}

.footer-bottom p {
  color: rgba(224, 224, 224, 0.45);
  font-size: 0.85rem;
  font-weight: 300;
  letter-spacing: 0.5px;
}

.footer-bottom .legal {
  font-size: 0.75rem;
  margin-top: 0.5rem;
  color: rgba(224, 224, 224, 0.35);
}

/* ==================== RESPONSIVE ==================== */
@media (max-width: 1200px) {
  .footer-grid {
    grid-template-columns: repeat(2, 1fr);
    gap: 2.5rem;
  }
}

@media (max-width: 968px) {
  .desktop-nav {
    display: none;
  }

  .mobile-menu-btn {
    display: flex;
  }

  .header-content {
    padding: 1.2rem 2rem;
  }

  .logo-img {
    height: 55px;
  }

  .footer-content {
    padding: 2rem 2rem 3rem;
  }

  .footer-grid {
    grid-template-columns: repeat(2, 1fr);
    gap: 2rem;
  }

  .footer-bottom {
    padding: 1.5rem 2rem;
  }
}

@media (max-width: 640px) {
  .header-content {
    padding: 1rem 1.5rem;
  }

  .mobile-nav-link {
    padding: 1rem 1.5rem;
  }

  .mobile-nav-link:hover {
    padding-left: 2rem;
  }

  .logo-img {
    height: 50px;
  }

  .footer-content {
    padding: 2rem 1.5rem 2rem;
  }

  .footer-logo {
    height: 70px;
  }

  .footer-grid {
    grid-template-columns: 1fr;
    gap: 2.5rem;
  }

  .footer-column {
    text-align: center;
  }

  .column-divider {
    margin-left: auto;
    margin-right: auto;
  }

  .social-links {
    justify-content: center;
  }

  .footer-bottom {
    padding: 1.5rem;
  }

  .footer-bottom p {
    font-size: 0.8rem;
    line-height: 1.6;
  }
}

@media (min-width: 969px) {
  .mobile-nav {
    display: none;
  }
}
</style>
