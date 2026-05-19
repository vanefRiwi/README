# ★🎸🎧⋆｡ °⋆ SHATTERED RIFFS — Rock Band Landing Page

> Single-page promotional website for the rock band **Shattered Riffs** and their *Rock the Night Tour 2026*. Built with plain HTML, CSS, and a minimal amount of vanilla JavaScript. No frameworks, no build tools, no dependencies.

Live at: https://vreniz.github.io/rock-band/
---



## Overview

Shattered Riffs is a fully static, single-page site. The design system is driven by CSS custom properties declared once in `:root` and referenced throughout. Every interactive element — the mobile menu, the album flip cards, the gallery hover effects — is powered by CSS alone. JavaScript handles only two small behaviours that CSS cannot achieve on its own.

---

## 🛠️ Technologies Used

<img src="./assets/icons/html.svg" alt="HTML5 Icon" height="48"> &nbsp;
<img src="./assets/icons/css.svg" alt="CSS3 Icon" height="48"> &nbsp;
<img src="./assets/icons/javascript.svg" alt="JavaScript Icon" height="48">

- **HTML5** — Semantic structure with ARIA accessibility attributes
- **CSS3** — Custom properties, Flexbox, Grid, CSS transitions, responsive media queries
- **JavaScript ES6+** — Vanilla, no frameworks or libraries
- 🔤 [Google Fonts](https://fonts.google.com/) 
---

## Live Sections

| Anchor | Section | Description |
|---|---|---|
| `#hero` | Hero | Two-column layout with headline, CTA buttons, and an animated "Now Playing" badge card |
| `#tour` | Tour Dates | Horizontally-scrollable table of four concert dates |
| `#about` | About | Flex row with band photo and biography highlights |
| `#music` | Discography | Four CSS-only 3D flip cards, one per album |
| `#gallery` | Gallery | Asymmetric CSS Grid with hover colour-reveal effect |
| `#video` | Video | Responsive YouTube video |
| `#contact` | Contact | Email subscription form for pre-sale access |
| `#sponsors` | Sponsors | Partner logo grid with greyscale-to-colour hover transition |

---

## 📁 Project Structure

```bash
Rock-band/
│
├── index.html          # 🏠 Main landing page
├── script.js           # ⚙️  JavaScript — badge animation, burger menu close
│
├── css/
│   └── styles.css      # 🎨 Main stylesheet — all sections and responsive rules
│
├── assets/
│   ├── img/            # 🖼️  Hero background, about image, gallery photos, zone images
│   └── icons/          # 🔷 SVG social icons + sponsor logos
│
└── README.md           # 📖 You are here!
```

---

## Key Features

### CSS-Only Burger Menu

The mobile navigation is controlled entirely by a hidden `<input type="checkbox">`. The `<label for="menu-toggle">` acts as the clickable hamburger icon. A CSS sibling selector shows and hides the dropdown with no JavaScript:

```css
.menu-toggle:checked ~ .nav-links {
  display: flex;
}
```

JavaScript only closes the menu after a nav link is tapped — a behaviour CSS alone cannot handle.

---

### 3D Flip Cards (Discography)

Each album card has a front face and a back face. `perspective` on the parent creates the 3D space. `backface-visibility: hidden` hides each face while it is rotated away from view.

```css
.zone-card        { perspective: 150rem; }
.zone-front,
.zone-back        { backface-visibility: hidden; transition: all 0.8s ease; }
.zone-back        { transform: rotateY(180deg); }

.zone-card:hover .zone-front { transform: rotateY(-180deg); }
.zone-card:hover .zone-back  { transform: rotateY(0); }
```

---

### Animated Badge Card

The "Now Playing" hero card starts hidden via CSS. JavaScript adds the `badge-visible` class after 600 ms to trigger the transition, then removes it at 3 600 ms:

```css
#badgeCard {
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 0.6s ease, transform 0.6s ease;
}
#badgeCard.badge-visible {
  opacity: 1;
  transform: translateY(0);
}
```

---

### Responsive Video

The YouTube iframe scales with its container at every viewport width using `aspect-ratio` instead of a fixed pixel height:

```css
.video-container iframe {
  width: 100%;
  aspect-ratio: 16 / 9;
  height: auto;
}
```

---

## JavaScript

`script.js` contains exactly two functions:

```js
// 1 — Badge card: fade in at 600ms, fade out at 3 600ms
window.addEventListener('load', function () {
  const badge = document.getElementById('badgeCard');
  if (!badge) return;
  setTimeout(() => badge.classList.add('badge-visible'),    600);
  setTimeout(() => badge.classList.remove('badge-visible'), 3600);
});

// 2 — Close the CSS-only burger menu when a nav link is clicked
document.querySelectorAll('.nav-links a').forEach(function (link) {
  link.addEventListener('click', function () {
    document.getElementById('menu-toggle').checked = false;
  });
});
```


---

## Colour Tokens

```css
:root {
  --bg:      #080808;               /* Page background — near black    */
  --surface: #111111;               /* Card and panel background        */
  --border:  rgba(232, 0, 61, .2);  /* Subtle red-tinted border         */
  --red:     #e8003d;               /* Brand accent                     */
  --orange:  #ff5500;               /* Secondary accent (reserved)      */
  --cyan:    #00c8a0;               /* Label highlights                 */
  --text:    #f0ede8;               /* Primary text — warm white        */
  --muted:   #6a6560;               /* Secondary and subdued text       */
}
```

---

## Responsive Breakpoints

### Tablet — `max-width: 1024px`

- Hero collapses to a single column; badge card is hidden
- Album grid drops from 4 columns to 2
- Gallery drops from 3 columns to 2
- About section stacks vertically
- Footer collapses to 2 columns

### Mobile — `max-width: 735px`

- Burger menu becomes active
- All grids collapse to a single column
- Tour dates table scrolls horizontally
- Subscription form stacks vertically


---

## 🚀 How to Run

### Option 1 — Open directly in the browser

1. Clone or download the repository:

```bash
git clone https://github.com/vreniz/rock-band.git
```

2. Open the project folder and locate `index.html`.
3. Double-click the file or right-click → **"Open with browser"**.

### Option 2 — Live Server in VS Code ⚡ (Recommended)

1. Install the [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) extension.
2. Open the project folder in VS Code.
3. Right-click `index.html` → **"Open with Live Server"**.

> The page reloads automatically on every file change. Best option for development.

> **Browser support:** All modern browsers (Chrome, Firefox, Safari, Edge). The CSS-only burger menu relies on the `:checked` sibling selector, which has full support across all current browsers.

---

## 👩🏻‍💻 Author

**Vanessa Fontalvo Reniz** <br>
Systems & Computing Engineer | Frontend Developer
