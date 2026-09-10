# A_Naturography

Nature & travel photography portfolio for **Ashwik Bire**, published at
[a_naturography.github.io](https://a_naturography.github.io).

This repository's `index.html` has been rebuilt from the ground up: same photos,
same identity, but a single valid, dependency-light HTML file with a dark
neumorphic design, real motion, and a working gallery/lightbox in place of the
old broken markup.

---

## What was wrong with the old file

The previous `index.html` mostly worked by accident. Fixed in this rebuild:

| # | Issue | Fix |
|---|---|---|
| 1 | Two full `<!DOCTYPE html><html>…</html>` documents were pasted **inside** the `<body>` (once in the header, once in the photo grid) | Removed — one valid document from top to bottom |
| 2 | `<link rel="stylesheet" href="CSS/Style.css">` pointed at a file that doesn't exist in the repo | Removed; all CSS now lives in one `<style>` block, no dead requests |
| 3 | `alert(location.hostname)` fired on every page load | Removed |
| 4 | Unclosed / mismatched tags, e.g. `<p>…</h3></p>`, a stray `");` inside a `<button>` attribute | Rewritten with valid, semantic HTML5 |
| 5 | 9 `<img>` tags pointed at files that don't exist or don't match the real filename (`IMG56.jpg` vs the actual `IMG.56.jpeg`, `IMG6.jpeg` vs `IMG6 .jpeg`, plus `IMG672.jpg`, `IMG85‑87.jpg`, `IMG93.jpg`, `IMG95.jpg`, none of which exist) | Gallery is now generated from a verified array of the 91 images that actually exist in the repo |
| 6 | Depended on old **W3.CSS** + **Font Awesome 4** + a `'Sofia'` font that was never loaded, so text silently fell back to the browser default | Two real, loaded typefaces (Fraunces + Manrope) and Font Awesome 6 |
| 7 | Contact form posted to `/action_page.php`, which doesn't exist | Replaced with a styled, validated form ready to wire up to a real form backend (see below) |
| 8 | No `alt` text, no meta description, no favicon, no semantic landmarks | Added throughout, plus Open Graph tags |
| 9 | Slideshow dot indicators didn't match the number of slides (bug in the original `onclick` handlers) | Old jQuery-free slideshow replaced with a hero Ken Burns crossfade and a proper quote carousel |

Your original bio line — recovered from a stray filename in the repo — is now
the real About-section copy: *"Welcome to A_Naturography — where I channel my
deep-rooted passion for nature into captivating visual stories…"*

---

## What's new in the design

- **Dark neumorphism**, built for this subject rather than a generic template:
  soft raised/pressed shadows on a deep moss‑charcoal base, warm gold and sage
  accents pulled from your sunset/forest photos.
- **Two typefaces**: [Fraunces](https://fonts.google.com/specimen/Fraunces)
  (editorial serif, used for headings) and
  [Manrope](https://fonts.google.com/specimen/Manrope) (UI/body).
- **Motion**: staggered hero title reveal, a Ken Burns crossfade in the hero
  frame, scroll-triggered fade-ups, animated skill bars and stat counters, an
  auto-rotating quote carousel, and hover/tap micro-interactions on every
  neumorphic surface. Everything respects `prefers-reduced-motion`.
- **Gallery**: all 91 usable photos from the repo, auto-tagged into
  *Wildlife / Flora / Travel / Landscape* by filename, laid out in a masonry
  grid with lazy loading and a full lightbox (arrow keys, click‑through,
  counter, captions).
- **Responsive** from a 1440px desktop down to a 375px phone, with a slide-in
  mobile menu.
- **Accessible**: visible keyboard focus states, `aria-label`s on icon-only
  controls, semantic sectioning, alt text on every image.
- **Real links**: the footer's LinkedIn, GitHub and portfolio icons go to your
  actual profiles instead of dead `href="#"` placeholders.

---

## File structure

```
/ (repo root)
├── index.html      ← the file in this delivery — replace your current one
├── README.md        ← this file
├── IMG1.jpeg … IMGG1.jpg, wolf.png, lotus.jpg, etc.   ← your existing images, unchanged
└── .jpeg             ← your existing logo, unchanged
```

**Nothing needs to move.** `index.html` references every image by its existing
filename (spaces are percent‑encoded, e.g. `Taj%20mahal.jpg`), so you can drop
this file straight into the repo root, next to the photos that are already
there, and it will work as-is on GitHub Pages.

`STR.py` and `.gitignore` were left untouched — they aren't part of the site.

---

## Editing the site

Everything — HTML, CSS and JS — lives in the one `index.html` file so there's
nothing to build or compile.

### Add or remove a gallery photo
Find the `GALLERY` array near the top of the `<script>` block:

```js
const GALLERY = [
  {src:"111.jpg", cat:"landscape"},
  {src:"LION.jpg", cat:"wildlife"},
  // ...
];
```
Add a new `{src:"yourfile.jpg", cat:"wildlife"}` line (categories:
`wildlife`, `flora`, `travel`, `landscape`) or delete a line to remove a
photo. Filenames with spaces need `%20` in place of the space.

### Change colors / fonts
All design tokens are CSS custom properties at the top of the `<style>`
block, under `:root`. Change `--gold`, `--sage`, `--bg`, etc. in one place to
re-theme the whole site.

### Connect the contact form
The form currently validates and shows a success message, but doesn't send
anywhere — there's no backend in a static GitHub Pages site. To make it
actually deliver messages to your inbox, the fastest options are:

- **[Formspree](https://formspree.io)** — add `action="https://formspree.io/f/yourFormId"`
  and `method="POST"` to the `<form>` tag, remove the `preventDefault()` call
  in the submit handler (or follow Formspree's fetch example instead).
- **[EmailJS](https://www.emailjs.com)** — send straight from the browser with
  their JS SDK, no backend needed.

Either is a five‑minute change inside the `contactForm` submit handler in the
`<script>` block.

---

## Deploying

This is a static site — commit `index.html` (and this `README.md`) to the
`main` branch of `a_naturography.github.io` alongside the existing images,
and GitHub Pages will publish it automatically at your existing URL. No build
step, no dependencies to install.

---

## Credits

- Photography: Ashwik Bire, A_Naturography
- Fonts: [Fraunces](https://fonts.google.com/specimen/Fraunces) &
  [Manrope](https://fonts.google.com/specimen/Manrope) via Google Fonts
- Icons: [Font Awesome 6](https://fontawesome.com) via cdnjs
- Nature quotes in the carousel are widely‑attributed public‑domain lines
  from John Burroughs, Rachel Carson, Henry David Thoreau, Richard Feynman
  and Jacques‑Yves Cousteau, carried over from the original site.
