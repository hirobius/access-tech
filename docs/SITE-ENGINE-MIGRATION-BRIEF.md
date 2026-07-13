# Site-Engine Migration Brief — Access Tech

**For:** an agent session working in `hirobius/site-engine` (with this repo readable, or this
file + `content/access-tech.json` + `/images` copied over).
**Goal:** rebuild the Access Tech site as the engine's **first real-client instance**, at full
parity with the live static build — as a **parallel pilot**, not a launch blocker.

---

## 1. Context you need

- **This repo** (`hirobius/access-tech`, renamed `access-t` on GitHub) is a single-file static
  site: `index.html` + `privacy.html` + `404.html` + `/images` + `/fonts`. It is
  **content-complete, QA'd on real devices, and launch-gated** only on business steps
  (payment, DNS, un-gating). It deploys via Vercel git-integration (project `access-tech`,
  production alias `access-tech-xi.vercel.app`, Deployment Protection ON, `noindex` ON).
- **The client** (Phil, Access Tech) approved a repositioning: *fire management & land
  stewardship consulting with in-house implementation* — "advisors first, operators second,"
  motto "Reclaim. Restore. Protect." The static build already reflects this.
- **The pilot rule:** the static site launches for Phil on its own timeline. The engine
  instance takes over production **only when it reaches parity** (checklist below). Do not
  modify this repo's `index.html` from the engine session.

## 2. Source of truth

- **`content/access-tech.json`** (repo root `content/`) — complete ClientConfig: business
  identity, theme tokens, SEO, nav, every section's copy in order, all 9 services, 5-step
  process, 3 real before/after pairs, full assessment-form spec, asset manifest.
  **Copy is client-approved. Do not rewrite it. Render it.**
- **`/images`** — all referenced assets, already EXIF-corrected + WebP-optimized. Copy as-is.
- **`/fonts`** — self-hosted latin subsets (Bricolage Grotesque variable + Hanken Grotesk
  400–800) + `fonts.css`. Reuse; do not reintroduce Google Fonts calls.
- **Design reference:** the live build (`access-tech-xi.vercel.app`, needs share link or
  Protection off). Match its look within reason — tokens in the JSON `theme` block; exact
  CSS is in this repo's `index.html` if a value is ambiguous.

## 3. Section order (must match)

utility bar (phones) → sticky nav + mobile overlay → hero → trust band → about →
**process (5 steps)** → services (9) → before/after gallery (3 pairs) → why-us (4) →
service area (tags + embedded map) → assessment form + phone cards → final CTA → footer.

## 4. Functional requirements (parity checklist — verify each)

- [ ] **Form** posts to Web3Forms (key in JSON) via AJAX with inline success/error, honeypot,
      all fields per spec (objectives = checkboxes, shared `name="objectives"`); subject line
      `"New property assessment request — Access Tech website"`; test a real submission
      end-to-end → lands at adrian@hirobius.com.
- [ ] **CTAs:** every estimate CTA reads exactly `Request a Free Assessment` with a
      forward-arrow icon (nav, hero, final CTA, form submit).
- [ ] **SEO:** title/meta/canonical/og/twitter from JSON; LocalBusiness JSON-LD;
      `robots.txt` + `sitemap.xml`; **`noindex` ON until launch flip**; og-image is
      `/images/og-image.jpg`.
- [ ] **Pages:** `/privacy.html` equivalent (copy in this repo) linked in footer; branded 404.
- [ ] **A11y:** alt text from JSON, `:focus-visible` outlines, skip link, WCAG-AA contrast
      (greens on light backgrounds must use the darker `emberDark`).
- [ ] **Perf gotchas learned the hard way (do not repeat):**
      - NO `content-visibility:auto` on sections containing `loading="lazy"` images/iframes
        (WebKit renders them blank).
      - Real content = real `<img>` elements with width/height attrs — never CSS-background
        divs whose height depends on children.
      - Photos of sunny forest compress poorly — WebP q58–66, ≤1600px, or sizes balloon.
      - Test at 390px width: form padding, nav overlay CTA, footer (no orphaned
        padding-bottom).
- [ ] **Map:** free Google embed (`maps.google.com/maps?q=Coeur+d%27Alene,+ID&z=7&output=embed`),
      no API key.

## 5. Deploy target

New Vercel project (suggest `clients-access-tech` per fleet convention), Deployment
Protection ON, `noindex` ON. Do NOT touch the existing `access-tech` Vercel project or the
`accesstechnw.com` domain — the static build owns production until cutover is explicitly
approved by Adrian.

## 6. Cutover criteria (Adrian decides, engine session prepares)

1. Side-by-side visual pass on phone + desktop vs the static build.
2. Real form submission delivered from the engine build.
3. Lighthouse ≥ static build (currently: single file, self-hosted fonts, preloaded WebP hero).
4. Then: point domain/alias at the engine project, archive this repo's site files (keep
   `content/` as the living config).

## 7. Open items that travel with the migration

- Dedicated hero shot from Phil may arrive → swap `hero` asset (crop recipe: center band,
  16:10, ~42% from top).
- Unplaced assets available (see JSON `assets.unplacedAvailable`), incl. the QTAC fire-pumper
  shot — a natural fit if the engine template has a "fire response" or equipment block.
- Analytics (Plausible/Umami) intended post-launch; leave a config slot.
- Privacy copy needs Adrian's final read regardless of stack.
- GitHub Issues in THIS repo are its task source of truth (fleet convention); file
  engine-side tasks in `site-engine`.
