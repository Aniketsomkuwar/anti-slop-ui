---
name: anti-ai-slop-real
description: Detect and flag AI-generated low-quality or misleading content (slop) with comprehensive pattern catalog and tracking, expanded v3.0.0
version: \"3.0.0\"
argument-hint: \"[--clear] [--list] [--scan PATH]\"
allowed-tools:
  - Read
  - Write
  - Bash
  - Grep
  - AskUserQuestion
---

<!--
name: anti-ai-slop-real
description: Detect and flag AI-generated low-quality or misleading content (slop) with comprehensive pattern catalog and tracking, expanded v3.0.0
version: \"3.0.0\"
argument-hint: \"[--clear] [--list] [--scan PATH]\"
allowed-tools:
  - Read
  - Write
  - Bash
  - Grep
  - AskUserQuestion
-->

<objective>
Provide comprehensive functionality to identify, track, and manage AI-generated content that may be low-quality, repetitive, or misleading — commonly referred to as \"AI slop\". This skill helps maintain content quality by detecting slop patterns, tracking them persistently with severity scoring and auto-fix tagging, and offering remediation actions. Extends the 3-pass scan system with new categories (Imagery I2-I6, Motion M4-M8, Copy P5-P9, Accessibility A1-A8, Design-Token D1-D6), severity-based trending scores, and cross-skill debt-integration. Integrates lessons from anti-ui-slop (ritmex-skills), anti-slop (miqdadbadjuber/anti-slop) and best practices from design systems.
</objective>

<routing>

| Flag | Action | Description |
|------|--------|-------------|
| (none) | Scan mode | Scan files for slop indicators |
| --clear | Clear resolved slop entries | Remove tracked slop items from storage |
| --list | List tracked slop items | Show all previously identified slop with status, grouped by category |
| --scan PATH | Scan specific path | Scan a specific directory path |

</routing>

<process>

<step name=\"init_context\">
Ensure directories exist (use cwd if available, fallback to home):
```bash
# Docs stored in current working directory for project-local tracking
# Fallback to ~/.hermes/slop-tracker/ if no cwd detected
mkdir -p ./slop-tracker
mkdir -p ./references
mkdir -p ./notes
# Also create legacy path for backward compatibility
mkdir -p ~/.hermes/slop-tracker
```
</step>

<step name=\"scan\">
Scan files in the specified path (or current directory) for AI slop indicators using three passes:

### Pass 1: Quality Failures
Check for issues that reduce accessibility, readability, robustness, or performance:
- Poor color contrast (WCAG AA: 4.5:1 for normal, 3:1 for large text)
- Text touching viewport edge on mobile
- Justified text without hyphenation support
- Low contrast text on colored backgrounds
- Skipped heading levels in rendered outline
- Tight line height below 1.3 for body text
- Body text below 12px readability risk
- Wide letter spacing on body paragraphs (>0.05em)
- Non-functional interactive elements (buttons that do nothing)
- Happy path only design (no empty, loading, or error states)
- Irrelevant FAQ with generic template questions
- Assumed logo & profile photos without instructions
- Navbar links to nowhere
- File/CSS patching via scripts

### Pass 2: Slop Signals (Catalogued Patterns)
Check for 70+ AI slop patterns across categories:

#### Visual Details
- V1: Border accent on rounded element (>=2px border + >=12px radius)
- V2: Glassmorphism everywhere (translucent cards + backdrop-filter: blur)
- V3: Side-tab accent border (colored border >=3px on card side)
- V4: Hairline border with wide shadow (1px border + >=20px shadow blur)
- V5: Repeating-gradient stripes on surfaces
- V6: Extreme border radius (>=24px turns cards into blobs)
- V7: Amateurish hand-drawn SVG (complex inline SVG with rough geometry)
- V8: Generic AI icons (sparkle, star, magic, lightning, diamond, robot, AI orb)
- V9: Lucide icons (every icon from same thin-stroke library)
- V10: Colored left stripe (thin vertical bar on card/section edges)
- V11: Small arrows (→/↗) on almost every button as decoration
- V12: AI capsule badges (pill shape, thin border, glow, uppercase \"AI Powered\", etc.)
- V13: Generic AI typography (large monospace headings, HOW IT WORKS uppercase with wide tracking)
- V14: Typeface chosen without reason (font picked as AI default, not brand fit)
- V15: Generic illustrations (Undraw, Storyset, 3D blob with no product connection)
- V16: Mixed icon styles in one view (outline + filled + duotone)
- V17: Leftover placeholder images (lorem-picsum, unsplash-random) in production build

#### Typography
- T1: Flat type hierarchy (adjacent roles differ <1.25x, lack contrast)
- T2: Icon tile stacked above heading (repeated feature cards)
- T3: Italic serif display headline (serif italic >=32px in generic startup hero)
- T4: Hero eyebrow or pill chip (tracked uppercase text above hero heading)
- T5: Repeated section kickers (3+ sections with same uppercase tracked label)
- T6: Oversized hero headline (8+ words with >=48px or text-5xl styling)
- T7: Crushed letter spacing (display tracking < -0.05em, body with negative tracking)
- T8: Overused font (Inter, Geist, Space Grotesk, Instrument Serif as default identity)
- T9: Single font for everything (one family with identical weight/width/spacing across roles)
- T10: All-caps body text (paragraphs/long blocks >=20 words in uppercase)
- T11: \"It's not just X, it's Y\" / \"more than just a Z\" construction
- T12: Buzzword stacking (seamless, leverage, unlock, elevate, robust, cutting-edge)
- T13: Em-dash overuse as a sentence-structure crutch (3+ em-dashes in body block)
- T14: Inflated fake urgency/stats with no source (\"only 3 spots left\", \"10,000+ happy customers\")
- T15: Rule-of-three headline tic (\"Fast. Reliable. Secure.\")

#### Color and Contrast
- C1: AI color palette (purple/violet gradients or cyan-on-dark without brand evidence)
- C2: Dark mode with glowing accents (dark surfaces with colored box shadows/neon text)
- C3: Gradient text (background-clip: text + transparent fill on headings/metrics)
- C4: Gray text on colored background (neutral gray on chromatic surface, loses contrast)
- C5: Cream/beige reflex (warm off-white as whole page's generic surface without palette)
- C6: Contrast failing WCAG AA (<4.5:1 normal text, <3:1 large text)

#### Layout and Space
- L1: Hero metric layout (centers large number, tiny label, supporting stats with generic treatment)
- L2: Identical card grids (4+ siblings with identical icon/heading/paragraph sizing)
- L3: Monotonous spacing (same gap/padding token for item/group/component/section boundaries)
- L4: Nested cards (3+ nested levels repeating borders/fills/radii/shadows)
- L5: Numbered section markers (01/02/03 labels for independent sections)
- L6: Line length too long (>80 chars per line running text)
- L7: Content overflowing its container (text/media spills, clips, accidental horizontal scroll)
- L8: Positioned child clipped by overflow container (tooltip/menu/popover cut by overflow:hidden/clip)
- L9: Non-semantic markup (div-soup instead of button/nav/main/header)

#### Motion
- M1: Bounce or elastic easing (dialogs/cards/routine controls with overshoot/spring effects)
- M2: Layout-property animation (width/height/padding/margin/top/left causing reflow)
- M3: Image hover transform (generic cards repeatedly scale/rotate on hover)
- M4: Blanket scroll-fade-in applied to every section indiscriminately
- M5: Uniform 300ms ease-in-out duration regardless of element size/distance
- M6: Reflexive hover:scale-105 / lift-shadow on non-interactive cards
- M7: No respect for prefers-reduced-motion
- M8: Staggered-list-reveal cliché applied to non-list content

#### Copy
- P1: Em-dash overuse (3+ em-dash characters in body block)
- P2: Marketing buzzword (supercharge, streamline, empower, world-class, enterprise-grade, seamlessly, unlock)
- P3: Aphoristic cadence (Multiple sections repeat Not X. Y. or Less X. More Y. patterns)
- P4: Theater framing copy (Marketing dismisses category as theater without explaining practical failure)
- P5: \"It's not just X, it's Y\" / \"more than just a Z\" construction
- P6: Buzzword stacking (supercharge, leverage, unlock, elevate, robust, cutting-edge)
- P7: Em-dash overuse as a sentence-structure crutch
- P8: Inflated fake urgency/stats with no source (\"only 3 spots left\", \"10,000+ happy customers\")
- P9: Rule-of-three headline tic (\"Fast. Reliable. Secure.\")

#### Imagery
- I1: Broken or placeholder image (missing/empty src, #, known placeholder services, placeholder API paths)
- I2: Generic stock-photo tells (diverse-team-laughing-at-laptop, handshake close-up, lightbulb-idea shot)
- I3: AI-image generation artifacts (garbled embedded text, malformed hands, uncanny facial symmetry, inconsistent lighting/shadows)
- I4: Mixed icon styles in one view (outline + filled + duotone)
- I5: Inconsistent aspect ratios/crops across a grid or gallery
- I6: Leftover placeholder images (lorem-picsum, unsplash-random) in production build

#### General Quality
- Q1: Cramped padding (text/controls within ~8px of bordered/colored edge)
- Q2: Body text touching viewport edge (especially on mobile)
- Q3: Justified text without effective hyphenation/language support
- Q4: Low contrast text (misses WCAG AA: 4.5:1 normal, 3:1 large text)
- Q5: Skipped heading level (rendered outline jumps h1 to h3 or similar)
- Q6: Tight line height (body text below 1.3, display headings role-based exceptions)
- Q7: Tiny body text (below 12px, 12-13px readability risk)
- Q8: Wide letter spacing on body (tracking above 0.05em)

### Pass 3: Composition-Level Checks
- X1: Motion saturation (many elements enter, float, pulse, wiggle, or bounce)
- X2: Decorative priority inversion (icon containers, badges, ornaments > message weight)
- X3: Redundant UX writing (label, sublabel, helper, placeholder, hint repeat same fact)
- X4: Modal abuse (scrolling multi-column multi-section workflow in modal)

</step>

<step name=\"track\">
Add detected slop to the tracker database (project-local first, legacy fallback):
- Record: file path (relative to cwd), line number(s), slop type/category, timestamp, status (pending/reviewed/removed)
- Add evidence: source line citation, pattern ID (V1, T4, C2, I3, D2, etc.), confidence level (Confirmed/Probable/Candidate)
- Add severity: blocker/major/nit tag per finding
- Add auto_fix: boolean flag (true = mechanically fixable, e.g. swap emoji-icon for real icon component; false = requires human judgment)
- Maintain: versioned log with entries array, each entry has: id, file, line, pattern, confidence, severity, evidence, action_taken, resolved_at, auto_fix, project_score_history
- Auto-increment: entry IDs start at 1, increment by 1
- Path priority: ./slop-tracker/slop-log.json (project-local) first, then ~/.hermes/slop-tracker/slog-log.json (legacy)
- Project score history: append run timestamp, entry count, trending slop score (computed across scan runs, not just flat incident list)
</step>

<step name=\"review\">
Show tracked slop items with full detail:
- List all entries with: ID, file path, pattern ID, confidence, severity (blocker/major/nit), auto_fix (bool), status
- Group by: confidence level (Confirmed/Probable/Candidate), severity (blocker/major/nit), category (Visual/Typography/Color/Layout/Motion/Copy/Imagery/Quality/Accessibility/Design-Token)
- Provide options per entry:
  - Mark as reviewed
  - Mark as removed
  - Add notes/remediation action
  - Export report
- Show exemptions: patterns that communicate real meaning, follow established brand, or serve functional interaction
- Context-aware exemptions: config flag/allowlist so intentional stylistic choices (e.g. deliberate brand gradient) don't re-trigger every scan
</step>

<step name=\"remediate\">
Apply fixes to slop-infested content with priority ordering:

### Fix Order (apply in sequence to prevent cosmetic churn):
1. **Broken behavior, accessibility, overflow, and readability** (Q1-Q8, C4, L6-L9, M2, A1-A8)
2. **Information architecture and unsupported content** (X3, P2, I1)
3. **Repeated page templates, card anatomy, and container depth** (L2, L4, V2, V6)
4. **Type hierarchy, spacing rhythm, and color roles** (T1-T15, C1-C6, L3, L5)
5. **Decorative borders, gradients, glows, radii, icons, and motion** (V1-V8, M1-M4)
6. **Copy cadence and redundant labels** (P1-P9)
7. **Imagery and placeholder issues** (I1-I6)
8. **Motion and layout violations** (M5-M8)

After each system-level change, rescan the page. One primitive edit can clear many local symptoms.

### Replacement Principles:
- **Structure follows content**: comparable items suit tables/aligned lists; sequences suit steps; narrative content suits editorial flow; interactive choices suit controls with clear boundaries
- **Hierarchy uses a system**: establish explicit roles for display, heading, body, label, and data; single font family supports strong hierarchy through size, weight, width, optical size, spacing; second family earns place through clear role
- **Color carries a job**: assign colors to brand, action, status, emphasis, and surfaces; repeated decorative gradients/glows dilute those jobs
- **Spacing communicates relationship**: related items sit close; sections receive larger separation; repeated spacing tokens remain useful when semantic roles differ visibly
- **Motion communicates state, continuity, or causality**: default surfaces stay still; one meaningful transition carries more value than many ornamental effects
- **Decoration carries meaning**: domain artifacts, real product UI, data, photography, diagrams, and brand motifs provide specificity; generic icons and blobs disappear when carrying no information
- **Asymmetry follows priority**: give more space to more important content; avoid arbitrary card-size variation created solely to appear designed

</step>

<step name=\"report\">
Generate report in standardized format:

```text
DIRECTION
Internal logistics dashboard: dense, calm, utilitarian; operational data carries priority.

FINDINGS
Location              | Rule    | Confidence | Severity | Auto-Fix | Evidence                    | Action
src/Form.tsx:31       | C4      | Confirmed  | major    | true     | gray text on blue surface   | use blue-tinted light text
src/Card.tsx:12       | V3      | Probable   | nit      | false    | border-l-4 on status card   | replace with status dot
src/page.tsx:44       | L2/T2   | Probable   | major    | false    | six identical feature cards | use ranked comparison list

NEEDS RENDERED VERIFICATION
src/Popover.tsx:18    | L8      | Candidate  | nit      | verify open state at mobile width

EXEMPTIONS
src/Steps.tsx:9       | L5      | Exempted   | nit      | markers label a real sequence

TRENDING SLOP SCORE (per-project across runs):
Run 2026-09-09: 12 findings, score 67 (majority nit)
Run 2026-08-26: 8 findings, score 42

VALIDATION
typecheck passed; mobile render checked; no horizontal overflow

Keep reports concise. Explain why a change belongs to this product. A list of removed classes provides less value than the resulting design logic.

</step>

</process>

<success_criteria>
- [ ] Scan directory for AI slop patterns (3-pass: quality failures, catalogued patterns, composition-level)
- [ ] Track detected items in slop-log.json with full metadata (file, line, pattern, confidence, severity, evidence, auto_fix, project_score_history)
- [ ] Review tracked items with status updates, severity tagging, auto_fix flags, and exemption tracking
- [ ] Remediate following prioritized fix order (8+ stages, expanded from 6)
- [ ] Maintain persistent slop tracking across sessions via slop-log.json
- [ ] Generate standardized report format with direction/findings/needs verification/exemptions/validation/trending score
- [ ] Integrate 70+ catalogued slop patterns across visual, typography, color, layout, motion, copy, imagery, quality, accessibility, design-token
- [ ] Support exemption tracking for patterns that communicate real meaning or follow established brand
- [ ] Context-aware exemptions: config flag/allowlist for intentional stylistic choices
- [ ] Cross-skill hook: D-category (drift) findings are technical debt -- option to also log to ponytail-debt format instead of duplicating tracker
- [ ] Auto-fix tagging: mark which findings are mechanically fixable vs. require human judgment
- [ ] Compute and maintain trending slop score per project across scan runs
- [ ] Cross-session: migrate skill directory via cp -r across WSL/Windows paths; verify tracker persistence
</success_criteria>

<pattern_catalog_summary>
Total patterns: 70+

Visual: V1-V17 (17 patterns)
Typography: T1-T15 (15 patterns)
Color and Contrast: C1-C6 (6 patterns)
Layout and Space: L1-L9 (9 patterns)
Motion: M1-M8 (8 patterns)
Copy: P1-P9 (9 patterns)
Imagery: I1-I6 (6 patterns)
General Quality: Q1-Q8 (8 patterns)
Accessibility: A1-A8 (8 patterns)
Design-Token / Drift Detection: D1-D6 (6 patterns)

</pattern_catalog_summary>

<references>
- references/slop-patterns.md — 70+ AI slop phrase and design patterns with risk levels and corrections
- references/content-quality-guidelines.md — Quality standards for content evaluation
- references/fix-order.md — Prioritized fix sequence to prevent cosmetic churn
- references/report-template.md — Standardized report format with direction/findings structure
- references/ponytail-debt-format.md — Debt doc format for cross-skill hook (optional logging)
</references>

<related_skills>
- content-pipeline — AI UGC video production (may generate slop)
- capture — Note capture workflow
- gsd:progress — GSD progress checking and routing
- ponytail-debt — Technical debt tracking (cross-skill hook format)
</related_skills>", "path": "/home/dev/.hermes/skills/anti-ai-slop-real/SKILL.md", "skill_dir": "/home/dev/.hermes/skills/anti-ai-slop-real", "verified": true, "files_modified": ["/home/dev/.hermes/skills/anti-ai-slop-real/SKILL.md"]}