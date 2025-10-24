# Implementation Plan: Portfolio Website

**Branch**: `001-portfolio-website` | **Date**: 23-10-2025 | **Spec**: [spec.md](spec.md)
**Input**: Feature specification from `/specs/001-portfolio-website/spec.md`

**Note**: This template is filled in by the `/speckit.plan` command. See `.specify/templates/commands/plan.md` for the execution workflow.

## Summary

The primary requirement is to create a fully accessible portfolio website using Angular 20+, CSS (with SCSS), and Bootstrap 5.3+ that maintains the aesthetic of HTML5 UP's Massively template. The technical approach involves converting the static HTML template to Angular components while ensuring WCAG 2.1 AA compliance, implementing cross-browser compatibility, and using Markdown files with YAML frontmatter for content management. The implementation follows Angular 20+, CSS, and Bootstrap 5.3+ community standards with detailed documentation as required by the project constitution.

## Technical Context

**Language/Version**: TypeScript 5.9 (via Angular 20.3+) with strict mode enabled and all compiler checks active  
**Primary Dependencies**: Angular Core 20.3+, Angular CLI 20.3+, RxJS 7.8+, Bootstrap 5.3.8, Angular Router, Angular Common, Angular Forms, Angular Platform Browser, Angular CDK, marked.js 12.0.0 for Markdown processing, DOMPurify 3.0.0 for content sanitization  
**Storage**: Static JSON and Markdown files with YAML frontmatter for content (content/projects/*.md)  
**Testing**: Jasmine/Karma for unit testing, Angular Testing Library for component testing, Cypress for e2e testing, axe-core for accessibility testing, Istanbul for code coverage  
**Target Platform**: Web browsers (Chrome 90+, Firefox 88+, Safari 15+, Edge 90+) with responsive design from 320px to 1920px width  
**Project Type**: Single-page web application with static content delivery  
**Performance Goals**: First Meaningful Paint < 3s, Time to Interactive < 5s, Lighthouse performance score ≥ 90, bundle size optimization with lazy loading  
**Constraints**: WCAG 2.1 AA compliance, responsive design (320px to 1920px), maintain Massively template aesthetic, ≥90% code coverage, zero accessibility violations  
**Scale/Scope**: Single portfolio site, up to 50 projects, global CDN deployment, up to 5000 monthly unique visitors

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

Based on the project constitution v1.3.0, this implementation plan complies with all core principles:

- **Component-First Architecture with CSS Best Practices**: Implementation uses Angular's standalone components pattern with proper SCSS styling and CSS custom properties following BEM methodology
- **Responsive Design First with CSS Integration**: Design follows Bootstrap 5.3+ responsive grid system with mobile-first approach using modern CSS features (Flexbox, Grid)
- **Test-First Development**: All components will have unit tests with ≥90% coverage using Angular Testing Library
- **Accessibility-First Development**: WCAG 2.1 AA compliance implemented from initial development with ARIA attributes and semantic HTML
- **Performance & Observability**: Performance targets FMP < 3s, TTI < 5s with analytics and RUM metrics
- **Documentation Standards**: All artifacts will be created in a very detailed, precise, meticulous, and in-depth way while remaining concise

All quality standards from the constitution will be met including code coverage ≥90%, zero accessibility violations, cross-browser compatibility with target browsers, CSS/SCSS validation with stylelint, and Angular style guide compliance.

## Project Structure

### Documentation (this feature)

```text
specs/001-portfolio-website/
├── plan.md              # This file (/speckit.plan command output)
├── research.md          # Phase 0 output (/speckit.plan command)
├── data-model.md        # Phase 1 output (/speckit.plan command)
├── quickstart.md        # Phase 1 output (/speckit.plan command)
├── contracts/           # Phase 1 output (/speckit.plan command)
│   └── api-contract.md
└── tasks.md             # Phase 2 output (/speckit.tasks command - NOT created by /speckit.plan)
```

### Source Code (repository root)

```text
src/
├── app/
│   ├── components/
│   │   ├── hero/
│   │   │   ├── hero.component.ts
│   │   │   ├── hero.component.html
│   │   │   ├── hero.component.scss
│   │   │   └── hero.component.spec.ts
│   │   ├── project-gallery/
│   │   │   ├── project-gallery.component.ts
│   │   │   ├── project-gallery.component.html
│   │   │   ├── project-gallery.component.scss
│   │   │   └── project-gallery.component.spec.ts
│   │   ├── navigation/
│   │   │   ├── navigation.component.ts
│   │   │   ├── navigation.component.html
│   │   │   ├── navigation.component.scss
│   │   │   └── navigation.component.spec.ts
│   │   ├── about/
│   │   │   ├── about.component.ts
│   │   │   ├── about.component.html
│   │   │   ├── about.component.scss
│   │   │   └── about.component.spec.ts
│   │   ├── contact/
│   │   │   ├── contact.component.ts
│   │   │   ├── contact.component.html
│   │   │   ├── contact.component.scss
│   │   │   └── contact.component.spec.ts
│   │   └── shared/
│   │       ├── project-card/
│   │       │   ├── project-card.component.ts
│   │       │   ├── project-card.component.html
│   │       │   ├── project-card.component.scss
│   │       │   └── project-card.component.spec.ts
│   ├── services/
│   │   ├── content.service.ts
│   │   ├── content.service.spec.ts
│   │   ├── accessibility.service.ts
│   │   ├── accessibility.service.spec.ts
│   │   └── seo.service.ts
│   ├── models/
│   │   ├── project.model.ts
│   │   ├── developer-profile.model.ts
│   │   └── contact.model.ts
│   ├── pages/
│   │   └── portfolio/
│   │       ├── portfolio.component.ts
│   │       ├── portfolio.component.html
│   │       ├── portfolio.component.scss
│   │       └── portfolio.component.spec.ts
│   ├── pipes/
│   │   └── safe-html.pipe.ts
│   ├── guards/
│   ├── interceptors/
│   ├── app.component.ts
│   ├── app.component.html
│   ├── app.component.scss
│   ├── app.component.spec.ts
│   ├── app.module.ts
│   └── app.routes.ts
├── assets/
│   ├── content/
│   │   ├── profile.json
│   │   └── projects/
│   │       ├── project-1.md
│   │       ├── project-2.md
│   │       └── ...
│   ├── images/
│   │   ├── avatar.jpg
│   │   ├── projects/
│   │   │   ├── project1-thumb.webp
│   │   │   ├── project1-full.jpg
│   │   │   └── ...
│   │   └── ui/
│   │       ├── placeholder.webp
│   │       └── ...
│   └── styles/
│       ├── main.scss
│       ├── _variables.scss
│       ├── _mixins.scss
│       └── _massively-theme.scss
├── environments/
│   ├── environment.ts
│   └── environment.prod.ts
├── index.html
├── main.ts
└── styles.scss

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

**Structure Decision**: Single web application using Angular's standalone component architecture with Bootstrap 5.3+ and modern CSS features (Grid, Flexbox, custom properties) for styling. Content is stored in Markdown files with YAML frontmatter under `src/assets/content/projects/` to enable easy updates while maintaining the static site deployment approach specified in the feature requirements. This structure follows Angular 20+ best practices and Bootstrap 5.3+ integration patterns while ensuring compliance with all constitutional requirements.

## Complexity Tracking

> **Fill ONLY if Constitution Check has violations that must be justified**

| Violation | Why Needed | Simpler Alternative Rejected Because |
|-----------|------------|-------------------------------------|
| [N/A] | [N/A] | [N/A] |
