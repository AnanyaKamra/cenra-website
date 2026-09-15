# Cenra Studios — cenra-website

This file is read automatically at the start of every Claude Code session in
this repo. It exists so you don't have to re-explain the brand, the format,
or the history every time. Read it before touching anything.

## What this is

Cenra Studios is Ananya Kamra's AI/brand design studio (Delhi). This repo is
the live site at **cenrastudios.com**, deployed on **Vercel**, auto-deploying
from **github.com/AnanyaKamra/cenra-website** on every push to `master`.

Core thesis: designing trust and clarity into AI products, and protecting
brands from going generic. Manifesto line used on-site: *"Competence is now
free — which is exactly why it's worth nothing."*

Two client pillars: (1) software founders building AI features, sold on the
UX pattern library (Intent Preview, Confidence Halo, Recovery Lane); (2)
brands drowning in AI-flattened genericness.

## Repo structure

Flat, no build step, no framework. Every page is a single self-contained
HTML file (HTML + CSS + JS inline). That's deliberate — it keeps the site
fast, portable, and easy to reason about page-by-page.

```
index.html              — homepage
spiral.html              — SPIRAL project page (the template for all future projects)
spiral-case-study.html   — SPIRAL's standalone deep-dive case study
CLAUDE.md                 — this file
```

All internal links are **relative** (`spiral.html`, not `/spiral` or an
absolute URL) so the site works identically opened locally, on a
`*.vercel.app` preview, or on the live domain.

## Brand system — locked, do not deviate without being asked

**Colour** (CSS vars: `--cream`, `--pitch`, `--cobalt`, `--cobalt-bright`,
`--ink`, `--ink-soft`, `--ink-faint`, `--light`, `--light-soft`,
`--light-faint`, `--rule`):
- Cream `#F5F1E8` · Pitch `#0F0E0C` · Cobalt `#2E3FCB` (accent on light) ·
  Cobalt-bright `#6478FF` (accent on dark) · Ink `#1A1816`
- Cobalt is the **sole** brand accent — punctuation and emphasis only, never
  a flood colour.

**Type:** Fraunces (display/serif, weight 300, italic for emphasis) ·
JetBrains Mono (kickers, labels, nav, uppercase, tracked) · Inter (body).
The project pages currently use Inter more broadly than the homepage does —
flagged in "Open items" below, not yet reconciled site-wide.

**Voice:** editorial cobalt — restrained, type-led, deadpan-serious.
Roman numeral folios (I/VIII etc.), ghost watermark digits, alternating
cream/pitch sections.

**Motion:** GSAP + Lenis smooth scroll. Word-by-word `.reveal-line` mask
reveals, `.rise` fade-ups, expo easing (`cubic-bezier(0.16,1,0.3,1)`).
**Never bounce easing** — it reads as generic SaaS, not editorial.

**Hard rules — ask before breaking any of these:**
- No "templates" language anywhere on the site.
- No pricing shown publicly.
- One CTA per offer ("Inquire" / "Book a Trust Scan").
- No FAQ sections, no process diagrams, no generic AI-flattened filler copy.
- No stock illustration — the only illustration source is the Figures
  library (see below) or a project's own real assets.

## Locked homepage decisions

- **Hero:** Warp Ink WebGL shader — dark, marbled, alive, cursor-reactive,
  with a seamless gradient fade to pitch at the bottom. This was chosen
  over several other shader directions (Paper Mesh, Dither, Tonal Fold,
  Liquid Fold, Drift Veil, Plume, Silk, Marble) — don't reopen that
  exploration without being asked.
- **Nav:** "Glass Bar" — transparent with light links at the top, detaches
  into a fully circular, backdrop-blurred glass pill on scroll
  (`.topbar.scrolled`). Buttons use a fill-wipe hover: transparent/outline
  at rest, a colour sweeps in from the left on hover, text flips colour.
  This hover pattern (see `.nav-cta`, `.btn-fill`) is the studio's signature
  button behaviour — reuse it for any new CTA rather than inventing a new
  hover style.
- **Selected Work:** a 3D coverflow "Curve" carousel (`.curve2-card`),
  wide 16:10 cards sized for website screenshots, centre card active by
  default. Clicking the centred card navigates via `window.location.href`
  to that project's `url`. Off-centre cards click to re-centre first.
- **Footer:** real contact info — `ananya@cenrastudios.com`,
  Cal.com (`cal.com/cenrastudios/free-brand-audit`), LinkedIn
  (linkedin.com/in/ananyakamra), Instagram (`@cenrastudios`).

## The project-page template (this is the repeatable pattern)

`spiral.html` is the locked template ("Option B — Design Reel"). Every
future project page should follow this exact section order:

1. **Cover** — full-bleed dark hero with the project name, a one-line
   premise/tagline, year, and a scope strip (what was done).
2. **Live frame** — a browser-chrome mock embedding the live project site
   in an `<iframe>` (same-origin auto-scroll isn't possible cross-origin,
   so this is manual-scroll) plus a "Visit the website →" button pointing
   at the real subdomain.
3. **Reel** — a run of real screenshots/video of the actual work. Prefer
   video/GIF over stills wherever the brand argument is about motion.
4. **The Thinking** — three key decisions, stated as "laws" or similar,
   each with a one-line reason.
5. **Brand Map** — a real type specimen (use the *project's* actual fonts,
   not Cenra's), the real palette swatches, and a "voice" panel showing the
   brand's actual copy lines as pull-quotes.
6. **The Journey** — the audience's path through the brand/product, with
   one node called out as the key trust moment.
7. **The Graveyard** — killed AI-generated directions, each with a real
   thumbnail and a one-line "why it died" caption ("Beautiful. Wrong.").
   **This section is non-negotiable** — it's the studio's proof of
   discipline and should never be cut or diluted for a new project.
8. **What We Did** — an editorial scope list (numbered deliverables), never
   naming an individual person — this is a studio's portfolio, not a
   freelancer's credit line.
9. **In the World** — lifestyle/campaign imagery, if available.
10. **Outcome** — results/claims, plus a "Read the full case study →" link
    to a standalone deep-dive page (see below), and a "See all work →" link
    back to `index.html#work`.

**Nav on project pages** uses the same Glass Bar as the homepage, adapted
for a dark cover — top-state links are light, not ink, since the cover is
dark (the homepage hero is also dark, so this now matches). Internal links
point at `index.html#section`, not absolute paths.

## The standalone case study

A separate, longer deep-dive (`spiral-case-study.html`) that the project
page's "Read the full case study" button opens in a new tab. These come
from Ananya as pre-built bundled HTML exports (large embedded images) — if
one exceeds ~20MB, **recompress before committing**: Vercel doesn't share
Cloudflare's hard 25MiB/file limit, but a multi-tens-of-MB HTML file is
still a bad experience and slow to push. Keep any single project file under
a few MB if at all reasonable.

Case study pages get a floating **"← Back to Cenra"** button injected
bottom-left, styled as a dark glass pill with the same cobalt fill-wipe
hover as the rest of the site, linking to `index.html`. If a case study is
a self-unpacking bundle (check for `<script type="__bundler/manifest">` or
similar), any injected UI must be **re-asserted on an interval after load**,
because bundle unpacking can `replaceWith()` the whole document and wipe a
one-time injection.

## Adding a new project — the actual workflow

1. Duplicate `spiral.html` → rename for the new project (e.g. `noema.html`).
   Keep the same section order from the template above; replace content.
2. If there's a separate deep-dive doc, add it as `<project>-case-study.html`
   and wire the "Read the full case study" button to it (relative link,
   same folder).
3. In `index.html`, add one entry to the `projects` array in the carousel
   script: `{name, tags, year, color, url, img}`. `img` should be a
   representative image (base64 data URI is fine for a single card image).
4. Test locally first — open `index.html` directly in a browser and click
   through the whole chain: card → project page → case study → back to
   home. Every internal link is relative and same-folder, so this only
   works if all files are actually sitting together.
5. `git add . && git commit -m "add <project>" && git push` — Vercel
   auto-deploys to cenrastudios.com within seconds. Hard-refresh
   (`Ctrl+Shift+R`) to see it — browsers cache aggressively, so "it's not
   updating" is very often just a stale cache, not a failed deploy.

## Working style — read before making creative calls

- Ananya reacts by eye, not by spec. Show options; don't just pick one and
  present it as final unless explicitly asked to lock something.
- She wants direct, honest creative pushback — including telling her when
  an idea trends toward a generic/templated look. Don't just execute
  uncritically.
- Depth over breadth: one flagship project done thoroughly (SPIRAL) is the
  model. Resist padding out the site with shallow placeholder work — it's
  fine and expected for the carousel to show fewer real projects with
  honest "Coming soon" placeholders rather than fabricated ones.
- She's still building terminal/git fluency — keep instructions concrete
  and step-by-step, and don't assume familiarity with CLI conventions.

## Open items / known divergences

- **Type system:** project pages lean more on Inter than the homepage's
  JetBrains Mono-heavy nav/labels. This divergence hasn't been reconciled
  site-wide — ask before unifying it, since it's a real design decision,
  not a bug.
- The homepage carousel currently has one real project (SPIRAL) and two
  honest "Coming soon" placeholder cards. Replace those as real projects
  are finished, per the workflow above.
- Domain DNS lives on **Namecheap**, not Cloudflare — do not suggest an
  nameserver migration without an explicit MX/TXT backup step first; this
  is flagged as a deliberate future task, not an oversight.
