# Hallmark Design Gates — Reference for Anti-AI-Slop Integration

Hallmark (nutlope/hallmark, v1.1.0) provides a deterministic design gate system that complements the probabilistic pattern-matching in anti-ai-slop-real. While anti-ai-slop-real detects and tracks slop with confidence levels, hallmark provides pre-emit design gates that refuse to hand back code matching generic LLM-trained defaults.

## Hallmark's 57 Slop-Test Gates (High-Level Categories)

### Philosophy Gates
- Rejects on-distribution LLM defaults
- Enforces "tactile rebellion" against generic UI patterns
- Refuses color-swapped clone templates

### Hierarchy Gates
- Establishes explicit display/heading/body/label roles
- Single font family supports hierarchy through size/weight/width/optical size/spacing
- Second family earns place through clear role definition

### Execution Gates
- 61-rule deterministic detector (from impeccable skill)
- Overused font guard: Inter/Geist/Space Grotesk without brand justification
- Purple/violet gradient dilution: action/status/surface/accent roles must be derived from existing product context
- Nested card depth: beyond 2 levels repeat borders/fills/radii/shadows unnecessarily
- Bounce/elastic easing on routine controls: overshoot/spring effects rejected
- Extreme border radius: >=24px turns cards into blobs, compounds with nesting

### Specificity Gates
- Rejects "Revolutionize your workflow" hero clichés
- No generic "AI Powered" capsule badges without functional reason
- No generic AI icons (sparkle, star, magic, lightning, diamond, robot, AI orb) without product relevance

### Restraint Gates
- One meaningful transition carries more value than many ornamental effects
- Default surfaces stay still; motion communicates state, continuity, or causality
- Decoration carries meaning: domain artifacts, real product UI, data, photography, diagrams, brand motifs

### Variety Gates
- Rejects identical card grids (4+ siblings with identical icon/heading/paragraph sizing)
- Rejects monotonous spacing (same gap/padding token for all boundaries)
- Rejects hero metric layout centers on large number with tiny label and generic supporting stats

## Integration with anti-ai-slop-real

### How hallmark gates complement our skill:

1. **Pre-emit filtering**: hallmark gates run before code is handed back, preventing slop from entering the codebase
2. **Post-detection validation**: anti-ai-slop-real can scan output after hallmark gates for residual patterns
3. **Confidence escalation**: hallmark's definitive "pass/fail" gates can upgrade anti-ai-slop-real Candidate findings to Confirmed/Probable
4. **Theme-aware remediation**: hallmark's 20 themes provide concrete design alternatives when our skill detects V1-V15, T1-T10 patterns

### Combined workflow:

```
Step 1: Hallmark build() — runs 57 gates, picks macrostructure, applies rule-set, runs slop test
Step 2: If gates pass → Code handed back
Step 3: If gates fail → anti-ai-slop-real scan() detects specific patterns (V1-V15, T1-T10, etc.)
Step 4: anti-ai-slop-real track() records findings in slop-log.json with confidence/severity
Step 5: anti-ai-slop-real remediate() applies 6-stage fix order
Step 6: anti-ai-slop-real report() generates standardized report with Direction/Findings/Exemptions/Validation
```

### Hallmark-inspired additions to anti-ai-slop-real fix order:

Add after Stage 6 (Copy cadence):
- **Stage 7 — Hallmark design gates**: Run hallmark's 57-gate pre-emit check on generated UI; fail-fast on any gate violation before code is persisted

### Report template enhancement:

Add Hallmark section to report-template.md:
```
HALLMARK
Gate results summary: PASS / FAIL count
Failed gates: [list with categories: philosophy/hierarchy/execution/specificity/restraint/variety]
Theme applied: [if any] | Rationale: [brief reason]
```

### Anti-pattern cross-reference table (expanded):

| Hallmark Gate Category | anti-ai-slop-real Patterns | Example Anti-Pattern |
|------------------------|---------------------------|----------------------|
| Philosophy | — | "Revolutionize your workflow" hero headline |
| Hierarchy | T1, T8, T9 | Flat type hierarchy, single font for everything |
| Execution | V6, M1, C1 | Extreme border radius, bounce easing, purple gradients |
| Specificity | V8, V12, P2 | Generic AI icons, AI capsule badges, marketing buzzwords |
| Restraint | M3, Q6 | Image hover transform, tight line height |
| Variety | L2, L3, L4 | Identical card grids, monotonous spacing, nested cards |