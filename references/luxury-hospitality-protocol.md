# Luxury Hospitality Protocol — Anti-Slop Patterns (H1-H12)

Detection and remediation reference for ultra-luxury hospitality, Michelin-grade
restaurants, and architectural destination venues.

**Scope gate:** H-patterns apply only when the target context is luxury hospitality,
fine dining, or a destination venue. A B2B dashboard, dev tool, or e-commerce
aggregator does not trigger them. Do not report H-findings outside that scope.

## Why the generic catalog misses this

V/T/C/L/Q patterns catch generic AI slop — the failure mode they were written for is
"SaaS template applied to everything". Luxury hospitality has a different failure mode:
**aggregator grammar applied to a domain whose entire value is sensory specificity.**
Card grids, live-status pills, and pastel maps do not read as *generic* — they read as
*booking site*. That is a distinct, detectable defect the base catalog does not name.

The base catalog scores these as at worst mild instances of L2 or V12. In this domain
they are blocker-severity, because they make a destination venue indistinguishable
from a listing aggregator.

---

## Forbidden Patterns (H1-H7)

| ID | Pattern | Tell | Confidence | Correction |
|----|---------|------|------------|------------|
| **H1** | Card-grid aggregation | Rows of identical rounded cards: cropped image header + plain text body | Source | Full-bleed canvas, asymmetric split viewport, or editorial index/ledger. Structure follows the venue's actual logic, not a uniform tile |
| **H2** | Generic status pills | Pill with pulsing green/red dot: "Open Today", "Live", "Active Now" | Source | State as a typographic ledger line or a meaning-bearing jewel dot. Never animate the indicator |
| **H3** | Fake chrome around media | Mock window headers, tab strips with close buttons, "LIVE MAP" bars wrapped around video/maps | Source | Render media as a full-bleed architectural plane. No simulated OS or browser UI |
| **H4** | Raw embedded maps | Unstyled Google Maps — pastel roads, yellow highways — inside a dark palette | Source | Monochromatic CSS filter + dark overlay, or purpose-built vector/static cartography |
| **H5** | Circular icon lists | Icon-in-a-circle stacked next to label rows for address/contact/hours | Source | Tabular concierge ledger, architectural key-value rows, or editorial prose |
| **H6** | Fintech sans pairing | Geometric startup sans (Outfit, Poppins, Inter) set against a luxury serif | Source | Humanist, Roman, or sharp editorial: Plus Jakarta Sans, Tenor Sans, Syne, Manrope |
| **H7** | Hover-gated core content | Dish photography, ingredients, or pricing hidden behind a hover reveal | Source | Static, confident presence. Hover may *add* information; it must never *gate* it |

---

## Mandatory Design Codes (H8-H12)

These are violations of *absence*. The defect is that the required treatment is missing.

| ID | Code | Violation tell | Correction |
|----|------|----------------|------------|
| **H8** | Canvas over card | Generic boxed containers where full-bleed would serve; no hairline architectural borders | Full-bleed backgrounds, `1px solid rgba(gold, 0.2)` hairline borders, asymmetric split viewports — not boxed cards |
| **H9** | Editorial typographic scale | Numbers, coordinates, and labels set as incidental UI text rather than design elements | Treat them as design: Roman or serif numerals ("01", "02"), wide tracking `0.2em`, small caps |
| **H10** | Discreet dietary indicators | Heavy "VEG" / "NON-VEG" badges | 4-6px glowing jewel dot framed in a glass disc. Meaning stays; the shout goes |
| **H11** | Cinematic media integration | Background video with hard edges, no scrim, or a scrim that fights the palette | Calibrated linear **and** vignette gradient scrims bleeding seamlessly into the dark palette — no hard edges |
| **H12** | Tabular concierge hierarchy | Arrival, contact, and venue data as scattered prose or icon rows | Five-star concierge dossier: category key on the left, refined Cormorant Garamond serif values on the right |

---

## Relationship to the Existing Catalog

H-patterns deliberately **refine or supersede** base patterns in this domain. Report the
H-ID, not both — double-firing inflates the score and sends the fixer at the wrong layer.

| H-ID | Overlaps | Resolution |
|------|----------|------------|
| H1 | L2 (identical card grids), V6 (extreme radius), I5 (inconsistent crops) | H1 supersedes L2 when the cards carry image headers. Fix H1; L2/V6/I5 usually resolve with it |
| H2 | V12 (capsule badges), M4/M6 (reflexive motion) | H2 supersedes V12 when the badge reports venue status. The pulse is the H2 tell, not a separate M finding |
| H3 | — | New. No base pattern names simulated chrome |
| H4 | C1 (color palette clash), C4 (contrast on chromatic surface) | H4 is the specific case; C1/C4 fire only on the residual contrast failure after the map is filtered |
| H5 | A4/L9 (non-semantic markup) | H5 supersedes when the icon list encodes contact/venue data |
| H6 | T8 (overused font), T14/V14 (unjustified typeface) | H6 supersedes T8 for this domain — it names the *pairing* failure, which T8 does not |
| H7 | — | New. No base pattern covers hover-gated content |
| H8 | L4 (nested cards), V6 | H8 is the positive-side framing; report H8 when the fix is "unbox", L4 when it is "un-nest" |
| H9 | T5 (repeated kickers), L5 (numbered markers) | H9 is the inverse: L5/T5 flag decorative overuse, H9 flags editorial treatment that is absent |
| H10 | V12 (capsule badges) | H10 supersedes V12 when the badge is dietary |
| H11 | C2 (glowing accents), C3 (gradient text) | H11 is about media scrims; C2/C3 about UI accents. Distinct — do not merge |
| H12 | X3 (redundant UX writing) | H12 is structural; X3 is duplication. Both may fire on the same block |

---

## Fix-Order Placement

H-findings route into the existing 8-stage sequence:

| Stage | H-patterns | Why here |
|-------|-----------|----------|
| 2 — Information architecture | H4, H7, H11 | Media integration and content gating are IA-level, not cosmetic |
| 3 — Templates and container depth | H1, H3, H5, H8, H12 | Card anatomy and container structure |
| 4 — Type hierarchy and color roles | H6, H9 | Typographic system |
| 5 — Decoration | H2, H10 | Indicator treatment |

Never fix H2 (pill pulse) or H10 (badge weight) before H1. Removing the pulse from a
card grid that should not exist is wasted work — Stage 3 deletes the card, and the pill
goes with it.

---

## Detection Heuristics

Source-level, no render required:

- **H1**: 3+ sibling elements sharing a rounded-container class, each containing an `<img>`
  and a short text block, with uniform padding/radius across the set
- **H2**: `animate-pulse`, `@keyframes` on a `rounded-full` dot, or status strings
  matching `(Open|Live|Active|Open Now)` inside a bordered pill
- **H3**: media element wrapped in a parent carrying `rounded-lg`/`shadow-xl` plus a
  child strip with three dots, or text matching `(LIVE|PREVIEW|localhost:)` near media
- **H4**: `google.com/maps/embed`, `maps.googleapis.com`, or an `<iframe>` with
  `maps` in src, with no `filter:` applied on an ancestor
- **H5**: repeated `rounded-full` icon wrapper as a direct sibling of an address, phone,
  email, or hours string
- **H6**: `Outfit`, `Poppins`, `Inter`, `DM Sans`, `Montserrat`, `Raleway` declared alongside
  `Cormorant`, `Playfair`, `EB Garamond`, `Tenor Sans`, or any display serif
- **H7**: `group-hover:opacity-100`, `hover:reveal`, or `:hover` rules controlling
  `opacity`/`visibility` on elements containing `<img>`, price strings, or ingredient lists

H8-H12 are detected as absences — search for the required treatment and report when absent:

- **H8**: count `rgba(*, 0.2)` / hairline borders and full-bleed sections; zero of either is a finding
- **H9**: no `font-variant: small-caps`, no tracking >= `0.15em` on labels, numerals set in the body font
- **H10**: dietary data rendered as a bordered badge, or absent where the venue serves dietary-specific menus
- **H11**: `<video>` or background media with no sibling/overlay element carrying a gradient
- **H12**: contact/arrival data not structured as a key-value ledger (check for a `<dl>`, or a
  two-column grid with a label column)

---

## Exemptions

Exempt — and record the reason — when:

- **H1** — the grid *is* the product (a genuine listing/taxonomy view the venue operates)
- **H2** — the status is real-time inventory the user is about to act on (table availability,
  booking window closing). Live data earns a live indicator
- **H4** — an interactive map is the primary interaction *and* has been restyled to the palette
  (the exemption is for the styling requirement, not the map itself)
- **H7** — the user explicitly instructed hover-gated content for a specific component
- **H9** — a house style guide mandates a different numeral treatment; cite the guide
- **H10** — regulatory or allergy-safety requirements mandate explicit dietary labelling.
  Safety labelling is never slop

---

## Report Rows

```text
FINDINGS
src/sections/Menu.tsx:88    | H1      | Confirmed  | major   | 6 identical rounded dish cards | replace with editorial index; keep 3 signature dishes as full-bleed
src/components/Status.tsx:14| H2      | Confirmed  | major   | animate-pulse dot on "Open Today" | static ledger line: "Open · 18:00-23:00"
src/Venue.tsx:51            | H4      | Confirmed  | blocker | raw maps iframe, no filter  | monochrome filter + dark overlay, or static cartography
src/Contact.tsx:22          | H5      | Probable   | major   | 4 icon-in-circle contact rows | concierge ledger: key left, serif value right
src/hero/Video.tsx:9        | H11     | Confirmed  | major   | background video, hard edges | linear + vignette scrim into palette
```
