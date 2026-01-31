# GitHub Pages Design System

En minimalistisk, mörk landing page för app-marknadsföring med flerspråksstöd.

---

## Översikt

- **Typ:** Statisk GitHub Pages-sida
- **Tema:** Dark mode (exklusivt)
- **Språk:** Engelska, Svenska, Spanska
- **Dependencies:** Inga (ren HTML, CSS, JS)

---

## Filstruktur

```
docs/
├── index.html          # Huvudsida
├── support.html        # Support/FAQ
├── privacy.html        # Integritetspolicy
├── styles.css          # Alla stilar
├── i18n.js             # Översättningar & språklogik
└── favicon.svg         # Ikon (SVG)
```

---

## Färgpalett

```css
:root {
  /* Bakgrunder */
  --color-background:        #0D0D0D;   /* Huvudbakgrund */
  --color-surface:           #1A1A1A;   /* Sektioner */
  --color-surface-elevated:  #242424;   /* Kort/upphöjda element */

  /* Accent */
  --color-accent:            #5B8FA8;   /* Primär interaktiv färg */
  --color-accent-hover:      #6BA0B9;   /* Hover-state */

  /* Text */
  --color-primary-text:      #F0F0F0;   /* Huvudtext */
  --color-secondary-text:    #A0A0A0;   /* Sekundär text */
  --color-muted-text:        #666666;   /* Tertiär text */
}
```

---

## Typografi

```css
:root {
  --font-display: -apple-system, BlinkMacSystemFont, 'SF Pro Display', system-ui, sans-serif;
  --font-body: -apple-system, BlinkMacSystemFont, 'SF Pro Text', system-ui, sans-serif;
}
```

### Storlekar

| Element | Storlek |
|---------|---------|
| H1 (Hero) | `clamp(2rem, 5vw, 3rem)` |
| H2 (Sektion) | `clamp(1.5rem, 4vw, 2rem)` |
| H3 (Kort) | `1.25rem` → `1.125rem` (mobil) |
| Body | `1.125rem` → `0.875rem` (mobil) |

---

## Spacing

```css
:root {
  --spacing-xs:   0.5rem;
  --spacing-sm:   1rem;
  --spacing-md:   1.5rem;
  --spacing-lg:   2rem;
  --spacing-xl:   3rem;
  --spacing-2xl:  5rem;

  --max-width:     1200px;  /* Container */
  --content-width: 800px;   /* Smalare innehåll */
}
```

---

## Sidstruktur

### HTML-mall

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="[Beskrivning]">

  <!-- Språkalternativ för SEO -->
  <link rel="alternate" hreflang="en" href="?lang=en">
  <link rel="alternate" hreflang="sv" href="?lang=sv">
  <link rel="alternate" hreflang="es" href="?lang=es">

  <link rel="icon" type="image/svg+xml" href="favicon.svg">
  <link rel="stylesheet" href="styles.css">
  <title>[Titel]</title>
</head>
<body>
  <nav class="navbar">...</nav>

  <section class="hero">...</section>
  <section class="features">...</section>
  <section class="how-it-works">...</section>
  <section class="disclaimer">...</section>
  <section class="download">...</section>

  <footer>...</footer>

  <script src="i18n.js"></script>
</body>
</html>
```

---

## Komponenter

### 1. Navbar

```html
<nav class="navbar">
  <div class="nav-content">
    <div class="logo">[App-namn]</div>
    <div class="language-switcher">
      <button class="lang-btn active" data-lang="en">EN</button>
      <button class="lang-btn" data-lang="sv">SV</button>
      <button class="lang-btn" data-lang="es">ES</button>
    </div>
  </div>
</nav>
```

```css
.navbar {
  position: fixed;
  top: 0;
  width: 100%;
  background: rgba(13, 13, 13, 0.9);
  backdrop-filter: blur(10px);
  z-index: 1000;
  padding: var(--spacing-sm) 0;
}

.lang-btn {
  background: transparent;
  border: 1px solid var(--color-accent);
  color: var(--color-accent);
  padding: 0.25rem 0.75rem;
  border-radius: 4px;
  cursor: pointer;
  transition: all 0.2s ease;
}

.lang-btn.active {
  background: var(--color-accent);
  color: var(--color-background);
}
```

### 2. Hero-sektion

```html
<section class="hero">
  <div class="hero-content">
    <h1 data-i18n="hero.title">[Rubrik]</h1>
    <p class="hero-subtitle" data-i18n="hero.subtitle">[Underrubrik]</p>
    <a href="#download" class="cta-button" data-i18n="hero.cta">[CTA-text]</a>
  </div>
  <div class="phone-mockup">
    <!-- Valfri app-preview -->
  </div>
</section>
```

```css
.hero {
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: calc(80px + var(--spacing-2xl)) var(--spacing-lg) var(--spacing-2xl);
}

.cta-button {
  display: inline-block;
  background: var(--color-accent);
  color: var(--color-background);
  padding: var(--spacing-sm) var(--spacing-lg);
  border-radius: 12px;
  text-decoration: none;
  font-weight: 600;
  transition: all 0.2s ease;
}

.cta-button:hover {
  background: var(--color-accent-hover);
  transform: translateY(-2px);
}
```

### 3. Feature-kort

```html
<section class="features">
  <div class="container">
    <div class="features-grid">
      <div class="feature-card">
        <span class="feature-icon">[Emoji]</span>
        <h3 data-i18n="features.item1.title">[Titel]</h3>
        <p data-i18n="features.item1.desc">[Beskrivning]</p>
      </div>
      <!-- Fler kort... -->
    </div>
  </div>
</section>
```

```css
.features-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: var(--spacing-lg);
}

.feature-card {
  background: var(--color-surface-elevated);
  padding: var(--spacing-xl);
  border-radius: 16px;
  text-align: center;
}

.feature-icon {
  font-size: 3rem;
  display: block;
  margin-bottom: var(--spacing-md);
}
```

### 4. Steg/Process

```html
<section class="how-it-works">
  <div class="container">
    <h2 data-i18n="howItWorks.title">[Sektionsrubrik]</h2>
    <div class="steps">
      <div class="step">
        <div class="step-number">1</div>
        <h3 data-i18n="howItWorks.step1.title">[Stegtitel]</h3>
        <p data-i18n="howItWorks.step1.desc">[Beskrivning]</p>
      </div>
      <!-- Fler steg... -->
    </div>
  </div>
</section>
```

```css
.steps {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: var(--spacing-xl);
}

.step-number {
  width: 48px;
  height: 48px;
  background: var(--color-accent);
  color: var(--color-background);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: bold;
  font-size: 1.25rem;
  margin: 0 auto var(--spacing-md);
}
```

### 5. Footer

```html
<footer>
  <div class="container">
    <div class="footer-links">
      <a href="support.html" data-i18n="footer.support">[Support]</a>
      <a href="privacy.html" data-i18n="footer.privacy">[Integritet]</a>
    </div>
    <p class="copyright" data-i18n="footer.copyright">[Copyright]</p>
  </div>
</footer>
```

```css
footer {
  background: var(--color-surface);
  padding: var(--spacing-xl) var(--spacing-lg);
  text-align: center;
}

.footer-links a {
  color: var(--color-secondary-text);
  text-decoration: none;
  margin: 0 var(--spacing-md);
  transition: color 0.2s ease;
}

.footer-links a:hover {
  color: var(--color-accent);
}
```

---

## Flerspråksstöd (i18n)

### Metod 1: Dynamisk (för index.html)

```javascript
const translations = {
  en: {
    "hero.title": "Your App Name",
    "hero.subtitle": "A short description",
    // ...
  },
  sv: {
    "hero.title": "Ditt appnamn",
    "hero.subtitle": "En kort beskrivning",
    // ...
  }
};

function setLanguage(lang) {
  document.querySelectorAll('[data-i18n]').forEach(el => {
    const key = el.getAttribute('data-i18n');
    if (translations[lang][key]) {
      el.textContent = translations[lang][key];
    }
  });

  document.documentElement.lang = lang;
  localStorage.setItem('preferred-lang', lang);
  window.history.replaceState({}, '', `?lang=${lang}`);

  // Uppdatera aktiv knapp
  document.querySelectorAll('.lang-btn').forEach(btn => {
    btn.classList.toggle('active', btn.dataset.lang === lang);
  });
}

function getPreferredLanguage() {
  const urlParams = new URLSearchParams(window.location.search);
  return urlParams.get('lang')
    || localStorage.getItem('preferred-lang')
    || navigator.language.split('-')[0]
    || 'en';
}

document.addEventListener('DOMContentLoaded', () => {
  setLanguage(getPreferredLanguage());

  document.querySelectorAll('.lang-btn').forEach(btn => {
    btn.addEventListener('click', () => setLanguage(btn.dataset.lang));
  });
});
```

### Metod 2: Statisk (för support.html, privacy.html)

```html
<div id="content-en" class="content-section">
  <!-- Engelskt innehåll -->
</div>
<div id="content-sv" class="content-section" style="display: none;">
  <!-- Svenskt innehåll -->
</div>
<div id="content-es" class="content-section" style="display: none;">
  <!-- Spanskt innehåll -->
</div>

<script>
function setLanguage(lang) {
  document.querySelectorAll('.content-section').forEach(el => {
    el.style.display = 'none';
  });
  document.getElementById(`content-${lang}`).style.display = 'block';
}
</script>
```

---

## Responsiv design

### Breakpoints

```css
/* Tablet */
@media (max-width: 768px) {
  .hero { flex-direction: column; text-align: center; }
  .features-grid { grid-template-columns: repeat(2, 1fr); }
}

/* Mobil */
@media (max-width: 480px) {
  .features-grid { grid-template-columns: 1fr; }
  .steps { grid-template-columns: 1fr; }
}
```

---

## Favicon (SVG)

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 32 32">
  <rect width="32" height="32" rx="6" fill="#0D0D0D"/>
  <circle cx="16" cy="14" r="8" fill="none" stroke="#5B8FA8" stroke-width="2"/>
  <path d="M11 17 Q16 22 21 17" fill="none" stroke="#5B8FA8" stroke-width="2" stroke-linecap="round"/>
</svg>
```

---

## Checklista för ny sida

- [ ] Kopiera filstrukturen (`docs/`)
- [ ] Uppdatera färgpalett i CSS-variabler
- [ ] Byt ut översättningar i `i18n.js`
- [ ] Ersätt favicon med egen ikon
- [ ] Uppdatera meta-taggar (title, description)
- [ ] Anpassa sektioner efter behov
- [ ] Testa alla tre språken
- [ ] Verifiera responsiv design
- [ ] Aktivera GitHub Pages i repo-inställningar

---

## Designprinciper

1. **Mörkt tema** - Minskar visuell stress
2. **Generöst whitespace** - Reducerar kognitiv belastning
3. **Emoji som ikoner** - Snabb rendering, inga bilder
4. **System-fonter** - Optimal prestanda
5. **Inga dependencies** - Omedelbar laddning
6. **Progressiv enhancement** - Fungerar utan JS
