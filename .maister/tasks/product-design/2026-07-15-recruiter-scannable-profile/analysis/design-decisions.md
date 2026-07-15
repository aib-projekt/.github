# Design Decisions — Recruiter-Scannable Profile README

## TL;DR
All four open decision areas resolved to the brainstormer's recommended combination: full top+bottom contact bookend (with calendar added), tech-stack badges repurposed as an accurate cross-project row moved higher, "About this org" replaced with one honest hook sentence, and both project entries compressed to a punchy-lead + detail shape with `coupon-service` staying first. Full alternatives and trade-offs are in `analysis/alternatives.md`.

## Key Decisions
- **Contact placement (Alternative 1A)** — keep the full top+bottom bookend, add the calendar link to both. Rationale: matches the user's own `assumptions.md` brief almost verbatim; low risk, small added cost on an already-short page.
- **Tech-stack section (Alternative 2B)** — repurpose as an accurate cross-project (backend + frontend) badge row, moved higher near the intro. Rationale: current Java-only badges would misrepresent the org once skill-flip's real stack is added; repositioning turns a former duplication liability into a genuine "range" signal read before the projects.
- **"About this org" (Alternative 3B)** — replace with one honest hook sentence disclosing the recruitment-exercise/portfolio framing. Rationale: near-direct implementation of the user's own brief; keeps the honesty disclosure in one clear, central place rather than cutting it (which would leave the constraint with no home) or scattering it per-project (which reads as an apology).
- **Project order/density (Alternative 4B)** — keep `coupon-service` first; compress both "Demonstrates" lines into a short bolded lead phrase + full detail underneath. Rationale: directly resolves the codebase-analysis's scan-speed concern while preserving every specific keyword (`WebFlux`, `Testcontainers`, `Vitest`, `GitHub Actions`) the user's brief wants visible to a CV-scanner; reordering to lead with skill-flip (4C) was rejected because it would undercut the seniority headline just established in the intro.

## Open Questions / Risks
- Alternative 3B's "one honest hook sentence" and 4B's "punchy lead phrase" both depend on execution quality, not just the structural choice — that risk moves to the specification phase (Phase 6), where the actual wording gets drafted and reviewed.
- Repositioning the tech-stack badges (2B) is a real structural change (not just a content edit) — worth a quick visual check after implementation to confirm GitHub's renderer handles the reordered page as expected.

---

## Selected Approach

The redesigned page follows this shape, top to bottom:

1. **Intro** — CV-aligned seniority headline ("Senior Software Engineer | Backend Architecture / Distributed Systems") + full three-channel badge row (LinkedIn, Email, Calendar)
2. **Tech-stack badges** — repositioned near the top, now an accurate backend + frontend cross-project row (functions as a pre-read range signal)
3. **Hook sentence** — replaces "About this org," one sentence disclosing the honest recruitment-exercise framing while bridging into the projects
4. **Projects** — `coupon-service` first, `skill-flip` second (now with real recovered content: live demo, Vite/TypeScript/Vitest/GitHub Actions stack), both with a bolded punchy lead phrase followed by full keyword detail
5. **Closing block** — full three-channel contact repeat (LinkedIn, Email, Calendar)

## Alternatives Considered

Full detail with trade-off matrices in `analysis/alternatives.md`. Summary of paths not taken:
- **1B/1C** (consolidate contact to one location) — rejected: contradicts the user's explicit stated preference for a bottom-of-page repeat.
- **2A/2C/2D** (cut, categorize, or fold tech-stack into intro) — rejected: 2A loses the badge-scanning affordance the user asked for; 2C is disproportionate design effort for ~8 badges; 2D crowds the highest-value intro real estate.
- **3A/3C/3D** (cut, per-project caveat, or unheaded lead-in) — rejected: 3A leaves the honesty constraint with no home on the page; 3C risks reading as an apology beside the strongest content; 3D was a fallback, not preferred once 3B was on the table.
- **4A/4C/4D** (keep dense style, reorder to lead with demo, or asymmetric density) — rejected: 4A doesn't solve the scan-speed problem; 4C creates a framing mismatch against the seniority headline; 4D risks skill-flip reading as a demoted afterthought.

## Trade-offs Accepted

- Some contact-channel redundancy (three channels appearing twice) in exchange for guaranteed CTA visibility at both natural stopping points (post-intro skim, post-projects deep read).
- A structural repositioning of the tech-stack section (rather than a same-spot edit) in exchange for accuracy and a genuine breadth signal.
- A small amount of scan-time cost for the hook sentence (vs. cutting "About this org" outright) in exchange for keeping the page's only honesty disclosure intact.
