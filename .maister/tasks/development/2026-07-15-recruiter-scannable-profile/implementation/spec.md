# Specification: Recruiter-Scannable Profile README — Content Replacement

## TL;DR
Replace the entire contents of `profile/README.md` with the approved "Full Assembled Page" block from the product-design task's `feature-spec.md` (lines 109–159), verbatim. This is a single-file content overwrite — no application code, no build step, one passive consumer (GitHub's org-profile renderer). The current working-tree file is a stale intermediate draft and must not be treated as a merge baseline. A repo-wide reusability search confirms no other file shares this content or its badge/`Demonstrates` conventions — there is nothing to reuse and nothing new to design; this spec exists to pin the exact target text and the verification steps around it.

## Key Decisions
- Full overwrite, not incremental diff — the working-tree draft differs materially (headline, 2- vs 3-badge contact set, tech-stack section position, unresolved `skill-flip` placeholders); patching it risks leaving stale content in place.
- Source of truth is `feature-spec.md`'s fenced "Full Assembled Page" block (lines 109–159) — not the git index (stale 12-line GitHub boilerplate) and not the current working tree.
- Stage only `profile/README.md` after the overwrite — the index currently holds an unrelated version, so `git add profile/README.md` must be re-run; no other pending changes (`.idea/.gitignore`, `CV.md`, `assumptions.md`) are swept in.

## Open Questions / Risks
- Local `draft` and `origin/draft` have diverged specifically over `profile/README.md` — explicitly deferred by the user to a separate manual sync step, not addressed by this task.
- The calendar link domain (`https://www.cal.eu/bartek/meeting`) is unverified per `feature-spec.md`'s own traceability note. Reachability is checked in this task's verification step; it does not block the content overwrite itself.
- The GitHub-native rendering check structurally requires the `draft` → `main` merge to have happened, so it is deferred to a manual post-merge step per user decision.

## Goal
Replace the stale, partially-drafted `profile/README.md` with the fully-approved, recruiter-scannable redesign — transcribed verbatim from `feature-spec.md` — so the AiB org profile front-loads seniority framing, an accurate cross-project tech-stack signal, and complete (placeholder-free) project descriptions.

## User Stories
- As a UK-based recruiter landing on the AiB GitHub org profile, I want to see seniority framing, tech breadth, and complete project descriptions within about 15 seconds, so I can quickly decide whether to read further or reach out.
- As Bartek (site owner), I want the profile page free of stale draft content and placeholder text, so recruiters never see an unfinished page.

## Core Requirements
1. Replace the entire content of `profile/README.md` with the exact text in "Exact Replacement Content" below — intro/contact block, tech-stack row, honest hook sentence, both project entries, closing contact block, in that order.
2. Preserve exact Unicode characters (em dashes `—`, middot `·`, emoji `👋 🎟️ 🎴 📫`) and backtick-wrapped inline code exactly as authored — no re-typing or auto-formatting substitutions.
3. Touch no other file — not `.idea/.gitignore`, `CV.md`, `assumptions.md`, or the root `README.md`. These have unrelated pending changes in the working tree and are explicitly out of scope.
4. Re-stage `profile/README.md` in git after the overwrite, since the currently-staged version is an unrelated stale copy.

## Visual Design
Screen `screen:profile-readme` (see `analysis/design-context/INDEX.md`) is the single screen this task implements: the full rendered `profile/README.md` page. Source mockup: `analysis/design-context/mockups/aib-org-profile-full-page-rendered-preview.html` — a mid-fidelity rendered preview approximating GitHub's Markdown styling, with live shields.io badges and inline annotations for each design decision (contact bookend, repositioned tech-stack row, honest hook sentence, punchy-lead project entries). Fidelity level: approximate, not pixel-identical to GitHub's own renderer — the product brief's own success criteria flag "renders cleanly after `draft` → `main` merge" as verified only via this mockup, with a real GitHub-render check still owed post-merge (see Open Questions above).

The mockup and `analysis/design-context/brief.md` (including its Acceptance Criteria checklist) are binding inputs for this task — there is no separate implementation-planner UI task group needed here (single content file, no componentized UI), but any `Visual References` the planner attaches to its task group(s) should point at this mockup path.

## Reusable Components

### Existing Code to Leverage
- None in the code sense — this is a static single Markdown file with no application logic, no shared components, and no other file in the repo to extend. A repo-wide search (`grep -rl "shields.io"` / `grep -rl "Demonstrates"` across all non-`.maister` Markdown files) confirms `profile/README.md` is the only file using these patterns — there is no sibling content page to reuse from or keep consistent with.
- The documented profile-authoring conventions in `.maister/docs/standards/profile/markdown-authoring.md` (centered `<div align="center">` blocks, shields.io badges) and `.maister/docs/standards/profile/structure.md` (`**Demonstrates:**` callout, backtick+middot tech-tag lists) are already fully embodied in the approved replacement content — nothing further to apply or reconcile.

### New Components Required
None. The "new" artifact is exact content that is already fully authored in `feature-spec.md`'s "Full Assembled Page" block — this task is transcription of approved, finished content, not content creation or code design.

## Technical Approach
Single-file overwrite: take the fenced block at `feature-spec.md` lines 109–159 (excluding the ` ```markdown ` fence delimiters themselves) and write it as the complete new contents of `profile/README.md`, replacing all 49 existing lines. No merge or line-by-line diff logic against the current draft — the codebase analysis already confirmed the two versions differ in headline, badge count, section order, and project-entry completeness, so reconciling differences would be strictly more work and more error-prone than a clean replace. Preserve GitHub-Flavored Markdown syntax exactly as given (headings, centered `<div>` blocks, image-linked badges, backtick code spans). After writing, stage only `profile/README.md`.

### Exact Replacement Content
The following is the full, approved, verbatim replacement for `profile/README.md` (source: `.maister/tasks/product-design/2026-07-15-recruiter-scannable-profile/analysis/feature-spec.md`, lines 109–159, "Full Assembled Page"):

```markdown
<div align="center">

# Hi, I'm Bartek 👋

Senior Software Engineer — Backend Architecture / Distributed Systems

[![LinkedIn](https://img.shields.io/badge/LinkedIn-connect-0A66C2?logo=linkedin&logoColor=white)](https://www.linkedin.com/in/bartekmarciniak)
[![Email](https://img.shields.io/badge/Email-contact-D14836?logo=gmail&logoColor=white)](mailto:puffed.08drifter@icloud.com)
[![Book a call](https://img.shields.io/badge/Book%20a%20call-schedule-4285F4)](https://www.cal.eu/bartek/meeting)

</div>

---

## Tech stack

![Java](https://img.shields.io/badge/Java-ED8B00?logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-6DB33F?logo=springboot&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?logo=postgresql&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?logo=typescript&logoColor=white)
![Vite](https://img.shields.io/badge/Vite-646CFF?logo=vite&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?logo=githubactions&logoColor=white)

---

This org hosts small, self-contained projects built as recruitment-task submissions and portfolio pieces — each one chosen to demonstrate a specific engineering skill in depth.

## Projects

### 🎟️ [coupon-service](https://github.com/aib-projekt/coupon-service)
REST API for discount coupon lifecycle management — creation, retrieval, and atomic redemption under concurrent load, with IP-based country restriction.

**Demonstrates:** **Reactive, lock-free concurrency at scale.** Built with Spring WebFlux + R2DBC; atomic redemption via `UPDATE ... WHERE ... RETURNING` (no locks); fail-closed error handling; integration-tested with Testcontainers; JaCoCo coverage gate ≥ 80%.

`Java 25` · `Spring Boot / WebFlux` · `PostgreSQL` · `Flyway` · `Docker` · `Maven`

### 🎴 [skill-flip](https://github.com/aib-projekt/skill-flip) · [Live demo](https://aib-projekt.github.io/skill-flip/)
A flip-card flashcard app for reviewing software-engineering terms — a weighted review algorithm concentrates practice time on what you keep missing.

**Demonstrates:** **Full front-to-back delivery, no framework.** Vanilla TypeScript with direct DOM manipulation; Vitest unit tests for logic and components; CI/CD via GitHub Actions → GitHub Pages, auto-deployed on push to `main`; bilingual (EN/PL) content with a documented, human-reviewed AI-assisted authoring pipeline.

`TypeScript` · `Vite` · `Vitest` · `GitHub Actions` · `GitHub Pages`

---

<div align="center">

📫 Let's talk — [LinkedIn](https://www.linkedin.com/in/bartekmarciniak/) · [Email](mailto:puffed.08drifter@icloud.com) · [Book a call](https://www.cal.eu/bartek/meeting)

</div>
```

Notes for transcription:
- Copy from `feature-spec.md` directly (do not retype from this spec) to eliminate a second transcription hop; this spec's copy is for review/traceability only.
- The current `profile/README.md` has no trailing newline; match whatever convention the tooling used to write the new content produces (not a functional concern given flexible/passive-consumer compatibility, but keep it consistent rather than accidental).

## Implementation Guidance

### Testing Approach
No automated test suite exists or applies (no code, no build step, per `.maister/docs/project/tech-stack.md`). "Testing" here is manual verification, scoped to small checklists per the project's 2-8-checks-per-group convention:

- **Group 1 — content fidelity (3 checks)**: (a) diff the written file against the "Exact Replacement Content" block above, character-for-character; (b) confirm no leftover stale content remains (old headline, 2-badge contact set, `## About this org` heading, `skill-flip` placeholder text); (c) confirm `git status` shows only `profile/README.md` staged for this change.
- **Group 2 — link/badge reachability (4 checks)**: (a) LinkedIn badge link resolves; (b) Email `mailto:` link is well-formed; (c) `skill-flip` live-demo link (`https://aib-projekt.github.io/skill-flip/`) is reachable; (d) all 7 tech-stack shields.io badge images render.
- **Deferred, not part of this task's pass/fail**: calendar link (`https://www.cal.eu/bartek/meeting`) reachability is checked but flagged informational per the open risk above; the GitHub-native rendered-page visual check is deferred to after `draft` → `main` is merged.

### Standards Compliance
- `.maister/docs/standards/profile/markdown-authoring.md` and `.maister/docs/standards/profile/structure.md` (both low-confidence/informational, not enforced) — the approved content already conforms to every documented pattern (centered div blocks, shields.io badges, `**Demonstrates:**` callout, backtick+middot tech tags). No conflicts to resolve.
- `.maister/docs/standards/global/minimal-implementation.md` and `.maister/docs/standards/global/conventions.md` — build only what's needed: this task is a verbatim transcription with no extra scaffolding, no speculative sections, no future-proofing.

## Out of Scope
- `.idea/.gitignore`, `CV.md`, `assumptions.md` — unrelated pending changes already in the working tree; not touched, staged, or committed by this task.
- Resolving the `draft` / `origin/draft` branch divergence over `profile/README.md` — explicitly deferred by the user to a separate manual step.
- The GitHub-native post-merge rendering visual check — structurally requires `draft` → `main` to be merged first; manual follow-up outside this task.
- Deep validation of the calendar link (`cal.eu`) domain beyond a basic reachability check.
- Any content, badges, or project entries beyond the approved "Full Assembled Page" block — no new sections, no speculative future-project placeholders.
- `roadmap.md` / `architecture.md` creation — intentionally not generated for this repo per `.maister/docs/INDEX.md`.

## Success Criteria
- `profile/README.md` content is character-for-character identical to the "Exact Replacement Content" block above.
- Zero placeholder text remains anywhere in the file (the `skill-flip` entry is fully resolved with real content and a live-demo link).
- Contact bookend present at both top and bottom: LinkedIn + Email + Book a call (3 badges/links each).
- The `## Tech stack` section is positioned immediately after the intro block, before `## Projects`, with all 7 badges present.
- `git status` shows only `profile/README.md` staged for this task's change — no unrelated files swept in.
- All checkable links/badges (LinkedIn, Email, `skill-flip` live demo, 7 tech-stack badge images) verified reachable/rendering before this task is marked complete.
- The calendar link check and the GitHub-native rendering check are explicitly logged as deferred/informational in the verification output, not silently skipped.
