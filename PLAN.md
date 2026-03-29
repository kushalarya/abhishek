# Website Redesign Plan: Abhishek Shaw Portfolio

## Design Principles (Inspired by RECOMMENDATION.md)

### Color Philosophy
- **Energetic but Not Pop**: Use muted, deeper tones instead of neon colors
- **Athlete Branding**: Colors represent endurance sports (Swim, Bike, Run)
- **60-30-10 Rule**: 60% dark base, 30% one main color, 10% accent highlight
- **Activated Colors**: Use muted default states, highlight active/progress states
- **Strategic Color Usage**: Only combine all 3 colors in special moments (hero, gradients)

### Refined Color Palette
```css
/* Base Colors */
--palette-primary: #000025;    /* 60% - Dark base */
--palette-surface: #0A0B2E;    /* Surface for depth */
--palette-card: #12133A;       /* Card backgrounds */
--palette-border: #1E204A;     /* Subtle borders */

/* Sport Colors (30% - One at a time) */
--palette-swim: #3AA6D0;       /* Deep water blue */
--palette-bike: #C9A227;       /* Warm gold */
--palette-run: #D94A3A;        /* Burnt red */

/* Text Hierarchy */
--palette-text: #E6E8F2;       /* Primary text */
--palette-muted: #8A8FB2;      /* Secondary text */

/* Special Combinations */
--gradient-hero: linear-gradient(90deg, #3AA6D0, #C9A227, #D94A3A);
```

### Color Usage Strategy
- **Hero Section**: Use all 3 colors in gradient for impact
- **Individual Sections**: One sport color per section
- **Default State**: Muted colors (#8A8FB2)
- **Active State**: Full sport color when engaged
- **Progression**: Visual flow from Swim → Bike → Run

## Current State Analysis

### HTML Structure
- Single-page layout with Barba.js data attributes
- Sections: home-header, home-intro, work-tiles, footer
- Interactive elements: magnetic buttons, sticky cursor, lazy images

### CSS Styles
- Dark theme (#000025, white text, yellow accent)
- Custom font (Boxing-Regular.woff2)
- Flexbox grid system
- Rounded div transitions
- Dots pattern background

### JavaScript Dependencies & Animations
- **GSAP**: Timeline animations, tweens
- **ScrollTrigger**: Scroll-based animations
- **Locomotive Scroll**: Smooth scrolling
- **Barba.js**: Page transitions
- **LazyLoad**: Image loading
- **jQuery**: DOM manipulation

#### Animation Types
1. Loading screens with rounded div morphing
2. Scroll-triggered text slides, fades, rotations
3. Magnetic button effects
4. Horizontal text rolling ("SWIM • BIKE • RUN")
5. Parallax scrolling effects
6. Page transition animations

## Proposed Modifications

### 1. No Loader Needed
- Remove loading screen animations
- Simplify initial page load to direct content display
- Keep content immediately visible

### 2. Dependency Analysis
**Can Remove:**
- **Barba.js**: Not needed for single-page site
- **Locomotive Scroll**: Replace with CSS `scroll-behavior: smooth`
- **GSAP & ScrollTrigger**: Replace with CSS animations/transitions

**Keep (if beneficial):**
- **LazyLoad**: Still useful for performance
- **jQuery**: Can be replaced with vanilla JS or removed entirely

### 3. Dual Theme Not Needed
- Remove theme switching functionality
- Stick to single refined dark theme with athlete color palette
- Simplify CSS by removing theme classes

### 4. Hamburger Menu Required
- Add responsive hamburger navigation
- Implement mobile menu overlay
- Use CSS-only solution where possible

### 5. Header Arrow Not Needed
- Remove rotating arrow element
- Simplify header design

### 6. Navigation Items
Add navigation menu with:
- Timeline (link to achievements section)
- Contact (link to footer/contact section)
- Possibly Home/Projects if expanding

### 7. Magnetic Animations Not Needed
- Remove magnetic button effects
- Use standard hover states with CSS transitions

### 8. Scroll Effects Not Needed
- Remove complex scroll-triggered animations
- Keep simple fade-ins if needed, but prefer static design
- Remove parallax effects

### 9. Utility Functions Not Needed
- Remove touch detection, viewport height handling
- Simplify to essential functionality only
- Remove CLS debugging and complex resize handlers

### 10. Mobile-Friendly Design
- Implement responsive design with CSS Grid/Flexbox
- Ensure proper touch targets (44px minimum)
- Test on various device sizes
- Use CSS media queries for breakpoints
- Maintain desktop experience while optimizing mobile

## New Architecture

### HTML Approach: Semantic-first (update added)
- Use semantic HTML tags for pages sections to maximize accessibility + SEO:
  - `<header>` for page header
  - `<nav>` for navigation
  - `<main>`, `<section>`, `<article>` for content
  - `<footer>` for contact/copyright
- Use `<div>` only for visual/layout wrappers when there's no semantic equivalent.
- Keep class names for style/behavior only (`.hero`, `.timeline`, `.work-grid`).

### HTML Structure (Semantic)
```html
<header class="hero">
  <nav class="main-nav">
    <div class="nav-brand">Abhishek Shaw</div>
    <button class="hamburger" aria-label="Menu">
      <span></span><span></span><span></span>
    </button>
    <ul class="nav-menu">
      <li><a href="#timeline">Timeline</a></li>
      <li><a href="#contact">Contact</a></li>
    </ul>
  </nav>
  <section class="hero-content">
    <!-- Hero content with gradient text -->
    <h1 class="hero-title">
      <span class="swim active">SWIM</span>
      <span class="spacer">•</span>
      <span class="bike">BIKE</span>
      <span class="spacer">•</span>
      <span class="run">RUN</span>
    </h1>
  </section>
</header>

<main>
  <section id="timeline" class="achievements">
    <!-- Achievements/timeline with sport-specific colors -->
  </section>
  <section class="work">
    <!-- Work tiles -->
  </section>
</main>

<footer id="contact" class="contact">
  <!-- Contact info -->
</footer>
```

### CSS Approach
- **Modern CSS**: Grid, Flexbox, Custom Properties
- **Color System**: Athlete-themed palette with activation states
- **Animations**: CSS keyframes, transitions
- **Responsive**: Mobile-first with container queries
- **Performance**: Critical CSS, optimized fonts/images

### JavaScript (Minimal)
- Only for progressive enhancement
- Hamburger menu toggle
- Lazy loading (if kept)
- Basic interactivity

## Implementation Phases (detailed)

### Phase 1 - Audit and Cleanup
- Locate and remove the following from `index.html`:
  - `<script defer src="https://unpkg.com/@barba/core"></script>`
  - `<script defer src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.9.1/gsap.min.js"></script>` and ScrollTrigger
  - `<script defer src="assets/js/locomotive-scroll.min.js"></script>`
  - `data-barba`, `data-scroll-section`, `data-scroll-speed` attributes
  - `theme-dark` class wrapper on sections
- In `assets/css/site.css`, remove/disable `.main`, `.main-wrap`, and `.section[data-scroll]` classes from locomotive setup.
- In `assets/js/index-new.js`, remove/or comment out `barba.init`, `initSmoothScroll`, `initScrolltriggerAnimations`, and loader functions.

### Phase 2 - Core HTML rebuilding
- Build hero block inside `index.html`:
  - include `<header class="hero">`, `.main-nav`, `.hamburger`, `.nav-menu`, and `.hero-content`
  - replace existing `.home-header` and `.big-name` structure with simpler text
- Build stable sections from existing content:
  - `#timeline` (from `.home-intro` text block)
  - `.work-grid` (from `.work-tiles-home ul li`, convert to card markup)
  - `#contact` from existing footer CTA
- Use existing copy (TATA Ultra Marathon, Ironman, etc.) for timeline & cards.

### Phase 3 - Full CSS replacement + theme
- Add root variables at top of `assets/css/site.css`:
  - `--palette-primary`, `--palette-surface`, `--palette-card`, etc.
- Create main new sections:
  - `.hero` (full screen, gradient background, center text)
  - `.hero-title span` with `.active` logic
  - `.achievements .timeline-card`
  - `.work-grid` and `.work-card`
  - `.contact-callout`
- Remove old `.rounded-div` and `.overlay` states from legacy styles.
- Add `@media` breakpoints:
  - 320–720 (mobile), 721–1024 (tablet), 1025+ (desktop)
- Add reduced motion support with `@media (prefers-reduced-motion: reduce)`.

### Phase 4 - Minimal JS and interactivity
- Rewrite `assets/js/index-new.js` to simple script:
  - toggling class `menu-open` on `.nav-menu` and `.hamburger`
  - closing menu on click outside
  - optional `document.querySelectorAll('[data-lazy]').forEach...` or use native `loading="lazy"` for images
- Remove jQuery and utility functions from JS and from `index.html` imports.

### Phase 5 - Testing and QA
- Verify performance and lints:
  - `index.html` loads with no 404s
  - no JS console errors
  - all interactive nav links work
  - mobile layout: nav, hero, timeline, work, contact
- Compare current and new UX consistency
- Validate meets success criteria

### Bonus Phase - polish
- Add a simple active item state to `SWIM/Bike/RUN` (CSS with `.active` class applied in HTML)
- Add a full `timeline` progressive indicator scroll effect using CSS (no JS), e.g. `scroll-snap` and `position: sticky` on headings.
- Replace existing heavy background images with optimized `img` + `loading="lazy"`.

## Content & Configuration Decisions (Finalized)

### 1. Hero Text (Refined Recommendation)
**Current:** "Triathlete • Ultra Cyclist"  
**Recommended refined:**
```
Endurance Athlete & Ultra Cyclist
From Kolkata to Kanchenjunga
```
*or*
```
Swim. Bike. Run.
620+ km. One mission.
```

### 2. Race/Record Timeline Structure
Replace static "achievements list" with expanded timeline:
```
- TATA Ultra Marathon 2025 (600+ km)
- Kanchenjunga Ultra Cycling Challenge (in progress)
- Ironman 70.3 Goa 2024 (7h 15m)
- Ironman 70.3 Goa 2023 (7h 42m)
- Half Marathon PB: 1:30
- Marathon PB: 3:20
- Decathlon Cycling Technician (current)
```
Use `.timeline-card` with date + distance + status indicators.

### 3. Service/Product Portfolio (converted from work tiles)
Replace generic links with athlete-focused services:
```
- Workshop: Triathlete 101 → Service card
- Workshop: Cycling 101 → Service card
- 1:1 Coaching (₹1200/hr) → Product card
- Strava Group → Community link
```
Structure: `.work-grid` with `.service-card` and `product-card` classes.

### 4. Avatar Image
Keep current `assets/img/profile_circular_notion.png` (painted style portrait).

### 5. Image Optimization: WebP + Fallback Strategy
```html
<picture>
  <source srcset="assets/img/optimized/hero.webp" type="image/webp">
  <img src="assets/img/optimized/hero.jpg" alt="...">
</picture>
```
Convert existing `.jpg` tiles to `.webp` using ImageOptim or TinyPNG.

### 6. Navigation Structure
Add nav items (in order):
```
- Home (anchor #hero)
- Timeline (anchor #timeline)
- Work (anchor #work)
- About (anchor #about) ← NEW
- Contact (anchor #contact)
```

### 7. "Get in Touch" CTA
**Keep existing:** Keep button and its CSS hover animation (no JS animation).  
Structure in footer as:
```html
<div class="contact-cta">
  <a href="mailto:abhishekshaw@gmail.com" class="btn btn-primary">
    Get in touch
  </a>
</div>
```

### 8. Section Reveal Animation (CSS-only, no JS)
Use CSS `@keyframes` + `IntersectionObserver` (lightweight):
- Fade-in + subtle upward slide on scroll into view
- No parallax, no GSAP
- Respects `prefers-reduced-motion`

### 9. Image Lazy Loading: NATIVE RECOMMENDATION
**Use native `loading="lazy"`** (modern browsers 90%+ support):
```html
<img src="..." loading="lazy" alt="...">
```
✅ Pros: No dependency, built-in, performant  
❌ Cons: Older IE/Opera not supported (acceptable for portfolio)  
**Recommendation:** Drop LazyLoad.js entirely, use native `loading="lazy"`.

### 10. Deployment Target
- **Primary:** Vercel (auto-deploy from GitHub)
- **Secondary:** GitHub Pages (fallback)
- Set base path to root `/` (Vercel default)

### 11. Remove Analytics
Remove from `index.html`:
```html
<!-- REMOVE: Vercel Speed Insights script -->
<script>
  window.si = window.si || function () { (window.siq = window.siq || []).push(arguments); };
</script>
<script defer src="/_vercel/speed-insights/script.js"></script>
```

## Success Criteria
- ✅ Loads instantly without loader
- ✅ Athlete-themed color palette creates progression and focus
- ✅ Works on all device sizes
- ✅ Clean, maintainable code
- ✅ Fast performance
- ✅ Accessible navigation
- ✅ Professional endurance athlete branding</content>
<parameter name="filePath">c:\Users\91750\Workspace\abhishek\abhishek\PLAN.md