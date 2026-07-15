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

📫 Let's talk — [LinkedIn](https://www.linkedin.com/in/bartekmarciniak) · [Email](mailto:puffed.08drifter@icloud.com) · [Book a call](https://www.cal.eu/bartek/meeting)

</div>
