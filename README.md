# BDS Technology — Website

A single-page marketing site for **BDS Technology**, a smart energy company whose flagship product is the **Electronic Capacitor Bank**: a wall-mounted power factor correction unit that cuts reactive power, removes utility penalty charges, and lowers the electricity bill for residential and commercial buildings.

Tagline: *Smart Energy Solutions for Buildings.*

The site is `index.html` (about 125 KB) plus one optimized product photo, `product-unit.png` (~540 KB). No build step, no dependencies to install, no backend. Open `index.html` and it runs.

---

## Quick start

**View it locally**
- Double-click `index.html`, or
- Serve the folder: `python3 -m http.server` then open `http://localhost:8000`.

**Host it**
Drop `index.html` on any static host and point your domain at it:
- Vercel, Netlify, Cloudflare Pages: drag the folder in, or connect a repo.
- Any web server / cPanel: upload `index.html` **and** `product-unit.png` to the web root (keep them in the same folder).
- The intended home is `bds-technology.com`.

The page loads Google Fonts and the local `product-unit.png`. Everything else, including the logo, is embedded as base64.

---

## What's in the file

| Part | Notes |
|------|-------|
| HTML | One semantic document, landmarks for nav / header / sections / footer. |
| CSS | All styles in a single `<style>` block. Design tokens live in `:root`. |
| JavaScript | One vanilla IIFE at the bottom. No framework, no libraries. |
| Logo | Embedded as base64 PNG, two variants (see *Logo handling*). |
| Fonts | Loaded from Google Fonts: Archivo, Inter, JetBrains Mono. |

There is intentionally **no** `localStorage`, `sessionStorage`, or external script.

---

## Tech stack

Plain HTML, CSS, and JavaScript. The dynamic pieces use:
- The Canvas 2D API for the hero "current field" background.
- SVG for the device illustration and the oscilloscope waveforms, animated via `requestAnimationFrame`.
- `IntersectionObserver` for scroll reveals.
- CSS keyframes and transitions for the rest of the motion.

Because it is framework-free, any developer can edit it, and it will keep working for years without dependency rot.

---

## Design system

Everything is **red / black / white**, derived from the brochure and logo.

### Color tokens (in `:root`)

| Token | Value | Use |
|-------|-------|-----|
| `--paper` | `#ffffff` | Page background, light sections |
| `--paper-2` | `#f4f3f1` | Warm off-white panels |
| `--ink` | `#0c0d10` | Near-black, dark sections and text |
| `--slate` | `#2b2f36` | Logo wordmark tone, secondary text |
| `--muted` | `#6a7079` | Body grey |
| `--red` | `#dd1a22` | Primary brand red |
| `--red-deep` | `#b3141b` | Hover / pressed red |

Change a token once in `:root` and it updates everywhere.

### Typography
- **Archivo** (700 to 900): headlines, eyebrows, labels. Carries the engineered, industrial feel.
- **Inter** (400 to 600): body copy.
- **JetBrains Mono**: all numbers and technical data (the `0.98` readout, stats, specs, phone numbers). Gives the instrument-panel feel.

### Layout
Centered 1200 px max width, generous vertical rhythm, diagonal red cuts echoing the brochure. Dark hero and dark product section bracket the lighter content in between.

---

## Sections

In order, with their anchor IDs:

1. **Nav** (`#top`) — logo, links, and a red "Free assessment" button. Transparent over the hero, turns solid white on scroll. The logo and wordmark switch between a light-background and dark-background version automatically.
2. **Hero** — the headline, the live Electronic Capacitor Bank with its `0.98` power-factor readout, and the primary calls to action.
3. **Stat strip** — four animated figures: target power factor, penalty charges, one-time install, real-time correction.
4. **Problem** (`#problem`) — why some buildings overpay, the before/after voltage and current waveforms, the common sources (elevators, pumps, HVAC, motors), and what high reactive power costs.
5. **Solution** (`#solution`) — the five-step "how it works" flow and the *Without PFC vs With BDS Technology* comparison table.
6. **Product** (`#product`) — the Electronic Capacitor Bank, its key benefits, and a short spec list.
7. **Results** (`#results`) — the closing pitch and calls to action.
8. **Contact / Footer** (`#contact`) — UAE and Türkiye phone lines, web, email, and the "Become a local distributor" card.

---

## Motion and interactions

The animation has one idea behind it: **current flowing through the system.** Everything serves that theme rather than decorating for its own sake.

- **Hero current field**: faint traces with red and white light pulses drifting across the background (Canvas). Masked so it never competes with the headline.
- **Power-on entrance**: on load, the hero copy rises in sequence and the device boots up. The readout sweeps from `0.00` to `0.98`.
- **Live device**: a moving scanline, a blinking status LED, a bargraph that behaves like a live equalizer, and a slow float.
- **Oscilloscope waveforms**: the voltage and current traces drift continuously. The before/after toggle snaps the current wave in and out of phase.
- **Process flow**: the five rings pop in one by one, then pulses of light travel along the red connectors between them.
- **Throughout**: a red scroll-progress bar at the top, staggered reveals on cards and table rows, a sheen on button hover, and small hover lifts and glows on cards and contact icons.

All continuous motion is paused when the operating system requests reduced motion (see *Accessibility*), and when the browser tab is hidden the hero canvas stops to save power.

---

## Logo handling

The logo is embedded directly in the HTML as base64 PNG, so there are no separate image files to lose. Two versions are generated from the same building-and-bolt mark:

- **Dark-on-light**: the original dark buildings with the red bolt. Used on the white scrolled nav.
- **White-on-dark**: white buildings with the red bolt kept. Used on the dark hero nav and the footer.

The wordmark "BDS TECHNOLOGY" and the tagline are set in live text (Archivo), not baked into the image, so they stay crisp at any size.

**To replace the logo** with a new file, the cleanest path is to regenerate the two base64 strings from a transparent source and swap them in. If you want this done, send the new artwork and it can be re-cropped and re-embedded.

---

## Customization guide

Common edits, and where to make them:

**Copy** — search the text in `index.html` and edit in place. Headlines and body text are plain HTML.

**Colors** — change the tokens in `:root` (see the table above). The red, in particular, flows to every accent, button, and highlight.

**Contact details** — the phone numbers, web, and email live in the footer (`#contact`) and in the call-to-action buttons. Current values:

| Channel | Value |
|---------|-------|
| UAE — WhatsApp | +971 58 546 1072 |
| UAE — Call | +971 58 546 1072 |
| Türkiye — Call | +90 530 710 7586 |
| Web | bds-technology.com |
| Email | info@bds-technology.com |

UAE WhatsApp and Call are now **separate** actions — a single link cannot both place a call and open WhatsApp, which is why the old combined "Call or WhatsApp" row was replaced. The WhatsApp link uses `https://wa.me/971585461072`, the call links use `tel:+971585461072`, and the email uses `mailto:`. Update all of these together if a number changes.

**Calls to action** — every "Get a free assessment" / "Free assessment" button points to WhatsApp. Change the `href` on those `<a>` tags to retarget them (for example, to a contact form once one exists).

**Specs and table rows** — the comparison table and the product spec list are plain HTML; edit the cells directly.

---

## Accessibility and performance

- **Reduced motion**: if the visitor's system is set to reduce motion, all continuous and entrance animations are switched off and every element stays fully visible. This is handled with `prefers-reduced-motion` and was verified.
- **Keyboard**: visible focus outlines on interactive elements.
- **Structure**: semantic landmarks and alt text on the logo.
- **Responsive**: tested down to a 390 px phone viewport. The nav collapses to a menu, grids reflow to one or two columns, and the comparison table restructures for small screens.
- **Weight**: `index.html` (~125 KB, logo inlined) plus `product-unit.png` (~540 KB). Network dependencies: the Google Fonts stylesheet and the product image.

---

## Browser support

Modern evergreen browsers (Chrome, Edge, Safari, Firefox). The site uses Canvas, SVG, CSS custom properties, `clip-path`, and `IntersectionObserver`, all broadly supported. Older browsers degrade gracefully: if the animations do not run, the content is still fully readable.

---

## Known limitations

- **No contact form backend.** Calls to action route to WhatsApp, phone, and email. There is no form that posts a lead anywhere yet.
- **The hero device is an SVG illustration** with the live animated readout; the Product section shows a real photo of the unit (`product-unit.png`) — a transparent render that floats on a dark studio background. The original AI render's garbled on-screen sub-label was retouched out, so the display reads a clean **0.98**. Icons throughout are from the [Tabler Icons](https://tabler.io/icons) library (MIT).

---

## Possible next steps

- Wire a real contact form to email or a CRM.
- Add localization. Given UAE and Türkiye, Arabic and Turkish versions are the natural follow-up.
- Use the real photo in the hero too (the hero currently keeps the animated SVG for the live 0.98 boot-up).
- A scroll-driven build where the unit assembles as the visitor scrolls.

---

*Built for BDS Technology. Single file, no dependencies, ready to host.*
