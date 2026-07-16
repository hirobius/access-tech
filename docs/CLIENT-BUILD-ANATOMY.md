# Client Build Anatomy — Access Tech (Hirobius template seed)

A code-accurate teardown of Hirobius's **first** client site so it can be turned into a
reusable template for mass-producing local-service marketing sites. Everything below is
read off the actual `index.html` (~1,194 lines, single self-contained file).

> **Naming note (important):** the code's two layouts are labeled by *theme tokens*, not by
> the README's "Full/Condensed" words. In the markup:
> - **Option 1** (`#layout-one`, the shipping design) uses the `--ember*` token family —
>   originally an **orange** accent, **recolored to green** (`--ember:#2f8f4e`).
> - **Option 2** (`#layout-two`, the alternate/condensed) uses the `--leaf*` token family —
>   natively **green**.
>
> So both render green, but via two different token sets and two different font pairings.
> The bottom toggle is a pitch artifact and is removed at launch (Option 1 ships).

---

## 1. Overview

| | |
|---|---|
| **Client** | Access Tech (owner: Phil) |
| **Service** | Forestry mulching, fuel reduction & land improvement |
| **Area** | North Idaho & Eastern Washington |
| **Phones** | ID 208-500-8988 · WA 509-789-0371 |
| **Domain** | accesstechnw.com |
| **Built by** | Hirobius (one-person agency, Adrian — adrian@hirobius.com) |
| **Stack** | One static `index.html`, inline CSS + JS, **no build step** |
| **Assets** | Self-hosted in `/images` |
| **Hosting** | Vercel (managed static; portable to Netlify / Cloudflare Pages) |
| **Form** | Web3Forms (host-agnostic, AJAX) → emails adrian@hirobius.com |
| **Business model** | Access Tech (one-off deal): $1,500 upfront build + case-by-case edits. **Standard model TBD — recurring component required.** Edits are request-based + AI-assisted (no client CMS) |

**Why custom static + AI editing (not Duda/Webflow/headless CMS):** margins and control.
A self-contained zero-dependency file is trivially hostable, portable, and cheap to run; the
token system means per-client re-theming is mostly variable swaps.

---

## 2. Page anatomy (Option 1 — the shipping layout)

Top-level wrapper: `<div id="layout-one">`. Sections in document order:

| # | Section | id / class | Purpose | Key content |
|---|---------|-----------|---------|-------------|
| 1 | Utility bar | `.utility` (`.u-phones`, `.u-area`) | Always-visible phones + area | `tel:` links for both states; "Serving North Idaho & Eastern Washington" |
| 2 | Nav | `header.nav` (`.brand`, `nav.menu#menu`, `.burger#burger`, `.nav-cta`) | Sticky header + mobile overlay menu | Logo (`/images/logo-white.png`), anchors to About/Services/Gallery/Why/Area, "Free Estimate" CTA |
| 3 | Hero | `.hero#top` (`.hero-bg`, `.hero-video`, `.hero-inner`) | Headline + primary CTA | Eyebrow, H1 "Professional Forestry Mulching **& Fuel Reduction**", sub-lead, two buttons; bg = `mulcher-cleared-area.jpg` poster on an empty `<video>` |
| 4 | Trust band | `.trust` (`.trust-item`) | 4 quick credibility points | Degreed Forester · Wildfire-Risk Focused · Local to ID & WA · Free On-Site Estimates |
| 5 | About | `.sec.paper#about` (`.about-grid`, `.about-copy`, `.about-visual`, `.creds`, `.cred`, `.about-badge`) | Owner story + credentials | Two paragraphs; cred cards "Forest Resource Management" / "Fire Ecology & Management"; visual = `mulcher-at-work.jpg`; badge "Practical / Results that last" |
| 6 | Services | `.sec.dark#services` (`.svc-grid`, `.svc`, `.svc-ic`) | Service catalog | 9 cards: Forestry Mulching, Fuel Reduction, Fire Mitigation, Property Cleanup, Understory Thinning, Trail Creation, Access Improvements, Small Tree Removal, Land Improvement |
| 7 | Before & After | `.sec.paper-2#gallery` (`.ba-grid`, `.ba-card`, `.ba-pair`, `.ba-flag`, `.ba-cap`) | Strongest proof | 3 before/after pairs (still **LoremFlickr placeholders** + placeholder captions "Project Name / Location") |
| 8 | Why | `.sec.paper#why` (`.why-grid`, `.why`, `.why-ic`) | Differentiators | 4 cards: forestry background, focused on protection, local to terrain, practical results |
| 9 | Service area | `.sec.dark#area` (`.area-grid`, `.area-copy`, `.area-tags`, `.area-tag`, `.area-map`, `.pin`) | Coverage | Tags (North Idaho, Eastern Washington, Rural Homeowners, Acreage & Timberland, HOAs & Communities); map = **LoremFlickr placeholder** with two animated `.pin`s |
| 10 | Estimate form | `.sec.paper#estimate` (`.est-grid`, `.est-side`, `.phone-card`, `form.est#estimate-form`) | Lead capture | Two phone cards + Web3Forms form (fields below); status line `#estimate-status` |
| 11 | Final CTA | `.final` | Closing conversion push | "Reclaim, restore & protect your land" + `.btn-dark` to `#estimate` |
| 12 | Footer | `footer` (`.foot-grid`, `.foot-bottom`) | Nav + contact + legal | Logo, explore links, contact links, `© 2026 Access Tech` |

**Form fields** (`form.est#estimate-form`, `action="https://api.web3forms.com/submit"` POST):
hidden `access_key`, hidden `subject`, hidden `from_name`, hidden honeypot `botcheck`;
visible `name`*, `phone`*, `email`*, `address`, `acreage` (select), `message`* (textarea),
`attachment` (file, image/\*). Submit handled via AJAX (`fetch`) with inline success/error.

**Option 2** (`#layout-two`) mirrors the same story more compactly — `.utility`, `.v2-bar`,
`.v2-hero`, `.v2-sec` services (6 cards), `.v2-mint` gallery, `.v2-dark` why (3 cards),
`.v2-mint-2` estimate, `.v2-foot`. Its form is a **dead preview** (`onsubmit` → `alert('…built in Carrd')`,
no field `name`s). Option 2 is slated for deletion at launch.

---

## 3. Design system (extracted from `:root`)

### Color tokens

**Palette (shared base):**

| Token | Hex | Token | Hex |
|---|---|---|---|
| `--pine-950` | `#0d1c14` | `--pine-900` | `#11241a` |
| `--pine-800` | `#16291f` | `--pine-700` | `#1d3527` |
| `--forest-600` | `#2f5a3a` | `--moss-500` | `#688a5c` |
| `--moss-300` | `#a9c19c` | `--bone` | `#f5f1e6` |
| `--bone-200` | `#ece5d4` | `--kraft` | `#d8c8a4` |
| `--ink` | `#1b1a14` | `--ink-soft` | `#48463d` |
| `--bark` | `#4a3a28` | | |

**Option 1 accent (`--ember*`, "recolored green to match the brand"):**
`--ember:#2f8f4e` · `--ember-dark:#236e3b` · `--ember-soft:#9bd9ad`

**Option 2 accent (`--leaf*`, native green):**
`--leaf:#2f8f4e` · `--leaf-dark:#236e3b` · `--leaf-soft:#9bd9ad` · `--leaf-deep:#13321f`
plus surfaces `--mint:#f2f8f1` · `--mint-2:#e7f1e6`

> The accent hexes are **identical** between `--ember` and `--leaf` (both `#2f8f4e` family);
> the two sets exist for historical/structural reasons, not visual difference.

**Lines & shadows:**
`--line:rgba(0,0,0,.10)` · `--line-light:rgba(255,255,255,.12)`
`--shadow:0 22px 55px -26px rgba(0,0,0,.5)` · `--shadow-sm:0 12px 32px -22px rgba(0,0,0,.45)`

### Spacing scale

`--s1:.5rem` · `--s2:1rem` · `--s3:1.5rem` · `--s4:2rem` · `--s5:3.5rem` · `--s6:5rem` · `--s7:7.5rem`
Section rhythm: `--section-y:clamp(6.5rem,9.5vw,10rem)`

### Layout / radius

`--maxw:1160px` · `--maxw-text:680px` · `--radius:6px` · `--radius-lg:12px`

### Type ramp + fonts

| | Option 1 | Option 2 (`#layout-two` overrides) |
|---|---|---|
| Display | `--font-display:'Bricolage Grotesque'` | `'Cabinet Grotesk'` (Fontshare) |
| Body | `--font-sans:'Hanken Grotesk'` | `'Satoshi'` (Fontshare) |
| Loaded via | Google Fonts CSS | Fontshare API CSS |
| Display weight | 700 | 500 (single uniform weight) |

Ramp values: `h1/h2/.display` line-height 1.06, letter-spacing −.022em; H1 `clamp(2.9rem,6vw,4.7rem)`;
section H2 `clamp(2.1rem,4.2vw,3.1rem)`; `.lead` `clamp(1.18rem,1.9vw,1.4rem)`; body line-height 1.7;
`.eyebrow` uppercase, letter-spacing .22em, .74rem.

### Buttons

| Class | Style |
|---|---|
| `.btn` | base: inline-flex, uppercase, .08em tracking, `padding:1.05rem 1.8rem`, `border-radius:var(--radius)` |
| `.btn-primary` | `background:var(--ember)`, white text; hover `--ember-dark` + lift |
| `.btn-ghost` | transparent, white text, translucent border (on dark) |
| `.btn-dark` | `background:var(--pine-900)`, bone text (used in final CTA) |
| `.v2-btn` / `.v2-btn-ghost` | Option 2 equivalents on `--leaf` |

---

## 4. Per-client vs shared — THE KEY SECTION

Everything below split into what **changes per client** (the seed `ClientConfig`) vs what is
**shared template** (write once, reuse across the fleet).

### Changes per client (every value that is Access-Tech-specific)

| Category | Per-client values (as they appear in this build) |
|---|---|
| **Identity** | Business name "Access Tech"; sub-label "Forestry & Land" / "Land Management"; owner "Phil" |
| **Tagline / H1** | "Professional Forestry Mulching & Fuel Reduction"; hero accent span; sub-lead copy |
| **Services** | The 9-item list (name + 1-line description + icon each) |
| **Trust points** | 4 items (Degreed Forester, Wildfire-Risk Focused, Local to ID & WA, Free On-Site Estimates) |
| **About copy** | 2 paragraphs + 2 credential cards (Forest Resource Management; Fire Ecology & Management) + badge text |
| **Why points** | 4 differentiator cards |
| **Service area** | Region names + audience tags + map pins (lat/region labels) |
| **Phones** | ID `208-500-8988` (`tel:2085008988`), WA `509-789-0371` (`tel:5097890371`) |
| **Brand colors** | `--ember`/`--leaf` accent (`#2f8f4e`) + `--ember-soft`/`--leaf-soft` |
| **Fonts** | Bricolage Grotesque + Hanken Grotesk (chosen pair) |
| **Logo** | `logo-white.png`, `logo-color.png`, `logo-icon.png` (+ favicon) |
| **Photos** | hero (`mulcher-cleared-area.jpg`), about (`mulcher-at-work.jpg`), gallery before/after pairs, `og-image.jpg` |
| **Copy (all of it)** | every headline, eyebrow, paragraph, button label, form placeholder, footer text |
| **Lead email** | adrian@hirobius.com (via Web3Forms `access_key` `31719ab4-…`) |
| **Domain** | accesstechnw.com (used in canonical/OG/JSON-LD URLs + footer) |
| **SEO** | `<title>`, meta description, OG/Twitter title+desc, `og:image` URL |
| **JSON-LD** | LocalBusiness name/description/url/logo/telephone/areaServed/knowsAbout/contactPoints |
| **Form subject** | hidden `subject`, `from_name` strings |

### Shared / template (write once, do not vary per client)

- The **section skeleton** + class/id system (utility → nav → hero → trust → about → services →
  gallery → why → area → estimate → final → footer).
- The **design-token contract** itself (token *names*: `--s1..--s7`, `--section-y`, `--radius*`,
  `--shadow*`, `--maxw*`, button classes). Only the *values* of brand tokens vary.
- All **layout CSS** (grids, responsive breakpoints at 900/680/420px, mobile overlay nav).
- **Behavior JS**: burger nav, IntersectionObserver scroll-reveal, Web3Forms AJAX submit handler.
- **Form structure + spam controls** (honeypot `botcheck`, required-field pattern, success/error states).
- **SEO scaffold shape** (the *tags*, not their content): favicon link, OG/Twitter blocks, JSON-LD schema.
- Generic icon set (currently inline SVG; migrating to Lucide).
- The `.topo` texture, `.ph` placeholder component, `.reveal` animation system.

---

## 5. Proposed `ClientConfig` shape

A single per-client config that the shared template renders from. TS-ish / JSON:

```jsonc
{
  "business": {
    "name": "Access Tech",
    "subLabel": "Forestry & Land",
    "owner": "Phil",
    "domain": "accesstechnw.com",
    "copyrightYear": 2026
  },
  "contact": {
    "leadEmail": "adrian@hirobius.com",        // Web3Forms target
    "web3formsAccessKey": "31719ab4-ebe8-484a-88bc-ed84acbc8b89",
    "phones": [
      { "label": "Idaho",      "regionCode": "US-ID", "display": "208-500-8988", "tel": "2085008988" },
      { "label": "Washington", "regionCode": "US-WA", "display": "509-789-0371", "tel": "5097890371" }
    ]
  },
  "serviceArea": {
    "blurb": "North Idaho & Eastern Washington",
    "regions": ["North Idaho", "Eastern Washington"],
    "audienceTags": ["Rural Homeowners", "Acreage & Timberland", "HOAs & Communities"],
    "pins": [
      { "label": "North Idaho", "top": "38%", "left": "30%" },
      { "label": "Eastern WA",  "top": "55%", "left": "62%" }
    ]
  },
  "theme": {
    "accent": "#2f8f4e",
    "accentDark": "#236e3b",
    "accentSoft": "#9bd9ad",
    "fonts": {
      "display": { "family": "Bricolage Grotesque", "provider": "google" },
      "body":    { "family": "Hanken Grotesk",      "provider": "google" }
    }
  },
  "assets": {
    "logoWhite": "/images/logo-white.png",
    "logoColor": "/images/logo-color.png",
    "logoIcon":  "/images/logo-icon.png",
    "favicon":   "/images/logo-icon.png",
    "ogImage":   "/images/og-image.jpg",
    "hero":      "/images/mulcher-cleared-area.jpg",
    "about":     "/images/mulcher-at-work.jpg"
  },
  "hero": {
    "eyebrow": "North Idaho & Eastern Washington",
    "headline": "Professional Forestry Mulching",
    "headlineAccent": "& Fuel Reduction",
    "sub": "Helping landowners reclaim, restore, and protect their property…",
    "primaryCta": { "label": "Request a Free Estimate", "href": "#estimate" },
    "secondaryCta": { "label": "View Services", "href": "#services" }
  },
  "trust": [
    { "icon": "trees",  "label": "Degreed Forester" },
    { "icon": "shield", "label": "Wildfire-Risk Focused" },
    { "icon": "pin",    "label": "Local to ID & WA" },
    { "icon": "check",  "label": "Free On-Site Estimates" }
  ],
  "about": {
    "eyebrow": "About Access Tech",
    "lead": "Professional forestry knowledge, backed by real field experience.",
    "paragraphs": ["…", "…"],
    "creds": [
      { "k": "Degree", "v": "Forest Resource Management" },
      { "k": "Degree", "v": "Fire Ecology & Management" }
    ],
    "badge": { "n": "Practical", "t": "Results that last" }
  },
  "services": [
    { "icon": "mulch", "title": "Forestry Mulching", "desc": "Grind brush, saplings…" }
    // …9 total
  ],
  "gallery": [
    { "title": "Project / Location", "blurb": "…", "before": "/images/…", "after": "/images/…" }
  ],
  "why": [
    { "icon": "trees", "title": "A real forestry background", "desc": "…" }
    // …4 total
  ],
  "form": {
    "subject": "New estimate request — Access Tech website",
    "fromName": "Access Tech Website",
    "acreageOptions": ["Under 1 acre","1–5 acres","5–10 acres","10–20 acres","20+ acres","Not sure"]
  },
  "seo": {
    "title": "Access Tech — Forestry Mulching & Fuel Reduction | North Idaho & Eastern WA",
    "description": "Professional forestry mulching, fuel reduction…",
    "ogImageUrl": "https://accesstechnw.com/images/og-image.jpg",
    "noindex": true   // flip to false at launch
  },
  "jsonLd": {
    "type": "LocalBusiness",
    "knowsAbout": ["Forestry Mulching","Fuel Reduction","Fire Mitigation", "…"]
  }
}
```

---

## 6. Moving parts / integrations

| Concern | How it works today | Notes / risk |
|---|---|---|
| **Hosting** | Vercel managed static; portable to Netlify / Cloudflare Pages | Deployment Protection must be turned off at launch |
| **Forms** | Web3Forms, `POST https://api.web3forms.com/submit`, AJAX `fetch` with inline success/error | `access_key` `31719ab4-…` embedded in HTML (public by design); honeypot `botcheck` is the only spam control |
| **Images** | Self-hosted in `/images`, optimized via Pillow | **Gallery + service-area map still hot-link LoremFlickr** (`loremflickr.com` / `live.staticflickr.com`) — not yet swapped |
| **Fonts** | Google Fonts (Bricolage + Hanken) **and** Fontshare (Cabinet + Satoshi) | Both pairs loaded render-blocking; drop the Fontshare pair when Option 2 is removed |
| **SEO** | `<title>`, meta description, OG + Twitter cards, LocalBusiness JSON-LD | `og:image` URL is absolute to accesstechnw.com — verify it resolves post-launch |
| **Favicon** | `<link rel="icon" type="image/png" href="/images/logo-icon.png">` | green icon PNG |
| **Layout toggle** | `.vtoggle` + JS, persists choice in `localStorage['accesstech-layout']` | Pitch artifact — **remove at launch** |
| **Analytics** | **None** | No Plausible/Umami/GA yet (Phase 1 in backlog) |
| **Icons** | Inline hand-rolled SVG | Migration to Lucide in progress |

---

## 7. Templatization plan

Goal: go from this one-off to a reusable engine **without over-building**. Sequenced per the
repo's own guidance ("don't templatize now — premature").

**Now (ship Access Tech, ~1 session):**
- Strip Option 2 + the toggle + the dead `--leaf*`/Fontshare/`.v2-*` CSS & JS.
- Self-host the remaining LoremFlickr images (gallery + area map); swap in real photos.
- Confirm the Web3Forms submit delivers; remove `noindex` at launch.

**Phase 1 (only at 2–3 clients):**
1. **Content-as-data** — extract all per-client values (Section 4) into one `content.json` =
   the `ClientConfig` (Section 5). Markup becomes a template that reads from it.
2. **Theme-via-tokens** — the `:root` brand tokens become the per-client theme block. The token
   *names* are the stable contract; only values vary. This is already ~half-built — the single
   genuine asset of this build.
3. **Per-client instances** — one shared template repo; each client = `content.json` + theme +
   `/images`. Render with a light SSG (**Astro**) once multiple sites/multi-page exist — not before.
4. **Snapshot/freeze on handoff** — pin each delivered site to a template version so a future
   template change can't silently restyle a live client site (**fleet-drift risk**). Provide an
   "eject to standalone" path so any client can be lifted out.
5. **Repo strategy** — template repo + thin per-client repos (or one monorepo of instances);
   decide at volume, not now.

**Flag as premature today:** SSG adoption, multi-tenant app, CMS, the AI lead→config engine.
The token system means the refactor is cheap to defer; do it when a 2nd/3rd client forces it.

---

## 8. Missing template pieces to add

What a production template should have that this build lacks. "Now" = fold into Phil's build
before launch; "Defer" = add when templatizing (Phase 1).

| Piece | Status today | Now or Defer | Rationale |
|---|---|---|---|
| **404 page** | none | Defer (host default OK) | Vercel/Netlify give a usable default for a one-pager |
| **Thank-you / confirmation** | inline JS success state only (no URL) | **Now** | Inline state exists; a real URL helps conversion-tracking later. Inline is acceptable for launch |
| **robots.txt** | none | **Now** | Cheap; pairs with removing `noindex` |
| **sitemap.xml** | none | **Now** | Single URL sitemap; trivial and helps indexing |
| **Privacy policy page** | none | **Now** | Form collects PII — backlog item 11 flags it for every client site |
| **Analytics** | none | **Now (lightweight)** | Plausible/Umami snippet; you cannot prove lead value without it |
| **Performance / image budget** | source JPGs are 0.7–1.4 MB each | **Now** | Compress + size; add `loading="lazy"` below the fold |
| **Accessibility** | real photos are CSS backgrounds (no `alt`); good focus rings exist | **Now (partial)** | Convert hero/about/gallery to `<img alt>`; verify contrast on green |
| **Canonical tag** | none | **Now** | One line; avoids duplicate-URL issues across www/preview |
| **Real OG image** | placeholder `og-image.jpg` | **Now** | Branded 1200×630 before launch |
| **Spam beyond honeypot** | honeypot only | Defer | Add Web3Forms captcha if spam appears |

---

## 9. Open items / gaps

> Superseded 2026-07-16 (site launched). This was a pre-launch snapshot. The live task
> source of truth is **GitHub Issues** (fleet convention) plus **BACKLOG.md**; kept here
> only for the few items still genuinely open in code.

**Resolved since the snapshot:** noindex removed at launch; fonts self-hosted (latin subsets,
no Google Fonts); gallery + service-area map now real (photos + embedded Google map, no
LoremFlickr); layout toggle removed; robots.txt / sitemap.xml / canonical added; accessibility
pass done (real `<img>` + alt, focus-visible, AA contrast); og:image is a real branded graphic;
privacy.html + 404.html added; domain pointed at Vercel, Deployment Protection off.

**Still open in code (see issues #12, #13, #14):**
- Parked Option 2 layout (`#layout-two`, all `.v2-*`) still ships, and `--ember*` / `--leaf*`
  are now identical greens. Delete Option 2 and collapse to one token set (#14, parked pending
  Adrian). This also clears the old token-naming ambiguity: Option 1 runs on the recolored
  `--ember` tokens, so the surviving set should get an unambiguous name.
- Lucide still loads from the jsDelivr CDN; self-host it locally (#12; fonts already done).
- Minify + lazy-load below-the-fold (#13, minor).

**Business / post-launch (BACKLOG sections 1-4):** invoice the $1,500; swap the form key to Phil;
Search Console + Google Business Profile; analytics; define the standard recurring pricing.
