# Review: Valuatum Company Page (Raahen Terästuote Oy)

Reviewed: `index.html` + live at `https://project-cn5oy.vercel.app` (Chrome,
1440×900 desktop). Benchmarked against Finder.fi, Asiakastieto, and Kauppalehti.
Scope: this is a **mockup** — valuation and PDF-upload live in separate
products; company basics (CEO, employees, founded, address, contact) are not
available as data; only long-term credit scoring exists (no short-term).

## Updated after your feedback

- ✂️ Dropped: adding valuation gauge, PDF-upload widget, CEO/employees/contact
  fields — out of scope.
- ✅ Kept & sharpened: AI narrative, peer benchmarking, credit-section
  reorg + moving it up, removing the short-term credit card.
- ➕ Added: live UI opinions from the Chrome session, Finder.fi comparison,
  new observations on blur strength, info panel emptiness, CTA split, and
  a concrete proposed section order.

---

## Live UI opinions (Chrome, 1440×900)

**What works well visually**
- The dark-green body + white cards is distinctive and reads as "premium
  finance tool" rather than "generic SaaS". Competitors (Finder, Asiakastieto)
  all use white backgrounds; this is a genuine identity.
- 42 px hero title with tight `letter-spacing:-.045em` and 800 weight is
  confident and feels Bloomberg/FT-tier.
- The 38 px white "Taloustiedot" section heading over the dark body is a
  great beat — it punctuates the page without adding a divider.
- The 6-column chart grid resolves cleanly at desktop: three equal KPI bars
  on top, two wide line charts below. Good rhythm.
- The 2024 bar is highlighted (solid green) while prior years are muted —
  small detail but makes "latest year" read instantly. Nice.
- Metric strip (Liikevaihto / Kasvu / EBIT-% / Happotesti) is already
  tighter and more scannable than Finder's equivalent.
- Shadow system (`--shadow` and `--shadow-soft`) is consistent — cards feel
  like they belong to the same product.

**What feels off**
- **The "Yritystiedot" panel has 2 rows and is 135 px of near-empty
  real estate.** Don't delete the data — fold it into the header (see
  "Metadata strip" below). Also: show the **5-digit NACE/TOL code
  `25.530`**, not the 2-digit `25`, for correctness and authority.
- **Page is 3 972 px tall at desktop; credit-risk starts at y≈2 980 (75 %
  down).** Given that credit-risk is the monetized section, it needs to
  appear earlier. See proposed order below.
- **The blur on locked values is too weak.** `filter:blur(3px)` leaves
  "BBB", "41,7", "0,3730 %", "8,6 %" readable if you squint — the teaser
  effectively gives the answer away. Either bump to `blur(7–9px)`, replace
  with a placeholder glyph (`●●●`), or show a gauge pointer without the
  number.
- **CTA split across the header is awkward.** "Vie talousluvut" sits at
  x≈1194 (top-right) while the two primary CTAs sit at x≈82 (bottom-left of
  the header), ~1100 px apart. Consolidate: put primary + secondary +
  ghost-export together, either as a single row top-right or a single row
  just under the hero paragraph.
- **"Vie talousluvut" is a button with no handler, and the gnav search has
  no `oninput/onkeydown`.** Expected in a mockup, but the "Vie" button
  would be more believable placed next to the ratio table (where an export
  semantically belongs) rather than in the hero.
- **Pricing card sits side-by-side with the credit teaser (917 + 312 px
  columns).** Users see the price before they've processed what they'd be
  buying. Better flow: teaser → "what you get" bullets → pricing → CTA.
- **"Uutta!" badge** is charming today but ages badly. Swap for
  "Päivitetty 04/2026" or drop after launch.
- **The reveal animation** starts everything at `opacity:0`. If JS fails or
  is slow, the user sees a blank page. Consider `.no-js` fallback or
  rendering the first viewport without the animation.
- **Charts are not keyboard/screen-reader accessible** — canvases with no
  data-table fallback. Add a visually-hidden `<table>` per chart with the
  same series.

**Small visual nits**
- Cards use `border:1px solid rgba(255,255,255,.74)` which reads as a faint
  outer glow against the dark body. I called this "weird" in the first pass;
  after viewing, it's subtle and intentional-looking. Keep.
- On `.metric-label` the green-gray text over `--green-softer` is borderline
  for 12 px; worth a contrast check.
- Line charts: 2024 point is the same size as prior years. Match the
  bar-chart emphasis (bigger / filled) so the "latest-year" language stays
  consistent across chart types.
- The `metric-strip` cards have `border-radius:8px` but `--r:8px` elsewhere;
  unified.
- In the JS: `const EBITDA = [154,134,449,237,208];` is declared and never
  used. Remove or render.

---

## Proposed section order

Current:
1. Intro banner
2. Company header (42 px title + about + metric strip + CTAs)
3. Yritystiedot (2 rows)
4. Taloustiedot (charts)
5. Tunnusluvut (ratio table)
6. Luottoriski (teaser + pricing)
7. Saman toimialan yritykset

Proposed:
1. Intro banner — convert the "Kokeile nyt ilmaiseksi" text link to a pill button
2. Company header — absorb Yritystiedot data into a compact metadata strip
   just under the meta row (Y-tunnus already shown + **TOL 25.530** + rekisterin
   tila + uusin tilikausi + "Päivitetty 04/2026"); consolidate CTAs
3. **Luottoriski** — moved up, redesigned as a sales-pitch spread (see below);
   AI narrative / risk-flags card introduces the section
4. Taloustiedot (charts) — with industry-median overlay
5. Tunnusluvut (ratio table) — with the new **"Lataa talousluvut"** split
   button pinned to its top-right
6. Saman toimialan yritykset — promote to mini peer-comparison with 2–3 KPIs
   per peer, and replace the plain text "Katso kaikki…" links with proper
   tiles (see below)
7. ~~Yritystiedot~~ — section removed; data moves to the header

---

## Design direction — fine-tuning moves

Stay with the current identity (dark-green body, white cards, 42 px hero) but
push it further towards **editorial Nordic finance** — the page should feel
like a quarterly investment magazine spread, not a SaaS dashboard. Every
suggestion below is additive polish, not a redesign.

### A. Typography lift

- **Introduce a display face for the hero + section titles.** Inter at 42 px
  800 is fine, but the page has magazine ambitions it isn't cashing in. Pair
  Inter (body, UI) with a serif display face only at the two big headings
  — the hero `company-title` and the 38 px white "Taloustiedot"/"Luottoriski"
  titles. Free options: **Instrument Serif**, **Fraunces** (variable, excellent
  opsz axis at display sizes), or **Young Serif**. Keep Inter everywhere else.
  One small font swap, big jump in perceived quality.
- **Tabular figures everywhere numbers live.** Add
  `font-variant-numeric: tabular-nums` to `.ftable`, `.metric-value`,
  `.credit-metric strong`, and Chart.js axis labels. Digits line up; the
  whole ratio table instantly reads as financial, not marketing.
- **Gold hairline above the hero kicker.** A 1 px × 56 px `--gold` rule
  above the `about-kicker` "YRITYSKUVAUS" — a magazine masthead cue.

### B. Header metadata strip (replaces Yritystiedot panel)

Below the current `.company-meta` row, add a second row styled as a quiet
editorial dateline:

```
Y-tunnus 3012953-4  │  TOL 25.530 Metallituotteiden valmistus  │  Aktiivinen  │
Tilikausi 2024  │  Päivitetty 04/2026
```

- 13 px, weight 550, `--text-2`, dividers `1px` `var(--border)`.
- Single line at desktop; wraps at tablet.
- No card, no panel — just a flow row inside the header card.

Keeps every datum the current panel has (plus context the user has asked for),
costs ~40 px of vertical space instead of 135 px, and reads as authoritative
metadata instead of a half-empty table.

### C. Luottoriski — the sales-pitch spread

Stop treating this section as "another panel with locks." Make it the page's
signature moment. It can look *different* from everything else on the page —
in fact it should.

**Palette inversion.** Section background becomes
`linear-gradient(180deg, #163B2D 0%, #0F2A20 100%)` (the existing `--green`
darkened); cards inside become **cream `#FAF7EF`** instead of pure white, with
warm `--gold #B98F42` as the accent colour instead of green. The cooler
greens of the rest of the page don't re-enter this section. The credit
section then visually reads as "the paid product", a little like a gold-foil
magazine insert.

**Layout — one hero tile, not a preview-grid.**

```
┌─────────────────────────────────────────────────────────────────────┐
│  LUOTTORISKI                                    Ilmoita virheestä › │
│  Arvonmäärittelyt ja päätökset, paremmin perusteltuina.             │
│                                                                     │
│  ┌───────────── credit gauge ──────────────┐  ┌─ Mitä saat? ──────┐ │
│  │   arc C──B──BB──[BBB]──A──AA──AAA       │  │ • 5 vuoden trendi │ │
│  │        ●●● / 100    ← locked number     │  │ • Konkurssiriski  │ │
│  │   ┌────────┬────────┬────────┐          │  │ • Luottoraja      │ │
│  │   │ Konk.  │ Luotto-│ Lainan │          │  │ • Vertailu        │ │
│  │   │ riski  │ raja   │ hinta  │          │  │   toimialaan      │ │
│  │   │ ●●●    │ ●●●    │ ●●●    │          │  │ • Selitys miksi   │ │
│  │   └────────┴────────┴────────┘          │  └───────────────────┘ │
│  └─────────────────────────────────────────┘                        │
│                                                                     │
│  ⚡ Päivittyy  🧭 Selitetty  🔓 2 € kertamaksu  ⭐ 12 400 raporttia  │
│                                                                     │
│  ┌─ 2 € ──┬─ 10 € ──┬─ 30 € ★──┬─ 50 € ──┐                          │
│  │ yks.   │ 10 rap. │ 50 rap. │ rajaton │     [ Osta 2 € — heti ]  │
│  └────────┴─────────┴─────────┴─────────┘                          │
└─────────────────────────────────────────────────────────────────────┘
```

**Concrete moves:**

1. **Arc gauge, not a 7-pill ladder.** Upgrade the rating scale to a true
   semicircle gauge with C–B–BB–BBB–A–AA–AAA along the arc, a gold pointer
   at the company's position, and the numeric score below it. An arc says
   "measurement" the way pills can't. The lock/`●●●` mask covers only the
   exact number, not the pointer position — that way the preview has real
   information value (the user sees "somewhere around BBB"), which *builds*
   desire rather than teasing it.
2. **`●●●` instead of `blur(3px)`.** Replace the blurred numbers with
   explicit dotted placeholders. Cleaner, more honest, accessible, and the
   Finder.fi convention people already recognise in this market.
3. **Drop the short-term card.** No data → delete the "Lyhyen aikavälin
   maksukäyttäytyminen" panel entirely. The credit section now has one
   confident subject.
4. **Replace the generic "Arvio perustuu…" paragraph with a three-column
   value-prop strip** (⚡ Päivittyy automaattisesti · 🧭 Mukana selitys
   mitä pisteet tarkoittavat · 🔓 Ei tilausta, ei sitoumuksia). Use small
   custom gold line icons rather than emoji in the final build. One line
   below them: social proof ("Käytössä 400+ yrityksessä · Yli 12 000
   raporttia generoitu" — mockup numbers).
5. **Pricing as a horizontal strip, not a sidebar card.** Four tiers in a
   single row directly under the value props. The recommended tier gets a
   thin gold border and a "SUOSITUS" micro-badge; others are neutral. All
   four fit on desktop; collapse to 2×2 at tablet.
6. **CTA button: price *inside* the button, gold-foil gradient.**
   `Osta luottoriskiraportti — 2 €` on a
   `linear-gradient(135deg, #B98F42 0%, #8C6A32 100%)` background with a
   soft gold glow (`0 0 0 4px rgba(185,143,66,0.18)` on hover). Right-aligned
   at the end of the pricing strip, so tier → price → action reads left-to-
   right. Underneath, 11 px cream text: "Raportti toimitetaan välittömästi
   maksun jälkeen. Ei kuukausimaksua."
7. **Drop the "Uutta!" badge.** The whole section now signals novelty on its
   own; the badge is redundant. If you want a timestamp, put "Raportti
   päivitetty 04/2026" as a small cream-on-green caption under the section
   title.
8. **Section title treatment.** Promote "Luottoriski" to the same 38 px white
   heading style as "Taloustiedot" — but in cream/gold over the dark green.
   Two main acts on the page, both get the magazine-spread treatment.

This is the section that earns money. It should feel like money.

### D. "Lataa talousluvut" split button

- Rename: `Vie talousluvut` → **`Lataa talousluvut`**.
- Shape: split button. Main click downloads the default (Excel). Caret opens
  a small menu: **Excel (.xlsx)** / **CSV (.csv)** / **Leikepöydälle**.
- Placement: remove from the header's top-right; pin to the **top-right of
  the ratio table** panel, next to (or replacing) the `Tunnusluvut (kEUR)`
  section title. That's where "export this data" semantically belongs.
- Visual: ghost style (`var(--border-strong)` 1 px, `var(--surface)`), 8 px
  radius, 12 × 14 px padding; caret is a 12 px chevron. Menu: white card,
  1 px `var(--border)`, `--shadow-soft`, 6 px radius, hover row
  `var(--green-softer)`. Small file-type glyph per row (a monochrome green
  `xlsx`/`csv` pill is enough).

### E. Peers — "Katso kaikki" as tiles

Replace the two plain underlined text links with a two-tile footer inside the
peers panel:

```
┌──────────────────────────────────┐ ┌──────────────────────────────────┐
│  Kaikki toimialan yritykset  →   │ │  Selaa kaikkia toimialoja    →   │
│  287 yritystä · TOL 25.530       │ │  743 toimialaa Suomessa          │
└──────────────────────────────────┘ └──────────────────────────────────┘
```

- Style: `.peer-item` on steroids — full-width card, 18 px padding,
  `var(--surface-muted)` background, 1 px `var(--border)`, 8 px radius,
  right-aligned arrow, hover lifts 1 px and tints `var(--green-softer)`.
- Typography: 14 px / weight 750 title, 12 px / weight 550 muted sub-line
  with counts.
- Grid: 2 columns at desktop, 1 at mobile.
- This turns the "leftover navigation" into proper wayfinding.

### F. Intro banner — CTA pill

Convert the inline underlined link to a proper right-aligned pill button
inside the banner: green outline, `→` arrow, matches the ghost/secondary
scale. The banner promises a product; give it an actual door.

### G. Metric strip — inline deltas

Each `.metric-card` gets a small second line under the value:

```
Liikevaihto 2024
2 499 kEUR
▲ +0,5 % vs. 2023
```

Delta chip in green/red (`var(--green-2)` / `var(--red)`), 11 px, tabular
nums. This lets you drop the redundant "Kasvu 2023–2024" card and add a more
useful one (e.g., Nettovelka YoY, which *did* move by 310 %).

### H. Charts — two micro-moves

- **Line-chart last-point emphasis.** 2024 point enlarged to 6 px with gold
  fill (`--gold`) on the profitability and solvency line charts, mirroring
  the bar charts' 2024-bar treatment.
- **Chart tooltip shows YoY.** Append "(+Δ % vs. prev.)" to each value in
  tooltips. Costs nothing, useful every time.

### I. Ambient details (optional, high-leverage if time allows)

- **0.4 % noise overlay on the dark body**, via a CSS pseudo-element with an
  SVG fractal-noise data-URI. Adds analog warmth, no performance cost. This
  is the "feels expensive" detail.
- **Breadcrumb** above the hero: thin uppercase green
  `Etusivu · Toimialat · 25.530 Metallituotteiden valmistus · Raahen
  Terästuote Oy`. 12 px, .08 em letter-spacing.
- **Sticky section anchor nav** appears after you scroll past the hero:
  5 pills (Yleiskuva · Luottoriski · Talous · Tunnusluvut · Vertaisryhmä),
  horizontal, with the active one highlighted. On a 4 000 px page this
  matters a lot.

---

---

## Competitor benchmarks

### Finder.fi ([Raahen Terästuote Oy](https://www.finder.fi/Konepajateollisuus+ja+metallity%C3%B6t/Raahen+Ter%C3%A4stuote+Oy/Raahe/yhteystiedot/3313829))

- Shows **percentile rankings vs industry** for each KPI (exact values gated
  behind Finder Pro). This is the feature to copy — you can reuse your
  existing peer list as the cohort and compute percentiles client-side.
- **News feed** at the bottom ("Raahen Terästuote among 11 regional companies
  at Alihankinta 2025 trade show", source Kauppalehti). If you have any news
  API or RSS, this is a cheap trust-signal section.
- **"Löysitkö etsimäsi tiedot?"** feedback prompt (thumbs up/down) at the
  end. Two lines of code, meaningful signal.
- **Multiple rating stacks** (Menestyjä, Alma Risk, Intrum Collection).
  Valuatum having a single rating is arguably *cleaner* — don't copy this.
- **5-year financial table** is nearly identical in structure to yours.
  Valuatum's visual presentation is better (emphasised last year, cleaner
  typography).
- **"PRO" masking** uses `●●●●` placeholders — simpler and more honest than
  a 3 px blur. Consider adopting this pattern.
- **Breadcrumbs at the top** (Etusivu > Haku > Raahe > Toimiala > Yritys).
  You have an empty/neutral header; breadcrumbs would fill it and help SEO.

### Asiakastieto
- 7 years of historicals (you show 5 — fine).
- Paid reports priced at €15–€627 — your €2 impulse price is a strong
  competitive wedge, don't lose it.
- Tab navigation (Yleiskuva / Perustiedot / Talous / Luottoriski /
  Päättäjät). A single scrolling page like yours feels more modern, but for
  long sessions a sticky section-nav (anchor links) would help.

### Kauppalehti
- Heavy on rating-authority visuals (Menestyjä medallions etc.). Doesn't
  apply directly — your narrative approach is better.
- News + filings sections. Same "add news if you have a feed" as Finder.

**Valuatum's defensible edges vs all three:** smaller price point, cleaner
UI, and the AI-narrative + peer-benchmarking opportunities below.

---

## Prioritised recommendations (updated)

| #  | Effort | Impact | Recommendation                                                                 |
|----|--------|--------|---------------------------------------------------------------------------------|
| 1  | M      | High   | **Redesign the Luottoriski section as a sales-pitch spread** — dark-green ground, cream cards, gold accent, arc gauge, horizontal pricing strip, price-in-CTA. Not a Finder clone. |
| 2  | S      | High   | **Move the credit section up** (after hero, before charts) and **remove the short-term card**. |
| 3  | L      | High   | **AI narrative block** at the top of the credit section — 3 bullets: YoY changes, anomalies, verdict. Replace the generic "Arvio perustuu…" paragraph. |
| 4  | S      | High   | **Replace Yritystiedot panel with a header metadata strip**, incl. **TOL 25.530** 5-digit code, rekisterin tila, tilikausi, "Päivitetty 04/2026". |
| 5  | M      | High   | **Peer/industry overlay on charts** + percentile chips on the metric strip, using the existing peer list as the cohort. |
| 6  | S      | High   | **"Lataa talousluvut" split button** (Excel / CSV / clipboard), pinned above the ratio table. Remove the old header button. |
| 7  | S      | High   | **Replace the peers-section "Katso kaikki…" text links with two tiles** that show counts and a right-arrow. |
| 8  | S      | Med    | **`●●●` placeholders** in place of `blur(3px)` on locked values. |
| 9  | S      | Med    | **Intro-banner CTA** — upgrade the underlined "Kokeile nyt ilmaiseksi" link to a right-aligned pill button. |
| 10 | S      | Med    | **Metric-strip inline deltas** (▲ +0,5 % vs. 2023) — lets you drop the redundant "Kasvu" card and add a more telling one. |
| 11 | S      | Med    | **Risk-flags card** (🔴🟡🟢 over ratio deltas) as the AI narrative's sidekick. |
| 12 | S      | Med    | **Tabular-nums** on the ratio table, metric values, chart axes. |
| 13 | S      | Med    | **Display serif** for hero + section titles (Instrument Serif / Fraunces). Keep Inter for everything else. |
| 14 | S      | Med    | **Sparkline column** on the ratio table + YoY delta chips on the 2024 column + metric tooltips on hover. |
| 15 | S      | Med    | **Mini peer-comparison** — 2–3 KPIs per peer card, not just names. |
| 16 | S      | Med    | **Sticky section nav** + breadcrumb with TOL 25.530 in the chain. |
| 17 | S      | Med    | **Meta description, OG tags, JSON-LD Organization** — SEO wins. |
| 18 | S      | Low    | **"Löysitkö etsimäsi?"** feedback prompt at the bottom (copy from Finder). |
| 19 | S      | Low    | **News feed** if a source is available — Finder surfaces this well. |
| 20 | S      | Low    | **Chart tooltip**: include YoY change alongside absolute value. |
| 21 | S      | Low    | **Line-chart last-point emphasis** on 2024 (bigger, gold fill). |
| 22 | S      | Low    | **Accessibility**: visually-hidden data tables per chart, `scope` on the ratio table, `aria-hidden` on masked tokens, focus-visible on nav. |
| 23 | S      | Low    | **Noise overlay** on the dark body (0.4 %). |
| 24 | XS     | Low    | Replace the "Uutta!" badge — its novelty signal is being replaced by the redesigned section. |
| 25 | XS     | Low    | Remove the unused `EBITDA` constant in JS. |

(Effort: XS <30 min, S < 1 day, M 1–3 days, L 1 week+.)

---

## One-screen summary

If you only do three things:

1. **Redesign Luottoriski as a dark-green / cream / gold sales spread** and
   move it up the page. The section should look different from everything
   else — that difference is the product.
2. **Add peer/industry overlays on the charts + an AI narrative block at
   the top of the credit section.** These are the two moves that actually
   differentiate Valuatum from Finder and Asiakastieto.
3. **Rebuild the header metadata (incl. TOL 25.530) into a single-line
   strip, replace `●●●` for the blur, and swap `Vie` for a proper `Lataa`
   split button at the ratio table.** Three small moves, finished feel.
