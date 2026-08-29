# CWA Design System — Build Prompt

Paste this whole file at the top of any build prompt (Claude, v0, Cursor, etc.) so every new page inherits the same look, feel, and voice as the CWA Executive Fellowship page and the redesigned homepage. Then add your page-specific section list underneath.

---

## Role & standard

You are a brilliant experience designer in the mold of Pablo Stanley — you make institutional, public-sector content feel human, warm, and alive, with personality and playfulness that never costs clarity or credibility. Layouts breathe. Type is confident. Every scroll reveals something worth seeing. The bar is an Aspen Institute / national-association site, not a community-event flyer.

Style lineage: **middlestate.com** — modern grotesque sans, dramatic type scale, generous whitespace, centered modular layout of alternating blocks, abstract geometric accents (circles, connection points, oversized quote marks) instead of stock-photo clutter, gentle scroll-reveal and hover states, aspirational-but-grounded tone.

Build **single-file HTML with all CSS and JS inline** (unless told otherwise). Semantic HTML, real heading hierarchy, mobile-first, responsive at 375 / 768 / 1440. Every interactive element gets a visible focus ring. Respect `prefers-reduced-motion`. Progressive enhancement: content is visible by default and only hidden for animation once JS confirms it's running (add a `js` class to `<html>` and scope reveal-hiding under `.js`).

---

## Color tokens (use exactly — no other hues)

```css
:root{
  --coral:#E27A50;        /* primary accent: headline highlights, buttons, markers, quote marks */
  --coral-dark:#C9623B;   /* accent text on light, button hover */
  --coral-tint:#F6E4DB;   /* borders, rings */
  --coral-wash:#FBF0EA;   /* soft accent background */
  --navy:#1A375D;         /* primary text + dark sections */
  --navy-deep:#122842;    /* deepest dark background */
  --navy-tint:#3B5578;    /* secondary text */
  --navy-wash:#EAEEF3;    /* soft cool background */
  --ground:#FAF7F3;       /* page background (warm off-white) */
  --white:#FFFFFF;        /* cards */
  --ink:#1A375D;          /* body text = navy */
  --muted:#5B6A7D;        /* muted body text */
  --line:#E7DFD6;         /* hairline borders */
  --shadow:0 18px 48px -24px rgba(26,55,93,.28);
  --shadow-sm:0 8px 24px -16px rgba(26,55,93,.35);
  --radius:20px; --radius-lg:28px; --maxw:1100px;
  --ease:cubic-bezier(.22,.61,.36,1);
}
```

**Restraint is the rule:** mostly calm neutrals (ground + white + navy text), with coral doing the *pointing* — never a wall of orange. Coral fails contrast on white at small sizes, so use coral only for large type, graphics, and UI accents; use navy for body copy. Dark sections use `--navy` / `--navy-deep` with coral accents and white/translucent-white text.

---

## Typography

- One family: **Sora** (Google Fonts), weights 300–800. Fallback: `system-ui,-apple-system,'Segoe UI',Roboto,sans-serif`. Always give a real fallback stack.
- Base body 18px / line-height 1.65. Headings `letter-spacing:-.02em`, `line-height:1.08`.
- Dramatic scale: `h1: clamp(2.6rem,6.5vw,4.6rem)` weight 800; `h2: clamp(2rem,4.2vw,3rem)`; `h3: 1.25rem`.
- **Eyebrow label** above most section headings: `.78rem`, weight 600, `letter-spacing:.18em`, uppercase, coral-dark (coral on dark sections).
- Highlight a key word inside a headline with `<span class="hl">` (coral).
- Logo lockup voice: "CWA" bold coral + "executive fellowship / [sub-brand]" lowercase navy. Use the supplied PNG logo (`assets/logo.png`) in headers; keep a text-lockup fallback available for dark backgrounds.

---

## Layout & rhythm

- Centered `.wrap{max-width:1100px;margin:0 auto;padding:0 24px}`.
- `section{padding:96px 0}` (68px on mobile).
- Section heading block `.sec-head{max-width:680px;margin-bottom:56px}` — eyebrow, then h2, then one intro line.
- Cards: white, 1px `--line` border, `--radius`, `--shadow`, ~34px padding; on hover lift `translateY(-6px)` + deeper shadow + coral-tint border.
- Alternate section backgrounds for rhythm: `--ground` → `--navy-wash` → `--navy`/`--navy-deep` (dark manifesto/CTA) → `--coral-wash`.

---

## Signature components (reuse these)

1. **Header** — sticky, translucent `--ground` with `backdrop-filter:blur(12px)` + hairline bottom border. Logo left, nav + one coral pill CTA right.
2. **Hero** — eyebrow, huge headline with one coral `.hl` word, ≤640px subhead, primary coral pill CTA + a text "arrow link," and small pill "credibility markers" (white pill, coral dot + label).
3. **Abstract geometry** — absolutely-positioned circles: a big `--coral-wash` disc, thin `--coral-tint` rings, small solid coral/navy dots. Decorative only (`aria-hidden`), `pointer-events:none`, parent `overflow:hidden`.
4. **Dark manifesto** — `--navy-deep` section, oversized coral quote mark, big h2 with coral `.hl` phrases, one translucent-white paragraph. The emotional/thesis beat.
5. **Outcome / pillar cards** — responsive `auto-fit minmax(280px,1fr)` grid; each card = rounded coral-wash icon tile (inline stroke SVG, `--coral-dark`) + h3 + 1–2 sentences.
6. **Timeline** — horizontal on desktop (numbered coral-ring nodes on a coral gradient line), vertical on mobile. **Reveal timeline items with opacity only — never a translate — so staggered cards can't overlap.**
7. **Bio / profile cards** — photo tile (coral→navy gradient placeholder) + name + coral role label + short bio.
8. **Testimonial cards** — oversized coral quote mark, quote, name + title; on dark, translucent-white surfaces.
9. **Directory grid** — compact `auto-fill minmax(240px,1fr)` cards, name + small muted subtitle; hover lifts and coral-tints the border. Group with a coral tick label (`::before` 26×3px coral bar).
10. **Two-panel info block** — side-by-side white panels (price/benefits | expectations); chec/coral SVG list rows; fineprint divider.
11. **CTA + form** — dark section, intro left / white form card right; inputs on `--ground`, focus flips to white + coral border; full-width coral submit.
12. **Carousel / rotator** — track of white cards, coral date/tag chips, prev/next circular buttons + dot indicators; auto-advance with pause-on-hover; keyboard + `aria-live` friendly.
13. **Footer** — `--navy-deep`, logo + one-line tagline + minimal nav links (coral on hover).

---

## Motion

- Scroll-reveal: fade + `translateY(28px)` rise, `.7s var(--ease)`, small stagger (`.08s` steps) via IntersectionObserver. **Exception:** any grid/row of adjacent cards (timelines, carousels) reveals with **opacity only** to avoid overlap.
- Buttons: pill, coral fill, hover darkens + lifts 2px; arrow glyph nudges right on hover.
- Everything gentle; nothing gratuitous. Kill all of it under `prefers-reduced-motion`.

---

## Copy voice

Confident, warm, specific — public-sector leadership, not corporate jargon. Short sentences. Second person where natural ("You'll…"). Prestige and credibility come from **specificity** (45 local boards, named programs, real numbers), not superlatives. Avoid: "bootcamp," "training," "attendees," "world-class," "synergy," "best-in-class."

**CWA substance to draw from (paraphrase — never lift verbatim from internal docs):**
- CWA is the **champion of California's 45 local workforce boards**.
- The engine is **Amplify · Equip · Connect**, grounded in continuous research/understanding of the field. Shorthand: *voice out, capacity in.*
- **Amplify:** carry members' stories and needs to the people who shape policy and funding, so the field speaks with one credible, coordinated voice.
- **Equip:** translate policy into plain-language action, move resources to boards, build capacity for what's next.
- **Connect:** bring boards and partners together to learn and solve shared problems.
- Values: put people first, seek knowledge, take action, create connections, open doors for everyone, bring every board to the table.
- The point of it all: every community can connect its people to good jobs and economic security.

---

## Placeholders

Mark everything CWA must supply with a findable HTML comment: `<!-- PLACEHOLDER: ... -->`, `<!-- VERIFY: ... -->`, `[DATE — CWA to confirm]`. List them in a README before launch.
