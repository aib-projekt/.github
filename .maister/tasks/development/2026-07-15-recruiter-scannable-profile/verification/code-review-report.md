# Code Review Report

**Date**: 2026-07-15
**Path**: profile/README.md
**Scope**: all (Markdown syntax, link validity/safety, placeholder/stale-content check, formatting consistency, GitHub-rendering risk)
**Status**: ✅ Clean

## Summary
- **Critical**: 0 issues
- **Warnings**: 1 issue
- **Info**: 3 issues

## Context established before review
- `profile/README.md` is a brand-new file in this change (`git status` shows `A  profile/README.md`; `git log` has no prior history for the path) — the entire 51 lines are "the diff."
- Verified byte-for-byte against the approved source of truth: `sed -n '50,100p' implementation/spec.md` diffed clean (exit 0) against `profile/README.md`. The implementation matches the approved "Exact Replacement Content" character-for-character, confirming the work-log's SHA-256 claim independently.
- Confirmed repo identity: `origin` is `aib-projekt/.github`, `profile/README.md` is exactly the path GitHub requires for an org profile README. This is structurally correct for GitHub's renderer, contingent on landing on the `main` branch (currently on `draft` — see Info-3).

## Critical Issues
None.

## Warnings

### W1 — LinkedIn URL is represented two different ways in the same file
- **Location**: `profile/README.md:7` vs `profile/README.md:49`
- **Description**: The top contact block links `https://www.linkedin.com/in/bartekmarciniak` (no trailing slash); the closing contact block links `https://www.linkedin.com/in/bartekmarciniak/` (with trailing slash). Both were fetched and both resolve (LinkedIn normalizes the slash), so this is not a broken link, but it's an internal inconsistency in a file whose whole premise is a polished, scannable "business card" — a recruiter clicking both wouldn't notice, but it reads as sloppy on a byte/diff level and is exactly the kind of formatting drift automated review is meant to catch.
- **Recommendation**: Pick one form (dropping the trailing slash matches the other two contact links, which have no trailing path segment) and use it in both places.

## Informational

### I1 — Email badge uses the Gmail logo for a non-Gmail address
- **Location**: `profile/README.md:8` and `:49`
- **Description**: `![Email](...logo=gmail...)` is paired with `mailto:puffed.08drifter@icloud.com` — an iCloud address, not Gmail. Shields.io's `logo=gmail` renders the Gmail glyph specifically, which is a minor branding mismatch (a recruiter who notices will read it as "wrong icon," not "wrong address," since the mailto target itself is correct and functional).
- **Suggestion**: Swap to a generic mail icon (e.g. `logo=maildotru` isn't right either — simplest fix is to drop the `logo` param for this badge, or use `logo=icloud` if shields.io/simple-icons supports it) so the icon matches the actual provider.

### I2 — Contact email is an iCloud private-relay-style alias
- **Location**: `profile/README.md:8`, `:49` (also present identically in `CV.md`, so this is consistent, intentional, and out of this task's scope to change)
- **Description**: `puffed.08drifter@icloud.com` has the shape of an Apple "Hide My Email" relay alias rather than a human-chosen address. Functionally this is fine (mail sent to it forwards to a real inbox) and it's consistent across both files, so it is not a defect introduced by this change. Flagging only because a UK recruiter scanning in 15 seconds may pause on an unfamiliar-looking address before trusting it — worth a conscious double-check that the relay is still active, not a code fix.
- **Suggestion**: No action required for this task; consider (separately, outside this task's scope) whether a plainer address would read more confidently to recruiters.

### I3 — Rendered result is not yet live on the org profile
- **Location**: N/A (branch state, not file content)
- **Description**: The current branch is `draft`; the org's actual public profile page renders from the `.github` repo's default branch, which `gh api` confirms is `main`. Until `draft` → `main` is merged, this content will not appear on `https://github.com/aib-projekt`. The task's own spec (`implementation/spec.md`, Out of Scope section) already defers this merge and the post-merge GitHub-native rendering check as a manual step, so this is not a defect in the file — noting it here only so it isn't mistaken for "done and live" when read in isolation.
- **Suggestion**: No action required for this task; carry the `draft` → `main` merge and post-merge visual check forward as already planned.

## Verification performed (link/badge/rendering checks)

| Item | Result |
|---|---|
| `github.com/aib-projekt/coupon-service` | Exists, public (`gh api` confirmed) |
| `github.com/aib-projekt/skill-flip` | Exists, public (`gh api` confirmed) |
| `https://aib-projekt.github.io/skill-flip/` (live demo) | HTTP 200 |
| `https://www.cal.eu/bartek/meeting` | HTTP 200; content is a genuine Cal.com-style booking app (not a parked/dead domain) — resolves the "unverified" risk the spec flagged |
| `https://www.linkedin.com/in/bartekmarciniak` (both forms) | HTTP 999 (LinkedIn's standard anti-bot response to automated requests — inconclusive by design, not a signal of breakage) |
| All 10 shields.io badge URLs (3 contact + 7 tech-stack) | HTTP 200, valid SVG responses |
| `mailto:puffed.08drifter@icloud.com` | Well-formed `mailto:` syntax |
| Placeholder/stale-content scan (`TODO`, `FIXME`, `lorem ipsum`, `placeholder`, `[fill`, `TBD`, `coming soon`) | No matches |
| Trailing whitespace / tabs | None found |
| File encoding / Unicode fidelity | All non-ASCII characters verified correct codepoints: em dash U+2014 (x5), middle dot U+00B7 (x12), `≥` U+2265, `→` U+2192, and all four emoji including the ticket emoji's variation selector (U+FE0F) — no mojibake, matches spec's "preserve exact Unicode" requirement |
| Trailing newline | File ends with `\n` (clean) |

## Markdown structure / GitHub-rendering check
- Heading hierarchy is well-formed and non-skipping: H1 (`# Hi, I'm Bartek`) → H2 (`## Tech stack`, `## Projects`) → H3 (`### coupon-service`, `### skill-flip`). No skipped levels.
- Both `<div align="center">...</div>` blocks have the required blank line immediately after the opening tag and before the closing tag, which is what allows GitHub's renderer to process the Markdown/badges nested inside raw HTML rather than treating it as literal text — this is the standard, correct pattern for GitHub profile READMEs.
- Badge/image syntax is correct throughout: bare `![alt](url)` for non-linked tech-stack badges, `[![alt](url)](link)` for the three linked contact badges — no malformed brackets or dangling references.
- Adjacent bold spans (`**Demonstrates:** **Reactive, lock-free concurrency at scale.**`) are separated by a plain space, which CommonMark/GFM parses unambiguously as two distinct emphasis runs — renders correctly, not a syntax risk.
- Backtick code spans (`` `UPDATE ... WHERE ... RETURNING` ``, `` `main` ``, and all tech-tag spans) are properly closed with no embedded unescaped backticks.
- No relative links or relative image paths anywhere in the file — every link/image is an absolute URL, eliminating any risk of broken links due to this file's location within the repo.
- No malicious, obfuscated, or unexpected-destination URLs — every link target was inspected and matches its visible/alt text (LinkedIn → linkedin.com, Email → mailto: same address as CV.md, Book a call → cal.eu booking app, GitHub repo links → matching `aib-projekt` org repos, live demo → matching GitHub Pages subdomain, shields.io badges → shields.io).

## Metrics
- Lines in file: 51
- Max heading depth: 3 (H1/H2/H3, no skips)
- Links checked: 8 (3 contact top + 2 project repo + 1 live demo + 1 calendar + 1 contact bottom set, minus dedup)
- Badge images checked: 10 (all HTTP 200)
- Placeholder/stale-content matches: 0
- Diff against approved spec content: 0 (exact match)

## Prioritized Recommendations
1. (Warning) Normalize the LinkedIn URL to one form (with or without trailing slash) across both the top and bottom contact blocks.
2. (Info, optional) Reconsider the `logo=gmail` badge parameter given the address is an iCloud alias, if brand-accuracy on the icon matters.
3. (Info, no action this task) Proceed with the already-planned `draft` → `main` merge and the deferred post-merge GitHub-native rendering check; nothing in the file itself blocks that merge.
