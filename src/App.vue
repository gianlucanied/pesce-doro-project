<script setup>
import { onMounted, ref } from 'vue'
import { useI18n } from 'vue-i18n'
import { RouterLink, RouterView } from 'vue-router'

const mobileMenuOpen = ref(false)
const { locale, t } = useI18n()

const toggleMobileMenu = () => {
  mobileMenuOpen.value = !mobileMenuOpen.value
}

const changeLanguage = (lang) => {
  locale.value = lang
  localStorage.setItem('language', lang)
  mobileMenuOpen.value = false
}

// Carica lingua salvata al mount
onMounted(() => {
  const savedLanguage = localStorage.getItem('language')
  if (savedLanguage) {
    locale.value = savedLanguage
  }
})
</script>

<template>
  <div class="page-wrapper">
    <header>
      <div class="header-ornament-top"></div>
      <div class="header-content">
        <div class="logo">
          <RouterLink to="/" @click="mobileMenuOpen = false">
            <img src="/image-copia.jpg" alt="Il Pesce d'Oro" class="logo-img" />
          </RouterLink>
        </div>

        <nav class="desktop-nav">
          <RouterLink to="/" class="nav-link">{{ t('nav.home') }}</RouterLink>
          <RouterLink to="/about" class="nav-link">{{ t('nav.about') }}</RouterLink>
          <RouterLink to="/contacts" class="btn-prenota">{{ t('nav.contacts') }}</RouterLink>

          <!-- Language Selector - Desktop con Dropdown -->
          <div class="language-selector">
            <div class="language-dropdown">
              <button class="current-lang-btn" aria-label="Select language">
                <span v-if="locale === 'it'">🇮🇹</span>
                <span v-if="locale === 'en'">🇬🇧</span>
                <span v-if="locale === 'es'">🇪🇸</span>
                <svg
                  class="dropdown-arrow"
                  width="12"
                  height="12"
                  viewBox="0 0 24 24"
                  fill="none"
                  stroke="currentColor"
                  stroke-width="2"
                >
                  <polyline points="6 9 12 15 18 9"></polyline>
                </svg>
              </button>

              <div class="language-dropdown-menu">
                <button
                  v-if="locale !== 'it'"
                  @click="changeLanguage('it')"
                  class="dropdown-lang-btn"
                >
                  🇮🇹 <span>Italiano</span>
                </button>
                <button
                  v-if="locale !== 'en'"
                  @click="changeLanguage('en')"
                  class="dropdown-lang-btn"
                >
                  🇬🇧 <span>English</span>
                </button>
                <button
                  v-if="locale !== 'es'"
                  @click="changeLanguage('es')"
                  class="dropdown-lang-btn"
                >
                  🇪🇸 <span>Español</span>
                </button>
              </div>
            </div>
          </div>
        </nav>

        <button class="mobile-menu-btn" @click="toggleMobileMenu" :aria-label="t('common.menu')">
          <span :class="{ open: mobileMenuOpen }"></span>
          <span :class="{ open: mobileMenuOpen }"></span>
          <span :class="{ open: mobileMenuOpen }"></span>
        </button>
      </div>

      <div class="mobile-nav" :class="{ open: mobileMenuOpen }">
        <!-- Pulsante Download Menu - Solo Mobile -->
        <a href="/menu.pdf" download class="mobile-menu-download" @click="mobileMenuOpen = false">
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
            <path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4" />
            <polyline points="7 10 12 15 17 10" />
            <line x1="12" y1="15" x2="12" y2="3" />
          </svg>
          <span>{{ t('nav.downloadMenu') }}</span>
        </a>

        <RouterLink to="/" class="mobile-nav-link" @click="toggleMobileMenu">
          {{ t('nav.home') }}
        </RouterLink>
        <RouterLink to="/about" class="mobile-nav-link" @click="toggleMobileMenu">
          {{ t('nav.about') }}
        </RouterLink>
        <RouterLink to="/contacts" class="mobile-nav-link" @click="toggleMobileMenu">
          {{ t('nav.contacts') }}
        </RouterLink>

        <!-- Language Selector Mobile -->
        <div class="mobile-language-selector">
          <button
            @click="changeLanguage('it')"
            :class="{ active: locale === 'it' }"
            class="mobile-lang-btn"
          >
            🇮🇹 Italiano
          </button>
          <button
            @click="changeLanguage('en')"
            :class="{ active: locale === 'en' }"
            class="mobile-lang-btn"
          >
            🇬🇧 English
          </button>
          <button
            @click="changeLanguage('es')"
            :class="{ active: locale === 'es' }"
            class="mobile-lang-btn"
          >
            🇪🇸 Español
          </button>
        </div>
      </div>
    </header>

    <main>
      <RouterView />
    </main>

    <footer>
      <div class="footer-ornament"></div>

      <div class="footer-content">
        <div class="footer-section footer-brand">
          <img src="/images1.png" alt="Il Pesce d'Oro" class="footer-logo" />
          <p class="footer-tagline">{{ t('footer.tagline') }}</p>
          <div class="footer-divider"></div>
        </div>

        <div class="footer-grid">
          <div class="footer-column">
            <h4>{{ t('footer.navigation') }}</h4>
            <div class="column-divider"></div>
            <RouterLink to="/">{{ t('nav.home') }}</RouterLink>
            <RouterLink to="/about">{{ t('nav.about') }}</RouterLink>
            <RouterLink to="/contacts">{{ t('nav.contacts') }}</RouterLink>
          </div>

          <div class="footer-column">
            <h4>{{ t('footer.openingHours') }}</h4>
            <div class="column-divider"></div>
            <p class="hours">12:30 - 14:30</p>
            <p class="hours">19:30 - 23:00</p>
          </div>

          <div class="footer-column">
            <h4>{{ t('footer.whereToFindUs') }}</h4>
            <div class="column-divider"></div>
            <p>{{ t('footer.address') }}</p>
            <p>{{ t('footer.city') }}</p>
            <p class="contact-info">☎ +39 079 952 602</p>
            <p class="contact-info">✉ info@pescedoroalghero.it</p>
          </div>

          <div class="footer-column">
            <h4>{{ t('footer.followUs') }}</h4>
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
            </div>
            <p class="social-text">{{ t('footer.shareExperience') }}</p>
          </div>
        </div>
      </div>

      <div class="footer-bottom">
        <div class="footer-bottom-divider"></div>
        <p>{{ t('footer.copyright') }}</p>
        <p class="legal">{{ t('footer.rights') }}</p>
      </div>
    </footer>
  </div>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Lora:wght@400;500;600;700&display=swap');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.page-wrapper {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  background: linear-gradient(135deg, #0a0a0a 0%, #1a1410 50%, #0a0a0a 100%);
  color: #fff;
  font-family: 'Lora', 'Georgia', serif;
}

/* ==================== HEADER MODERNO ==================== */
header {
  background: black;
  backdrop-filter: blur(10px);
  position: sticky;
  top: 0;
  z-index: 1000;
  border-bottom: 1px solid rgba(212, 175, 55, 0.2);
  box-shadow:
    0 8px 32px rgba(0, 0, 0, 0.4),
    0 2px 8px rgba(212, 175, 55, 0.1);
}

.header-ornament-top {
  height: 2px;
  background: linear-gradient(
    90deg,
    transparent 0%,
    rgba(225, 155, 29, 0.3) 25%,
    #e19b1d 50%,
    rgba(225, 155, 29, 0.3) 75%,
    transparent 100%
  );
  box-shadow: 0 0 20px rgba(212, 175, 55, 0.4);
  animation: shimmer 3s ease-in-out infinite;
}

@keyframes shimmer {
  0%,
  100% {
    opacity: 0.6;
  }
  50% {
    opacity: 1;
  }
}

.header-content {
  max-width: 1400px;
  height: 90px;
  margin: 0 auto;
  padding: 0 3rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
  position: relative;
}

.header-content::before {
  content: '';
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 100%;
  height: 100%;
  background: radial-gradient(ellipse at center, rgba(225, 155, 29, 0.03) 0%, transparent 70%);
  pointer-events: none;
}

.logo {
  position: relative;
  z-index: 2;
}

.logo a {
  display: block;
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
  position: relative;
}

.logo a::after {
  content: '';
  position: absolute;
  inset: -10px;
  background: radial-gradient(circle at center, rgba(225, 155, 29, 0.15) 0%, transparent 70%);
  opacity: 0;
  transition: opacity 0.4s ease;
  border-radius: 50%;
}

.logo a:hover::after {
  opacity: 1;
}

.logo a:hover {
  transform: translateY(-2px);
}

.logo-img {
  height: 75px;
  width: auto;
  display: block;
  transition: filter 0.4s ease;
}

.logo a:hover .logo-img {
  filter: drop-shadow(0 6px 20px rgba(225, 155, 29, 0.4));
}

/* ==================== MOBILE MENU DOWNLOAD BUTTON - NO HOVER ==================== */
.mobile-menu-download {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.8rem;
  background: linear-gradient(135deg, rgba(225, 155, 29, 0.12) 0%, rgba(225, 155, 29, 0.06) 100%);
  border: none;
  border-bottom: 1px solid rgba(212, 175, 55, 0.25);
  color: #e19b1d;
  padding: 1.5rem 2rem;
  text-decoration: none;
  font-size: 1rem;
  font-weight: 500;
  letter-spacing: 0.8px;
  font-family: 'Lora', 'Georgia', serif;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.05),
    0 2px 8px rgba(225, 155, 29, 0.1);
}

.mobile-menu-download svg {
  filter: drop-shadow(0 2px 6px rgba(225, 155, 29, 0.4));
  transition: transform 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.mobile-menu-download:active {
  background: linear-gradient(135deg, rgba(225, 155, 29, 0.18) 0%, rgba(225, 155, 29, 0.1) 100%);
  transform: scale(0.98);
}

.mobile-menu-download:active svg {
  transform: translateY(2px);
}

/* ==================== DESKTOP NAV MODERNO ==================== */
.desktop-nav {
  display: flex;
  gap: 2.5rem;
  align-items: center;
  position: relative;
  z-index: 2;
}

.nav-link {
  color: rgba(230, 199, 127, 0.9);
  text-decoration: none;
  font-size: 0.95rem;
  font-weight: 400;
  letter-spacing: 0.5px;
  position: relative;
  padding: 0.5rem 0;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.nav-link::before {
  content: '';
  position: absolute;
  bottom: -2px;
  left: 50%;
  transform: translateX(-50%);
  width: 0;
  height: 2px;
  background: linear-gradient(90deg, transparent, #e19b1d, transparent);
  transition: width 0.4s cubic-bezier(0.4, 0, 0.2, 1);
  box-shadow: 0 0 10px rgba(225, 155, 29, 0.5);
}

.nav-link::after {
  content: '';
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 0;
  height: 0;
  background: radial-gradient(circle, rgba(225, 155, 29, 0.1) 0%, transparent 70%);
  border-radius: 50%;
  transition: all 0.4s ease;
  opacity: 0;
}

.nav-link:hover::after {
  width: 120px;
  height: 120px;
  opacity: 1;
}

.nav-link:hover {
  color: #e19b1d;
  transform: translateY(-1px);
}

.nav-link:hover::before {
  width: 100%;
}

.nav-link.router-link-active {
  color: #e19b1d;
}

.nav-link.router-link-active::before {
  width: 100%;
}

/* ==================== BTN PRENOTA MODERNO ==================== */
.btn-prenota {
  background: linear-gradient(135deg, #e19b1d 0%, #d4af37 50%, #e19b1d 100%);
  background-size: 200% 200%;
  color: #0a0a0a;
  padding: 0.85rem 2.2rem;
  border: none;
  text-decoration: none;
  font-weight: 600;
  font-size: 0.9rem;
  letter-spacing: 0.5px;
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
  position: relative;
  overflow: hidden;
  box-shadow:
    0 4px 15px rgba(225, 155, 29, 0.3),
    inset 0 1px 0 rgba(255, 255, 255, 0.2);
  border-radius: 6px;
  animation: gradientShift 3s ease infinite;
}

@keyframes gradientShift {
  0%,
  100% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
}

.btn-prenota::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.3), transparent);
  transition: left 0.6s ease;
}

.btn-prenota:hover::before {
  left: 100%;
}

.btn-prenota:hover {
  transform: translateY(-3px);
  box-shadow:
    0 8px 25px rgba(225, 155, 29, 0.5),
    inset 0 1px 0 rgba(255, 255, 255, 0.3);
}

/* ==================== LANGUAGE SELECTOR MODERNO ==================== */
.language-selector {
  padding-left: 1.5rem;
  margin-left: 1rem;
  border-left: 1px solid rgba(225, 155, 29, 0.2);
}

.language-dropdown {
  position: relative;
}

.current-lang-btn {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  background: linear-gradient(135deg, rgba(225, 155, 29, 0.08) 0%, rgba(225, 155, 29, 0.04) 100%);
  border: 1.5px solid rgba(225, 175, 55, 0.25);
  color: #e6c77f;
  padding: 0.6rem 1rem;
  font-size: 1.2rem;
  cursor: pointer;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  border-radius: 6px;
  box-shadow:
    0 2px 8px rgba(225, 155, 29, 0.1),
    inset 0 1px 0 rgba(255, 255, 255, 0.05);
}

.dropdown-arrow {
  color: #e19b1d;
  transition: transform 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.current-lang-btn:hover {
  border-color: rgba(225, 155, 29, 0.4);
  background: linear-gradient(135deg, rgba(225, 155, 29, 0.12) 0%, rgba(225, 155, 29, 0.06) 100%);
  box-shadow:
    0 4px 12px rgba(225, 155, 29, 0.2),
    inset 0 1px 0 rgba(255, 255, 255, 0.08);
  transform: translateY(-1px);
}

.language-dropdown:hover .dropdown-arrow {
  transform: rotate(180deg);
}

/* Dropdown Menu Moderno */
.language-dropdown-menu {
  position: absolute;
  top: calc(100% + 0.8rem);
  right: 0;
  background: rgba(10, 10, 10, 0.98);
  backdrop-filter: blur(12px);
  border: 1.5px solid rgba(225, 155, 29, 0.3);
  border-radius: 8px;
  box-shadow:
    0 12px 40px rgba(0, 0, 0, 0.6),
    0 0 0 1px rgba(225, 155, 29, 0.1),
    inset 0 1px 0 rgba(255, 255, 255, 0.05);
  min-width: 160px;
  opacity: 0;
  visibility: hidden;
  transform: translateY(-10px) scale(0.95);
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  z-index: 1000;
  overflow: hidden;
}

.language-dropdown:hover .language-dropdown-menu {
  opacity: 1;
  visibility: visible;
  transform: translateY(0) scale(1);
}

.dropdown-lang-btn {
  display: flex;
  align-items: center;
  gap: 0.8rem;
  width: 100%;
  background: transparent;
  border: none;
  color: rgba(230, 199, 127, 0.9);
  padding: 1rem 1.3rem;
  font-size: 0.95rem;
  cursor: pointer;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  text-align: left;
  border-bottom: 1px solid rgba(225, 155, 29, 0.08);
  font-family: 'Lora', 'Georgia', serif;
  position: relative;
}

.dropdown-lang-btn::before {
  content: '';
  position: absolute;
  left: 0;
  top: 0;
  bottom: 0;
  width: 0;
  background: linear-gradient(90deg, rgba(225, 155, 29, 0.15) 0%, transparent 100%);
  transition: width 0.3s ease;
}

.dropdown-lang-btn:hover::before {
  width: 100%;
}

.dropdown-lang-btn:last-child {
  border-bottom: none;
}

.dropdown-lang-btn span {
  font-size: 0.9rem;
  font-weight: 400;
  letter-spacing: 0.3px;
  position: relative;
  z-index: 1;
}

.dropdown-lang-btn:hover {
  color: #e19b1d;
  padding-left: 1.8rem;
}

/* ==================== MOBILE LANGUAGE SELECTOR - NO HOVER ==================== */
.mobile-language-selector {
  display: flex;
  flex-direction: column;
  gap: 0;
  border-top: 1px solid rgba(225, 155, 29, 0.25);
  margin-top: 0.5rem;
  padding-top: 0.5rem;
  background: linear-gradient(135deg, rgba(225, 155, 29, 0.06) 0%, transparent 100%);
}

.mobile-lang-btn {
  background: transparent;
  border: none;
  color: rgba(230, 199, 127, 0.9);
  padding: 1.2rem 2rem;
  font-size: 1rem;
  font-weight: 400;
  letter-spacing: 0.6px;
  cursor: pointer;
  text-align: left;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  border-bottom: 1px solid rgba(225, 155, 29, 0.1);
  font-family: 'Lora', 'Georgia', serif;
  position: relative;
  display: flex;
  align-items: center;
  gap: 0.8rem;
}

.mobile-lang-btn::after {
  content: '';
  position: absolute;
  left: 0;
  top: 50%;
  transform: translateY(-50%);
  width: 3px;
  height: 0;
  background: linear-gradient(180deg, #e19b1d, #ffa500);
  transition: height 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  box-shadow: 0 0 8px rgba(225, 155, 29, 0.6);
}

.mobile-lang-btn.active {
  background: linear-gradient(
    90deg,
    rgba(225, 155, 29, 0.15) 0%,
    rgba(225, 155, 29, 0.05) 50%,
    transparent 100%
  );
  color: #e19b1d;
  box-shadow: inset 0 0 20px rgba(225, 155, 29, 0.1);
}

.mobile-lang-btn.active::after {
  height: 70%;
}

.mobile-lang-btn:active {
  background: linear-gradient(
    90deg,
    rgba(225, 155, 29, 0.2) 0%,
    rgba(225, 155, 29, 0.08) 50%,
    transparent 100%
  );
  transform: scale(0.98);
}

/* ==================== MOBILE MENU BUTTON MODERNO ==================== */
.mobile-menu-btn {
  display: none;
  flex-direction: column;
  background: linear-gradient(135deg, rgba(225, 155, 29, 0.1) 0%, rgba(225, 155, 29, 0.05) 100%);
  border: 1.5px solid rgba(225, 155, 29, 0.3);
  cursor: pointer;
  padding: 0.6rem;
  border-radius: 8px;
  box-shadow:
    0 2px 10px rgba(225, 155, 29, 0.2),
    inset 0 1px 0 rgba(255, 255, 255, 0.08);
  position: relative;
  width: 48px;
  height: 48px;
  justify-content: center;
  align-items: center;
  gap: 0;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.mobile-menu-btn:active {
  transform: scale(0.95);
  box-shadow:
    0 1px 5px rgba(225, 155, 29, 0.3),
    inset 0 1px 0 rgba(255, 255, 255, 0.05);
}

.mobile-menu-btn span {
  width: 26px;
  height: 2.5px;
  background: linear-gradient(90deg, #e19b1d, #ffa500);
  transition: all 0.4s cubic-bezier(0.68, -0.55, 0.265, 1.55);
  box-shadow: 0 0 8px rgba(225, 155, 29, 0.5);
  display: block;
  position: absolute;
  border-radius: 3px;
}

.mobile-menu-btn span:nth-child(1) {
  top: 13px;
}

.mobile-menu-btn span:nth-child(2) {
  top: 50%;
  transform: translateY(-50%);
}

.mobile-menu-btn span:nth-child(3) {
  bottom: 13px;
}

/* Stato APERTO - forma la X con animazione elastica */
.mobile-menu-btn span.open:nth-child(1) {
  top: 50%;
  transform: translateY(-50%) rotate(45deg);
  box-shadow: 0 0 12px rgba(225, 155, 29, 0.8);
}

.mobile-menu-btn span.open:nth-child(2) {
  opacity: 0;
  transform: translateY(-50%) scale(0) rotate(180deg);
}

.mobile-menu-btn span.open:nth-child(3) {
  bottom: 50%;
  transform: translateY(50%) rotate(-45deg);
  box-shadow: 0 0 12px rgba(225, 155, 29, 0.8);
}

/* ==================== MOBILE NAV CON ANIMAZIONI FLUIDE ==================== */
.mobile-nav {
  max-height: 0;
  overflow: hidden;
  transition:
    max-height 0.5s cubic-bezier(0.4, 0, 0.2, 1),
    opacity 0.4s ease,
    transform 0.4s cubic-bezier(0.4, 0, 0.2, 1);
  background: rgba(10, 10, 10, 0.98);
  backdrop-filter: blur(15px);
  border-top: 1px solid rgba(225, 155, 29, 0.15);
  opacity: 0;
  transform: translateY(-10px);
}

.mobile-nav.open {
  max-height: 800px;
  opacity: 1;
  transform: translateY(0);
  box-shadow:
    inset 0 10px 30px rgba(0, 0, 0, 0.4),
    inset 0 1px 0 rgba(225, 155, 29, 0.1);
}

/* Animazione staggered per i link */
.mobile-nav-link,
.mobile-menu-download {
  opacity: 0;
  transform: translateX(-20px);
  animation: none;
}

.mobile-nav.open .mobile-menu-download {
  animation: slideInLeft 0.4s cubic-bezier(0.4, 0, 0.2, 1) 0.1s forwards;
}

.mobile-nav.open .mobile-nav-link:nth-child(2) {
  animation: slideInLeft 0.4s cubic-bezier(0.4, 0, 0.2, 1) 0.15s forwards;
}

.mobile-nav.open .mobile-nav-link:nth-child(3) {
  animation: slideInLeft 0.4s cubic-bezier(0.4, 0, 0.2, 1) 0.2s forwards;
}

.mobile-nav.open .mobile-nav-link:nth-child(4) {
  animation: slideInLeft 0.4s cubic-bezier(0.4, 0, 0.2, 1) 0.25s forwards;
}

.mobile-nav.open .mobile-language-selector {
  animation: slideInLeft 0.4s cubic-bezier(0.4, 0, 0.2, 1) 0.3s forwards;
}

@keyframes slideInLeft {
  from {
    opacity: 0;
    transform: translateX(-20px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

.mobile-nav-link {
  display: block;
  color: rgba(230, 199, 127, 0.9);
  text-decoration: none;
  padding: 1.3rem 2rem;
  font-size: 1rem;
  font-weight: 400;
  letter-spacing: 0.6px;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  border-bottom: 1px solid rgba(225, 155, 29, 0.1);
  position: relative;
}

.mobile-nav-link::after {
  content: '';
  position: absolute;
  left: 0;
  top: 50%;
  transform: translateY(-50%);
  width: 3px;
  height: 0;
  background: linear-gradient(180deg, #e19b1d, #ffa500);
  transition: height 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  box-shadow: 0 0 8px rgba(225, 155, 29, 0.6);
}

.mobile-nav-link:active {
  background: linear-gradient(90deg, rgba(225, 155, 29, 0.15) 0%, transparent 100%);
  transform: scale(0.98);
}

.mobile-nav-link.router-link-active {
  background: linear-gradient(
    90deg,
    rgba(225, 155, 29, 0.15) 0%,
    rgba(225, 155, 29, 0.05) 50%,
    transparent 100%
  );
  color: #e19b1d;
  box-shadow: inset 0 0 20px rgba(225, 155, 29, 0.1);
}

.mobile-nav-link.router-link-active::after {
  height: 70%;
}

/* ==================== MAIN ==================== */
main {
  flex: 1;
  width: 100%;
}

/* ==================== FOOTER ==================== */
footer {
  background: linear-gradient(135deg, #0a0a0a 0%, #1a1410 100%);
  margin-top: auto;
  border-top: 3px solid rgba(212, 175, 55, 0.4);
  position: relative;
  box-shadow: 0 -4px 20px rgba(212, 175, 55, 0.15);
}

footer::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background:
    radial-gradient(circle at 30% 50%, rgba(212, 175, 55, 0.08) 0%, transparent 50%),
    radial-gradient(circle at 70% 50%, rgba(212, 175, 55, 0.08) 0%, transparent 50%);
  pointer-events: none;
}

.footer-ornament {
  text-align: center;
  color: #e19b1d;
  font-size: 2rem;
  padding: 2rem 0 1rem;
  opacity: 1;
  text-shadow: 0 0 20px rgba(212, 175, 55, 0.6);
  position: relative;
  z-index: 1;
}

.footer-content {
  max-width: 1400px;
  margin: 0 auto;
  padding: 2rem 3rem 3rem;
  position: relative;
  z-index: 1;
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
  filter: drop-shadow(0 0 20px rgba(212, 175, 55, 0.4));
}

.footer-tagline {
  color: #e6c77f;
  font-size: 1rem;
  font-weight: 300;
  letter-spacing: 0.5px;
  line-height: 1.6;
  font-style: italic;
}

.footer-divider {
  width: 100px;
  height: 2px;
  background: linear-gradient(90deg, transparent, #e19b1d, transparent);
  margin: 2rem auto 3rem;
  box-shadow: 0 0 10px rgba(212, 175, 55, 0.5);
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
  color: #e19b1d;
  font-size: 0.95rem;
  margin-bottom: 1rem;
  font-weight: 600;
  letter-spacing: 1px;
  text-shadow: 0 0 10px rgba(212, 175, 55, 0.3);
}

.column-divider {
  width: 40px;
  height: 2px;
  background: linear-gradient(90deg, #e19b1d, transparent);
  margin-bottom: 1.2rem;
  box-shadow: 0 0 8px rgba(212, 175, 55, 0.4);
}

.footer-column a,
.footer-column p {
  color: #e0e0e0;
  text-decoration: none;
  font-size: 0.9rem;
  line-height: 2;
  font-weight: 300;
  transition: all 0.3s ease;
  display: block;
}

.footer-column a:hover {
  color: #e19b1d;
  padding-left: 8px;
  text-shadow: 0 0 8px rgba(212, 175, 55, 0.3);
}

.day-range {
  color: #e6c77f;
  font-weight: 400;
  margin-bottom: 0.5rem;
}

.footer-column .hours {
  color: #e0e0e0;
  font-weight: 300;
  line-height: 1.8;
}

.footer-column .closed {
  color: #e19b1d;
  font-style: italic;
  margin-top: 0.8rem;
  font-size: 0.85rem;
  text-shadow: 0 0 8px rgba(212, 175, 55, 0.3);
}

.footer-column .contact-info {
  color: #e6c77f;
  font-weight: 400;
}

.social-links {
  display: flex;
  gap: 0.8rem;
  margin-bottom: 1rem;
}

.social-link {
  color: #e19b1d;
  width: 38px;
  height: 38px;
  display: flex;
  align-items: center;
  justify-content: center;
  border: 2px solid rgba(212, 175, 55, 0.4);
  transition: all 0.3s ease;
  position: relative;
  background: linear-gradient(135deg, rgba(212, 175, 55, 0.05), transparent);
  box-shadow: 0 2px 10px rgba(212, 175, 55, 0.1);
}

.social-link::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(135deg, #e19b1d, #c9a028);
  transform: scale(0);
  transition: transform 0.3s ease;
}

.social-link:hover {
  border-color: #e19b1d;
  box-shadow: 0 4px 15px rgba(212, 175, 55, 0.4);
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
  color: #e6c77f;
  font-style: italic;
}

/* Footer Bottom */
.footer-bottom {
  padding: 2rem 3rem;
  text-align: center;
  position: relative;
  z-index: 1;
  background: linear-gradient(135deg, rgba(212, 175, 55, 0.05), transparent);
}

.footer-bottom-divider {
  width: 200px;
  height: 2px;
  background: linear-gradient(90deg, transparent, rgba(212, 175, 55, 0.5), transparent);
  margin: 0 auto 2rem;
  box-shadow: 0 0 10px rgba(212, 175, 55, 0.4);
}

.footer-bottom p {
  color: #e6c77f;
  font-size: 0.85rem;
  font-weight: 300;
  letter-spacing: 0.5px;
}

.footer-bottom .legal {
  font-size: 0.75rem;
  margin-top: 0.5rem;
  color: rgba(230, 199, 127, 0.7);
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
    height: 80px;
  }

  .logo-img {
    height: 65px;
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
    height: 75px;
  }

  .mobile-nav-link {
    padding: 1.2rem 1.5rem;
  }

  .mobile-lang-btn {
    padding: 1.1rem 1.5rem;
  }

  .mobile-menu-download {
    padding: 1.4rem 1.5rem;
  }

  .logo-img {
    height: 55px;
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

  .mobile-menu-download {
    display: none;
  }
}
</style>
