# Fresh — Website Project

## Student information
- **Name:** Rayan Jaymar Bvulani
- **Student number:** 10497168
- **Subject:** Web Development
- **Subject code:** WEDE5020

## Project overview
Fresh is a bold, black-and-yellow streetwear brand offering versatile clothing and accessories for people who want their look to stand out — without overthinking it. This repository contains the static website build for Fresh, developed as part of the Web Development coursework.

The full research and planning behind this site — organisation overview, goals and KPIs, competitor analysis, and design rationale — is covered in the accompanying Website Project Proposal document submitted separately for Part 1 of this project.

## Pages included
| Page | File | Description |
|---|---|---|
| Homepage | `index.html` | Hero banner, "Shop now" CTA, Fresh Picks grid, #StayFresh social strip |
| Shop | `shop.html` | Full product grid with category, size, and price filters |
| Product page | `product.html` | Product detail, image gallery, size selection, "Complete the Look" suggestions |
| Lookbook | `lookbook.html` | Editorial photo grid, style journal articles, #StayFresh strip |
| About & Contact | `about.html` | Brand story and a contact form |

All pages share one stylesheet (`style.css`) and one script (`script.js`) for consistent styling, navigation, and interactivity.

## How to view the site
1. Keep all files and folders together in one place — `.html` files, `style.css`, `script.js`, and the `images/` folder. The pages link to each other and to their assets using relative paths.
2. Open `index.html` in any modern web browser (Chrome, Firefox, Edge, Safari) to start browsing the site.
3. Resize the browser window, or use browser dev tools' device toolbar, to see the responsive breakpoints in action (see Section 3 below).

## Technical details
- Built with plain HTML5, CSS3, and a small amount of vanilla JavaScript — no build tools or frameworks required.
- Fonts: Bebas Neue (headings), Inter (body text), JetBrains Mono (prices and labels), loaded via Google Fonts.
- A CSS reset and a set of design tokens (`:root` custom properties for colour, spacing, and a fluid type scale) sit at the top of `style.css` and drive the rest of the stylesheet.
- Layout uses CSS Grid (product grids, shop/product/about page structure) and Flexbox (header, buttons, footer).
- Interactive states are implemented with `:hover`, `:focus-visible`, and `:active` pseudo-classes on all buttons, links, nav items, and form fields.
- `script.js` powers the mobile navigation toggle (hamburger menu), the product size selector, and the site-wide toast notification system (see "Toast notifications and interactivity" below).
- Responsive images use `srcset`/`sizes` (resolution switching) and `<picture>` with a `<source media>` (art direction) for the hero, one product image, and the About page photo — see `images/` for the multiple resolutions generated for this. Remaining product thumbnails are still placeholders pending real photography.

## 2. CSS styling (desktop solution)
- **2.1 External stylesheet:** one stylesheet, `style.css`, linked from all five pages via `<link rel="stylesheet" href="style.css">`.
- **2.2 Base style / reset:** a reset at the top of `style.css` removes default browser margin/padding and sets `box-sizing: border-box` globally; base font family, size, and colour scheme are set on `body`.
- **2.3 Typography:** `font-family`, `font-size` (via a `clamp()`-based fluid type scale), `line-height`, and `letter-spacing` are applied across headings and body text.
- **2.4 Layout structure:** CSS Grid is used for the header/hero/product grids and the shop/product/about page structures; Flexbox is used for the header bar, nav list, buttons, and footer.
- **2.5 Visual styles:** `color`, `background-color`, `border`, and `box-shadow` (on product card hover) are used throughout, alongside `:hover`, `:focus-visible`, and `:active` states on every interactive element.

## 3. Responsive design
- **3.1 Breakpoints:** three tiers — desktop (default, > 1024px), tablet (≤ 1024px), and mobile (≤ 600px) — defined with `@media` queries in `style.css`. Multi-column layouts (shop filters + grid, product gallery + info, about text + photo) collapse to a single column on tablet and mobile; the desktop nav is replaced with a hamburger-triggered mobile menu (`script.js`) below 600px.
- **3.2 Relative units:** spacing uses a `rem`-based scale (`--space-xs` through `--space-xl`), typography uses `rem` and `clamp()`, and layout widths use `%`/`fr` units rather than fixed pixels.
- **3.3 Responsive images:** see Technical details above — `srcset`/`sizes` and `<picture>` are implemented for the hero, one product image, and the About page photo.
- **3.4 Test and iterate:** see Screenshot evidence below.

## Toast notifications and interactivity
A reusable `showToast(message, options)` helper in `script.js` (styled in the "Toast notifications" block of `style.css`) gives the user feedback on their actions. Toasts stack (maximum three), dismiss automatically after four seconds, pause while hovered or focused, and can be closed with the × button. They sit in an `aria-live="polite"` region so screen readers announce them.

| Page | Interaction | Toast feedback |
|---|---|---|
| Home / Shop / Product ("Complete the look") | "Quick add" button, injected by `script.js` onto every card that shows a rand price | Success toast with an **Undo** action; the header cart count updates |
| Product | "Add to cart" without choosing a size | Error toast asking the user to select a size |
| Product | "Add to cart" with a size chosen | Success toast including the size, with **Undo** |
| Product | "Add to wishlist" | Toggles saved/removed; button label updates and the state is remembered |
| Contact (About) | Form submit | Validated in JavaScript (name, email format, message length). Invalid fields get `aria-invalid` styling and an error toast; a valid form shows a success toast and resets. No message is actually sent, as the site is static. |
| Home / Lookbook | "Copy #StayFresh" button (`data-copy`) | Copies the hashtag to the clipboard and confirms with a toast |
| All pages | Account / Cart links in the header | Info toast instead of jumping to the top of the page (these pages do not exist yet) |

The cart and wishlist are stored in `localStorage`, so the cart count in the header persists as the user moves between pages. Storage access is wrapped in `try/catch` so the site still works if the browser blocks it.

**Testing:** these behaviours were checked with an automated browser script (Playwright/Chromium) covering all five pages at desktop and mobile widths, including cart persistence across pages, form validation, undo, the three-toast limit, and that no JavaScript errors occur.

## Screenshot evidence
Desktop-width screenshots of each page, captured from the live site to confirm the layout, navigation, and styling render correctly:

### Homepage
![Homepage – hero](screenshots/homepage-hero-desktop.png)
![Homepage – Fresh Picks](screenshots/homepage-picks-desktop.png)

### Shop
![Shop page](screenshots/shop-desktop.png)

### Lookbook
![Lookbook page – top](screenshots/lookbook-desktop-1.png)
![Lookbook page – scrolled](screenshots/lookbook-desktop-2.png)

### About
![About page](screenshots/about-desktop.png)

**Still to add:** tablet (~800px) and mobile (~390px) screenshots for each page, to fully demonstrate the responsive breakpoints described in Section 3.1. Capture these with your browser's dev tools device toolbar (F12 → toggle device toolbar) and add them here in the same format, e.g. `screenshots/homepage-mobile.png`.

## Changelog
Edits made in this round, addressing Part 1 feedback and implementing the Part 2 requirements:

- **Fixed invalid HTML carried over from early drafts** — corrected a malformed `<img>` tag, a broken link href, and `<section>`/`<footer>` elements that were sitting outside `<body>`.
- **Added a CSS reset and base style layer** to `style.css` (margin/padding reset, `box-sizing: border-box`, consistent base typography) per section 2.2 of the brief.
- **Introduced a fluid typography scale** using `clamp()` and `rem` units, replacing fixed pixel font sizes, per section 2.3.
- **Reworked layout using explicit CSS Grid and Flexbox**, including named layout sections in the stylesheet, per section 2.4.
- **Added visual and interaction states** — `box-shadow` on product card hover, and `:hover`/`:focus-visible`/`:active` states on all buttons, links, nav items, and form fields — per section 2.5.
- **Implemented three responsive breakpoints** (desktop/tablet/mobile) with `@media` queries, collapsing multi-column layouts to single-column on smaller screens, per section 3.1.
- **Replaced the previous "just hide the nav" mobile behaviour with a working hamburger menu**, built with `script.js`, so navigation is still usable on mobile rather than disappearing.
- **Converted spacing and sizing to relative units** (`rem`/`%`/`fr`) throughout, per section 3.2.
- **Added responsive images** (`srcset`/`sizes` and `<picture>` with art-directed `source`) for the hero banner, one product image, and the About page photo, per section 3.3.
- **Added a toast notification system** (`showToast` in `script.js`, styles in `style.css`) so every user action gets visible feedback: success, error and info variants, auto-dismiss, pause on hover/focus, an optional **Undo** action, and an ARIA live region for screen readers.
- **Added working cart and wishlist behaviour** — "Quick add" buttons on product cards, size validation on the product page, a live cart count in the header, and state saved in `localStorage` so it persists between pages.
- **Replaced the product page's "Add to cart"/"Add to wishlist" links with real `<button>` elements** (they were `<a href="#">` links that jumped to the top of the page), and removed the pre-selected size so users must choose one.
- **Added JavaScript validation to the contact form** with inline `aria-invalid` styling and toast error messages, replacing the browser's default validation popups.
- **Added a "Copy #StayFresh" button** to the Home and Lookbook pages using the Clipboard API.
- **Header Account and Cart links no longer scroll the page to the top** — they now show an explanatory toast, since those pages are not built yet.

> If your actual Part 1 feedback included specific comments not covered above, add them as additional changelog entries here with the date and a short description of the fix, as the brief requires.

## References
References used in researching and planning this project are listed in the Website Project Proposal document. Sources used for the Part 2 build:

- Google (2026) *Google Fonts*. Available at: https://fonts.google.com (Accessed: 2 November 2026).
- MDN Web Docs (2026) *Using media queries*. Available at: https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_media_queries/Using_media_queries (Accessed: 2 November 2026).
- MDN Web Docs (2026) *ARIA live regions*. Available at: https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Live_Regions (Accessed: 2 November 2026).
- MDN Web Docs (2026) *Web Storage API*. Available at: https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API (Accessed: 2 November 2026).
- MDN Web Docs (2026) *Clipboard.writeText()*. Available at: https://developer.mozilla.org/en-US/docs/Web/API/Clipboard/writeText (Accessed: 2 November 2026).
