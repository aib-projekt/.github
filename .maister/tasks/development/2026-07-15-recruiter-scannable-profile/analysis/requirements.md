# Requirements — Recruiter-Scannable Profile README Implementation

## TL;DR
Full verbatim replacement of `profile/README.md` with the approved content from the product-design workflow. No new discovery path, no reusable code/components beyond documented profile conventions, no additional visual assets needed — everything required is already ingested in `analysis/design-context/`.

## Key Decisions
- No architectural/technical clarification needed (risk_level: low, single well-defined change).
- Existing `analysis/design-context/` (brief.md + mockup + INDEX.md) is the complete visual/requirements source — no new mockups needed.

## Open Questions / Risks
- None outstanding.

---

## Initial Description

Implement the approved product-design brief: replace the contents of `profile/README.md` with the redesigned content specified in the "Full Assembled Page" block of `.maister/tasks/product-design/2026-07-15-recruiter-scannable-profile/analysis/feature-spec.md`.

## Q&A

**User Journey**: No change to discovery/access — same GitHub org-profile URL, same single audience (UK-based recruiters), no new entry points. *(Confirmed)*

**Existing Code Reuse**: Nothing to reuse beyond documented profile conventions (centered divs, shields.io badges, Demonstrates callout pattern) in `.maister/docs/standards/profile/`. No code, components, or backend patterns apply — pure Markdown content. *(Confirmed)*

**Visual Assets**: Mockup and product brief already ingested into `analysis/design-context/` during initialization — sufficient, no additional assets needed. *(Confirmed)*

## Similar Features Identified

None — no comparable prior page redesign exists in this repo's history (2 commits total).

## Visual Assets and Insights

- `analysis/design-context/brief.md` — the binding product brief (acceptance criteria, design decisions, success criteria)
- `analysis/design-context/mockups/aib-org-profile-full-page-rendered-preview.html` — approved rendered preview
- `analysis/design-context/INDEX.md` — screen inventory (1 screen: the full page)

## Functional Requirements Summary

1. Replace the entire content of `profile/README.md` with the "Full Assembled Page" block from the source product-design task's `analysis/feature-spec.md` (lines 109–159), verbatim.
2. Preserve exact Unicode characters (em dashes, middot separators, emoji) and inline-code formatting.
3. No other files are modified as part of this change.

## Reusability Opportunities

None applicable — single static content file, no code to extract or share.

## Scope Boundaries

**In scope**: `profile/README.md` content replacement only.
**Out of scope**: `.idea/.gitignore` cleanup, `CV.md`/`assumptions.md` changes, `draft`/`origin/draft` branch divergence resolution — all explicitly deferred per Phase 1 clarifications.

## Technical Considerations

- Plain GitHub-Flavored Markdown, no build step, no framework.
- Git staging: the index currently holds an unrelated stale version of `profile/README.md` (12-line GitHub boilerplate) — must be re-staged after the overwrite, not assumed current.
- Verification: badge/link reachability (LinkedIn, Email, Calendar, skill-flip live demo) checked during Phase 11; GitHub-native rendering check deferred to post-merge (per Phase 2 decision).
