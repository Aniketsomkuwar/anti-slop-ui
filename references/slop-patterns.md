# AI Slop Pattern Reference (46+ Patterns)

This reference documents all AI slop patterns detectable by the anti-ai-slop-real skill, integrated from anti-ui-slop (ritmex-skills) and anti-slop (miqdadbadjuber/anti-slop).

## Visual Details (V1-V15)

| ID | Pattern | Tell | Confidence | Correction |
|----|---------|------|------------|------------|
| **V1** | Border accent on rounded element | Colored border >=2px and radius >=12px on same generic card | Source | Choose one: neutral 1px border, lower radius, or no border |
| **V2** | Glassmorphism everywhere | Repeated translucent cards + backdrop-filter: blur on static content | Judgment | Use opaque surfaces; express hierarchy through contrast, spacing, elevation |
| **V3** | Side-tab accent border | One side of card has colored border >=3px | Source | Use status dot, icon, label, or restrained tint when meaning exists; remove empty decoration |
| **V4** | Hairline border with wide shadow | 1px border + shadow blur >=20px on one element | Source + opt-in | Keep crisp edge OR soft elevation (not both) |
| **V5** | Repeating-gradient stripes | repeating-linear-gradient or repeating-conic-gradient on surface | Source + opt-in | Use solid surface or existing brand texture |
| **V6** | Extreme border radius | Radius >=24px turns small card/section/input into blob | Judgment | Use role-based radius scale; common cards: 8-16px |
| **V7** | Amateurish hand-drawn SVG | Complex inline SVG scene/mascot with rough geometry | Judgment | Use real asset, simplify to purposeful diagram, or remove illustration |
| **V8** | Generic AI icons | Sparkle, star, magic, lightning, diamond, robot, AI orb | Source | Replace with product-relevant icons or remove |
| **V9** | Lucide icons | Every icon from same thin-stroke rounded library | Source | Use product-specific icons or vary styles |
| **V10** | Colored left stripe | Thin colored vertical bar on left edge of cards/rows/sections | Source | Remove or use as status indicator with meaning |
| **V11** | Small arrows (→/↗) | Placed on almost every button as pure decoration | Source | Remove or add functional meaning (sort, expand, etc.) |
| **V12** | AI capsule badges | Pill shape, thin border, glow, small dot, uppercase "AI Powered" etc. | Source | Remove or use as functional status badge with reason |
| **V13** | Generic AI typography | Large monospace headings, "HOW IT WORKS" uppercase with wide tracking | Source | Use brand typeface; reserve monospace for code/context |
| **V14** | Typeface chosen without reason | Font picked because it's AI default, not because it fits brand | Source | Choose font based on brand character; Inter valid if justified |
| **V15** | Generic illustrations | Undraw, Storyset, or 3D blob characters with no real product connection | Source | Use product-relevant illustrations or remove |

## Typography (T1-T10)

| ID | Pattern | Tell | Confidence | Correction |
|----|---------|------|------------|------------|
| **T1** | Flat type hierarchy | Adjacent roles differ <1.25x and lack contrast in weight/family/spacing/color | Source | Define fewer roles with clearer combined contrast; use ratio as screening heuristic |
| **T2** | Icon tile stacked above heading | Repeated feature cards use rounded-square icon tile directly above heading | Source | Align icon and heading; place icon in flow; remove container |
| **T3** | Italic serif display headline | Serif italic >=32px leads generic startup hero | Source | Use roman styling or display treatment from brand register |
| **T4** | Hero eyebrow/pill chip | Tiny tracked uppercase text/pill sits immediately above hero heading | Source | Fold information into heading, navigation context, or body copy |
| **T5** | Repeated section kickers | 3+ sections repeat same uppercase tracked mini-label | Source | Let heading hierarchy, artifacts, section-specific structure create navigation |
| **T6** | Oversized hero headline | Heading with 8+ words uses >=48px or text-5xl styling | Source | Shorten claim or reduce responsive size so supporting content visible |
| **T7** | Crushed letter spacing | Display tracking < -0.05em; body text carries negative tracking | Source | Restore character shapes; use modest optical tightening around 0 to -0.02em |
| **T8** | Overused font | Inter, Geist, Space Grotesk, or Instrument Serif appears as default identity | Source, weak | Report only with other convergence signals; strengthen roles with existing fonts first |
| **T9** | Single font for everything | One family uses nearly identical weight/width/spacing/proportions across every role | Source, weak | Build contrast inside family or add second family with defined display/body/data role |
| **T10** | All-caps body text | Paragraphs/long blocks >=20 words in uppercase | Quality | Use sentence case; reserve uppercase for short labels |

## Color and Contrast (C1-C5)

| ID | Pattern | Tell | Confidence | Correction |
|----|---------|------|------------|------------|
| **C1** | AI color palette | Purple/violet gradients or cyan-on-dark dominate without brand evidence | Source, weak | Report only as cluster signal; derive action/status/surface/accent from existing product context |
| **C2** | Dark mode with glowing accents | Dark surfaces repeat colored box shadows or neon text shadows | Source | Use neutral elevation and bounded state indicators; focus rings/exempt |
| **C3** | Gradient text | background-clip: text + transparent fill on headings/metrics/labels | Source | Use solid text color; express emphasis through hierarchy |
| **C4** | Gray text on colored background | Neutral gray on chromatic surface loses contrast | Source/Render | Use light/dark tint related to surface hue; verify contrast |
| **C5** | Cream/beige reflex | Warm off-white becomes whole page's generic tasteful surface without palette | Source, weak | Establish deliberate surface, ink, accent, and status colors |

## Layout and Space (L1-L8)

| ID | Pattern | Tell | Confidence | Correction |
|----|---------|------|------------|------------|
| **L1** | Hero metric layout | Hero centers large number, tiny label, supporting stats with generic accent | Judgment | Lead with product/artifact/verified evidence; preserve only meaningful metrics |
| **L2** | Identical card grids | 4+ siblings repeat icon, heading, paragraph with identical sizing | Judgment | Choose structure from content: ranked layout, table, list, accordion, or genuine uniform controls |
| **L3** | Monotonous spacing | Same gap/padding token serves item/group/component/section boundaries | Source | Map spacing tokens to semantic relationships; create clear grouping contrast |
| **L4** | Nested cards | 3+ nested levels repeat borders/fills/radii/shadows | Source | Remove redundant surfaces; group with spacing, headings, dividers, or one shared container |
| **L5** | Numbered section markers | Display 01/02/03 labels decorate independent sections | Source | Keep numbers for real sequences, timelines, ranks, or references |
| **L6** | Line length too long | Running text exceeds ~80 chars per line | Quality | Constrain prose to roughly 60ch-75ch; code/tables/deliberate data exempt |
| **L7** | Content overflowing container | Text/media spills, clips, creates accidental horizontal scroll | Quality | Wrap, constrain, truncate with accessible affordance; provide deliberate scrolling |
| **L8** | Positioned child clipped by overflow | Tooltip/menu/popover cut by ancestor using overflow:hidden/clip | Quality | Move layer outside clipping context; use portal; change overflow where safe |

## Motion (M1-M3)

| ID | Pattern | Tell | Confidence | Correction |
|----|---------|------|------------|------------|
| **M1** | Bounce/elastic easing | Dialogs/cards/routine controls use overshoot curves/repeated spring effects | Source | Use restrained ease-out curve and shorter travel |
| **M2** | Layout-property animation | Large/repeated transitions animate width/height/padding/margin/top/left causing reflow | Quality | Prefer transform and opacity; use bounded disclosure for necessary height changes |
| **M3** | Image hover transform | Generic cards repeatedly scale/rotate imagery on hover | Source + opt-in | Keep imagery still or use restrained overlay, caption, or border response |

## Copy (P1-P4)

| ID | Pattern | Tell | Confidence | Correction |
|----|---------|------|------------|------------|
| **P1** | Em-dash overuse | Body block contains 3+ em-dash characters or repeated HTML entities | Source | Rewrite with sentence boundaries, commas, colons, or parentheses |
| **P2** | Marketing buzzword | Generic claims: supercharge, streamline, empower, world-class, enterprise-grade, seamlessly, unlock | Source | Name exact action, object, user, and result |
| **P3** | Aphoristic cadence | Multiple sections repeat patterns: Not X. Y. or Less X. More Y. | Source | Replace with direct product facts and natural sentence rhythm |
| **P4** | Theater framing copy | Marketing dismisses category as theater without explaining practical failure | Source + opt-in | State the behavior, limitation, or consequence directly |

## Imagery (I1)

| ID | Pattern | Tell | Confidence | Correction |
|----|---------|------|------------|------------|
| **I1** | Broken/placeholder image | Rendered image markup has missing/empty src, #, known placeholder services, or placeholder API paths | Quality | Use real asset, generated asset with authorization, fallback, or remove element |

## General Quality (Q1-Q8)

| ID | Pattern | Tell | Confidence | Correction |
|----|---------|------|------------|------------|
| **Q1** | Cramped padding | Text/controls within ~8px of bordered/colored edge | Render | Provide enough internal space for component's role; 12-16px suits common controls/cards |
| **Q2** | Body text touching viewport edge | Running text reaches viewport edge, especially on mobile | Render | Add responsive content gutter, commonly at least 16px on narrow screens |
| **Q3** | Justified text | Screen body copy uses text-align: justify without effective hyphenation/language support | Source | Left-align body copy or enable tested hyphenation for editorial use case |
| **Q4** | Low contrast text | Text misses WCAG AA: 4.5:1 for normal, 3:1 for large text | Source/Render | Adjust foreground, background, weight, or size; verify computed result |
| **Q5** | Skipped heading level | Rendered outline jumps from h1 to h3 or similar | Source/Render | Restore sequential semantic levels; keep visual styling in classes |
| **Q6** | Tight line height | Multi-line body text uses line height below ~1.3 | Source | Use roughly 1.45-1.7 according to typeface and measure |
| **Q7** | Tiny body text | Running body text below 12px; 12-13px readability risk | Source | Use at least 14px for body copy; 16px is strong default |
| **Q8** | Wide letter spacing on body | Paragraphs use tracking above 0.05em | Source | Restore normal tracking; reserve wide tracking for short labels |

## Composition Checks Beyond Catalog

| ID | Check | Description |
|----|-------|-------------|
| **X1** | Motion saturation | Many elements enter, float, pulse, wiggle, or bounce; keep motion tied to single state change/spatial relationship |
| **X2** | Decorative priority inversion | Icon containers, badges, ornaments occupy more visual weight than message they introduce |
| **X3** | Redundant UX writing | Label, sublabel, helper, placeholder, hint repeat same fact |
| **X4** | Modal abuse | Scrolling multi-column multi-section workflow lives in modal |

## Convergence Cross-Reference

The following patterns frequently co-occur and should be fixed together to prevent cosmetic churn:

- **V6 + L4** (Extreme border radius + Nested cards): Radius >=24px often accompanies 3+ nested card levels. Fix L4 (remove redundant surfaces) first — this alone often resolves V6 by eliminating the nested card that needs extreme radius.

- **C1 + T8** (AI color palette + Overused font): Purple/violet gradients defaulting to Inter/Geist/Space Grotesk without brand justification. Fix T8 first by strengthening font roles with existing family — this often reduces C1 risk by making color choices more deliberate.

- **M1 + V2** (Bounce easing + Glassmorphism): Overshoot/spring effects on translucent cards feel especially jarring. Fix V2 (replace glassmorphism with opaque surfaces) first — the harder bounce becomes less noticeable on solid surfaces.

- **V3 + L2** (Side-tab accent border + Identical card grids): Colored border >=3px on card side commonly appears with 4+ identical feature cards. Fix L2 (replace uniform grid with ranked layout) first — the accent border becomes redundant.

- **P2 + P4** (Marketing buzzword + Theater framing): Generic claims ("supercharge", "empower") often coexist with theater framing ("we dismiss this category as theater"). Fix P2 first with exact action/object/user/result — the theater framing loses its audience when claims are concrete.

*After each system-level change, rescan. One primitive edit can clear many local symptoms.*

## Fix Order (apply sequentially)

1. Broken behavior, accessibility, overflow, readability
2. Information architecture and unsupported content
3. Repeated page templates, card anatomy, container depth
4. Type hierarchy, spacing rhythm, color roles
5. Decorative borders, gradients, glows, radii, icons, motion
6. Copy cadence and redundant labels

After each system-level change, rescan. One primitive edit can clear many local symptoms.

## Replacement Principles

- **Structure follows content**: comparable items suit tables/aligned lists; sequences suit steps; narrative content suits editorial flow; interactive choices suit controls with clear boundaries
- **Hierarchy uses a system**: establish explicit roles for display, heading, body, label, data; single font family supports hierarchy through size/weight/width/optical size/spacing; second family earns place through clear role
- **Color carries a job**: assign colors to brand, action, status, emphasis, surfaces; repeated decorative gradients/glows dilute those jobs
- **Spacing communicates relationship**: related items sit close; sections receive larger separation; repeated spacing tokens useful when semantic roles differ visibly
- **Motion communicates state, continuity, or causality**: default surfaces stay still; one meaningful transition carries more value than many ornamental effects
- **Decoration carries meaning**: domain artifacts, real product UI, data, photography, diagrams, brand motifs provide specificity; generic icons/blobs disappear when carrying no information
- **Asymmetry follows priority**: give more space to more important content; avoid arbitrary card-size variation created solely to appear designed