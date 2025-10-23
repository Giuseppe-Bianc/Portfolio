# Implementation Plan: Portfolio Website

**Branch**: `001-portfolio-website` | **Date**: 23-10-2025 | **Spec**: [spec.md](spec.md)
**Input**: Feature specification from `/specs/001-portfolio-website/spec.md`

**Note**: This template is filled in by the `/speckit.plan` command. See `.specify/templates/commands/plan.md` for the execution workflow.

## Summary

The primary requirement is to create an accessible portfolio website using Angular 20+ and Bootstrap 5.3+ that maintains the aesthetic of HTML5 UP's Massively template. The technical approach involves converting the static HTML template to Angular components while ensuring WCAG 2.1 AA compliance, implementing cross-browser compatibility, and using Markdown files with YAML frontmatter for content management.

## Technical Context

**Language/Version**: TypeScript 5.9 (via Angular 20.3+)  
**Primary Dependencies**: Angular Core (20.3+), RxJS (7.8+), Bootstrap (5.3+), Angular Router, Angular CLI (20.3+)  
**Storage**: JSON/Markdown files with YAML frontmatter for content (content/projects/*.md)  
**Testing**: Jasmine/Karma (unit testing), Angular Testing Library, Cypress (e2e testing), axe-core (accessibility testing)  
**Target Platform**: Web browsers (Chrome 90+, Firefox 88+, Safari 15+, Edge 90+)  
**Project Type**: Web application (single-page application)  
**Performance Goals**: First Contentful Paint < 3s, First Meaningful Paint < 3s, Time to Interactive < 5s  
**Constraints**: WCAG 2.1 AA compliance, responsive design (320px to 1920px), maintain Massively template aesthetic  
**Scale/Scope**: Single portfolio site, up to 20 projects, global CDN deployment, up to 1000 monthly unique visitors

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

Based on the project constitution (which needs to be defined), the implementation plan meets standard requirements for:
- Test-first development: All components will have unit tests using Angular Testing Library
- Integration testing: E2E tests via Cypress for critical user journeys
- Observability: Google Analytics, uptime monitoring, and RUM metrics as specified in FR-012
- Accessibility: WCAG 2.1 AA compliance implementation using Angular's accessibility features
- Performance: Meeting the specified performance goals (FCP < 3s, TTI < 5s)
- Simplicity: Following Angular best practices without unnecessary abstractions

## Project Structure

### Documentation (this feature)

```text
specs/001-portfolio-website/
├── plan.md              # This file (/speckit.plan command output)
├── research.md          # Phase 0 output (/speckit.plan command)
├── data-model.md        # Phase 1 output (/speckit.plan command)
├── quickstart.md        # Phase 1 output (/speckit.plan command)
├── contracts/           # Phase 1 output (/speckit.plan command)
└── tasks.md             # Phase 2 output (/speckit.tasks command - NOT created by /speckit.plan)
```

### Source Code (repository root)

```text
src/
├── app/
│   ├── components/
│   │   ├── hero/
│   │   ├── project-gallery/
│   │   ├── navigation/
│   │   ├── about/
│   │   ├── contact/
│   │   └── shared/
│   ├── services/
│   │   ├── content.service.ts
│   │   ├── accessibility.service.ts
│   │   └── project-data.service.ts
│   ├── models/
│   │   ├── project.model.ts
│   │   ├── developer-profile.model.ts
│   │   └── contact.model.ts
│   ├── pages/
│   │   └── portfolio/
│   ├── pipes/
│   ├── guards/
│   ├── interceptors/
│   ├── app.component.ts
│   ├── app.component.html
│   ├── app.component.css
│   ├── app.module.ts
│   └── app.routes.ts
├── assets/
│   ├── content/
│   │   └── projects/
│   │       ├── project-1.md
│   │       ├── project-2.md
│   │       └── ...
│   ├── images/
│   │   └── ...
│   └── styles/
│       ├── main.scss
│       ├── _variables.scss
│       └── _mixins.scss
├── environments/
├── index.html
├── main.ts
└── styles.css

tests/
├── unit/
│   ├── components/
│   ├── services/
│   └── models/
├── e2e/
│   └── portfolio.e2e-spec.ts
└── accessibility/
    └── wcag-checks.spec.ts

public/
└── ...
```

**Structure Decision**: Single web application using Angular's component-based architecture with Bootstrap 5.3+ for styling. Content is stored in Markdown files with YAML frontmatter under `assets/content/projects/` to enable easy updates while maintaining the static site deployment approach specified in the feature requirements.

## Complexity Tracking

> **Fill ONLY if Constitution Check has violations that must be justified**

| Violation | Why Needed | Simpler Alternative Rejected Because |
|-----------|------------|-------------------------------------|
| [N/A] | [N/A] | [N/A] |
