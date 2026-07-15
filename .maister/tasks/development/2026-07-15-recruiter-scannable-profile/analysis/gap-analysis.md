# Gap Analysis: Recruiter-Scannable Profile — Content Replacement

## TL;DR
The gap is fully characterized already by Phase 1: the working-tree `profile/README.md` (49 lines) is a stale intermediate draft that differs from the approved "Full Assembled Page" block in `feature-spec.md` (lines 109–159) in headline framing, contact-badge count (2 vs. 3), tech-stack section position/content, and unresolved `skill-flip` placeholders. This is a single-file, content-only overwrite with no application code, no new entities, no data-layer, and no traditional interactive UI — none of the five characteristic triggers fire strongly except "modifies existing code." Risk and effort are both low. No critical decisions block implementation; one important, non-blocking verification-timing item is flagged.

## Key Decisions
- Treated as full overwrite, not incremental diff — confirmed by Phase 1 codebase-analysis and user clarification; the target state is fully specified and ready to transcribe.
- `ui_heavy` determined false despite visual/badge content — the detection signals (components/forms/views/templates, stylesheet files, route/nav changes) are all absent. The page's scannability/information-hierarchy design was already resolved in the separate product-design workflow (mockup approved); no open UI-design question remains for this development phase.
- `involves_data_operations` and `creates_new_entities` determined false — no data entity with backend/UI/access layers, no new file/route/integration point; the same static file is rewritten in place.

## Open Questions / Risks
- `draft`/`origin/draft` have diverged specifically over this file (already surfaced in Phase 1, explicitly deferred by the user — not re-opened here).
- The calendar link domain in the approved content, `https://www.cal.eu/bartek/meeting`, is unusual and unverified per `feature-spec.md`'s own traceability table ("⚠️ Renders cleanly after draft → main merge — not yet verified"). Doesn't block writing the file but should be resolved before considering the task fully done.
- No automated verification exists in this repo (documentation-only, no CI/tests) — all acceptance checks (badge images, live-demo link, calendar link, GitHub-rendered visual check) are manual.

---

## Summary

- **Risk Level**: Low
- **Estimated Effort**: Low
- **Detected Characteristics**: `modifies_existing_code` only (others assessed and ruled out — see justification below)

## Task Characteristics

- **Has reproducible defect**: No — no error, crash, or stack trace; the current draft's shortcomings are content-completeness gaps against an already-approved spec, not a functional defect.
- **Modifies existing code**: Yes — `profile/README.md` exists with real (if stale-draft) content today; the task fully rewrites that content in place. This is the only characteristic that clearly fires.
- **Creates new entities**: No — no new files, routes, APIs, or components are introduced. The new calendar/live-demo links are new content within the existing file, not new entities requiring integration-point analysis.
- **Involves data operations**: No — no data entity with a backend/UI/access three-layer structure here. The file is simultaneously "the data" and "the display," rendered directly by GitHub with no persistence, API, or separate UI component layer.
- **UI heavy**: No — despite being visually consumed content (badges, headings, centered divs), the detection signals (components/forms/views/templates, stylesheet files, routes/buttons/navigation) are all absent. One static Markdown file, no navigation tree, no framework. The page's actual UX/scannability design was already fully worked through and approved in the separate product-design workflow; this development task is pure transcription of that approved output.

## Change Classification

- **Change type**: Modificative — the visible content changes materially (headline, badge count/order, section position, hook sentence, project copy), not merely additive and not a behavior-preserving refactor.
- **Compatibility requirements**: Flexible — the only consumer is GitHub's passive org-profile renderer; no other file, API, or process depends on this file's exact current structure or content.

## Gaps Identified

### Missing Features
None in the traditional sense — no capability is absent; every element the approved page needs already exists in fully-written form in `feature-spec.md`. The "gap" is entirely that the wrong content is currently in place.

### Incomplete Features
**`skill-flip` project entry**: Currently has unresolved placeholder text (`*[fill in — e.g. front-end fundamentals, state handling, UX for spaced repetition]*`, `*[add JS/CSS frameworks used, if any]*`, and a commented-out placeholder for a live-demo link). The approved version replaces all of this with real content: a punchy "Demonstrates" line, real tech tags (`TypeScript` · `Vite` · `Vitest` · `GitHub Actions` · `GitHub Pages`), and a live-demo link (`https://aib-projekt.github.io/skill-flip/`) placed directly in the section heading.

### Behavioral (Content) Changes Needed
- **Headline**: "Java / Spring Boot backend engineer — this org hosts sample projects referenced in my CV." → "Senior Software Engineer — Backend Architecture / Distributed Systems"
- **Contact badges (top and bottom)**: 2-badge set (LinkedIn, Email) → 3-badge set (LinkedIn, Email, Book a call/Calendar), full bookend at both top and bottom
- **Tech-stack section**: Moves from near the bottom (after Projects, 5 badges) to immediately after the intro (7 badges: adds TypeScript/Vite/GitHub Actions, drops Maven from this row only)
- **"About this org" section**: Replaced entirely with a single un-headed honest hook sentence disclosing the recruitment-exercise/portfolio framing
- **Project entries**: Both compressed into a bolded punchy-lead + detail shape under **Demonstrates:**; `coupon-service` stays first; `skill-flip` fully resolved

## User Journey / Content-Scannability Impact

| Dimension | Current | After | Assessment |
|-----------|---------|-------|------------|
| Reachability | Root org-profile URL (GitHub auto-render) | Unchanged | No change (not applicable to content edit) |
| Information scent (seniority signal) | Buried in a generic "backend engineer" line | Front-loaded in the very first line | Improved |
| Tech-stack signal position | After Projects | Immediately after intro, before Projects | Improved |
| Contact completeness | 2 channels, no scheduling option | 3 channels, same bookend top and bottom | Improved |
| Content completeness | `skill-flip` shows visible placeholder text | Fully resolved, real content with live-demo link | Improved |

## Data Lifecycle Analysis

Not applicable. No data entity with distinct backend/UI/user-access layers — the Markdown file is simultaneously the "data" and its own "display," with GitHub's renderer as the sole, passive consumer.

## Defect Analysis

Not applicable — no reproducible defect, no error/crash signal, no regression risk beyond the single target file.

## Issues Requiring Decisions

### Critical (Must Decide Before Proceeding)
None. The task is fully specified, scope was explicitly confirmed in Phase 1 clarifications, and there is no architectural, data, or UI ambiguity left to resolve.

### Important (Should Decide)
1. **Verification timing for unconfirmed links**: The approved content's calendar link (`https://www.cal.eu/bartek/meeting`) uses a domain that cannot be independently confirmed, and `feature-spec.md`'s own traceability table marks the post-merge visual/link check as "not yet verified."
   - Options: (a) Run reachability checks (badge images, `skill-flip` live-demo link, calendar link) as part of this task's implementation-verification step, immediately after the overwrite; (b) defer all link/visual verification to a separate manual step after `draft` → `main` is merged.
   - Default if no response: (a) for anything checkable pre-merge, (b) only for the GitHub-native rendering check (structurally requires the merge to have happened).

## Recommendations

1. Overwrite `profile/README.md` verbatim with the fenced block at `feature-spec.md` lines 109–159 (excluding the fence delimiters) — no line-by-line merge against the current draft.
2. After writing, diff the new content against the `feature-spec.md` block to confirm exact fidelity of Unicode characters, emoji, and backtick-wrapped inline code.
3. Stage only `profile/README.md` — the index currently holds a third, unrelated 12-line boilerplate version. Do not sweep in `.idea/.gitignore`, `CV.md`, or `assumptions.md`.
4. Run the reachability checks called out above before marking this task complete; leave only the GitHub-native post-merge visual check for after `draft` → `main`.
5. Do not attempt to resolve the `draft`/`origin/draft` divergence over this file as part of this task — already explicitly deferred by the user in Phase 1.

## Risk Assessment

- **Complexity Risk**: Minimal — single Markdown file, no logic, no build step.
- **Integration Risk**: Minimal — one passive consumer (GitHub's org-profile renderer).
- **Regression Risk**: Minimal — no test suite exists or is needed.
- **Process Risk** (the actual risk surface here): Transcription fidelity (Unicode/backtick accuracy) and git-staging hygiene are the only real failure modes.

---

```yaml
risk_level: "low"
effort_estimate: "low"
task_characteristics:
  has_reproducible_defect: false
  modifies_existing_code: true
  creates_new_entities: false
  involves_data_operations: false
  ui_heavy: false
change_type: "modificative"
compatibility_requirements: "flexible"
decisions_needed:
  critical: []
  important:
    - id: "verify-links-timing"
      issue: "Calendar link domain (cal.eu) and other acceptance-criteria links are unverified per feature-spec.md's own traceability table"
      default: "Run pre-merge-checkable items now; defer only the post-merge GitHub render check"
scope_expansion_recommended: false
```
