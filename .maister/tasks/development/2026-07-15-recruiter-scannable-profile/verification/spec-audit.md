# Specification Audit: Recruiter-Scannable Profile README — Content Replacement

**Audited spec**: `.maister/tasks/development/2026-07-15-recruiter-scannable-profile/implementation/spec.md`
**Source of truth checked against**: `.maister/tasks/product-design/2026-07-15-recruiter-scannable-profile/analysis/feature-spec.md`
**Method**: Independent file reads + byte-level diff/MD5 comparison + live `git` inspection (not trusting the spec's own fidelity/scope claims)

## TL;DR
**Verdict: Pass-with-concerns.** The core claim — that the spec's "Exact Replacement Content" block is a verbatim, byte-identical copy of `feature-spec.md` lines 109–159 — is independently confirmed (MD5 match, 51/51 lines, 0 diff). The out-of-scope boundary is also independently confirmed accurate against live `git status`/`git log`. Issues found: 0 Critical, 0 High, 2 Medium, 4 Low. Nothing here blocks a direct find/replace implementation, but two Medium items (a self-contradicting git-status acceptance criterion, and an overstated "no standards conflicts" claim) are worth a quick look before sign-off.

## Key Decisions
- Treated "byte-identical" literally and verified via MD5 checksum + `diff`, not eyeballing — this is the one claim in the spec most likely to hide a subtle Unicode/whitespace bug, so it got the strictest check.
- Did not penalize the deliberately-deferred trailing-newline ambiguity or the branch-divergence framing — both are explicitly flagged as non-blocking by the spec/clarifications and independently confirmed accurate, so they're documented as Low/informational rather than gaps.

## Open Questions / Risks
- Does "`git status` shows only `profile/README.md` staged for this task's change" (Success Criteria, Core Req. 4) mean literally "the only staged file in the repo" (currently false and unachievable without violating the out-of-scope rule) or "the only file staged *by this task's actions*" (true, achievable)? See Finding M-1.
- Should the profile standards docs (`markdown-authoring.md`, `structure.md`) be re-run through `/maister:standards-discover` after this task lands, since several of their quoted examples and line-number citations will no longer match the new file? Not addressed anywhere in the spec or its upstream analysis docs. See Finding M-2.

---

## 1. Content Fidelity — Independently Verified

**Claim** (spec.md TL;DR, Technical Approach): the "Exact Replacement Content" block (spec.md lines 50–100) is the fenced block at `feature-spec.md` lines 109–159, verbatim, excluding fence delimiters.

**Verification performed**:
- Extracted `spec.md` lines 50–100 and `feature-spec.md` lines 109–159 with `sed`.
- `diff` → **empty** (identical).
- `md5` of both extracts → **`5dd82305483684342ad6d913868290db`** for both files — byte-for-byte identical, including Unicode em dashes (`—`), middots (`·`), and emoji (`👋 🎟️ 🎴 📫`).
- Confirmed fence boundaries independently: `spec.md` line 49 = ` ```markdown `, line 101 = ` ``` `; `feature-spec.md` line 108 = ` ```markdown `, line 160 = ` ``` `. The claimed line range (109–159) is exactly the fenced content, correctly excluding the fence markers themselves.
- Confirmed line counts match: 51 lines each (50–100 inclusive, 109–159 inclusive).

**Result**: **Confirmed accurate.** No discrepancy found. This is the highest-risk claim in the spec (a single mistyped em dash or dropped emoji would fail the "character-for-character" success criterion) and it holds up under independent byte-level scrutiny.

**Category**: N/A (verified correct) | **Severity**: N/A

---

## 2. Requirements Completeness/Unambiguity for Direct Implementation

### Finding M-1 (Medium): Self-contradicting git-status acceptance criterion

**Spec Reference**: Core Requirement 4 ("Re-stage `profile/README.md`..."), Success Criteria bullet 5 ("`git status` shows only `profile/README.md` staged for this task's change — no unrelated files swept in"), and Testing Approach Group 1 check (c) ("confirm `git status` shows only `profile/README.md` staged for this change").

**Evidence**: Live `git status` in the repo right now shows, in "Changes to be committed":
```
new file:   .idea/.gitignore
new file:   .maister/tasks/product-design/2026-07-15-recruiter-scannable-profile/context/CV.md
new file:   .maister/tasks/product-design/2026-07-15-recruiter-scannable-profile/context/assumptions.md
new file:   profile/README.md
```
These three unrelated files are *already* staged before this task begins, and the spec's own Out of Scope section correctly forbids touching (which includes un-staging) them. So after a correct implementation, `git status` will show **four** staged files, not one.

**Gap Description**: Read literally, "`git status` shows only `profile/README.md` staged" is false for any compliant implementation — it's only true if quietly reinterpreted as "the only file staged *as a result of this task's actions*" (i.e., ignore the three pre-existing staged files). The spec never states this qualifier explicitly, so a literal-minded implementer or an automated verification step could flag a correct implementation as failing this checklist item, or conversely could be tempted to `git restore --staged` the unrelated files to make the literal check pass — which would violate the "touch no other file" requirement.

**Category**: Ambiguous
**Severity**: Medium — this is a checklist-gating acceptance criterion (used in both Success Criteria and the verification Testing Approach), and its most literal reading is unachievable without breaking a different explicit requirement. Low likelihood of derailing the actual 2-line content overwrite, but real likelihood of causing a confusing false-fail at verification time or prompting an unauthorized `git restore --staged` on unrelated files.

**Recommendation**: Reword to something unambiguous, e.g.: "`git status` shows `profile/README.md` as the only *newly* staged/modified file introduced by this task; the three pre-existing staged files (`.idea/.gitignore`, `context/CV.md`, `context/assumptions.md`) remain exactly as they were before this task started, untouched."

---

### Finding M-2 (Medium): "No standards conflicts" claim overstates alignment; standards docs will go stale post-task

**Spec Reference**: Standards Compliance section — "the approved content already conforms to every documented pattern (centered div blocks, shields.io badges, `**Demonstrates:**` callout, backtick+middot tech tags). No conflicts to resolve."; Reusable Components section — same claim, "already fully embodied... nothing further to apply or reconcile."

**Evidence**: `.maister/docs/standards/profile/markdown-authoring.md` documents three patterns from the *current* (soon-to-be-replaced) file, one of which is:
> "### Inline Placeholders for Incomplete Content — Incomplete sections are marked with inline HTML comments or bracketed placeholder text... Source: `profile/README.md`, e.g. `*[fill in — e.g. front-end fundamentals, state handling, UX for spaced repetition]*` and `<!-- Optional: add a live demo link here if skill-flip is hosted -->`."

The approved replacement content contains **zero** placeholders anywhere (confirmed by direct inspection of the "Exact Replacement Content" block, and this is itself a stated Success Criterion of the very same spec: "Zero placeholder text remains anywhere in the file"). So this documented standard isn't "conformed to" — it's being made permanently inapplicable by design. Separately, `structure.md` line 10 quotes the *old* Demonstrates text ("reactive programming (Spring WebFlux + R2DBC), safe concurrency without locks...") as its example source, and `markdown-authoring.md` line 10 cites specific old line numbers ("opening block, lines 1-10; closing contact block, lines 46-50") — both citations point at text/positions that will no longer exist in `profile/README.md` once this task lands.

**Gap Description**: The spec's blanket claim of "no conflicts, nothing to reconcile" is not quite accurate — one of the three documented conventions is being retired rather than followed (which is fine, arguably an improvement, since the standards are explicitly low-confidence/informational), but the spec doesn't acknowledge this, and doesn't flag that the standards docs themselves will contain stale quotes/line citations after the overwrite. This is not a functional defect in the implementation (the standards are non-enforced, informational, and the codebase-analysis doc even notes in passing that "the 'placeholder' convention becomes moot"), but it's an unaddressed, real side effect of this task that no document in the workflow proposes a follow-up for.

**Category**: Incorrect (claim), Missing (follow-up action)
**Severity**: Medium for the accuracy-of-claim issue (a stated "no conflicts" is technically wrong), downgraded in practical impact to Low because the standards are explicitly non-enforced/informational and no user-facing or implementation harm results.

**Recommendation**: Either soften the claim ("conforms to the two enforceable-in-spirit conventions; the placeholder convention is intentionally retired by this change, consistent with the 'zero placeholder text' success criterion") or add a follow-up note to re-run `/maister:standards-discover --scope=profile` after this task merges, so the standards docs' stale citations get refreshed.

---

### Finding L-1 (Low): Trailing-newline handling left deliberately unresolved

**Spec Reference**: Notes for transcription — "The current `profile/README.md` has no trailing newline; match whatever convention the tooling used to write the new content produces (not a functional concern given flexible/passive-consumer compatibility, but keep it consistent rather than accidental)."

**Evidence**: Independently confirmed the current working-tree file ends with `>` (no trailing `\n`, byte `3e`), while the currently-staged/index version ends with a newline (byte `0a`). The spec is aware of this discrepancy and explicitly declines to mandate one or the other.

**Category**: Ambiguous (deliberately, and acknowledged)
**Severity**: Low — explicitly called out as non-functional by the spec itself; GitHub's renderer doesn't care. Flagged only because "character-for-character identical to the Exact Replacement Content block" (Success Criteria bullet 1) is technically underspecified at the very last byte, but this has no practical consequence.

---

### Finding L-2 (Low): Out-of-scope file list inconsistency between Core Requirements and Out of Scope section

**Spec Reference**: Core Requirement 3 lists four untouched files/paths: "`.idea/.gitignore`, `CV.md`, `assumptions.md`, or the root `README.md`." The "Out of Scope" section's file bullet lists only three: "`.idea/.gitignore`, `CV.md`, `assumptions.md`" — the root `README.md` is not repeated there (it only appears elsewhere, implicitly, via "no other file... touched").

**Evidence**: Independently confirmed the root `README.md` (9 bytes, content `# .github`) has no pending git changes at all, so this inconsistency carries no practical risk — nothing would sweep it in regardless.

**Category**: Incomplete (list) / Ambiguous
**Severity**: Low — cosmetic inconsistency between two lists in the same document; no functional risk since the file in question has nothing pending to accidentally include.

---

### Finding L-3 (Low): Out-of-scope filenames given without full repo-relative paths

**Spec Reference**: Core Requirement 3 and Out of Scope section both refer to "`CV.md`" and "`assumptions.md`" by bare filename.

**Evidence**: Independently searched the entire repository (`find . -name "CV.md" -o -name "assumptions.md"`) — there is exactly one of each, both at `.maister/tasks/product-design/2026-07-15-recruiter-scannable-profile/context/CV.md` and `.../context/assumptions.md`. No root-level files by these names exist.

**Category**: Ambiguous (in form only)
**Severity**: Low — no actual ambiguity exists in this repo today (uniqueness confirmed), but the spec would be more precise citing full paths rather than bare filenames, especially since `git status` run from the repo root will display the full nested path, not the bare name used in the spec.

---

## 3. Out-of-Scope Boundary — Independently Verified

**Claim**: `.idea/.gitignore`, `CV.md`, `assumptions.md`, and the `draft`/`origin/draft` divergence over `profile/README.md` are correctly excluded from this task.

**Verification performed**:
- `git status`: confirmed `.idea/.gitignore` is staged-then-deleted (`AD`) — a pre-existing, unrelated pending change, untouched by this task's scope. ✓
- Confirmed `.maister/tasks/product-design/2026-07-15-recruiter-scannable-profile/context/CV.md` and `context/assumptions.md` are staged/modified independently of `profile/README.md` — unrelated content from the upstream product-design task's context ingestion. ✓
- `git log --oneline draft` vs `git log --oneline origin/draft`: confirmed local `draft` has a commit (`2383c03`, docs/standards init — does **not** touch `profile/README.md`) not on `origin/draft`; `origin/draft` has a commit (`af216ef`, "Initial README.md for AiB Projekt site") not in local history, which added the exact 12-line GitHub boilerplate now sitting in the local index. This precisely matches the Phase 1 clarification's Q1 answer ("origin has the original 12-line GitHub boilerplate from commit `af216ef`, not in local history"). ✓
- Confirmed the root `README.md` (untouched, 9 bytes) has no pending changes and is not a factor. ✓

**Result**: **Confirmed accurate and safely drawn.** All four excluded items are genuinely unrelated to this content-only task, and the branch-divergence framing is independently corroborated by `git log`, not just asserted.

**Category**: N/A (verified correct) | **Severity**: N/A

---

## 4. Single-File Markdown Replacement — Additional Risk Scan

Beyond M-1/M-2/L-1 above:

- **Character encoding**: Since the spec's copy and the source are byte-identical (MD5-confirmed), there is no encoding divergence to worry about *in the spec text itself*. The remaining risk is purely at execution time — whoever writes the new file must copy from `feature-spec.md` (or the verified-identical spec.md block) via a method that doesn't re-encode/normalize Unicode (e.g., avoid retyping emoji manually). The spec already anticipates this: "Copy from `feature-spec.md` directly (do not retype from this spec) to eliminate a second transcription hop." This is a sound mitigation. No further gap found.
- **Git staging instructions**: Concrete enough ("stage only `profile/README.md`" = `git add profile/README.md`) aside from the M-1 ambiguity above.
- **HTML companion (`spec.html`) drift check**: Spot-checked that `spec.html` contains the same distinctive replacement-content strings ("Reactive, lock-free concurrency at scale", `cal.eu/bartek/meeting`) as `spec.md` — not stale/drifted.

---

## 5. Cross-Check Against Profile Standards Docs

- `standards/profile/markdown-authoring.md` — "Centered HTML Div Blocks" and "Shields.io Badges" patterns: **confirmed embodied** in the replacement content (intro/closing `<div align="center">` blocks present; all badges are shields.io images). No conflict.
- `standards/profile/markdown-authoring.md` — "Inline Placeholders for Incomplete Content": **not embodied**, by design (see Finding M-2). The spec's claim of full conformance is inaccurate on this one point, though the underlying design choice (zero placeholders) is correct and intentional per this same spec's success criteria.
- `standards/profile/structure.md` — "Demonstrates" callout, per-project entry shape, backtick+middot tech-tag formatting: **confirmed embodied** in both project entries of the replacement content. No conflict.
- Both standards docs will contain stale example quotes/line citations after this task lands (see Finding M-2) — not itself a spec defect, but an unaddressed side effect.

---

## Summary of Findings

| ID | Finding | Category | Severity |
|----|---------|----------|----------|
| — | Content fidelity (spec vs. feature-spec, byte-level) | Verified correct | N/A |
| — | Out-of-scope boundary (git status/log corroborated) | Verified correct | N/A |
| M-1 | Self-contradicting git-status acceptance criterion | Ambiguous | Medium |
| M-2 | "No standards conflicts" claim overstated; docs will go stale | Incorrect/Missing | Medium |
| L-1 | Trailing-newline handling deliberately unresolved | Ambiguous (acknowledged) | Low |
| L-2 | Root `README.md` inconsistently listed between two sections | Incomplete list | Low |
| L-3 | Bare filenames instead of full repo-relative paths for out-of-scope files | Ambiguous (in form) | Low |

**Totals**: 0 Critical, 0 High, 2 Medium, 3 Low (issues) — plus 2 areas independently verified as fully accurate.

## Compliance Status

**⚠️ Pass-with-concerns.** This spec is implementable as a direct find/replace today without any blocking clarification. The two Medium findings are worth a quick resolution before implementation sign-off (both are cheap fixes: reword one success-criteria bullet, soften one overstated claim / add a documentation follow-up note) but neither would produce an incorrect `profile/README.md` if an implementer proceeds as-is and uses judgment on the ambiguous phrasing. No Critical or High findings were identified — the content-fidelity claim (the highest-stakes claim in a transcription-only task) held up under independent byte-level verification, and the out-of-scope boundary held up under independent `git`/`git log` inspection.

## Recommendations

1. Reword Success Criteria bullet 5 / Testing Approach Group 1(c) to disambiguate "only `profile/README.md` staged" (Finding M-1).
2. Soften or caveat the "no standards conflicts" claim, and consider adding a one-line follow-up note to re-run standards discovery on the profile docs after this task merges (Finding M-2).
3. No action strictly required for L-1/L-2/L-3 — cosmetic/precision nits, safe to proceed as-is.
