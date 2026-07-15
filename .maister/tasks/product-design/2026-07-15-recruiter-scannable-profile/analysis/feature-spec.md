# Feature Specification — Recruiter-Scannable Profile README

## TL;DR
Full replacement content for `profile/README.md`, built section-by-section per the approved design decisions (`analysis/design-decisions.md`): CV-aligned seniority intro with a three-channel contact bookend, a repositioned accurate cross-project tech-stack row, an honest one-sentence hook replacing "About this org," and two project entries (both real content, no placeholders) using a punchy-lead + detail shape.

## Key Decisions
- (see `analysis/design-decisions.md` for the four area-level decisions this spec implements)

## Open Questions / Risks
- (tracked per-section below as each is drafted)

---

## Section 1: Intro & Top Contact Block

```markdown
<div align="center">

# Hi, I'm Bartek 👋

Senior Software Engineer — Backend Architecture / Distributed Systems

[![LinkedIn](https://img.shields.io/badge/LinkedIn-connect-0A66C2?logo=linkedin&logoColor=white)](https://www.linkedin.com/in/bartekmarciniak)
[![Email](https://img.shields.io/badge/Email-contact-D14836?logo=gmail&logoColor=white)](mailto:puffed.08drifter@icloud.com)
[![Book a call](https://img.shields.io/badge/Book%20a%20call-schedule-4285F4)](https://www.cal.eu/bartek/meeting)

</div>
```

**Rationale**: Role line upgraded to CV-aligned seniority framing (Alternative selected in Phase 2). Dropped the old "this org hosts sample projects referenced in my CV" clause — that context now lives in the Section 3 hook sentence instead. Added a third badge for the calendar link (Decision Area 1, Alternative 1A). Kept purely descriptive, no job-search-status language.

**Status**: Approved.

---

## Section 2: Tech-Stack Signal (repositioned)

```markdown
## Tech stack

![Java](https://img.shields.io/badge/Java-ED8B00?logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-6DB33F?logo=springboot&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?logo=postgresql&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?logo=typescript&logoColor=white)
![Vite](https://img.shields.io/badge/Vite-646CFF?logo=vite&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?logo=githubactions&logoColor=white)

---
```

**Rationale**: Moved from its old position (near the bottom, after Projects) to right after the intro — functions as a pre-read range signal (Decision Area 2, Alternative 2B). Now genuinely cross-project: backend (Java, Spring Boot, PostgreSQL, Docker) from `coupon-service` + frontend/tooling (TypeScript, Vite, GitHub Actions) from `skill-flip`. Dropped `Maven` to avoid crowding — it's a build-tool detail that doesn't add to the breadth signal.

**Status**: Approved.

---

## Section 3: Honest Hook + Projects

```markdown
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
```

**Rationale**: Replaces "About this org" with one honest hook sentence (Decision Area 3, Alternative 3B) — discloses the recruitment-exercise/portfolio framing and bridges into the projects. Both entries compressed to a bolded punchy-lead + detail shape (Decision Area 4, Alternative 4B): `coupon-service` stays first (matches the seniority/backend headline), `skill-flip` now has full real content (no placeholders) with its live demo linked in the heading.

**Status**: Approved.

---

## Section 4: Closing Contact Block

```markdown
<div align="center">

📫 Let's talk — [LinkedIn](https://www.linkedin.com/in/bartekmarciniak/) · [Email](mailto:puffed.08drifter@icloud.com) · [Book a call](https://www.cal.eu/bartek/meeting)

</div>
```

**Rationale**: Adds the calendar link as a third option, completing the full contact bookend (Decision Area 1, Alternative 1A). Otherwise unchanged from the current page — same centered plain-link format.

**Status**: Approved.

---

## Full Assembled Page

All four sections combined in order, ready to replace the entire contents of `profile/README.md`:

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

## Traceability to Success Criteria

- ✅ Recruiter grasps who/what/how-to-contact within ~15 seconds — seniority headline + repositioned tech-stack row + punchy Demonstrates leads all front-load the key signals
- ✅ Zero placeholder text — `skill-flip` fully filled with real, verified content
- ✅ Contact = LinkedIn + email + calendar, full bookend — present in Sections 1 and 4
- ✅ Intro purely descriptive, no open-to-work framing — confirmed in Section 1
- ✅ Honest recruitment-exercise framing preserved — Section 3 hook sentence
- ⚠️ Renders cleanly after `draft` → `main` merge — not yet verified; recommend a quick visual check (Phase 7 mockup / post-merge GitHub preview) before finalizing
