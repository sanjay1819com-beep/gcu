# GARDEN CITY — lusion.co-format studio site

A single-file website built in the exact format of [lusion.co](https://lusion.co)
(original design & code, Lusion-style layout): light editorial theme, pixel-logo
preloader with a big counter, statement hero over a **dark rounded WebGL frame**,
giant masked headlines, staggered 2-column **Featured Work** grid, **PLAY REEL**
block, approach rows, dark footer with outlined wordmark.

The 3D centrepiece is a real-time **particle garden**: ~22,000 GPU points that
assemble from scattered noise during the loader, then morph
**bloom → sphere → helix → knot** as you scroll, react to your cursor inside the
frame, and burst on click.

---

## ▶ Run it in VS Code (no build step)

1. Open this folder in VS Code.
2. Install the **Live Server** extension (Ritwick Dey) if you haven't.
3. Right-click `index.html` → **Open with Live Server**.

Or any static server:
```bash
python3 -m http.server 8000     # then open http://localhost:8000
```
Libraries (Three.js, GSAP, Lenis, Google Fonts) load from CDNs — internet needed on first open.

---

## 🖼 Swapping in YOUR files (logo, images, reel)

| What | Where to put it | What to edit |
|---|---|---|
| **Garden City logo** | `images/logo.svg` (or .png) — overwrite the file | nothing else; header `<img id="brandLogo">` picks it up. Preloader pixel-mark: edit the `<svg class="px-logo">` rects in `#loader`, or replace with `<img>` of your logo |
| **Project images** (8) | `images/projects/p1…p8.svg` → overwrite with your `.jpg/.png/.webp` and rename, or change each `src` in the `<!-- 🖼 SWAP THESE IMAGES -->` block | card titles/meta are plain text next to each `src` |
| **Studio photo** (manifesto) | `images/projects/studio.svg` → overwrite | — |
| **Showreel video** | `images/reel.mp4` | nothing — the PLAY REEL modal auto-detects it (until then it shows a placeholder note) |
| Favicon | inline data-URI in `<head>` | swap the `<link rel="icon">` |

The 8 `p*.svg` + `studio.svg` files are generated placeholders labelled
"REPLACE ME" — delete them once your images are in.

## ✏️ Quick edits

- **Brand / copy** — all text is plain HTML in `<main>`; footer email appears twice
  (`mailto:` links) — search for `gardencity.studio`.
- **Colors** — top of `<style>`: `--bg`, `--ink`, `--accent` (garden green), `--frame`.
- **Particles** — in the module script: `COUNT` (22000), `COLORS` array,
  `setShape(i, dur)` morph speed, formations in `shapeBloom/Sphere/Helix/Knot`,
  point size `155./vD` and alpha line in the fragment shader.
- **Intro timing** — the `intro` GSAP timeline near the bottom (loader count,
  wipe, line reveals, first morph).

## 📄 Page structure (lusion format)

1. **Preloader** — black screen, pixel-sprout logo assembles, counter 0→100 bottom-left, wipe-up reveal.
2. **Header** — logo left; orb button + `LET'S TALK` dark pill + `MENU` pill right (magnetic).
3. **Hero** — 3-line statement with masked line reveal → rounded dark frame with the live WebGL particle garden, `+` corner markers, "SCROLL TO EXPLORE".
4. **Manifesto** — giant 2-line headline, green arc, duotone studio image, right column + "OUR APPROACH" pill.
5. **Featured Work** — giant headline + 2-col staggered card grid (rounded media, meta line, hover zoom + VIEW cursor).
6. **Play Reel** — rounded frame, PLAY ▶ REEL, opens a modal that plays `images/reel.mp4`.
7. **Approach** — 4 numbered hover rows.
8. **Footer** — dark, "Let's grow something rare.", contact pill, link columns, outlined GARDEN CITY wordmark.
9. **Menu overlay** — full-screen clip-path wipe with staggered giant links.

Also: Lenis smooth scroll, custom cursor (flips light over dark zones), film grain,
`prefers-reduced-motion` fallback, touch-device fallbacks, render pauses when the
frame is off-screen.

## 🚀 Deploy

Static — drop the folder on Netlify / Vercel / Cloudflare Pages / GitHub Pages.
No build command, publish directory `.`.
