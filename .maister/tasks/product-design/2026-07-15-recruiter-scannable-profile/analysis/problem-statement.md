# Problem Statement — Recruiter-Scannable Profile README

## TL;DR
`profile/README.md` reads as internal documentation, not a recruiter pitch. It undersells Bartek's seniority, has one incomplete project entry, and carries redundant content that slows a fast scan. Redesign target: a UK-recruiter-facing page that communicates who/what/how-to-contact within ~15 seconds.

## Key Decisions
- Lead the intro with CV-aligned seniority framing ("Senior Software Engineer | Backend Architecture / Distributed Systems") — rationale: matches actual CV positioning and sets the right bar immediately, rather than undersells with the current "backend engineer" framing.
- Add the meetings-calendar link (`https://www.cal.eu/bartek/meeting`) alongside LinkedIn/email — rationale: low-friction path straight to a booked slot, since inbound recruiter contact is the whole point of the page.
- Keep the intro purely descriptive, no "open to work" / job-search-status framing — rationale: avoids reading as less senior or dating quickly.

## Open Questions / Risks
- Whether to keep duplicate top/bottom contact blocks, and whether the standalone "Tech stack" badge section (redundant with per-project tags) should be trimmed or kept — deferred to alternatives/convergence (Phase 4/5), not decided here.

---

## Problem Statement

`profile/README.md` currently reads as an internal index/documentation page rather than a recruiter-facing pitch. It undersells Bartek's actual seniority, has one incomplete project entry (`skill-flip`), and carries redundant content (duplicate contact info, an overlapping standalone tech-stack section) that slows down a fast scan. UK-based recruiters landing on this page need to grasp *who he is*, *what he can concretely do*, and *how to reach him* — inside about 15 seconds.

## Constraints

- Stay plain GitHub-Flavored Markdown — no build step, no framework (core repo differentiator)
- English-only copy (inbound recruiters are predominantly UK-based)
- Only two real projects exist (`coupon-service`, `skill-flip`) — content must work within that, not invent more
- Both projects must be honestly framed as recruitment-exercise/portfolio pieces, not production company work
- Must render correctly via GitHub's native org-profile auto-render
- Landing-page length — technical depth stays in each project's own README

## Success Criteria

- A recruiter can determine, within ~15 seconds: who Bartek is (Senior Software Engineer, backend architecture/distributed systems — matching CV framing), what he demonstrably can do (via two concrete, skill-tagged project entries), and how to reach him
- Zero placeholder text — `skill-flip` fully filled in with its real content (live demo, real tech stack, genuine "Demonstrates" line)
- Contact channels are LinkedIn, email, and the calendar link (`https://www.cal.eu/bartek/meeting`) — easy to find without unnecessary redundancy
- Intro is purely descriptive (no "open to work" framing)
- Page renders cleanly on GitHub after `draft` → `main` merge

## Key Assumptions

- Only these two projects exist and will be featured — no fabricated content
- `skill-flip`'s recovered real content (demo + stack, see `analysis/design-context.md` § 3) supersedes the old placeholder
- Whether to keep duplicate top/bottom contact blocks and the standalone "Tech stack" section are open styling questions, deferred to the alternatives/convergence phase
