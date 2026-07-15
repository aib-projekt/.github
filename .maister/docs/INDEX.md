# Documentation Index

**IMPORTANT**: Read this file at the beginning of any development task to understand available documentation and standards.

## Quick Reference

### Project Documentation
Project vision and technology stack are documented below. Roadmap and Architecture were intentionally not generated for this repository (see note below).

### Technical Standards
Coding standards, conventions, and best practices organized by domain. **Global** standards are initialized for this project, and **profile** standards (auto-discovered from the org profile page) are also present; frontend, backend, and testing standards are not yet set up.

---

## Project Documentation

Located in `.maister/docs/project/`

### Vision (`project/vision.md`)
Pitch, problem statement, target users (recruiters, clients/collaborators, Bartek himself), key features (personal intro, contact links, per-project sections with "Demonstrates" callouts, shields.io tech-stack badges), success criteria, and differentiators (framework-agnostic plain Markdown, skills-focused project write-ups) for the AiB GitHub organization profile page.

### Tech Stack (`project/tech-stack.md`)
Documents this repository as documentation-only: 100% GitHub Flavored Markdown with no build step, no frameworks/backend/database/testing (the Java/Spring Boot/PostgreSQL/Docker stack referenced in the profile belongs to linked projects, not this repo), no CI/CD, GitHub org-profile auto-rendering as hosting, shields.io as the sole external dependency, and Git with a `draft` → `main` branch workflow.

### Roadmap and Architecture — Not Generated (Intentional)
Per explicit user selection during initialization, `project/roadmap.md` and `project/architecture.md` were **not created**. This is a documentation-only GitHub org profile repository with no application code and no planned feature roadmap, so these documents were judged not applicable. If project direction changes (e.g., the org profile evolves into something roadmap-worthy), add them using the docs-manager skill's "Add Documentation File" operation.

---

## Technical Standards

### Global Standards

Located in `.maister/docs/standards/global/`

#### Error Handling (`standards/global/error-handling.md`)
Clear user-facing error messages without leaking internals, fail-fast input validation, typed/specific exceptions, centralized error handling at boundaries, graceful degradation for non-critical failures, retry with exponential backoff for transient failures, and guaranteed resource cleanup.

#### Validation (`standards/global/validation.md`)
Server-side validation as the source of truth (with client-side for UX only), validate-early principle, specific field-level error messages, allowlists over blocklists, systematic type/format/range checks, input sanitization against injection attacks, business-rule validation, and consistent enforcement across all entry points.

#### Development Conventions (`standards/global/conventions.md`)
Predictable project structure, up-to-date READMEs, clean version control practices (commit messages, feature branches, PR descriptions), environment variables for config/secrets, minimal/justified dependencies, defined code review process, required test coverage before merge, feature flags instead of long-lived branches, changelog maintenance, and building only what's needed.

#### Coding Style (`standards/global/coding-style.md`)
Consistent naming across variables/functions/classes/files, automated formatting, descriptive naming over cryptic abbreviations, small focused functions, uniform indentation enforced by tooling, no dead code, avoiding unnecessary backward-compatibility paths, and DRY (don't repeat yourself).

#### Commenting (`standards/global/commenting.md`)
Prefer self-explanatory code over comments, comment sparingly and only where logic isn't obvious, and avoid changelog-style "what changed" comments in favor of timeless explanations.

#### Minimal Implementation (`standards/global/minimal-implementation.md`)
Build only methods/classes/functions that are actually called, avoid future stubs and speculative abstractions (factories/strategies/adapters without immediate need), delete unused exploration artifacts, and review new code before commit to confirm every addition has a caller or clear readability purpose.

### Frontend Standards

*Not initialized for this project. If you need frontend standards, you can:*
- *Add them manually using the docs-manager skill*
- *Run `/maister:standards-discover --scope=frontend` to auto-discover*

### Backend Standards

*Not initialized for this project. If you need backend standards, you can:*
- *Add them manually using the docs-manager skill*
- *Run `/maister:standards-discover --scope=backend` to auto-discover*

### Testing Standards

*Not initialized for this project. If you need testing standards, you can:*
- *Add them manually using the docs-manager skill*
- *Run `/maister:standards-discover --scope=testing` to auto-discover*

### Profile Standards

Located in `.maister/docs/standards/profile/`

Auto-discovered via `/maister:standards-discover` on 2026-07-15 by analyzing `profile/README.md` (the GitHub org profile page — this repo has no application code, so these standards govern how that Markdown page itself is authored). Based on a 2-entry sample; all standards are **Low confidence** (informational observations to keep new entries consistent, not enforced rules) — revisit once more project entries exist.

#### Markdown Authoring (`standards/profile/markdown-authoring.md`)
Centered `<div align="center">` HTML blocks for the intro and closing/contact sections instead of plain paragraphs; inline HTML comments or bracketed placeholder text (e.g. `*[fill in — ...]*`) to mark incomplete sections instead of leaving them blank or guessing content; shields.io badge images for contact links and tech-stack summaries instead of plain text/links.

#### Structure (`standards/profile/structure.md`)
A bolded "**Demonstrates:**" line in each project entry connecting the project to specific engineering skills; a consistent per-project entry shape (H3 heading with emoji + repo link, one-line description, **Demonstrates:** line, closing tech-tag line); tech-stack tags wrapped in backticks and joined with a middle-dot (" · ") separator instead of commas or bullets.

---

## How to Use This Documentation

1. **Start Here**: Always read this INDEX.md first to understand what documentation exists
2. **Project Context**: Read relevant project documentation before starting work
3. **Standards**: This index only points to the standards — open and follow the specific standard files relevant to your task; don't rely on the index alone
4. **Keep Updated**: Update documentation when making significant changes
5. **Customize**: Adapt all documentation to your project's specific needs

## Updating Documentation

- Project documentation should be updated when goals, tech stack, or architecture changes
- Technical standards should be updated when team conventions evolve
- Always update INDEX.md when adding, removing, or significantly changing documentation
