# Product Brief — Recruiter-Scannable Profile README

## TL;DR
Full replacement content for `profile/README.md`, redesigned so a UK-based recruiter can determine who Bartek is, what he can concretely do, and how to reach him within ~15 seconds. Ready for handoff: `analysis/feature-spec.md` contains the complete, approved page content; `analysis/mockups/` contains a rendered visual preview. No implementation work is needed beyond replacing the file's contents — this is a content/documentation change, not application code.

## Key Decisions
- Lead with CV-aligned seniority framing ("Senior Software Engineer | Backend Architecture / Distributed Systems") instead of the prior modest "backend engineer" wording.
- Full contact bookend (LinkedIn + Email + new Calendar link) at both top and bottom of the page.
- Tech-stack badges repurposed into an accurate, cross-project (backend + frontend) row and repositioned right after the intro.
- "About this org" replaced with one honest hook sentence disclosing the recruitment-exercise/portfolio framing.
- Both project entries (`coupon-service`, `skill-flip`) compressed into a bolded punchy-lead + detail shape; `skill-flip`'s placeholder resolved with real recovered content (live demo, actual tech stack).

## Open Questions / Risks
- None outstanding — the one open risk from Phase 6 (page renders cleanly) was resolved by the Phase 7 mockup review.

---

## Problem Statement (condensed)

`profile/README.md` read as internal documentation rather than a recruiter pitch — it undersold seniority, had one incomplete project entry, and carried redundant content that slowed a fast scan. Full detail: `analysis/problem-statement.md`.

## Target Users

UK-based external recruiters and hiring managers landing on the AiB GitHub org profile page, typically scanning for ~15 seconds before deciding whether to read further or reach out. (Persona exploration was skipped per task scope — single well-defined audience, not greenfield/complex.)

## Feature Overview (condensed)

Full replacement page for `profile/README.md`, in four parts:
1. **Intro** — seniority-framed headline + three-channel contact badges (LinkedIn, Email, Calendar)
2. **Tech stack** — repositioned, accurate cross-project badge row (backend + frontend)
3. **Hook + Projects** — one honest sentence, then `coupon-service` and `skill-flip` entries with punchy-lead "Demonstrates" callouts
4. **Closing** — repeated three-channel contact

Full content: `analysis/feature-spec.md` (includes the complete assembled page, ready to paste into `profile/README.md`).

## Constraints

- Plain GitHub-Flavored Markdown only — no build step, no framework
- English-only copy
- Only two real projects exist (`coupon-service`, `skill-flip`) — no fabricated content
- Both projects honestly framed as recruitment-exercise/portfolio pieces
- Must render via GitHub's native org-profile auto-render
- Landing-page length — technical depth stays in each project's own README

## Success Criteria

- Recruiter grasps who/what/how-to-contact within ~15 seconds ✅
- Zero placeholder text — `skill-flip` fully filled with real content ✅
- Contact = LinkedIn + email + calendar, full bookend ✅
- Intro purely descriptive, no open-to-work framing ✅
- Honest recruitment-exercise framing preserved ✅
- Renders cleanly after `draft` → `main` merge ✅ (verified via Phase 7 mockup)

## Acceptance Criteria

- [ ] `profile/README.md` content replaced with the "Full Assembled Page" block from `analysis/feature-spec.md`
- [ ] All shields.io badge URLs resolve correctly (verified live in the Phase 7 mockup)
- [ ] `skill-flip`'s live demo link (`https://aib-projekt.github.io/skill-flip/`) is reachable
- [ ] Calendar link (`https://www.cal.eu/bartek/meeting`) is correct and reachable
- [ ] Page reviewed on GitHub itself after merging `draft` → `main` (mockup approximates GitHub's rendering but isn't pixel-identical)

---

## Layer 2: Design Decisions

Four decision areas resolved (full detail and rejected alternatives in `analysis/design-decisions.md` and `analysis/alternatives.md`):

| Area | Selected | Rationale |
|---|---|---|
| Contact placement | Full bookend, calendar added to both | Matches the user's own `assumptions.md` brief |
| Tech-stack section | Repurposed as accurate cross-project row, moved higher | Fixes accuracy problem, adds genuine breadth signal |
| "About this org" | One honest hook sentence | Near-direct match to user's brief, keeps honesty disclosure a home |
| Project order/density | Keep `coupon-service` first, compress both to punchy-lead + detail | Resolves scan-speed without framing mismatch or demotion risk |

Trade-offs accepted: some contact-channel redundancy for guaranteed CTA visibility; a structural repositioning of the tech-stack section for accuracy; a small scan-time cost for the hook sentence to preserve the page's only honesty disclosure.

## Layer 3: Mockup Reference

- `analysis/mockups/aib-org-profile-full-page-rendered-preview.html` — mid-fidelity rendered preview approximating GitHub's markdown styling, with live shields.io badges and annotations marking each design decision. Approved on first review.

---

## References

- `analysis/design-context.md` — unified context synthesis (project docs, CV, user's own design brief, recovered skill-flip content)
- `analysis/codebase-analysis.md` — current-state content analysis
- `analysis/problem-statement.md` — full problem statement, constraints, success criteria
- `analysis/alternatives.md` — 16 alternatives across 4 decision areas with trade-off analysis
- `analysis/design-decisions.md` — selected approach and rationale
- `analysis/feature-spec.md` — full section-by-section spec + the complete assembled page ready to implement
- `analysis/mockups/` — rendered visual preview
