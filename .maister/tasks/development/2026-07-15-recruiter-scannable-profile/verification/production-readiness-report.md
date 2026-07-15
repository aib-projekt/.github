# Production Readiness Report

**Date**: 2026-07-15
**Path**: `profile/README.md` (staged content change), repo root `/Users/bartek/Documents/Projects/AiB/GitHub-main-page`
**Target**: production (`main` branch of a GitHub org-profile repo — GitHub's native org-profile renderer; no servers, no deploy pipeline, no runtime)
**Status**: With Concerns

## Executive Summary

- **Recommendation**: GO WITH MITIGATIONS
- **Overall Readiness**: 75%
- **Deployment Risk**: Medium
- **Blockers**: 2  Concerns: 1  Recommendations: 1

This is a documentation-only GitHub org-profile repository: one Markdown file (`profile/README.md`), rendered natively by GitHub on the org's home page once it reaches the default branch (`main`). There is no application code, no server, no build, no CI/CD, and no runtime to monitor. Most conventional production-readiness categories (monitoring, resilience/retry logic, performance/scaling, deployment-pipeline rollback) **do not apply** and are marked N/A below rather than padded with invented findings.

The two things that *do* apply and *do* need attention before this goes live are (1) the already-known `draft`/`origin/draft` divergence over this exact file, which is confirmed still present and will block a clean merge to `main` until resolved, and (2) a newly-observed risk: two unrelated files staged in the same git index as `profile/README.md` contain unredacted personal contact data (phone number, city) that would be permanently exposed in a public repo's history if swept into the same commit.

The content itself (the recruiter-scannable profile text) is verified clean and ready: verbatim-matches its approved specification, contains no leftover placeholders, no secrets, and no malformed links/badges.

## Category Breakdown

| Category | Score | Status |
|----------|-------|--------|
| Configuration | N/A | Not applicable |
| Monitoring | N/A | Not applicable |
| Resilience | N/A | Not applicable |
| Performance | N/A | Not applicable |
| Security | 70% | Concern (PII co-staging risk) |
| Deployment | 60% | Blocker (branch divergence) |

## Not Applicable (stated explicitly, not scored down)

- **Configuration management** — no env vars, no config files, no secrets to externalize; the file is static Markdown with no runtime configuration surface.
- **Monitoring & observability** — no logs, no metrics, no error tracker, no health-check endpoint; there is no running process. GitHub's own infrastructure serves the rendered page.
- **Error handling & resilience** — no code paths, no promises, no external calls, no circuit breakers, no graceful-shutdown handler; none of this exists for a Markdown file.
- **Performance & scalability** — no connection pooling, no caching layer, no rate limiting, no request timeouts; the "backend" is GitHub's static-content CDN, entirely outside this repo's control or responsibility.
- **CI/CD / automated tests** — confirmed (per `.maister/docs/project/tech-stack.md`) this repo has no build step and no test suite; "testing" for this task was manual verification checklists, which is the correct and only applicable form here.

Applying the full traditional checklist to this repo would produce noise, not signal — these are correctly out of scope for a static org-profile page.

## Blockers (Must Fix)

### B-1: `draft`/`origin/draft` divergence over `profile/README.md` — confirmed still present, will conflict on merge

**Location**: git refs `draft` vs `origin/draft`, file `profile/README.md`

**Current state (independently verified just now)**:
- `git status` shows branch tracking as `draft...origin/draft [ahead 1, behind 1]`.
- Local-only commit: `2383c03` ("Initialize project documentation and standards") — does **not** touch `profile/README.md`.
- Origin-only commit: `af216ef` ("Initial README.md for AiB Projekt site") — **adds** `profile/README.md` with the 12-line default GitHub-generated boilerplate ("Hi there 👋" + HTML-comment starter template).
- The new, approved recruiter-scannable content (51 lines) is currently staged locally (`git show :profile/README.md`) but **not yet committed** to local `draft` — local `draft`'s HEAD has no commit touching this file at all.
- `main` has neither commit and does not contain `profile/README.md` at all yet (`git show main:profile/README.md` → "exists on disk, but not in 'main'"). `origin` (`aib-projekt/.github`) reports `main` as its default/HEAD branch, so `main` is what GitHub actually renders as the org profile — nothing has reached it yet.

**Why this blocks**: Once the staged content is committed to local `draft`, pushing will be rejected (non-fast-forward, `draft` is already "behind 1"). Reconciling requires a merge or rebase against `origin/draft`, and because both sides independently created `profile/README.md` from a common ancestor that had no such file, git will report this as a conflict on the same file path (not a clean auto-merge) — the two versions share no common lines to align (12-line boilerplate vs. 51-line new content). This must be resolved (favoring the local 51-line version, discarding the boilerplate) before `draft` can be pushed and subsequently merged into `main`.

**Status vs. task scope**: This is the same risk already flagged and explicitly deferred to a manual step in this task's own specification (`implementation/spec.md`, "Open Questions / Risks" and "Out of Scope": *"Resolving the `draft` / `origin/draft` branch divergence over `profile/README.md` — explicitly deferred by the user to a separate manual step"*) and corroborated independently in `verification/spec-audit.md` §3. **This check confirms that risk is accurate, unresolved, and current as of this report** — it has not been addressed since it was first flagged, and it sits directly on the path to "merged to `main` and live."

**How to fix**: Before pushing `draft`: commit the staged `profile/README.md`, then either (a) rebase/merge `origin/draft` into local `draft`, resolving the conflict by keeping the new 51-line content and discarding the 12-line boilerplate, or (b) force-push local `draft` to `origin/draft` if the boilerplate commit is confirmed disposable (a deliberate, low-risk choice — no one else has built on it). Either way this is a manual git decision, not an automated fix; not something this checker performs.

### B-2: Unrelated PII-bearing files staged in the same git index as the go-live content

**Location**: `.maister/tasks/product-design/2026-07-15-recruiter-scannable-profile/context/CV.md` (staged, `git status` shows `A`) and `.../context/assumptions.md` (staged, shows `AM`)

**Evidence**: Both files sit in the same staging area as `profile/README.md` right now. `CV.md` contains, unredacted: full name, city ("Warsaw, Poland"), personal email, and a personal phone number (`+48 601 352 977`). Neither file is covered by `.gitignore` (which only excludes `.git` and `.idea`), and `.maister/` content is already tracked in this repo's history (12 files from commit `2383c03`), so there is no existing pattern that would keep these out of a commit automatically.

**Why this matters for "going live"**: `aib-projekt/.github` is a public-facing org-profile repository — its entire purpose is to be viewed by recruiters. If a commit is made without deliberately excluding these two files (e.g., via a blanket `git add -A`/`git commit -a` rather than `git add profile/README.md` as this task's own spec instructs), a personal phone number and other PII would be pushed to a public GitHub repository and become permanently visible in git history, independent of any later deletion.

**Relationship to task scope**: These files are explicitly listed as "Out of Scope" / "untouched" in this task's spec (`implementation/spec.md`, Core Requirement 3 and "Out of Scope") and confirmed pre-existing/unrelated by the independent spec audit (`verification/spec-audit.md` §3, Finding M-1). That framing correctly says this task's *implementation* must not touch them — but it does not eliminate the operational risk that they are currently staged and could be swept into the actual commit/push that ships `profile/README.md` to `main`. That risk is squarely a production/go-live concern, which is why it's flagged here even though it's outside this task's content-authoring scope.

**How to fix**: When committing, stage explicitly (`git add profile/README.md` only, as the spec itself directs) rather than committing everything staged; or `git restore --staged` the two unrelated files first if they aren't meant to ship at all in this push. Confirm with `git status`/`git diff --cached --stat` immediately before the commit that only the intended file(s) are included.

## Concerns (Should Fix)

### C-1: Trailing-newline convention was resolved but wasn't decided deliberately

**Location**: `profile/README.md`, end of file

**Evidence**: The now-staged content ends with a trailing newline (confirmed via `git show :profile/README.md | xxd`, final bytes `...3c2f6469763e0a` = `</div>\n`). The previous working-tree draft had no trailing newline. This has zero functional impact (GitHub's Markdown renderer and shields.io badges are indifferent to it), and the task's own spec explicitly logged this as a deliberately-unresolved, non-blocking ambiguity. Noted here only so it's on record as a resolved non-issue, not silently skipped.

**Recommendation**: No action needed; documented for completeness.

## Recommendations (Nice to Have)

### R-1: Re-run profile standards discovery after this merges

**Location**: `.maister/docs/standards/profile/markdown-authoring.md`, `.maister/docs/standards/profile/structure.md`

Both standards docs quote example text and line numbers from the *current* (pre-replacement) `profile/README.md`, including a "placeholder" convention that the new content deliberately eliminates entirely. Once this change lands, those docs' examples/citations will be stale (already flagged independently in `verification/spec-audit.md` Finding M-2). Not a blocker — these standards are explicitly low-confidence/informational — but worth a follow-up `/maister:standards-discover --scope=profile` pass for accuracy.

## Content Verification Performed (for context, not a gap)

Independently re-checked as part of this readiness pass, corroborating the implementation work-log and spec audit:
- Working tree and git index for `profile/README.md` are identical (`git diff -- profile/README.md` → no output) — the file is stable and fully staged, not mid-edit.
- No leftover placeholder markers (`TODO`, `FIXME`, `[fill in`, `placeholder`, `lorem ipsum`) anywhere in the staged content.
- No secrets, API keys, or credentials present — the only personal data in the file (name, LinkedIn, email, calendar link) is intentional, public-facing contact information per the approved spec, not an inadvertent leak.
- `main` currently has no `profile/README.md` at all, so this will be the first time the org-profile content reaches the branch GitHub actually renders (`main` is confirmed as `origin`'s HEAD/default branch).

## Next Steps

1. **Before committing**: stage only `profile/README.md` (`git add profile/README.md`); explicitly leave `CV.md`, `assumptions.md`, and `.idea/.gitignore` out of this commit, or `git restore --staged` them first if they shouldn't ship yet (resolves B-2).
2. **Resolve the branch divergence**: reconcile local `draft` with `origin/draft` (merge/rebase, keeping the new 51-line content over the 12-line boilerplate at `af216ef`) before pushing (resolves B-1). This is a manual decision for the repo owner, not something to automate away.
3. **Then**: push `draft`, merge `draft` → `main`, and do the manual GitHub-native rendering spot-check on the live org page — already logged in this task's spec as a deferred, post-merge, out-of-task step.
4. Optional follow-up: re-run `/maister:standards-discover --scope=profile` to refresh the now-stale profile standards docs (R-1).
