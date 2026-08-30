# Chosen Consultancy — codebase

Single-page static landing site. No framework, no build step, no npm install. Open `index.html` and it runs.

Last updated: 30 August 2026

## Total footprint

| | |
| --- | --- |
| Files that ship | 22 |
| Total shipped size | ~1.5 MB (mostly images and fonts) |
| Page markup | `index.html` — 46 KB, 427 lines |
| Runtime | `support.js` (69 KB) + `image-slot.js` (65 KB) |
| Build step | none |
| Installed dependencies | none — Montserrat comes from the Google Fonts CDN |

## What ships

```
index.html                     the page — deploy this
support.js                     rendering runtime
image-slot.js                  drop-zone behaviour for the 9 editable images
vercel.json                    immutable cache headers for /assets and /fonts
README.md
CODEBASE.md                    this file
github.md                      repo association record

_ds/organic-20c9cf7b…/         Organic design system
  styles.css                   design tokens
  _ds_bundle.js                component bundle

assets/
  yt-analytics.png             YouTube Studio dashboard — 9.6Cr views
  yt-channel.jpg               channel avatar, links to the YT channel
  screelx.jpg                  ScreelX logo
  fx120.png                    FITX120 logo
  playbooks.avif               SOP / playbook illustration
  slots/
    hero-tower.webp            hero photograph
    offer-take-over.webp      ─┐
    offer-inhouse.webp         │
    offer-concepts.webp        │  the 8 "what we offer"
    offer-packaging.webp       │  card images
    offer-frameworks.webp      │
    offer-performance.webp     │
    offer-leadgen.webp         │
    offer-editing.webp        ─┘
    _manifest.json             slot id → file map

fonts/
  TTInterphasesPro-Regular.ttf
  TTInterphasesPro-Medium.ttf
  TTInterphasesPro-DemiBold.ttf
  TTInterphasesPro-Bold.ttf
  TTInterphasesProMono-Regular.ttf
  TTInterphasesProMono-Bold.ttf
```

## Editing source (keep in the repo, not needed to deploy)

```
Chosen Consultancy Landing.dc.html   editable source — 45 KB, 428 lines
.image-slots.state.json              images dropped through the editor, as data URLs
uploads/                             raw material you sent (PDF reference, screenshots,
                                     font zip) — safe to delete before pushing
```

`index.html` and the `.dc.html` are now structurally the same page. Both carry the 9 images
as `<image-slot>` elements with a `src` fallback, so each one renders the committed file on
the deployed site **and** stays a drop zone in the editor. Replacing an image in the editor
overrides the file for that browser only — to change it for everyone, replace the file in
`assets/slots/` and commit.

## Page structure

One document, sections in order:

| # | Section id | Content |
| --- | --- | --- |
| — | header | Brand mark, sticky, CTA button |
| — | hero | Headline, subhead, CTA, 4-stat strip, hero photo |
| — | marquee | Scrolling capability list |
| 01 | `#who` | Who we are — three paragraphs, sticky heading |
| 02 | `#offer` | What we offer — 8 image cards on a 6-column grid |
| 03 | `#numbers` | Dashboard screenshot (80%) + 4 counting stats (20%) |
| 04 | `#process` | Sixteen weeks — 4 steps + what we need from you |
| 05 | `#proof` | YouTube from scratch · ScreelX · FITX120 |
| 06 | `#call` | Centered CTA → Calendly |
| — | footer | Strapline + CTA link |

## Design tokens

CSS variables, declared once in the document head.

```
--ink       #11110F   page ground
--panel     #191914   card surface
--panel-2   #202018   input surface
--cream     #F3F0E8   body text
--white     #FAF8F3   headings
--muted     #A8A096   secondary text
--accent    #B09878   gold — CTAs, kickers, numbers
```

Type: Montserrat (headings, body, CTAs) · TT Interphases Pro (labels) · TT Interphases Mono Bold (kickers, stat labels)

Layout styling is inline on the elements. The only rules in `<style>` are `@font-face`,
`@keyframes` (marquee, film grain), the token block, body resets, and four media queries.

## Behaviour

Three pieces of JavaScript, all in one class in the page:

1. **Scroll reveal** — an `IntersectionObserver` fades and lifts every `[data-reveal]` element on entry, staggered 90ms by index.
2. **Counting numbers** — an `IntersectionObserver` animates every `[data-count]` from 0 to its `data-to` over 1.5s, cubic ease-out.
3. **Film grain** — an SVG turbulence overlay at `mix-blend-mode: soft-light`, stepped on a 7s loop.

No forms, no state, no API calls. All 4 booking links point at
`https://calendly.com/contact-chosenconsultancy/30min` and open in a new tab.

## Deploying

Static. No build command, no output directory.

- **Vercel** — import the repo, framework preset *Other*, leave build settings empty.
- **Locally** — `python3 -m http.server 8000`, then open http://localhost:8000

**Folder structure must be preserved on upload.** The current repo has all 45 files
flattened at the root, which is why images 404 on the deployed site — `index.html` asks for
`assets/slots/hero-tower.webp` and there is no `assets/` folder. Re-upload keeping `assets/`,
`assets/slots/`, `fonts/` and `_ds/` intact. Dragging the *folders* into GitHub's web uploader
preserves them; dragging a flat selection of files does not.

## Known items

- TT Interphases Pro is the **trial** licence. Buy a web licence before a production domain.
- `uploads/` is working material, not shipped content.
- Offer-card images are compressed WebP pulled out of the editor. Re-export larger if any look soft.
