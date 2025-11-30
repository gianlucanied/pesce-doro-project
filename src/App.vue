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

        <!-- Pulsante Download Menu - Desktop -->
        <a href="/menu.pdf" download class="btn-menu-download desktop-menu-btn">
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

        <nav class="desktop-nav">
          <RouterLink to="/" class="nav-link">{{ t('nav.home') }}</RouterLink>
          <RouterLink to="/about" class="nav-link">{{ t('nav.about') }}</RouterLink>
          <RouterLink to="/contacts" class="btn-prenota">{{ t('nav.contacts') }}</RouterLink>

          <!-- Language Selector -->
          <div class="language-selector">
            <button
              @click="changeLanguage('it')"
              :class="{ active: locale === 'it' }"
              class="lang-btn"
              aria-label="Italiano"
            >
              🇮🇹
            </button>
            <button
              @click="changeLanguage('en')"
              :class="{ active: locale === 'en' }"
              class="lang-btn"
              aria-label="English"
            >
              🇬🇧
            </button>
            <button
              @click="changeLanguage('es')"
              :class="{ active: locale === 'es' }"
              class="lang-btn"
              aria-label="Español"
            >
              🇪🇸
            </button>
          </div>
        </nav>

        <button class="mobile-menu-btn" @click="toggleMobileMenu" :aria-label="t('common.menu')">
          <span :class="{ open: mobileMenuOpen }"></span>
          <span :class="{ open: mobileMenuOpen }"></span>
          <span :class="{ open: mobileMenuOpen }"></span>
        </button>
      </div>

      <div class="mobile-nav" :class="{ open: mobileMenuOpen }">
        <!-- Pulsante Download Menu - Mobile -->
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

/* ==================== HEADER ==================== */
header {
  background: linear-gradient(135deg, #0a0a0a 0%, #1a1410 100%);
  position: sticky;
  top: 0;
  z-index: 1000;
  border-bottom: 2px solid rgba(212, 175, 55, 0.4);
  box-shadow: 0 4px 20px rgba(212, 175, 55, 0.15);
}

.header-ornament-top {
  height: 3px;
  background: linear-gradient(90deg, transparent, #e19b1d, transparent);
  box-shadow: 0 0 10px rgba(212, 175, 55, 0.5);
}

.header-content {
  /* max-width: 1400px; */
  height: 100px;
  margin: 0 auto;
  padding: 0 3rem;
  display: flex;
  background-color: black;
  justify-content: space-between;
  align-items: center;
  /* background: linear-gradient(135deg, rgba(212, 175, 55, 0.03), transparent); */
}

.logo a {
  display: block;
  transition: all 0.3s ease;
}

.logo a:hover {
  opacity: 0.85;
  transform: scale(1.05);
}

.logo-img {
  height: 85px;
  width: auto;
  display: block;
}

/* ==================== DOWNLOAD MENU BUTTON ==================== */
.btn-menu-download {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  background: linear-gradient(135deg, rgba(212, 175, 55, 0.12), rgba(218, 165, 32, 0.06));
  border: 2px solid rgba(212, 175, 55, 0.4);
  color: #e19b1d;
  padding: 0.7rem 1.5rem;
  text-decoration: none;
  font-weight: 500;
  font-size: 0.9rem;
  letter-spacing: 1px;
  transition: all 0.3s ease;
  border-radius: 2px;
  box-shadow: 0 2px 10px rgba(212, 175, 55, 0.15);
}

.btn-menu-download svg {
  transition: transform 0.3s ease;
}

.btn-menu-download:hover {
  background: linear-gradient(135deg, rgba(212, 175, 55, 0.2), rgba(218, 165, 32, 0.12));
  border-color: #e19b1d;
  transform: translateY(-2px);
  box-shadow: 0 4px 15px rgba(212, 175, 55, 0.3);
  color: #ffa500;
  text-shadow: 0 0 10px rgba(212, 175, 55, 0.4);
}

.btn-menu-download:hover svg {
  transform: translateY(3px);
}

/* Mobile Menu Download Button */
.mobile-menu-download {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.8rem;
  background: linear-gradient(135deg, rgba(212, 175, 55, 0.15), rgba(218, 165, 32, 0.08));
  border: none;
  border-bottom: 2px solid rgba(212, 175, 55, 0.3);
  color: #e19b1d;
  padding: 1.5rem 3rem;
  text-decoration: none;
  font-size: 1rem;
  font-weight: 500;
  letter-spacing: 1px;
  transition: all 0.3s ease;
  font-family: 'Lora', 'Georgia', serif;
}

.mobile-menu-download:hover {
  background: linear-gradient(135deg, rgba(212, 175, 55, 0.25), rgba(218, 165, 32, 0.15));
  color: #ffa500;
  padding-left: 3.5rem;
  text-shadow: 0 0 8px rgba(212, 175, 55, 0.3);
}

.mobile-menu-download svg {
  transition: transform 0.3s ease;
}

.mobile-menu-download:hover svg {
  transform: translateY(3px);
}

.desktop-nav {
  display: flex;
  gap: 3rem;
  align-items: center;
}

.nav-link {
  color: #e6c77f;
  text-decoration: none;
  font-size: 1rem;
  font-weight: 400;
  letter-spacing: 1px;
  position: relative;
  padding: 0.5rem 0;
  transition: all 0.3s ease;
}

.nav-link::before {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 0;
  height: 2px;
  background: linear-gradient(90deg, #e19b1d, #ffa500);
  transition: width 0.3s ease;
  box-shadow: 0 0 8px rgba(212, 175, 55, 0.5);
}

.nav-link:hover {
  color: #e19b1d;
  text-shadow: 0 0 10px rgba(212, 175, 55, 0.3);
}

.nav-link:hover::before {
  width: 100%;
}

.nav-link.router-link-active {
  color: #e19b1d;
  text-shadow: 0 0 10px rgba(212, 175, 55, 0.3);
}

.nav-link.router-link-active::before {
  width: 100%;
}

.btn-prenota {
  background: linear-gradient(135deg, #e19b1d, #c9a028);
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
  box-shadow: 0 4px 15px rgba(212, 175, 55, 0.3);
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
  box-shadow: 0 6px 25px rgba(212, 175, 55, 0.5);
}

/* ==================== LANGUAGE SELECTOR ==================== */
.language-selector {
  display: flex;
  gap: 0.5rem;
  align-items: center;
  padding-left: 1rem;
  border-left: 2px solid rgba(212, 175, 55, 0.3);
}

.lang-btn {
  background: linear-gradient(135deg, rgba(212, 175, 55, 0.08), transparent);
  border: 2px solid rgba(212, 175, 55, 0.3);
  color: #e6c77f;
  padding: 0.5rem 0.7rem;
  font-size: 1.2rem;
  cursor: pointer;
  transition: all 0.3s ease;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(212, 175, 55, 0.1);
}

.lang-btn:hover {
  border-color: #e19b1d;
  background: linear-gradient(135deg, rgba(212, 175, 55, 0.15), rgba(218, 165, 32, 0.1));
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(212, 175, 55, 0.25);
}

.lang-btn.active {
  border-color: #e19b1d;
  background: linear-gradient(135deg, rgba(212, 175, 55, 0.2), rgba(218, 165, 32, 0.15));
  box-shadow: 0 0 15px rgba(212, 175, 55, 0.4);
}

/* Mobile Language Selector */
.mobile-language-selector {
  display: flex;
  flex-direction: column;
  gap: 0;
  border-top: 2px solid rgba(212, 175, 55, 0.3);
  margin-top: 1rem;
  padding-top: 1rem;
  background: linear-gradient(135deg, rgba(212, 175, 55, 0.05), transparent);
}

.mobile-lang-btn {
  background: transparent;
  border: none;
  color: #e6c77f;
  padding: 1rem 3rem;
  font-size: 1rem;
  font-weight: 400;
  letter-spacing: 1px;
  cursor: pointer;
  text-align: left;
  transition: all 0.3s ease;
  border-bottom: 1px solid rgba(212, 175, 55, 0.1);
  font-family: 'Lora', 'Georgia', serif;
}

.mobile-lang-btn:hover {
  background: linear-gradient(135deg, rgba(212, 175, 55, 0.1), transparent);
  color: #e19b1d;
  padding-left: 3.5rem;
  text-shadow: 0 0 8px rgba(212, 175, 55, 0.3);
}

.mobile-lang-btn.active {
  background: linear-gradient(135deg, rgba(212, 175, 55, 0.15), rgba(218, 165, 32, 0.08));
  color: #e19b1d;
  border-left: 4px solid #e19b1d;
  box-shadow: inset 0 0 15px rgba(212, 175, 55, 0.2);
}

/* Mobile Menu Button */
.mobile-menu-btn {
  display: none;
  flex-direction: column;
  background: linear-gradient(135deg, rgba(212, 175, 55, 0.1), transparent);
  border: 2px solid rgba(212, 175, 55, 0.3);
  cursor: pointer;
  padding: 0.6rem;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(212, 175, 55, 0.15);
  position: relative;
  width: 45px;
  height: 45px;
  justify-content: center;
  align-items: center;
  gap: 0;
}

.mobile-menu-btn span {
  width: 25px;
  height: 2px;
  background: linear-gradient(90deg, #e19b1d, #ffa500);
  transition: all 0.3s ease;
  box-shadow: 0 0 5px rgba(212, 175, 55, 0.4);
  display: block;
  position: absolute;
}

.mobile-menu-btn span:nth-child(1) {
  top: 12px;
}

.mobile-menu-btn span:nth-child(2) {
  top: 50%;
  transform: translateY(-50%);
}

.mobile-menu-btn span:nth-child(3) {
  bottom: 12px;
}

/* Stato APERTO - forma la X */
.mobile-menu-btn span.open:nth-child(1) {
  top: 50%;
  transform: translateY(-50%) rotate(45deg);
}

.mobile-menu-btn span.open:nth-child(2) {
  opacity: 0;
  transform: translateY(-50%) scale(0);
}

.mobile-menu-btn span.open:nth-child(3) {
  bottom: 50%;
  transform: translateY(50%) rotate(-45deg);
}

.mobile-menu-btn:hover {
  border-color: #e19b1d;
  background: linear-gradient(135deg, rgba(212, 175, 55, 0.15), rgba(218, 165, 32, 0.1));
  box-shadow: 0 4px 12px rgba(212, 175, 55, 0.25);
}

/* Mobile Navigation */
.mobile-nav {
  max-height: 0;
  overflow: hidden;
  transition: max-height 0.4s cubic-bezier(0.4, 0, 0.2, 1);
  background: linear-gradient(135deg, #0a0a0a, #1a1410);
  border-top: 2px solid rgba(212, 175, 55, 0.2);
}

.mobile-nav.open {
  max-height: 800px;
  box-shadow: inset 0 10px 20px rgba(212, 175, 55, 0.1);
}

.mobile-nav-link {
  display: block;
  color: #e6c77f;
  text-decoration: none;
  padding: 1.2rem 3rem;
  font-size: 1rem;
  font-weight: 400;
  letter-spacing: 1px;
  transition: all 0.3s ease;
  border-bottom: 1px solid rgba(212, 175, 55, 0.1);
}

.mobile-nav-link:hover {
  background: linear-gradient(135deg, rgba(212, 175, 55, 0.1), transparent);
  color: #e19b1d;
  padding-left: 3.5rem;
  text-shadow: 0 0 8px rgba(212, 175, 55, 0.3);
}

.mobile-nav-link.router-link-active {
  background: linear-gradient(135deg, rgba(212, 175, 55, 0.15), rgba(218, 165, 32, 0.08));
  color: #e19b1d;
  border-left: 4px solid #e19b1d;
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

  .desktop-menu-btn {
    display: none;
  }

  .header-content {
    padding: 1.2rem 2rem;
  }

  .logo-img {
    height: 70px;
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

  .mobile-lang-btn {
    padding: 1rem 1.5rem;
  }

  .mobile-lang-btn:hover {
    padding-left: 2rem;
  }

  .mobile-menu-download {
    padding: 1.5rem 1.5rem;
  }

  .mobile-menu-download:hover {
    padding-left: 2rem;
  }

  .logo-img {
    height: 60px;
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
