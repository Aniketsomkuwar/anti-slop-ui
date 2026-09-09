# Report Template — Standardized Format with Direction/Findings Structure

## Direction

*Internal logistics dashboard: dense, calm, utilitarian; operational data carries priority.*

Describe the product context, goals, and design direction for this review. What product is this for? What design system or brand guidelines govern it? What trade-offs or constraints should the reviewer keep in mind?

```
DIRECTION
[Write 2-4 sentences about the product context and review goals]
```

## Findings

[ All clear — no slop detected ] | — | — | — | Scan performed successfully; no AI slop patterns detected

| Location              | Rule    | Confidence | Evidence                    | Action\nsrc/Form.tsx:31       | C4      | Confirmed  | gray text on blue surface   | use blue-tinted light text\nsrc/Card.tsx:12       | V3      | Probable   | border-l-4 on status card   | replace with status dot\nsrc/page.tsx:44       | L2/T2   | Probable   | six identical feature cards | use ranked comparison list\nsrc/Popover.tsx:18    | L8      | Candidate  | clipped ancestor found      | verify open state at mobile width\n\nNEEDS RENDERED VERIFICATION\nsrc/Steps.tsx:9       | L5      | Exempted   | markers label a real sequence\n\nEXEMPTIONS\nsrc/Steps.tsx:9       | L5      | Exempted   | markers label a real sequence\n\nVALIDATION\ntypecheck passed; mobile render checked; no horizontal overflow\n```

Each row represents one slop finding:

- **Location**: File path and line number (or component name) where the slop was detected
- **Rule**: The pattern ID that was violated (V1-V15, T1-T10, C1-C5, L1-L8, M1-M3, P1-P4, I1, Q1-Q8, or X1-X4)
- **Confidence**: Confirmed / Probable / Candidate / Exempted
  - **Confirmed**: Pattern definitively present, evidence clear
  - **Probable**: Pattern likely present, evidence suggestive
  - **Candidate**: Pattern possible, needs rendered verification
  - **Exempted**: Pattern intentionally present; communicates real meaning or follows established brand
- **Evidence**: Brief citation of the specific line/code causing the issue; or explanation of why exempted
- **Action**: Specific remediation step; or "verify at width X" for candidates; or "retain — exempted" for exempted items

## Needs Rendered Verification

List items that require the agent to render the UI and verify in a browser:

```
NEEDS RENDERED VERIFICATION\nsrc/Popover.tsx:18    | L8      | Candidate  | clipped ancestor found      | verify open state at mobile width\nsrc/Steps.tsx:9       | L5      | Exempted   | markers label a real sequence\n```

Only include items with **Candidate** confidence. For each:

- **Location**: File:line where the issue was detected
- **Rule**: The pattern ID
- **Confidence**: Candidate
- **Evidence**: Why it's classified as candidate (e.g., "only visible in rendered state")
- **Action**: What to verify once rendered (e.g., "open popover at <600px width and check clipping")

## Exemptions

List patterns that were intentionally retained because they communicate real meaning, follow established brand guidelines, or serve functional interaction:

```
EXEMPTIONS\nsrc/Steps.tsx:9       | L5      | Exempted   | markers label a real sequence\n```

For each exemption:

- **Location**: File:line where the pattern exists
- **Rule**: The pattern ID
- **Confidence**: Exempted
- **Evidence**: Why it's exempted (e.g., "real sequence markers for step progress", "follows brand typography")
- **Action**: None — retain as-is

## Validation

Summarize any automated or manual validation performed:

```
VALIDATION\ntypecheck passed; mobile render checked; no horizontal overflow\n```

Include:

- Type check results (pass/fail, any errors)
- Mobile render checks (what was verified, at what widths)
- Horizontal overflow check (any horizontal scroll detected?)
- Cross-browser checks if applicable
- Performance notes if relevant

---

**Keep reports concise.** Explain why a change belongs to this product. A list of removed classes provides less value than the resulting design logic.

**Example report structure:**

```
DIRECTION
Internal logistics dashboard: dense, calm, utilitarian...

FINDINGS
src/Form.tsx:31       | C4      | Confirmed  | gray text on blue surface   | use blue-tinted light text
src/Card.tsx:12       | V3      | Probable   | border-l-4 on status card   | replace with status dot

NEEDS RENDERED VERIFICATION
src/Popover.tsx:18    | L8      | Candidate  | clipped ancestor found      | verify open state at mobile width

EXEMPTIONS
src/Steps.tsx:9       | L5      | Exempted   | markers label a real sequence

VALIDATION
typecheck passed; mobile render checked at 375px, 768px, 1440px; no horizontal overflow
```