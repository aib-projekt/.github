## Markdown Authoring

> **Auto-discovered**: These standards were auto-discovered via `/maister:standards-discover` on 2026-07-15 from a 2-entry sample (`profile/README.md`). All are **Low confidence** (informational). Treat these as documented observations to help keep consistency as new project entries are added — not as strict rules — and revisit once more project entries exist to confirm the pattern.

### Centered HTML Div Blocks for Intro/Footer
Intro and closing/contact sections use centered `<div align="center">` HTML blocks rather than plain Markdown paragraphs.

Confidence: 30/100 (single-source, low sample size — informational, not enforced).

Source: `profile/README.md` (opening block, lines 1-10; closing contact block, lines 46-50); also documented in `project/tech-stack.md`.

Example:
```
<div align="center">

# Hi, I'm Bartek 👋

</div>
```

### Inline Placeholders for Incomplete Content
Incomplete sections are marked with inline HTML comments or bracketed placeholder text as authoring notes, rather than left silently blank or filled with guessed content.

Confidence: 30/100 (informational).

Source: `profile/README.md`, e.g. `*[fill in — e.g. front-end fundamentals, state handling, UX for spaced repetition]*` and `<!-- Optional: add a live demo link here if skill-flip is hosted -->`.

Example:
```
**Demonstrates:** *[fill in — e.g. front-end fundamentals, state handling, UX for spaced repetition]*

<!-- Optional: add a live demo link here if skill-flip is hosted -->
```

### Shields.io Badges for Contact and Tech Stack
Contact links and tech-stack summaries are rendered as shields.io badge images rather than plain text/links.

Confidence: 35/100 (informational).

Source: `profile/README.md`, e.g. `[![LinkedIn](https://img.shields.io/badge/LinkedIn-connect-0A66C2?logo=linkedin&logoColor=white)](...)`.

Example:
```
[![LinkedIn](https://img.shields.io/badge/LinkedIn-connect-0A66C2?logo=linkedin&logoColor=white)](https://www.linkedin.com/in/bartekmarciniak)
```
