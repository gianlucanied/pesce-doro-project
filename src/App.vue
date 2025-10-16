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
      <div class="header-content">
        <div class="logo">
          <RouterLink to="/" @click="mobileMenuOpen = false">
            <img src="https://i.imgur.com/8ZqK9Xo.png" alt="Il Pesce d'Oro" class="logo-img" />
          </RouterLink>
        </div>

        <nav class="desktop-nav">
          <RouterLink to="/" class="nav-link">Home</RouterLink>
          <RouterLink to="/about" class="nav-link">Chi Siamo</RouterLink>
          <RouterLink to="/menu" class="nav-link">Menu</RouterLink>
          <RouterLink to="/contacts" class="nav-link">Contatti</RouterLink>
          <a href="#prenota" class="btn-prenota">Prenota</a>
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
        <RouterLink to="/menu" class="mobile-nav-link" @click="toggleMobileMenu">Menu</RouterLink>
        <RouterLink to="/contacts" class="mobile-nav-link" @click="toggleMobileMenu"
          >Contatti</RouterLink
        >
        <a href="#prenota" class="mobile-nav-link" @click="toggleMobileMenu">Prenota</a>
      </div>
    </header>

    <main>
      <RouterView />
    </main>

    <footer>
      <div class="footer-top">
        <div class="footer-content">
          <div class="footer-brand">
            <img src="https://i.imgur.com/8ZqK9Xo.png" alt="Il Pesce d'Oro" class="footer-logo" />
            <p class="footer-tagline">Tradizione e autenticità dal 1985</p>
          </div>

          <div class="footer-links">
            <div class="footer-column">
              <h4>Navigazione</h4>
              <RouterLink to="/">Home</RouterLink>
              <RouterLink to="/about">Chi Siamo</RouterLink>
              <RouterLink to="/menu">Menu</RouterLink>
              <RouterLink to="/contacts">Contatti</RouterLink>
            </div>

            <div class="footer-column">
              <h4>Orari</h4>
              <p>Martedì - Domenica</p>
              <p class="hours">12:00 - 15:00</p>
              <p class="hours">19:00 - 23:00</p>
              <p class="closed">Lunedì chiuso</p>
            </div>

            <div class="footer-column">
              <h4>Contatti</h4>
              <p>Via Roma, 123</p>
              <p>10100 Torino</p>
              <p class="contact-info">+39 011 123 4567</p>
              <p class="contact-info">info@pescedoro.it</p>
            </div>

            <div class="footer-column">
              <h4>Seguici</h4>
              <div class="social-links">
                <a href="#" aria-label="Facebook">
                  <svg
                    width="20"
                    height="20"
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
                <a href="#" aria-label="Instagram">
                  <svg
                    width="20"
                    height="20"
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
                <a href="#" aria-label="TripAdvisor">
                  <svg
                    width="20"
                    height="20"
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
            </div>
          </div>
        </div>
      </div>

      <div class="footer-bottom">
        <p>&copy; 2025 Il Pesce d'Oro - Alghero. Tutti i diritti riservati. | P.IVA 12345678901</p>
      </div>
    </footer>
  </div>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Playfair+Display:wght@400;500;600;700&display=swap');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.page-wrapper {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  background-color: #000;
  color: #fff;
  font-family:
    'Inter',
    -apple-system,
    BlinkMacSystemFont,
    sans-serif;
}

/* HEADER */
header {
  background: rgba(0, 0, 0, 0.95);
  backdrop-filter: blur(20px);
  position: sticky;
  top: 0;
  z-index: 1000;
  border-bottom: 1px solid rgba(220, 152, 28, 0.15);
}

.header-content {
  max-width: 1600px;
  margin: 0 auto;
  padding: 1.2rem 3rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo a {
  display: block;
  transition:
    opacity 0.3s ease,
    transform 0.3s ease;
}

.logo a:hover {
  opacity: 0.85;
  transform: scale(1.02);
}

.logo-img {
  height: 60px;
  width: auto;
  display: block;
}

.desktop-nav {
  display: flex;
  gap: 2.5rem;
  align-items: center;
}

.nav-link {
  color: rgba(255, 255, 255, 0.85);
  text-decoration: none;
  font-size: 0.95rem;
  font-weight: 500;
  position: relative;
  padding: 0.5rem 0;
  transition: color 0.3s ease;
  letter-spacing: 0.3px;
}

.nav-link::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 0;
  height: 2px;
  background: #dc981c;
  transition: width 0.3s ease;
}

.nav-link:hover {
  color: #dc981c;
}

.nav-link:hover::after {
  width: 100%;
}

.nav-link.router-link-active {
  color: #dc981c;
}

.nav-link.router-link-active::after {
  width: 100%;
}

.btn-prenota {
  background: linear-gradient(135deg, #dc981c 0%, #b8761a 100%);
  color: #000;
  padding: 0.75rem 1.8rem;
  border-radius: 6px;
  text-decoration: none;
  font-weight: 600;
  font-size: 0.9rem;
  letter-spacing: 0.5px;
  transition: all 0.3s ease;
  box-shadow: 0 4px 15px rgba(220, 152, 28, 0.2);
}

.btn-prenota:hover {
  background: linear-gradient(135deg, #ffa500 0%, #dc981c 100%);
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(220, 152, 28, 0.35);
}

/* Mobile Menu Button */
.mobile-menu-btn {
  display: none;
  flex-direction: column;
  gap: 6px;
  background: none;
  border: none;
  cursor: pointer;
  padding: 0.5rem;
}

.mobile-menu-btn span {
  width: 26px;
  height: 2px;
  background: #dc981c;
  border-radius: 2px;
  transition: all 0.3s ease;
}

.mobile-menu-btn span.open:nth-child(1) {
  transform: rotate(45deg) translate(7px, 7px);
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
  background: rgba(0, 0, 0, 0.98);
}

.mobile-nav.open {
  max-height: 500px;
  border-top: 1px solid rgba(220, 152, 28, 0.15);
}

.mobile-nav-link {
  display: block;
  color: rgba(255, 255, 255, 0.85);
  text-decoration: none;
  padding: 1.2rem 3rem;
  font-size: 1rem;
  font-weight: 500;
  transition: all 0.3s ease;
  border-bottom: 1px solid rgba(255, 255, 255, 0.05);
}

.mobile-nav-link:hover {
  background: rgba(220, 152, 28, 0.08);
  color: #dc981c;
  padding-left: 3.5rem;
}

.mobile-nav-link.router-link-active {
  background: rgba(220, 152, 28, 0.12);
  color: #dc981c;
}

/* MAIN CONTENT */
main {
  flex: 1;
  width: 100%;
}

/* FOOTER */
footer {
  background: #000;
  margin-top: auto;
}

.footer-top {
  border-top: 1px solid rgba(220, 152, 28, 0.2);
  padding: 4rem 0 2rem;
}

.footer-content {
  max-width: 1600px;
  margin: 0 auto;
  padding: 0 3rem;
  display: grid;
  grid-template-columns: 1.2fr 2fr;
  gap: 4rem;
  align-items: start;
}

.footer-brand {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.footer-logo {
  height: 80px;
  width: auto;
}

.footer-tagline {
  color: rgba(255, 255, 255, 0.6);
  font-size: 0.9rem;
  font-weight: 400;
  letter-spacing: 0.3px;
  line-height: 1.6;
  max-width: 300px;
}

.footer-links {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 3rem;
}

.footer-column h4 {
  color: #dc981c;
  font-size: 0.85rem;
  margin-bottom: 1.2rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 1.5px;
}

.footer-column a,
.footer-column p {
  color: rgba(255, 255, 255, 0.65);
  text-decoration: none;
  font-size: 0.9rem;
  line-height: 2.2;
  font-weight: 400;
  transition: color 0.3s ease;
  display: block;
}

.footer-column a:hover {
  color: #dc981c;
  padding-left: 5px;
}

.footer-column .hours {
  color: rgba(255, 255, 255, 0.75);
  font-weight: 500;
  line-height: 1.8;
}

.footer-column .closed {
  color: rgba(220, 152, 28, 0.8);
  font-style: italic;
  margin-top: 0.5rem;
}

.footer-column .contact-info {
  color: rgba(255, 255, 255, 0.75);
  font-weight: 500;
}

.social-links {
  display: flex;
  gap: 0.8rem;
  margin-top: 0.5rem;
}

.social-links a {
  color: rgba(255, 255, 255, 0.65);
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  border: 1px solid rgba(220, 152, 28, 0.3);
  border-radius: 8px;
  transition: all 0.3s ease;
}

.social-links a:hover {
  background: #dc981c;
  border-color: #dc981c;
  color: #000;
  transform: translateY(-3px);
}

.footer-bottom {
  border-top: 1px solid rgba(255, 255, 255, 0.08);
  padding: 2rem 3rem;
  text-align: center;
}

.footer-bottom p {
  color: rgba(255, 255, 255, 0.4);
  font-size: 0.85rem;
  font-weight: 400;
}

/* RESPONSIVE */
@media (max-width: 1200px) {
  .footer-links {
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
    padding: 1rem 2rem;
  }

  .logo-img {
    height: 50px;
  }

  .footer-content {
    grid-template-columns: 1fr;
    gap: 3rem;
    padding: 0 2rem;
  }

  .footer-links {
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
    height: 45px;
  }

  .footer-top {
    padding: 3rem 0 1.5rem;
  }

  .footer-content {
    padding: 0 1.5rem;
  }

  .footer-links {
    grid-template-columns: 1fr;
    gap: 2rem;
  }

  .footer-column {
    text-align: center;
  }

  .footer-brand {
    align-items: center;
    text-align: center;
  }

  .footer-tagline {
    max-width: 100%;
  }

  .social-links {
    justify-content: center;
  }

  .footer-bottom {
    padding: 1.5rem;
  }

  .footer-bottom p {
    font-size: 0.75rem;
    line-height: 1.6;
  }
}

@media (min-width: 969px) {
  .mobile-nav {
    display: none;
  }
}
</style>
