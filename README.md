# anti-ai-slop-real v2.0.0

Detect and flag AI-generated low-quality or misleading content (slop) with comprehensive pattern catalog and tracking.

## Quick Start

```bash
# Load the skill
/skill anti-ai-slop-real

# Scan current directory for slop
/skill anti-ai-slop-real --scan

# Scan specific path
/skill anti-ai-slop-real --scan /path/to/project

# List tracked slop items
/skill anti-ai-slop-real --list

# Clear resolved entries
/skill anti-ai-slop-real --clear
```

## 3-Pass Scan System

**Pass 1: Quality Failures** — accessibility, readability, robustness, performance issues
- WCAG AA contrast, viewport-edge text, justified text without hyphenation, skipped heading levels, tight line height, tiny body text (<12px), wide letter spacing (>0.05em), non-functional interactive elements, happy-path-only design

**Pass 2: Catalogued Patterns** — 46+ patterns across 9 categories
- Visual: V1-V15 (borders, glassmorphism, icons, radius, gradients, illustrations)
- Typography: T1-T10 (hierarchy, fonts, tracking, all-caps)
- Color: C1-C5 (palettes, dark mode, gradient text, contrast issues)
- Layout: L1-L8 (identical grids, spacing, overflow, clipped children)
- Motion: M1-M3 (bounce easing, layout animations, hover transforms)
- Copy: P1-P4 (em-dash overuse, buzzwords, cadence, theater framing)
- Imagery: I1 (broken/placeholder images)
- Quality: Q1-Q8 (padding, contrast, line height, tiny text, letter spacing)

**Pass 3: Composition-Level Checks** — higher-level structural issues
- Motion saturation, decorative priority inversion, redundant UX writing, modal abuse

## Tracking

Detected slop logged to `~/.hermes/slop-tracker/slop-log.json` with:
- File path, line number, pattern ID, confidence (Confirmed/Probable/Candidate/Exempted)
- Severity (Critical/High/Medium/Low), evidence citation, status (pending/reviewed/removed)
- Exemption tracking for patterns communicating real meaning or following established brand

## Fix Order (6 stages — apply sequentially)

1. Broken behavior, accessibility, overflow, readability
2. Information architecture and unsupported content
3. Repeated page templates, card anatomy, container depth
4. Type hierarchy, spacing rhythm, color roles
5. Decorative borders, gradients, glows, radii, icons, motion
6. Copy cadence and redundant labels

*After each stage: rescan. One primitive edit can clear many local symptoms.*

## Report Format

```text
DIRECTION
Internal logistics dashboard: dense, calm, utilitarian; operational data carries priority.

FINDINGS
Location              | Rule    | Confidence | Evidence                    | Action
src/Form.tsx:31       | C4      | Confirmed  | gray text on blue surface   | use blue-tinted light text

NEEDS RENDERED VERIFICATION
src/Popover.tsx:18    | L8      | Candidate  | clipped ancestor found      | verify open state at mobile width

EXEMPTIONS
src/Steps.tsx:9       | L5      | Exempted   | markers label a real sequence

VALIDATION
typecheck passed; mobile render checked; no horizontal overflow
```

## Reference Files (in `references/` directory)

- `slop-patterns.md` — 46+ AI slop phrase and design patterns with risk levels and corrections
- `content-quality-guidelines.md` — Quality standards for content evaluation
- `fix-order.md` — Prioritized fix sequence to prevent cosmetic churn
- `report-template.md` — Standardized report format with direction/findings structure
- `hallmark-gates.md` — Hallmark design gates integration (57 slop-test gates, 20 themes)

## AI Agent Integration

Invoke directly: `/skill anti-ai-slop-real --scan PATH`

Output is JSON-parsable with pattern IDs, confidence levels, severity, and evidence. Interoperable with other Hermes skills. Evidence hierarchy: Source/Render/Judgment/Confidence with Confirmed/Probable/Candidate/Exempted levels and Critical/High/Medium/Low severity.

## Why This Skill Stands Out

1. 46+ documented patterns across 9 categories (integrated from multiple anti-slop sources)
2. 3-pass scan system: Quality failures → catalogued patterns → composition-level checks
3. Every detection includes source line citation, confidence level, and severity
4. Cross-session slop history in `slop-log.json` with exemption tracking
5. 6-stage fix sequence prevents cosmetic churn when making changes
6. Replacement principles for meaningful substitutions, not just removals
7. Standardized direction/findings/needs verification/exemptions/validation report format
8. Designed for direct invocation by other AI systems with predictable output

## Installation

Ensure directories exist:

```bash
mkdir -p ~/.hermes/skills/anti-ai-slop-real/references
mkdir -p ~/.hermes/slop-tracker/
mkdir -p ~/.hermes/notes/
```

Skill directory: `/home/dev/.hermes/skills/anti-ai-slop-real/` (local) or install globally via `hermes skills install`.

## Credits

Created by Aniket Somkuwar. Integrates 46+ slop patterns from miqdadbadjuber/anti-slop and discountry/ritmex-skills anti-ui-slop. Pattern catalog covers visual (V1-V15), typography (T1-T10), color/contrast (C1-C5), layout/space (L1-L8), motion (M1-M3), copy (P1-P4), imagery (I1), and quality (Q1-Q8).