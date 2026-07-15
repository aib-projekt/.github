# Implementation Plan: Recruiter-Scannable Profile README — Content Replacement

## TL;DR
One task group, one file, one execution wave: overwrite `profile/README.md` with the verbatim "Exact Replacement Content" block already pinned in `implementation/spec.md`, re-stage it in git, and run the 7 manual verification checks the spec itself defines (no automated test suite applies to this docs-only repo). No dependencies, no parallelism to schedule, no Testing Review group — this is deliberately not broken up further than the single action it is.

## Key Decisions
- Single task group, not split into content/verification groups — the entire scope is one file overwrite plus checks of that same content; splitting would add coordination overhead with zero parallelism benefit for a 1-file change.
- Adapted the standard "write tests first" step into "define the verification checklist first" — no automated test suite exists for this repo (per `.maister/docs/project/tech-stack.md`: docs-only, no build step). The spec's own 7-item manual checklist (3 content-fidelity + 4 link-reachability checks) fills the same role and stays within the 2-8-per-group convention.
- No "Test Review & Gap Analysis" group added — that group is only warranted when total implementation groups ≥ 3; with exactly 1 group here it would be pure process overhead for a content transcription task.

## Open Questions / Risks
- Spec-audit Finding M-1 (Medium): read literally, "`git status` shows only `profile/README.md` staged" is unachievable — three unrelated files (`.idea/.gitignore`, `context/CV.md`, `context/assumptions.md`) are already staged before this task starts, and the spec's own Out-of-Scope rule forbids touching them. Step 1.4(c) below is written to check the *delta introduced by this task* (profile/README.md is the only newly-staged file) rather than the absolute staged-file count, per the audit's recommended disambiguation. No plan change needed beyond this phrasing; the spec's Success Criteria bullet 5 could still be reworded for clarity but that's a spec edit, not an implementation step.
- Spec-audit Finding M-2 (Medium): after this overwrite, `.maister/docs/standards/profile/markdown-authoring.md` and `structure.md` will contain stale example quotes/line citations pointing at content that no longer exists. This is out of scope for this task's implementation (it's a separate documentation-maintenance action, not a Core Requirement of this spec) — flagged here for operator visibility, not as a plan task.
- Calendar link (`cal.eu`) reachability and the GitHub-native post-merge rendering check are both explicitly deferred per spec's Out of Scope section. Step 1.4 logs them as informational, not gating.

## Overview
Total Steps: 4
Task Groups: 1
Expected Verification Checks: 7 (no automated tests apply — docs-only repo; see Key Decisions)

## Implementation Steps

### Task Group 1: Profile README Content Replacement
**Dependencies:** None
**Files to Modify:** profile/README.md
**Visual References:**
- mockup: analysis/design-context/mockups/aib-org-profile-full-page-rendered-preview.html
  element: screen:profile-readme
  locator: `.markdown-body` content block (mockup lines 282-327) — intro block lines 283-291, tech-stack row lines 295-304, hook sentence line 308, `coupon-service` entry lines 312-315, `skill-flip` entry lines 317-320, closing contact block lines 324-326
  acceptance: section order is intro → tech stack → hook sentence → Projects (`coupon-service` then `skill-flip`) → closing contact, matching spec's Core Requirement 1; both the intro and closing blocks show exactly 3 contact badges/links (LinkedIn, Email, Book a call); the `## Tech stack` section sits immediately after the intro block and before `## Projects`, with exactly 7 badges (Java, Spring Boot, PostgreSQL, Docker, TypeScript, Vite, GitHub Actions); each project entry opens with a bolded `**Demonstrates:**` line whose lead phrase is bolded (e.g. "Reactive, lock-free concurrency at scale.") followed by supporting detail, per `structure.md`'s Demonstrates-callout convention; the `skill-flip` heading includes its "Live demo" link and neither project entry contains any placeholder text
**Estimated Steps:** 4

- [x] 1.0 Complete profile README content replacement
  - [x] 1.1 Define the verification checklist before touching the file (7 checks total, adapting the standard test-first step since no automated test suite applies to this docs-only repo — per spec.md's own "Testing Approach"):
    - Content-fidelity checks (3): (a) written file diffs clean, character-for-character, against spec.md's "Exact Replacement Content" block (spec.md lines 50-100); (b) no stale content remains (old headline, 2-badge contact set, `## About this org` heading, `skill-flip` placeholder text); (c) `profile/README.md` is the only file newly staged by this task's actions (see 1.4(c) for the precise check)
    - Link/badge-reachability checks (4): (d) LinkedIn badge link resolves; (e) Email `mailto:` link is well-formed; (f) `skill-flip` live-demo link (`https://aib-projekt.github.io/skill-flip/`) is reachable; (g) all 7 tech-stack shields.io badge images render
  - [x] 1.2 Overwrite `profile/README.md` with the exact "Exact Replacement Content" block from `implementation/spec.md` (lines 50-100) — copy verbatim from `spec.md` (or the identical source at `.maister/tasks/product-design/2026-07-15-recruiter-scannable-profile/analysis/feature-spec.md` lines 109-159), do not retype, preserving Unicode em dashes (`—`), middots (`·`), emoji (`👋 🎟️ 🎴 📫`), and backtick-wrapped inline code exactly as authored. Replace all existing lines in the file — this is a full overwrite, not a line-by-line merge against the current stale draft.
  - [x] 1.3 Re-stage only `profile/README.md` in git (`git add profile/README.md`) — leave `.idea/.gitignore`, `.maister/tasks/product-design/2026-07-15-recruiter-scannable-profile/context/CV.md`, `context/assumptions.md`, and any other already-staged files exactly as they were; do not run `git restore --staged` on anything.
  - [x] 1.4 Run the 7 checks defined in 1.1 against the written file — do NOT run any repo-wide test suite (none exists/applies):
    - (a)-(b) content fidelity and no-stale-content, per 1.1
    - (c) `git status` shows `profile/README.md` as the only *newly* staged/modified file introduced by this task — the three pre-existing staged files from before this task started remain unchanged (resolves spec-audit Finding M-1's literal-vs-delta ambiguity)
    - (d)-(g) link/badge reachability, per 1.1
    - Log as deferred/informational, not part of pass/fail: calendar link (`https://www.cal.eu/bartek/meeting`) reachability; the GitHub-native rendered-page visual check (structurally requires `draft` → `main` merge first, per spec Out of Scope)

**Acceptance Criteria:**
- All 7 checks from 1.1/1.4 pass
- `profile/README.md` is character-for-character identical to spec.md's "Exact Replacement Content" block
- Zero placeholder text remains anywhere in the file
- Contact bookend present at both top and bottom: LinkedIn + Email + Book a call (3 badges/links each)
- `## Tech stack` section positioned immediately after the intro block, before `## Projects`, with all 7 badges present
- `git status` shows `profile/README.md` as the only newly-staged file introduced by this task; pre-existing staged files remain untouched
- Calendar link check and GitHub-native rendering check are explicitly logged as deferred/informational, not silently skipped
- Implementation matches each `acceptance` criterion declared under Visual References above

## Execution Order

1. Group 1 — Profile README Content Replacement (4 steps)

No parallelism to schedule and no dependency chain beyond this single group.

## Standards Compliance

Follow standards from `.maister/docs/standards/`:
- `global/minimal-implementation.md` and `global/conventions.md` — build only what's needed; this is a verbatim transcription with no extra scaffolding.
- `profile/markdown-authoring.md` and `profile/structure.md` — the approved replacement content already embodies the centered `<div align="center">` blocks, shields.io badges, `**Demonstrates:**` callout, and backtick+middot tech-tag conventions documented there. Note (per spec-audit Finding M-2): the "inline placeholder" pattern documented in `markdown-authoring.md` is intentionally retired by this change, not followed — that's correct per this task's own "zero placeholder text" success criterion, not a deviation to fix.

## Notes

- Verification-Driven: the single group defines its checklist before writing the file, and verifies against that same checklist after — mirroring the test-driven pattern with manual checks in place of automated tests (none apply to this docs-only repo).
- Run Incrementally: only the 7 checks defined in 1.1 are run; there is no broader suite to run.
- Mark Progress: check off steps 1.1-1.4 as completed.
- Reuse First: N/A — spec confirms no reusable or new components exist for this content-only change.
- Task-tracking note: this environment does not expose a `TaskCreate`/`TaskUpdate` tool, so group-level tracking is the markdown checkboxes above only (no parallel Task-system items were created).
