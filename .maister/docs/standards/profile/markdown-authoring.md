## Markdown Authoring

> **Auto-discovered**: These standards were auto-discovered via `/maister:standards-discover` on 2026-07-15 from a 2-entry sample (`profile/README.md`). All are **Low confidence** (informational). Treat these as documented observations to help keep consistency as new project entries are added — not as strict rules — and revisit once more project entries exist to confirm the pattern.

### Centered HTML Div Blocks for Intro/Footer
Intro and closing/contact sections use centered `<div align="center">` HTML blocks rather than plain Markdown paragraphs.

Confidence: 30/100 (single-source, low sample size — informational, not enforced).

Source: `profile/README.md` (opening block, lines 1-11; closing contact block, lines 47-51); also documented in `project/tech-stack.md`.

Example:
```
<div align="center">

# Hi, I'm Bartek 👋

</div>
```

### Inline Placeholders for Incomplete Content — Retired
**Status (2026-07-15): retired.** This pattern was observed when `profile/README.md` still had an unfinished `skill-flip` entry. That entry was completed with real content (including a live-demo link) during the recruiter-scannable redesign, so no placeholder text remains anywhere in the file — the observed pattern no longer applies. Keeping this entry as a historical note: if a future project entry is added before it's fully ready, placeholder text or an HTML comment note remains a reasonable stopgap, but zero-placeholder-text is now the page's actual success criterion (see `project/vision.md`), not this pattern.

Confidence: 30/100 (informational, now superseded).

### Shields.io Badges for Contact and Tech Stack
Contact links and tech-stack summaries are rendered as shields.io badge images rather than plain text/links.

Confidence: 35/100 (informational).

Source: `profile/README.md`, e.g. `[![LinkedIn](https://img.shields.io/badge/LinkedIn-connect-0A66C2?logo=linkedin&logoColor=white)](...)`.

Example:
```
[![LinkedIn](https://img.shields.io/badge/LinkedIn-connect-0A66C2?logo=linkedin&logoColor=white)](https://www.linkedin.com/in/bartekmarciniak)
```
