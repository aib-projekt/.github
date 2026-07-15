# Design Context Index

Ingested from product-design task: `.maister/tasks/product-design/2026-07-15-recruiter-scannable-profile/`

## Screens

| ID | Source Mockup | Description |
|---|---|---|
| `screen:profile-readme` | `mockups/aib-org-profile-full-page-rendered-preview.html` | Full rendered preview of the redesigned `profile/README.md` — single-page GitHub org profile: intro w/ seniority headline + 3-channel contact badges, repositioned cross-project tech-stack row, honest hook sentence, two project entries (`coupon-service`, `skill-flip`) with punchy-lead "Demonstrates" callouts, closing contact repeat. |

## Components

No reusable UI components — this is a single static Markdown content page, not an application with componentized UI.

## Notes

- `brief.md` (copied from the product-design task's `outputs/product-brief.md`) is the binding source of requirements — see especially its "Acceptance Criteria" checklist and "Layer 2: Design Decisions" table.
- The actual ready-to-paste page content lives in the product-design task's `analysis/feature-spec.md` (not copied here, but referenced from `brief.md`) — the implementation is a direct content replacement of `profile/README.md`, not new application code.
