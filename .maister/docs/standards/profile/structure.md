## Structure

> **Auto-discovered**: These standards were auto-discovered via `/maister:standards-discover` on 2026-07-15 from a 2-entry sample (`profile/README.md`). All are **Low confidence** (informational). Treat these as documented observations to help keep consistency as new project entries are added — not as strict rules — and revisit once more project entries exist to confirm the pattern.

### "Demonstrates" Callout Pattern
Each project entry includes a bolded "**Demonstrates:**" line connecting the project to specific engineering skills, instead of just listing technologies.

Confidence: 35/100 (informational).

Source: `profile/README.md`, e.g. "**Demonstrates:** reactive programming (Spring WebFlux + R2DBC), safe concurrency without locks...".

### Per-Project Entry Structure
Each project section follows the same shape: H3 heading with emoji + repo link, one-line description, a bolded **Demonstrates:** line, then a closing line of tech-stack tags. Inferred from the two existing project entries (coupon-service, skill-flip), which both follow this shape identically.

Confidence: 45/100 (small sample size — only 2 entries observed).

Source: `profile/README.md` (coupon-service and skill-flip entries).

Example:
```
### 🎟️ [coupon-service](https://github.com/aib-projekt/coupon-service)
REST API for coupon lifecycle management — creation, retrieval, and **atomic redemption** under concurrent load.

**Demonstrates:** reactive programming (Spring WebFlux + R2DBC), safe concurrency without locks.

`Java 25` · `Spring Boot / WebFlux` · `PostgreSQL`
```

### Tech Tag List Formatting
Tech-stack tags within a project entry are each wrapped in backticks and joined with a middle-dot (" · ") separator, rather than commas or a bulleted list.

Confidence: 50/100 (small sample size — only 2 entries observed).

Source: `profile/README.md`, e.g. `` `Java 25` · `Spring Boot / WebFlux` · `PostgreSQL` · `Flyway` · `Docker` · `Maven` ``.
