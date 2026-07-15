# Design Alternatives: Recruiter-Scannable Profile README

## TL;DR
Four open decision areas (contact placement, tech-stack section, "About this org", project order/density) each have 4 genuine alternatives below. Recommended combination: keep the top+bottom contact bookend (add the calendar link to both), repurpose the standalone tech-stack badges as an accurate cross-project ("backend + frontend") signal moved higher on the page, replace "About this org" with one honest hook sentence, and keep `coupon-service` first while compressing both projects' "Demonstrates" lines into the same punchy-lead-plus-detail shape. None of these are locked — Phase 4/5 convergence should confirm or override each independently.

## Key Decisions
- Lean: keep contact bookend (Alternative 1A), not consolidate — matches the user's own stated preference in `assumptions.md` ("recruiters who scroll to the bottom look for it there too").
- Lean: repurpose tech-stack badges rather than cut (Alternative 2B) — cutting would contradict the stated "recruiters scan badges before text" preference; keeping as-is would misrepresent skill-flip's real (non-Java) stack once filled in.
- Lean: replace "About this org" with a single honest sentence (Alternative 3B) — directly matches `assumptions.md` point 4's own phrasing ("one honest sentence").
- Lean: keep `coupon-service` first, compress both entries to the same punchy-lead format (Alternative 4B) — avoids the framing mismatch of leading with skill-flip against a "Backend Architecture" headline, while fixing the scan-speed problem the codebase analysis flagged.

## Open Questions / Risks
- Contact bookend (1A) keeps some redundancy by design — if the user has grown to dislike repetition more than `assumptions.md` originally implied, Alternative 1D (asymmetric: full badges top, single calendar nudge bottom) is the fallback.
- Repositioning the tech-stack badges higher (2B) changes page flow more than a pure content edit — confirm this is acceptable "restructuring latitude" given the low-confidence profile standards, or fall back to 2A (cut) if any structural change is unwanted.
- Compressing `coupon-service`'s five-item Demonstrates line (4B) risks losing specific keywords (`WebFlux`, `Testcontainers`, `R2DBC`) that `assumptions.md` explicitly wants recruiters to see — the compressed lead phrase must still surface the secondary detail clause, not replace it.
- None of the four areas are independent of each other — e.g., if "About this org" is cut to a bare hook line (3B), the honest recruitment-exercise framing has nowhere else to live except per-project; convergence should treat these as one coherent page decision, not four isolated toggles.

---

## Context Recap

The following are **fixed constraints**, not open for re-litigation in this document (per `problem-statement.md`):
- Intro leads with CV-aligned seniority framing: "Senior Software Engineer | Backend Architecture / Distributed Systems"
- Contact channels are LinkedIn + email + calendar (`https://www.cal.eu/bartek/meeting`) — the calendar link is new, not currently on the page
- Intro stays purely descriptive, no "open to work" language
- Only two real projects exist (`coupon-service`, `skill-flip`); both must be honestly framed as recruitment-exercise/portfolio pieces
- Plain GFM only, English-only, landing-page length, must render via GitHub's org-profile auto-render

This document explores **how** to resolve the four decision areas the problem statement explicitly left open (see `problem-statement.md` § Open Questions / Risks and the task brief's "Open decision areas"). It does not touch the fixed constraints above.

## How Might We Questions

1. **HMW** make three contact channels easy to find without the page feeling repetitive?
2. **HMW** keep an accurate, at-a-glance tech-stack signal without duplicating what's already in each project's tag line — especially now that skill-flip's real (non-Java) stack is being added?
3. **HMW** replace internal meta-commentary ("this page is just the index") with something that is both an honest recruitment-exercise disclosure *and* a scan-hook?
4. **HMW** order and phrase two project entries so the "Backend Architecture / Distributed Systems" headline and the genuine skill-breadth story (backend + frontend/testing/CI-CD) both land inside a 15-second scan?

---

## Decision Area 1: Contact Placement & Redundancy

**Current state**: top intro block has LinkedIn + Email as shields.io badges; bottom closing block repeats the same two destinations as plain-text links. The calendar link exists nowhere yet and must be added per the fixed constraints.

### Alternative 1A: Keep the bookend, add calendar to both
Keep contact in both the top badge row and the bottom closing block, adding the calendar link to each so all three channels appear twice.

- **Strengths**: Matches the user's own stated brief almost verbatim (`assumptions.md` point 5: "contact repeated at the end — recruiters who scroll to the bottom look for it there too"); zero risk of a recruiter who only reads the bottom missing a channel; minimal structural change.
- **Weaknesses**: Three channels × two locations is more visual weight than two channels × two locations currently; if the page is genuinely 15-seconds short, is a full second contact block earning its space, or just eating scroll?
- **Best when**: The 15-second reader model assumes recruiters skim top-to-bottom and often stop reading at the first project that interests them, then jump straight to the bottom for a CTA — i.e., bottom-of-page contact is a distinct conversion moment, not pure duplication.
- **Evidence**: `design-context.md` § 3 (`assumptions.md` point 5, directly authored by the user); `codebase-analysis.md` "Concerns" flags the *duplication* but does not conclude it's wrong — only that it's a deliberate choice to confirm.

### Alternative 1B: Consolidate to a single top block
Keep the three-channel badge row in the intro only; remove the bottom closing block entirely.

- **Strengths**: Removes 100% of contact duplication; shortens total scroll length, which directly serves the 15-second goal; a single source of truth means one place to update if a channel ever changes.
- **Weaknesses**: Directly contradicts the user's own stated preference in `assumptions.md`; a recruiter who scans projects first and stops scrolling near the bottom has to scroll back up to act — added friction at exactly the moment of highest interest (post-projects, ready to reach out).
- **Best when**: The page is short enough (it is — ~50 lines) that scrolling back up costs under a second, and the team prioritizes minimal redundancy over redundant-but-convenient CTAs.
- **Evidence**: `codebase-analysis.md` "Recommendations" #4 flags contact duplication as a redundancy to "decide deliberately on," listing consolidation as the leaner option if no distinct scanning value is found.

### Alternative 1C: Consolidate to a single bottom block
Move all contact off the intro (keep only name + role there); put the full three-channel CTA once, right after the projects, positioned as the page's single conversion moment.

- **Strengths**: Intro reads as pure identity/positioning with nothing competing with the seniority headline for attention; contact appears exactly when a convinced recruiter is ready to act (immediately after seeing the evidence).
- **Weaknesses**: A meaningful share of recruiters want the contact link *immediately* and never read past the intro — removing it from the top adds friction for that segment; also a structural change bigger than the other options, since it strips an established element (intro badges) rather than trimming a duplicate.
- **Best when**: Evidence strongly suggests recruiters read the whole page before acting rather than clicking through opportunistically — not clearly true here, since the whole premise of a "15-second scan" is that some readers act fast without reading everything.
- **Evidence**: Contradicts `assumptions.md` point 1, which explicitly wants intro-level contact ("link to CV/LinkedIn/email so the recruiter can immediately move on") — included here as a genuine alternative, not because evidence favors it.

### Alternative 1D: Asymmetric bookend — full row top, single nudge bottom
Keep the full three-badge row in the intro as the primary CTA; replace the bottom block with a single, distinct line (e.g., just the calendar link as a "ready to talk? book a slot" nudge) rather than repeating all three.

- **Strengths**: Preserves a bottom-of-page CTA (satisfying the "recruiters who scroll to the bottom" concern) while cutting two-thirds of the literal duplication; differentiates the bottom block's *purpose* (book a call) from the top block's purpose (multiple ways to reach out) instead of just repeating.
- **Weaknesses**: A recruiter who specifically wants LinkedIn or email at the bottom (not a scheduling link) won't find it there — asymmetry could read as inconsistent rather than intentional if not labeled well.
- **Best when**: The team wants to reduce redundancy but still believes in a distinct closing conversion moment — a middle ground between 1A and 1B.
- **Evidence**: Synthesizes `assumptions.md` point 5 (bottom CTA wanted) with `codebase-analysis.md`'s redundancy concern — no direct evidence for this specific split, it's a reasoned compromise.

### Trade-Off Matrix — Decision Area 1

| | 1A: Full bookend | 1B: Top only | 1C: Bottom only | 1D: Asymmetric bookend |
|---|---|---|---|---|
| Technical feasibility | Trivial — pure copy edit | Trivial | Trivial, but moves intro structure | Trivial |
| User impact | High — CTA available at both natural stopping points | Medium — fast readers served, scroll-back cost for others | Medium — post-evidence CTA strong, but early-exit readers lose it | High — CTA at both points, less repetitive |
| Simplicity | One extra duplicated block | Simplest — single source of truth | Simple, but reshapes intro | Slightly more design nuance (two different formats) |
| Risk | Low — matches stated preference, fully reversible | Low technically, but risks contradicting explicit user brief | Medium — bigger structural change, could underdeliver on top-of-page CTA | Low — reversible, but relies on the nudge being noticed |
| Scalability | Fine if a 4th channel is ever added (list just grows) | Best if channel list grows (only one place to edit) | Fine | Slightly awkward if more than one "distinct" bottom CTA is wanted later |

**Lean**: 1A (keep the bookend, add calendar to both) — most directly evidenced by the user's own brief, lowest risk of contradicting a stated preference, and the added redundancy cost is small (one more link) since the page is already very short.

**Why not the others**: 1B saves scroll length but directly overrides a preference the user already wrote down themselves — not clearly a problem this task was asked to solve. 1C is the most structurally invasive option for a benefit (post-evidence conversion) that 1D achieves with far less change. 1D is a reasonable fallback if the user decides three-times-two redundancy feels like too much once they see it rendered.

---

## Decision Area 2: Standalone "Tech Stack" Section

**Current state**: five badges (Java, Spring, PostgreSQL, Docker, Maven) — all backend/Java, all already present in `coupon-service`'s own tag line. Once `skill-flip` is filled in with its real stack (Vite, TypeScript, Vitest, GitHub Actions), this section will not just duplicate — it will actively misrepresent the org as Java-only.

### Alternative 2A: Cut entirely
Remove the "Tech stack" section; rely solely on each project's own tech-tag line.

- **Strengths**: Removes 100% of the duplication the codebase analysis flagged; forces the page to stay accurate by construction (nothing to fall out of sync); shortens the scroll.
- **Weaknesses**: Loses the "scan badges before reading text" affordance the user explicitly asked for in `assumptions.md` point 3; a recruiter who wants a single-glance stack overview before committing to read two project descriptions has to open both entries to piece it together.
- **Best when**: Per-project tags are judged sufficient on their own and an aggregate view is considered pure redundancy rather than a distinct scanning aid.
- **Evidence**: `codebase-analysis.md` "Recommendations" #4 explicitly floats cutting the tech-stack section if it "adds distinct scanning value" fails the test — which it currently does, being 100% Java/Spring overlap with `coupon-service`.

### Alternative 2B: Repurpose as an accurate cross-project badge row, moved higher
Keep a standalone badge row, but make it a genuine aggregate — include both the backend stack (Java, Spring, PostgreSQL) and the frontend/tooling stack (TypeScript, Vite, GitHub Actions) — and move it up near the intro so it functions as a pre-read "range" signal rather than a post-read recap.

- **Strengths**: Preserves the "badge scanner" affordance from `assumptions.md`; actually adds new information versus either project's tag line alone (backend *and* frontend breadth is a genuine selling point neither entry states on its own); positioned before the projects, it primes the reader rather than repeating what they just read.
- **Weaknesses**: Two places to keep in sync if either project's stack changes later; repositioning is a bigger structural change than a same-spot content edit; doesn't fully test as "different information" once a reader reaches the second project anyway.
- **Best when**: The two projects' stacks are different enough (they are — backend/reactive vs. frontend/vanilla-TS) that an aggregate view is genuinely new signal, not just a repeat.
- **Evidence**: `design-context.md` § 4 explicitly notes the two projects "cover a wider skill spread than the current half-finished page conveys" — this alternative is the direct structural answer to that cross-reference insight.

### Alternative 2C: Reframe as grouped "skills breadth" categories
Keep a dedicated section, but organize by category (Backend / Frontend / DevOps) rather than a flat badge row, to make the breadth argument explicit rather than implicit in a badge list.

- **Strengths**: Makes the "range across two different stacks" argument unmissable rather than requiring the reader to notice it themselves; still badge-based, so visually consistent with existing conventions.
- **Weaknesses**: More design effort than the task's `is_simple` classification calls for; a 50-line landing page arguably doesn't need a categorized taxonomy for five to eight badges — risk of over-engineering a section that's meant to be scanned in under two seconds.
- **Best when**: The stack list is long or varied enough that an unsorted row would be genuinely hard to parse — not really the case here with roughly 8 total badges.
- **Evidence**: No direct evidence calls for this; flagged here as a legitimate but likely disproportionate option given `codebase-analysis.md`'s "Overall: Simple" complexity rating.

### Alternative 2D: Fold into the intro as a one-line rollup, no dedicated section
Remove the "Tech stack" heading and badge block; add a single descriptive clause to the intro (e.g., referencing both backend and frontend work in one sentence) instead of a separate visual section.

- **Strengths**: Delivers the aggregate-range signal at the point of maximum attention (the first 3 seconds) rather than the bottom of the page where attention has already dropped off; removes an entire section's worth of scroll.
- **Weaknesses**: Makes the intro block denser and puts it in competition with the seniority-framing headline for the reader's very first glance; loses the badge-scanning visual format `assumptions.md` specifically asked for ("recruiters sometimes scan badges before reading text").
- **Best when**: The intro has room to spare and the team is comfortable trading "badges recruiters scan visually" for "one more descriptive clause recruiters read."
- **Evidence**: Partially satisfies `assumptions.md` point 3 (aggregate signal) but abandons its specific *format* request (badges) — a genuine alternative, not a strawman, but a weaker fit to the literal brief than 2B.

### Trade-Off Matrix — Decision Area 2

| | 2A: Cut | 2B: Repurpose + reposition | 2C: Grouped categories | 2D: Fold into intro |
|---|---|---|---|---|
| Technical feasibility | Trivial | Trivial (copy + reorder) | Low-medium — more layout decisions | Trivial |
| User impact | Medium — loses badge-scan aid | High — adds real new signal at the right moment | Medium-high, but diminishing returns for 8 badges | Medium — signal moves to text, not badges |
| Simplicity | Highest — nothing to maintain twice | Medium — two places to keep in sync | Lowest — most structure for the content volume | High — no separate section at all |
| Risk | Low | Low-medium (position change) | Medium — disproportionate effort for `is_simple` task | Low, but risks diluting the seniority headline |
| Scalability | Degrades gracefully if a 3rd project appears (still just per-project tags) | Needs one more update if a 3rd stack is added, but pattern holds | Scales best if stack list grows a lot (unlikely here) | Gets unwieldy if more than one extra clause is ever needed |

**Lean**: 2B (repurpose as an accurate cross-project badge row, moved higher) — resolves the accuracy problem (current badges would misrepresent skill-flip's real stack), honors the explicit "badge scanning" preference, and turns a former duplication liability into new signal about range.

**Why not the others**: 2A is the safest simplification but forfeits a preference the user explicitly stated. 2C solves a scale problem (many badges, hard to parse) the page doesn't actually have — over-engineered for `is_simple`. 2D achieves a similar goal to 2B but sacrifices the specific badge format the brief asked for and crowds the highest-value real estate on the page (the intro).

---

## Decision Area 3: "About this org" Section

**Current state**: one paragraph of meta-commentary — "A small collection of self-contained projects I've built to demonstrate specific engineering skills... this page is just the index." Both the user's own brief and the independent codebase analysis flag this as the biggest single scan-speed loss after the `skill-flip` placeholder.

### Alternative 3A: Cut entirely
Remove the section and its heading; go directly from the intro to "Projects."

- **Strengths**: Maximizes scan speed — removes an entire section that both source documents agree adds no recruiter value today; simplest possible edit.
- **Weaknesses**: Removes the *only* place on the page that currently states (even poorly) that these are personal/demonstration projects rather than production work — without a replacement, the "honest recruitment-exercise framing" constraint has no home anywhere on the page.
- **Best when**: The per-project entries themselves are judged sufficient to convey "these are demonstration projects" (e.g., if each project's own README already states this, which `coupon-service`'s does) — but the *profile page itself* would then carry no such framing, which is a gap against the stated constraint.
- **Evidence**: `codebase-analysis.md` Recommendations #2 says "cut or radically shorten" — cutting entirely is the extreme end of that same recommendation, not a strawman.

### Alternative 3B: Replace with one honest hook sentence
Replace the paragraph with a single sentence that both discloses the recruitment-exercise/portfolio framing and functions as a bridge into the projects (e.g., pitching *how* the two projects show real working style, not just *that* they exist).

- **Strengths**: Matches `assumptions.md` point 4's own phrasing almost exactly ("one honest sentence noting these are sample/recruitment-exercise projects"); keeps the disclosure in one clear, central place rather than scattering it; still functions as a transition rather than a dead stop.
- **Weaknesses**: Still costs a couple of seconds of the 15-second budget versus cutting outright; quality of the single sentence matters a lot — a weak version would recreate the current problem in miniature.
- **Best when**: The team wants the honesty disclosure to have one authoritative home rather than being implied per-project or left off the page entirely.
- **Evidence**: Directly implements `assumptions.md` point 4 and `codebase-analysis.md` Recommendation #2's "shorten" branch; also satisfies `vision.md`'s existing differentiator of transparent, skills-first framing (per `design-context.md` § 1).

### Alternative 3C: Cut the section, push the disclosure to per-project tags
Remove the "About this org" heading/paragraph entirely; instead, add a small honest tag next to each project title (e.g., a parenthetical "(recruitment exercise)" or similar) so the disclosure sits exactly where the claim needs qualifying.

- **Strengths**: Removes the whole section-level scroll-stop while keeping the honesty requirement scoped precisely to where a reader might otherwise assume "production work" — right next to the project itself.
- **Weaknesses**: A caveat sitting directly beside the strongest content on the page risks undercutting confidence at exactly the wrong moment — reads more like a disclaimer/apology than the confident single-sentence framing `assumptions.md` asked for; also duplicates the same small phrase twice (once per project) rather than stating it once.
- **Best when**: The team wants zero standalone "meta" text anywhere on the page and is comfortable with a lighter per-entry caveat instead.
- **Evidence**: No direct evidence recommends this specific placement; included as a genuine structural alternative to 3B, weighed against the risk that `structure.md`'s documented per-project shape (H3 → description → Demonstrates → tags) has no natural slot for a caveat without disrupting that shape.

### Alternative 3D: Fold into a lead-in line above "Projects," no dedicated heading
Keep a one-line honest/hook sentence (similar content to 3B) but remove the `## About this org` heading entirely — the sentence becomes an unheaded transition line directly above `## Projects`, not its own titled section.

- **Strengths**: Removes a whole heading level and the sense of "another section to get through," while still preserving the honesty disclosure content; cheapest structural edit that still keeps the sentence.
- **Weaknesses**: Without a heading, the line may read as a stray, less-intentional sentence rather than a deliberate framing statement; slightly unusual visually compared to the rest of the page's heading-driven structure.
- **Best when**: The team wants every possible unit of scroll-friction removed but isn't ready to drop the honesty sentence altogether (i.e., a compromise between 3A and 3B).
- **Evidence**: Synthesizes `codebase-analysis.md`'s "radically shorten" language with `assumptions.md`'s one-sentence request — no direct evidence for dropping the heading specifically, a reasoned compromise.

### Trade-Off Matrix — Decision Area 3

| | 3A: Cut entirely | 3B: One hook sentence | 3C: Per-project caveat | 3D: Unheaded lead-in line |
|---|---|---|---|---|
| Technical feasibility | Trivial | Trivial | Trivial, but touches two entries instead of one | Trivial |
| User impact | Highest scan speed, but no honesty framing anywhere | High — fast and still transparent | Medium — honesty present but placed awkwardly | High — fast and still transparent |
| Simplicity | Simplest | Simple — one sentence, one place | Adds a repeated micro-pattern across entries | Simple, slightly unusual (no heading) |
| Risk | Risks violating the "honest framing" constraint | Low — directly matches stated brief | Medium — caveat next to strongest content could undercut it | Low-medium — sentence may look unintentional without a heading |
| Scalability | Fine | Fine if a 3rd project is added later (framing stays general) | Must repeat the caveat for every future project | Fine |

**Lean**: 3B (replace with one honest hook sentence, keep it as its own small section) — this is close to a direct implementation of the user's own brief and resolves both source documents' top concern without introducing the placement risk of 3C or the "no honesty framing at all" gap of 3A.

**Why not the others**: 3A goes further than the brief asked and leaves the recruitment-exercise disclosure with no home on the profile page itself (each project's own README carries it, but the constraint is about the page). 3C scopes the honesty claim well but risks reading as an apology beside the two entries that are supposed to be selling points. 3D is a reasonable fallback if, after seeing 3B rendered, the heading still feels like unnecessary ceremony for one sentence.

---

## Decision Area 4: Project Entry Order & Density

**Current state**: `coupon-service` first (complete, dense five-item comma-separated "Demonstrates" line), `skill-flip` second (placeholder). Real `skill-flip` content is now available: live demo, Vite/TypeScript/Vitest/GitHub Actions stack, weighted-review algorithm, bilingual content, AI-assisted content pipeline with human review.

### Alternative 4A: Keep order, keep current dense style for both
Leave `coupon-service` first; write `skill-flip`'s real content in the same dense, five-or-so-item comma-list style `coupon-service` currently uses.

- **Strengths**: Minimal change — only fills the gap, doesn't touch anything else; both entries end up structurally identical (same shape, same density), which best matches the documented "consistent per-project entry shape" convention.
- **Weaknesses**: Keeps the exact verbosity the codebase analysis flagged as a scan-speed problem ("dense 5-item list... a second look at the same facts rather than new signal" in spirit, though stated re: tech stack — the same critique applies to a long comma list); doesn't address the density/scan-speed half of the open question at all.
- **Best when**: Consistency of shape is valued over compression, and the current density hasn't actually been shown to slow scanning enough to matter.
- **Evidence**: `codebase-analysis.md` Recommendation #3 explicitly suggests tightening the dense list rather than keeping it as-is — this alternative is included as the "don't fix what might not be broken" baseline, not because evidence favors it.

### Alternative 4B: Keep order, compress both entries into a punchy-lead + detail shape
Leave `coupon-service` first; rewrite both "Demonstrates" lines as a short bolded lead phrase (3-6 words capturing the headline skill) followed by the existing detailed comma list as secondary, scannable-but-skippable detail.

- **Strengths**: Directly implements `codebase-analysis.md` Recommendation #3; gives a fast reader a one-glance takeaway per project while preserving every specific "selling" keyword (`WebFlux`, `Testcontainers`, `Vitest`, `GitHub Actions`) that `assumptions.md` wants visible for CV-scanning; applied uniformly, neither entry looks more "finished" than the other.
- **Weaknesses**: Requires careful compression — a lead phrase that's too vague ("solid engineering practices") would lose the specificity that makes "Demonstrates" lines credible in the first place; some editorial judgment risk.
- **Best when**: The goal is genuinely faster scanning without losing the CV-keyword detail underneath — i.e., serving both the 3-second skimmer and the 15-second reader.
- **Evidence**: `codebase-analysis.md` Recommendation #3 (verbatim: "tightening... into a punchier lead phrase, keeping depth as secondary/scannable detail"); `assumptions.md` point 2 (concrete "selling" phrases a CV-scanner looks for) confirms the detail must survive compression, not disappear.

### Alternative 4C: Reorder — lead with skill-flip because it has a live demo
Put `skill-flip` first, since it has a clickable live demo (`aib-projekt.github.io/skill-flip`) — a working link a recruiter can immediately click is a stronger first-glance hook than code-only description, even though `coupon-service` is architecturally deeper.

- **Strengths**: Front-loads the one piece of content on the page a recruiter can actually *interact with* rather than just read; directly implements `assumptions.md` point 8's spirit ("a working link is stronger than code alone") by putting that link first, not second.
- **Weaknesses**: Creates a framing mismatch — the intro headline is "Senior Software Engineer | Backend Architecture / Distributed Systems," and the very first proof point a reader sees would then be a solo frontend flashcard app, not the backend/concurrency project that actually matches that headline; risks undercutting the seniority framing right after establishing it.
- **Best when**: The team is confident recruiters value interactivity over architectural depth as a first impression, or the seniority framing is expected to carry itself regardless of which project appears first.
- **Evidence**: `assumptions.md` point 8 supports demo-first thinking in the abstract, but nothing in the research suggests it should override project *order* specifically — the codebase analysis's own Recommendation #5 explicitly says to lead with `coupon-service` "as the strongest, most complete entry." This alternative directly contradicts that recommendation, included here for genuine exploration, not because evidence favors it.

### Alternative 4D: Keep order, deliberately asymmetric density (coupon-service full, skill-flip lean)
Leave `coupon-service` first with its fuller original density (flagship entry, matching the "Backend Architecture" headline); write `skill-flip`'s "Demonstrates" line intentionally shorter (2-3 items: vanilla front-end fundamentals, automated testing, CI/CD) rather than matching `coupon-service`'s length.

- **Strengths**: Reflects the projects' actual relative scope honestly — `coupon-service` genuinely engages more senior-level concerns (concurrency, reactive architecture, coverage gates) while `skill-flip` is real but simpler in scope; avoids inflating skill-flip to match a length it doesn't substantively need.
- **Weaknesses**: Risks reading as "the lesser project" rather than genuine breadth — the whole point of including skill-flip is to demonstrate range (frontend + testing + CI/CD) as a complement to the backend story, and a visibly shorter entry could look like padding instead; also breaks the documented "consistent per-project entry shape" convention (even though that convention is low-confidence and open to revision).
- **Best when**: The team wants to be scrupulously honest about relative depth rather than presenting both projects as equally weighty, and is comfortable with visibly asymmetric treatment.
- **Evidence**: `design-context.md` § 4 frames skill-flip as complementary breadth, not a co-equal flagship — this alternative takes that framing literally into visual asymmetry; but `structure.md`'s "consistent shape" observation (even if low-confidence) cuts against it.

### Trade-Off Matrix — Decision Area 4

| | 4A: Keep order, keep dense style | 4B: Keep order, compress both uniformly | 4C: Reorder, skill-flip first | 4D: Keep order, asymmetric density |
|---|---|---|---|---|
| Technical feasibility | Trivial | Low-medium — needs careful editorial compression | Trivial to reorder | Trivial |
| User impact | Medium — accurate but slower to scan | High — fast lead-in, full detail preserved underneath | Medium — demo-first hook, but framing mismatch risk | Medium — honest, but skill-flip may read as minor |
| Simplicity | Simplest edit | Medium editorial effort, structurally simple | Simple reorder, no density change needed | Simple, but breaks the shared entry-shape convention |
| Risk | Low technically; misses the stated scan-speed goal | Low — directly matches the codebase analysis's own recommendation | Medium — undercuts the seniority headline just established | Medium — could look like padding/demotion |
| Scalability | Fine if a 3rd project is added later | Pattern (lead + detail) extends cleanly to future entries | Fine, but same mismatch risk would recur with any future non-backend project led first | Asymmetric pattern gets harder to justify with a 3rd project |

**Lean**: 4B (keep `coupon-service` first, compress both entries into a punchy-lead + detail shape) — best resolves the actual open question (scan speed vs. depth) without introducing the framing risk of 4C or the demotion risk of 4D, and is the only option directly evidenced by the codebase analysis's own recommendation.

**Why not the others**: 4A is the status quo shape and leaves the density problem unsolved. 4C is the most interesting contrarian option (demo-first) but creates a direct tension with the seniority framing the intro was just changed to establish — a real risk, not a minor one, given the whole page now opens by asserting "Backend Architecture / Distributed Systems." 4D is honest about relative depth but risks making skill-flip look like a lesser afterthought rather than genuine range, which undercuts the very reason it's being included in full.

---

## Recommended Combination (if all four leans are accepted)

Read top to bottom, the recommended page shape would be:

1. Intro — CV-aligned seniority headline (fixed, not in scope here) + full three-channel badge row (LinkedIn, Email, Calendar) — per 1A.
2. Repositioned, accurate cross-project tech-stack badge row (backend + frontend combined) — per 2B — functioning as a pre-read range signal.
3. One honest hook sentence replacing "About this org" — per 3B.
4. Projects: `coupon-service` first, `skill-flip` second, both with a bolded punchy lead phrase + secondary detail clause — per 4B.
5. Closing block — full three-channel repeat — per 1A.

This is a **starting direction for convergence**, not a final decision — each area above can be independently accepted, rejected, or swapped for one of its alternatives without invalidating the others, except where noted (e.g., 3A would remove the only home for the honesty disclosure that 1-4 assume exists somewhere).

## Deferred Ideas

- **Standards update**: once the page's structure is finalized, `.maister/docs/standards/profile/markdown-authoring.md` and `structure.md` (both currently low-confidence, 2-entry-sample) could be refreshed to reflect the new shape — out of scope for this design task, a natural follow-up per CLAUDE.md's "Standards Evolution" note.
- **Visual/media additions** (profile photo, project screenshots, embedded GIFs of the skill-flip demo): not requested by any source document and would add asset-management overhead to a currently zero-asset, pure-Markdown repo — out of scope.
- **GitHub stats/contribution badges** (commit graphs, language-usage badges, etc.): a common profile-page pattern generally, but not mentioned in `assumptions.md`, the CV, or the problem statement — flagged as a stretch idea only, not incorporated into any alternative above.
- **Bilingual (EN/PL) profile content**: explicitly ruled out by the problem statement's English-only constraint (recruiters are UK-based) — noted only because `skill-flip` itself is bilingual; that bilingual nature is a "Demonstrates" talking point, not a reason to bilingual-ize the profile page itself.

## Assumptions Underlying These Recommendations

- `assumptions.md`'s stated preferences (bottom contact repeat, badge scanning, one honest sentence) are still the user's actual current preferences as of this task, not stale notes from an earlier draft.
- The two projects' relative technical depth (backend/concurrency vs. frontend/testing/CI-CD) is accurately captured in `design-context.md` § 3 — if `skill-flip` is judged more architecturally significant than currently described, Alternative 4C (demo-first reorder) becomes more attractive.
- GitHub's org-profile renderer treats a repositioned/reworded page identically to the current one (no rendering quirks tied to section order) — reasonable given `tech-stack.md`'s confirmation of plain GFM with no build step, but worth a quick visual check after implementation regardless.

## Confidence

**Medium-high.** All four leans are directly evidenced by either the user's own `assumptions.md` brief or the independent codebase analysis's recommendations, and the two sources converge rather than conflict (per `design-context.md` § 4). The main residual uncertainty is editorial quality of execution (Alternative 3B's "one sentence" and 4B's "punchy lead phrase" both depend on how well they're actually written, not just the structural choice) — that risk sits with the specification/implementation phase, not this exploration.
