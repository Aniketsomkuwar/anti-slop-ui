# Content Quality Evaluation Guidelines

Standards for evaluating content quality and identifying AI slop, integrated from multiple skill references.

## Quality Markers (Good Content)

- **Specific**: Contains concrete details, examples, or data specific to the topic
- **Grounded**: Claims are supported by evidence, citations, or personal experience
- **Varied**: Sentence structures vary; not formulaic or repetitive
- **Context-aware**: Shows understanding of the specific situation/problem
- **Actionable**: Provides clear next steps or specific guidance

## Slop Red Flags (AI-Low Quality)

- **Generic assertions** without supporting evidence
- **Formulaic transitions** that could apply to any topic
- **Overused phrases** that AI models favor (see slop-patterns.md)
- **Empty claims** like "the best," "state-of-the-art," "industry-leading" without qualification
- **Repetitive sentence structures** starting with the same patterns
- **Lack of source citations** for factual claims
- **Vague time/place references** that don't ground the content

## Remediation Guidance

When slop is detected, follow the 6-stage fix order:

1. **Broken behavior, accessibility, overflow, readability** — Fix critical issues first
2. **Information architecture and unsupported content** — Remove redundant/unnecessary sections
3. **Repeated page templates, card anatomy, container depth** — Address system-level repetition
4. **Type hierarchy, spacing rhythm, color roles** — Apply consistent typography and spacing
5. **Decorative borders, gradients, glows, radii, icons, motion** — Remove decorative defaults without purpose
6. **Copy cadence and redundant labels** — Fix formulaic copy patterns

## Tracking

All detected slop should be logged in `~/.hermes/slop-tracker/slop-log.json` with:
- File path and line number
- Pattern ID (V1-V15, T1-T10, C1-C5, L1-L8, M1-M3, P1-P4, I1, Q1-Q8)
- Confidence level (Confirmed/Probable/Candidate)
- Severity (Critical/High/Medium/Low)
- Evidence: source line citation
- Remediation action taken
- Status: pending/reviewed/removed
- Exemption: if pattern communicates real meaning, follows established brand, or serves functional interaction