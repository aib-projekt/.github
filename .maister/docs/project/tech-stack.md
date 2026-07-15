# Technology Stack

## Overview
This document describes the technology choices for the AiB GitHub Organization Profile repository. This is a documentation-only repository (no application code) — it exists solely to render `profile/README.md` on the AiB organization's GitHub homepage.

## Languages

### Markdown (GitHub Flavored)
- **Usage**: 100% of repository content
- **Rationale**: Native format for GitHub org profile READMEs; no build step required
- **Key Features Used**: Headings, centered `<div align="center">` blocks, inline HTML comments as authoring notes, badge images via Markdown image links

## Frameworks
Not applicable — this repository contains no application code.

### Frontend
None.

### Backend
None. (The profile mentions Java / Spring Boot / PostgreSQL / Docker as the tech stack of the *linked* projects — e.g. `coupon-service` — not of this repository itself.)

### Testing
None.

## Database
Not applicable.

## Build Tools & Package Management
None — no package manager, no build tooling. Content is authored directly as Markdown.

## Infrastructure

### Containerization
Not applicable to this repository.

### CI/CD
None configured.

### Hosting
GitHub org-profile rendering — `profile/README.md` is displayed automatically on the AiB organization's GitHub homepage; no separate hosting needed.

## Development Tools

### Linting & Formatting
None configured.

### Type Checking
Not applicable.

## Key Dependencies
- [shields.io](https://shields.io) — badge images for tech stack and contact links

## Version Management
Git, with a `draft` branch used for in-progress edits before merging to `main`.

## Migration Path (for legacy projects)
Not applicable — new project.

---
*Last Updated*: 2026-07-15
*Auto-detected*: Language (Markdown), badge service (shields.io), absence of build tools/frameworks/dependencies — detected via project analysis. Project purpose and goals confirmed by user.
