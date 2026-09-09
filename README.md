# anti-ai-slop-real v2.0.0

Detect and flag AI-generated low-quality or misleading content (slop) with comprehensive pattern catalog and tracking.

## Installation

```bash
# The skill is stored at:
# /home/dev/.hermes/skills/anti-ai-slop-real/

# Ensure directories exist:
mkdir -p ~/.hermes/skills/anti-ai-slop-real/references
mkdir -p ~/.hermes/slop-tracker/
mkdir -p ~/.hermes/notes/

# Reference files are included:
# - references/slop-patterns.md (46+ patterns)
# - references/content-quality-guidelines.md (quality standards)
```

## Usage

### Loading the skill

```bash
/skill anti-ai-slop-real
```

### Available Commands

| Flag | Action | Description |
|------|--------|-------------|
| (none) | Scan mode | Scan files for slop indicators |
| `--clear` | Clear resolved slop entries | Remove tracked slop items from storage |
| `--list` | List tracked slop items | Show all previously identified slop with status |
| `--scan PATH` | Scan specific path | Scan a specific directory path |

### Scanning

```bash
# Scan current directory
/skill anti-ai-slop-real --scan

# Scan specific path
/skill anti-ai-slop-real --scan /path/to/project

# List tracked slop items
/skill anti-ai-slop-real --list

# Clear resolved entries
/skill anti-ai-slop-real --clear
```

### How It Works

The skill runs a **3-pass scan system**:

#### Pass 1: Quality Failures
Checks for issues reducing accessibility, readability, robustness, or performance:
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

#### Pass 2: Slop Signals (Catalogued Patterns)
Checks for 46+ AI slop patterns across categories:

**Visual Details (V1-V15):** Border accents, glassmorphism, side-tab borders, hairline borders, repeating gradients, extreme radius, hand-drawn SVGs, generic AI icons, Lucide icons, colored left stripes, small arrows, AI capsule badges, generic AI typography, unjustified typefaces, generic illustrations

**Typography (T1-T10):** Flat type hierarchy, icon-above-heading, italic serif display, hero eyebrow, repeated kickers, oversized headlines, crushed letter spacing, overused fonts, single font for everything, all-caps body text

**Color and Contrast (C1-C5):** AI color palettes, dark mode with glowing accents, gradient text, gray on colored backgrounds, cream/beige reflex

**Layout and Space (L1-L8):** Hero metric layouts, identical card grids, monotonous spacing, nested cards, numbered section markers, long line length, content overflow, positioned children clipped by overflow

**Motion (M1-M3):** Bounce/elastic easing, layout-property animation, image hover transforms

**Copy (P1-P4):** Em-dash overuse, marketing buzzwords, aphoristic cadence, theater framing copy

**Imagery (I1):** Broken or placeholder images

**General Quality (Q1-Q8):** Cramped padding, body text touching viewport, justified text, low contrast, skipped heading levels, tight line height, tiny body text, wide letter spacing

#### Pass 3: Composition-Level Checks
- Motion saturation (many elements animating)
- Decorative priority inversion (icons > message weight)
- Redundant UX writing (repeating facts)
- Modal abuse (multi-section workflow in modal)

### Tracking

Detected slop items are logged to `~/.hermes/slop-tracker/slop-log.json` with metadata:
- File path and line number(s)
- Slop type/category (pattern ID)
- Confidence level (Confirmed/Probable/Candidate)
- Severity (Critical/High/Medium/Low)
- Evidence: source line citation
- Remediation action taken
- Status: pending/reviewed/removed
- Exemption: if pattern communicates real meaning or follows established brand

### Report Generation

Generate standardized reports in this format:

```
DIRECTION
Internal logistics dashboard: dense, calm, utilitarian; operational data carries priority.

FINDINGS
Location              | Rule    | Confidence | Evidence                    | Action
src/Form.tsx:31       | C4      | Confirmed  | gray text on blue surface   | use blue-tinted light text
src/Card.tsx:12       | V3      | Probable   | border-l-4 on status card   | replace with status dot
src/page.tsx:44       | L2/T2   | Probable   | six identical feature cards | use ranked comparison list

NEEDS RENDERED VERIFICATION
src/Popover.tsx:18    | L8      | Candidate  | clipped ancestor found      | verify open state at mobile width

EXEMPTIONS
src/Steps.tsx:9       | L5      | Exempted   | markers label a real sequence

VALIDATION
typecheck passed; mobile render checked; no horizontal overflow
```

### Fix Order (apply sequentially to prevent cosmetic churn)

1. **Broken behavior, accessibility, overflow, readability** (Q1-Q8, C4, L6-L8, M2)
2. **Information architecture and unsupported content** (X3, P2, I1)
3. **Repeated page templates, card anatomy, container depth** (L2, L4, V2, V6)
4. **Type hierarchy, spacing rhythm, color roles** (T1-T10, C1-C5, L3, L5)
5. **Decorative borders, gradients, glows, radii, icons, motion** (V1-V7, M1, M3)
6. **Copy cadence and redundant labels** (P1-P4)

After each system-level change, rescan the page. One primitive edit can clear many local symptoms.

### Replacement Principles

- **Structure follows content**: comparable items suit tables/aligned lists; sequences suit steps; narrative content suits editorial flow; interactive choices suit controls with clear boundaries
- **Hierarchy uses a system**: establish explicit roles for display, heading, body, label, data; single font family supports hierarchy through size, weight, width, optical size, spacing; second family earns place through clear role
- **Color carries a job**: assign colors to brand, action, status, emphasis, and surfaces; repeated decorative gradients/glows dilute those jobs
- **Spacing communicates relationship**: related items sit close; sections receive larger separation; repeated spacing tokens useful when semantic roles differ visibly
- **Motion communicates state, continuity, or causality**: default surfaces stay still; one meaningful transition carries more value than many ornamental effects
- **Decoration carries meaning**: domain artifacts, real product UI, data, photography, diagrams, and brand motifs provide specificity; generic icons and blobs disappear when carrying no information
- **Asymmetry follows priority**: give more space to more important content; avoid arbitrary card-size variation created solely to appear designed

### Reference Files

- `references/slop-patterns.md` — 46+ AI slop phrase and design patterns with risk levels and corrections
- `references/content-quality-guidelines.md` — Quality standards for content evaluation
- `references/regex-debugging.md` — Common regex debugging patterns and fixes for scan script

### Related Skills

- `content-pipeline` — AI UGC video production (may generate slop)
- `capture` — Note capture workflow
- `gsd:progress` — GSD progress checking and routing

### For AI Agents (Claude, CodeX, OpenAI, Hermes, etc.)

This skill is designed for direct integration by other AI agents:

**Invocation**: Use `/skill anti-ai-slop-real` to load, then run `--scan`, `--list`, or `--clear`

**Pattern Catalog**: The 46+ patterns in `references/slop-patterns.md` provide a comprehensive catalog that any AI system can reference when evaluating content quality.

**Evidence Hierarchy**: Results follow Source/Render/Judgment/Confidence model with Confirmed/Probable/Candidate/Exempted confidence levels and Critical/High/Medium/Low severity.

**Persistent Tracking**: All detected slop is stored in `~/.hermes/slop-tracker/slop-log.json` with auto-incrementing IDs, enabling cross-session tracking and remediation history.

**Standardized Reporting**: The report format (direction/findings/needs verification/exemptions/validation) is consistent and machine-parsable.

**Interoperability**: Designed to work alongside other AI skills in a Hermes ecosystem, with compatible JSON output format and tracking structure.

### Why This Skill Stands Out

1. **Complete pattern catalog**: 46+ documented patterns across 9 categories, integrated from multiple anti-slop sources
2. **3-pass scan system**: Quality failures → catalogued patterns → composition-level checks, preventing missed issues
3. **Evidence-aware**: Every detection includes source line citation, confidence level, and severity
4. **Persistent tracking**: Cross-session slop history in `slop-log.json` with exemption tracking
5. **Prioritized fix order**: 6-stage fix sequence prevents cosmetic churn when making changes
6. **Replacement principles**: Guidelines for meaningful replacements, not just removals
7. **Standardized reports**: Consistent direction/findings/needs verification/exemptions/validation format
8. **Agent-ready**: Designed for direct invocation by other AI systems with predictable JSON output