# Design Context — Recruiter-Scannable Profile README

## TL;DR
`profile/README.md` (50 lines, the AiB org's public GitHub profile) needs to become a "15-second recruiter business card" — the user already wrote this brief themselves in `assumptions.md`. Three concrete gaps block it today: `skill-flip`'s "Demonstrates" line is an unfilled placeholder (real content now recovered from the actual project — live demo + real tech stack), "About this org" reads as internal meta-commentary instead of a hook, and the page's role framing ("Java / Spring Boot backend engineer") undersells the CV's actual seniority (Senior Software Engineer, distributed systems, technical leadership). Documented profile-authoring conventions are low-confidence (≤50/100) and explicitly open to revision.

## Open Questions / Risks
- CV shows "Senior Software Engineer" with technical-leadership scope (migrations, architecture decisions, mentoring-adjacent work); current README says "backend engineer" — worth confirming with the user which framing/seniority level they want to lead with (Phase 2).
- CV lists a "meetings calendar" contact link not present in the current README — confirm whether to include it.
- `assumptions.md` asks for English-only copy since inbound recruiters are UK-based — current README is already English, so this is a constraint to preserve, not a gap.
- Two CV employment entries appear to overlap in dates (HRS 2018–2026 vs SeaChange 2021–2023) — not this task's concern (CV content, not the README), flagging only in case it's relevant to how confidently to phrase timeline-dependent claims.

---

## 1. Project Documentation (`.maister/docs/project/`)

**Vision** (`vision.md`): Org profile page helping recruiters, clients, and collaborators quickly understand Bartek's engineering work. Target users: recruiters/hiring managers, potential clients, Bartek himself. Success criteria: no placeholder text, every project accurately described, renders cleanly after `draft`→`main` merge. Differentiators: framework-agnostic Markdown, skills-first "Demonstrates" sections.

**Tech stack** (`tech-stack.md`): Confirms documentation-only repo — 100% GitHub-Flavored Markdown, no build step, shields.io the only dependency, GitHub's native org-profile rendering as hosting, Git `draft`→`main` workflow.

Neither doc currently encodes a "scannability in N seconds" requirement — that's the new lens this task introduces on top of the existing vision, not a contradiction of it.

## 2. Codebase/Content Analysis (`analysis/codebase-analysis.md`, via codebase-analyzer)

Full current structure of `profile/README.md`:
1. Centered intro block (H1 + role line + LinkedIn/Email badges)
2. "About this org" — one paragraph, reads as meta-commentary ("this page is just the index")
3. "Projects" — `coupon-service` (complete, strong) and `skill-flip` (placeholder "Demonstrates" + tech-tag line)
4. "Tech stack" — standalone badge row, largely duplicates per-project tags
5. Centered closing contact block (plain-text links, same destinations as intro badges)

Documented profile standards (`standards/profile/markdown-authoring.md`, `structure.md`) — centered divs, shields.io badges, "Demonstrates" callout, per-project entry shape, tech-tag formatting — are all explicitly low-confidence (≤50/100, 2-entry sample) and invite revision. No binding constraint blocks a restructure.

Assessed to preserve: centered blocks, badges, the "Demonstrates" callout *concept*, tech-tag formatting, per-project H3+emoji shape.
Assessed to likely change: "About this org" framing, `skill-flip` placeholders, redundant contact/tech-stack duplication, density of `coupon-service`'s Demonstrates line.

## 3. User-Supplied Context

### `context/CV.md` (full CV)
- Header framing: **"Senior Software Engineer | Backend Architecture | Distributed Systems"** — notably more senior/specific than the profile page's current "Java / Spring Boot backend engineer."
- ~28 years of experience (1996–2026), most recently 8 years at HRS Group (SOAP→AWS migration, GDS Kubernetes migration of 50 microservices, Control Plane audit-system design), plus SeaChange Polska (distributed media-catalog microservices, C/C++ performance components).
- Core skills emphasize distributed systems architecture, event-driven architecture, technical leadership/system ownership, incremental modernization, CI/CD.
- Contact channels: email, phone, LinkedIn, GitHub (`github/aib-projekt`), and a **meetings calendar link** (not currently on the profile page).
- Notes AI-tool usage in professional work (ChatGPT/Copilot/Claude for migration planning and building the audit library) — interesting context but not directly a profile-page talking point; the profile showcases *personal portfolio repos*, not day-job work.

### `context/assumptions.md` (user's own design brief, Polish — translated/summarized)
The user already specified almost the entire brief:
1. **Short "who am I"**: role, stack, optionally current search status; link to CV/LinkedIn/email so the recruiter can immediately move on.
2. **Projects section reframed as "what this demonstrates"**, not a repo list: 1-2 sentence description, tech stack (badges/table), and — most important — the specific skill/concept demonstrated (concrete "selling" phrases a CV-scanner looks for, e.g. reactive/WebFlux, atomicity under concurrency, API design, Testcontainers testing). Link to repo and demo if available.
3. **Aggregate stack badges** — recruiters sometimes scan badges before reading text.
4. **Organization context**: one honest sentence noting these are sample/recruitment-exercise projects (confirmed accurate — `coupon-service`'s own README states it's "Implementation of a recruitment task") so it doesn't read as a company's production project.
5. **Contact repeated at the end** — recruiters who scroll to the bottom look for it there too.
6. English-only (not bilingual) since inbound recruiters are mostly UK-based.
7. Keep it landing-page short; leave technical depth in each repo's own README.
8. **If `skill-flip` has a live demo, add it** — a working link is stronger than code alone.

### New finding: `skill-flip` real content (recovered from local project, not previously on the profile page)
The local project at `~/Documents/Projects/AiB/rekrutacje/Skill Flip` has a complete README that resolves the placeholder entirely:
- **Live demo**: https://aib-projekt.github.io/skill-flip/
- **What it is**: a flip-card flashcard app for reviewing curated software-engineering terms — weighted review algorithm (concentrates review time on terms you keep missing), filterable/searchable browse grid, bilingual EN/PL glossary content, documented AI-assisted content-authoring pipeline (with a human-review rubric gate).
- **Real tech stack**: Vite, TypeScript (vanilla — no UI framework, direct DOM manipulation), Vitest (unit tests for logic/components), GitHub Actions + GitHub Pages (CI validates content and auto-deploys on push to `main`), plain CSS custom properties for theming. Fully static, zero backend, zero secrets.
- **What it demonstrates** (mirroring the "Demonstrates" pattern the user wants): vanilla front-end fundamentals without a framework crutch, a non-trivial spaced-repetition-style algorithm, automated testing (Vitest), CI/CD pipeline design (GitHub Actions → Pages), and a documented AI-assisted-but-human-reviewed content pipeline (relevant given the CV's stated AI-tooling experience).

`coupon-service`'s local README was also checked for accuracy — confirmed consistent with the current profile entry and explicitly self-describes as "Implementation of a recruitment task," validating the "honest framing" requirement in `assumptions.md`.

## 4. Cross-Reference Insights

- The user's own `assumptions.md` brief and the codebase-analyzer's independent assessment converge almost exactly (both flag "About this org" as too meta, both flag `skill-flip` as unfinished, both endorse keeping "Demonstrates" as the core recruiter-facing device). This gives high confidence in the direction without needing much additional exploration.
- The CV's stronger seniority framing vs. the README's modest framing is a gap neither document explicitly resolves — this is the main open question for Phase 2.
- `skill-flip` is actually a *stronger* demonstration piece than its placeholder suggests once real content is pulled in — front-end fundamentals, testing, and CI/CD, which nicely complements `coupon-service`'s backend/reactive/concurrency focus. Together they cover a wider skill spread than the current half-finished page conveys.

## 5. Implications for Design

- Phase 2 (Problem Exploration) can be genuinely abbreviated (2-3 questions per `is_simple`) since most scope questions are already answered by `assumptions.md` — remaining open items are the seniority/framing question and the meetings-calendar-link question above.
- Phase 4/5 (alternatives/convergence) has a natural decision area: how to frame the intro (current modest framing vs. CV-aligned senior framing) — this is the one real open design choice, not fully pre-answered by the user's own brief.
- Content for `skill-flip` no longer needs to be invented or left as a placeholder — real, verified content exists and can go straight into the spec.
