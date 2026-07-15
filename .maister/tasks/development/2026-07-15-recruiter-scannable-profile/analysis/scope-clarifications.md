# Phase 2 Scope Clarifications

## TL;DR
User confirmed: verify reachable links (badge images, calendar link, skill-flip live demo) during this task's verification phase; defer only the GitHub-native rendering check to after `draft`→`main` merge (which structurally can't be checked before merge anyway). No critical scope decisions — proceeding to Phase 5.

## Key Decisions
- Link/badge reachability checks run during this task's implementation-verification step (Phase 11), not deferred entirely.
- The GitHub-rendered visual check remains a manual post-merge step, since it requires the merge to have happened.

## Open Questions / Risks
None outstanding for this phase.

---

## Q&A

**Q1 — Verification timing**: When should the unverified calendar link and skill-flip live-demo link be checked?
**A**: Check reachable links now (during this task); defer only the GitHub-render check to post-merge.

**Q2 — Routing**: Continue to Phase 5, skipping Phases 3 (no reproducible defect) and 4 (not UI-heavy)?
**A**: Yes, continue to Phase 5.
