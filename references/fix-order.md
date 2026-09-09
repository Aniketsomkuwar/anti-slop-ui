# Fix Order — Prioritized Fix Sequence to Prevent Cosmetic Churn

Apply fixes in this exact sequence. Each stage, if applied out of order, can trigger
re-work in later stages. After each system-level change, rescan the page.

## Stage 1 — Broken behavior, accessibility, overflow, readability

Fix all issues that affect functionality, screen reader access, or basic readability:

- **Q1-Q8** — General quality: cramped padding, viewport-edge text, justified text without hyphenation, low contrast text, skipped heading levels, tight line height, tiny body text (<12px), wide letter spacing on body
- **C4** — Gray text on colored background: verify contrast, adjust foreground/background/weight/size
- **L6** — Line length too long: constrain prose to ~60–75ch; code/tables/deliberate data exempt
- **L7** — Content overflowing container: wrap, constrain, truncate with accessible affordance; provide deliberate scrolling
- **L8** — Positioned child clipped by overflow: move layer outside clipping context; use portal; change overflow where safe
- **M2** — Layout-property animation: prefer transform and opacity; use bounded disclosure for necessary height changes

## Stage 2 — Information architecture and unsupported content

Fix structural and content-level issues:

- **I1** — Broken or placeholder image: use real asset, generated asset with authorization, fallback, or remove element
- **X3** — Redundant UX writing: remove duplicate labels/sublabels/helpers/placeholders/hints that repeat the same fact
- **P2** — Marketing buzzword: replace generic claims (supercharge, streamline, empower, world-class, enterprise-grade, seamlessly, unlock) with exact action, object, user, and result
- **P4** — Theater framing copy: state the behavior, limitation, or consequence directly instead of dismissing a category as "theater"

## Stage 3 — Repeated page templates, card anatomy, and container depth

Fix repeated structural patterns across the page:

- **L2** — Identical card grids: choose structure from content (ranked layout, table, list, accordion, or genuine uniform controls). Avoid 4+ siblings with identical icon/heading/paragraph sizing
- **L4** — Nested cards: remove redundant surfaces; group with spacing, headings, dividers, or one shared container. Avoid 3+ nested levels repeating borders/fills/radii/shadows
- **V2** — Glassmorphism everywhere: use opaque surfaces; express hierarchy through contrast, spacing, elevation instead of repeated translucent cards + backdrop-filter: blur
- **V6** — Extreme border radius: use role-based radius scale; common cards: 8–16px. Avoid >=24px that turns small cards/sections/inputs into blobs

## Stage 4 — Type hierarchy, spacing rhythm, and color roles

Fix typographic and color system issues:

- **T1** — Flat type hierarchy: define fewer roles with clearer combined contrast; use ratio (1.25x) as screening heuristic between adjacent roles
- **T2** — Icon tile stacked above heading: align icon and heading; place icon in flow; remove unnecessary container
- **T7** — Crushed letter spacing: restore character shapes; use modest optical tightening around 0 to −0.02em. Avoid display tracking < −0.05em or body with negative tracking
- **C1** — AI color palette: report only as cluster signal; derive action/status/surface/accent from existing product context. Avoid purple/violet gradients or cyan-on-dark without brand evidence
- **C5** — Cream/beige reflex: establish deliberate surface, ink, accent, and status colors. Avoid warm off-white as whole page's generic surface without palette

## Stage 5 — Decorative borders, gradients, glows, radii, icons, and motion

Fix decorative and ornamental issues:

- **V1** — Border accent on rounded element: choose one: neutral 1px border, lower radius, or no border. Avoid >=2px border + >=12px radius on same generic card
- **V3** — Side-tab accent border: use status dot, icon, label, or restrained tint when meaning exists; remove empty decoration. Avoid colored border >=3px on card side
- **V4** — Hairline border with wide shadow: keep crisp edge OR soft elevation (not both). Avoid 1px border + shadow blur >=20px on one element
- **V5** — Repeating-gradient stripes on surfaces: use solid surface or existing brand texture. Avoid repeating-linear-gradient or repeating-conic-gradient on surfaces
- **M1** — Bounce or elastic easing: use restrained ease-out curve and shorter travel. Avoid overshoot curves/repeated spring effects on dialogs/cards/routine controls
- **M3** — Image hover transform: keep imagery still or use restrained overlay, caption, or border response. Avoid generic cards repeatedly scale/rotate on hover

## Stage 6 — Copy cadence and redundant labels

Final copy-level fixes:

- **P1** — Em-dash overuse: rewrite body block with 3+ em-dash characters or repeated HTML entities using sentence boundaries, commas, colons, or parentheses
- **P3** — Aphoristic cadence: replace repeated patterns (Not X. Y. or Less X. More Y.) with direct product facts and natural sentence rhythm

---

**After each stage:** Rescan the page. One primitive edit can clear many local symptoms.

**Never apply Stage N+1 before completing Stage N.** The stages are ordered to prevent cosmetic churn — fixing a decorative border (Stage 5) before fixing overflow (Stage 1) will just produce a new overflow problem.