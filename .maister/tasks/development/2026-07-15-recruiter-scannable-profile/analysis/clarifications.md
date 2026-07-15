# Phase 1 Clarifications

## TL;DR
User confirmed: (1) proceed with the local content implementation now, handle the `draft`/`origin/draft` divergence over `profile/README.md` as a separate manual step later; (2) full verbatim overwrite of `profile/README.md` with the approved feature-spec.md content, touching no other files.

## Key Decisions
- Proceed with implementation now; branch divergence (local `draft` vs `origin/draft`, diverged specifically over `profile/README.md`) is deferred to a separate manual sync step — not blocking this task.
- Full overwrite of `profile/README.md`, not a merge/patch of the current stale draft. No other files (`.idea/.gitignore`, `CV.md`, `assumptions.md`) are touched, staged, or committed as part of this task.

## Open Questions / Risks
- resolved: branch divergence flagged to user, explicitly deferred rather than blocking

---

## Q&A

**Q1 — Branch divergence**: Local `draft` and `origin/draft` have diverged specifically over `profile/README.md` (origin has the original 12-line GitHub boilerplate from commit `af216ef`, not in local history). Editing now will likely produce a merge conflict later.
**A**: Proceed now; handle branch sync separately later.

**Q2 — Scope confirmation**: Confirm full overwrite of the stale working-tree draft with the approved `feature-spec.md` content, touching only `profile/README.md`.
**A**: Yes — full overwrite, touch only `profile/README.md`.
