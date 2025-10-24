<!-- 
SYNC IMPACT REPORT:
Version change: 1.2.0 → 1.3.0
Modified principles: I, II (enhanced with Angular 20+ CSS styling standards and Bootstrap 5.3+ specific guidelines)
Added sections: None
Removed sections: None
Templates requiring updates: 
- ✅ .specify/templates/plan-template.md - No changes needed
- ✅ .specify/templates/spec-template.md - No changes needed  
- ✅ .specify/templates/tasks-template.md - No changes needed
- ✅ .specify/templates/commands/*.md - No changes needed
- ✅ Runtime guidance docs - No changes needed
Follow-up TODOs: None
-->

# Portfolio Website Constitution

## Core Principles

### I. Component-First Architecture with CSS Best Practices (Angular 20+ Standards)
Every feature starts as a self-contained Angular component using standalone components pattern; Components must be independently testable with TestBed and follow Angular style guide; Clear separation of concerns required with services for business logic - no tightly coupled presentation and business logic. All components must use OnPush change detection strategy where possible and implement proper input/output patterns for loose coupling. Component styling must follow Angular's encapsulation patterns with SCSS for component-specific styles, utilizing CSS custom properties for theming and following BEM methodology where appropriate.

### II. Responsive Design First with CSS Integration (Bootstrap 5.3+ Standards)
All UI elements must be designed mobile-first with Bootstrap 5.3+ responsive grid system and utility classes; Design must work on screen sizes from 320px to 1920px using Bootstrap breakpoints (xs, sm, md, lg, xl, xxl); Accessibility and usability on mobile devices is non-negotiable with touch-friendly interactions and appropriate spacing per Bootstrap 5.3+ guidelines. CSS must follow modern standards including Flexbox, Grid, and custom properties for maintainable, scalable styling that integrates seamlessly with Bootstrap's utility-first approach.

### III. Test-First (NON-NEGOTIABLE) - Angular 20+ Best Practices
TDD mandatory using Jasmine/Karma: Unit tests written → Tests fail → Then implement; Component tests with Angular Testing Library and mock services required; Red-Green-Refactor cycle strictly enforced for all features; All components must have 100% branch coverage for critical paths and use Angular's built-in test utilities.

### IV. Accessibility-First Development (Angular + Bootstrap Standards)
All features must comply with WCAG 2.1 AA standards from initial development; ARIA attributes, semantic HTML, and proper contrast ratios per Angular and Bootstrap accessibility guidelines required; Keyboard navigation and screen reader compatibility mandatory for all interactive elements; Use Angular's built-in accessibility utilities and Bootstrap's accessible component patterns.

### V. Performance & Observability (Angular 20+ Optimization)
All features must meet performance targets: First Meaningful Paint < 3s, Time to Interactive < 5s; Google Analytics and basic RUM metrics required for user journey tracking; Bundle size optimization using Angular's lazy loading and Bootstrap's CSS tree-shaking; Use Angular's built-in profiling tools and implement proper image optimization strategies per Web Vitals guidelines.

## Additional Constraints

### Technology Stack Requirements
- Angular 20+ with TypeScript 5.9+, following Angular style guide and best practices
- Bootstrap 5.3+ with SCSS for CSS framework and responsive utilities, using utility-first approach where appropriate
- RxJS 7.8+ for reactive programming patterns following Angular's reactive forms and state management patterns
- Angular CLI 20.3+ for build and development tooling
- Modern CSS features (custom properties, Grid, Flexbox) following MDN Web Standards
- Markdown files with YAML frontmatter for content management
- Static site deployment with global CDN (Netlify or equivalent)

### Quality Standards
- Code coverage must be ≥90% for all components and services
- All components must pass axe-core accessibility tests with zero violations
- Cross-browser compatibility: Chrome 90+, Firefox 88+, Safari 15+, Edge 90+
- All code must follow Angular style guide and pass ESLint with Angular-specific rules and Prettier formatting standards
- CSS/SCSS must pass stylelint validation with consistent formatting
- Use Angular's strict mode and enable all compiler checks

## Development Workflow

### Code Review Process
- All pull requests require at least one peer review with Angular expertise
- Review must verify compliance with Angular style guide and accessibility standards
- Performance impact must be validated before approval using Angular DevTools
- Code must pass all automated tests before merging
- Component selectors must follow Angular naming conventions (app-prefix)
- CSS/SCSS changes must follow established patterns and maintain consistency

### Quality Gates
- Component tests must pass (≥90% coverage)
- Accessibility tests must pass (zero violations for WCAG 2.1 AA)
- Performance metrics must meet targets (Lighthouse score ≥90)
- Cross-browser testing must validate functionality
- CSS validation: no unused styles, proper naming conventions, responsive behavior
- Template validation: no inline styles, proper input/output usage

### VI. Documentation Standards
- All code must be documented in a very detailed, precise, meticulous, and in-depth way while remaining concise
- All documentation artifacts (research.md, quickstart.md, data-model.md, and any other docs) must be created in a very detailed, precise, meticulous, and in-depth way
- Use TypeScript JSDoc comments for all public methods, interfaces, and classes with @param, @returns, and @description tags
- Feature specifications must include detailed user scenarios and edge cases
- Implementation plans must include detailed technical context and architecture decisions
- Document decision rationales for all significant implementation choices
- Follow Angular documentation standards and maintain consistency across all documentation artifacts

## Governance

All pull requests and code reviews must verify compliance with these principles and Angular 20+/Bootstrap 5.3+ community standards. New features must align with the component-first architecture and accessibility-first approach. Complexity must be justified with clear user value. Use QWEN.md for runtime development guidance.

**Version**: 1.3.0 | **Ratified**: 2025-10-23 | **Last Amended**: 2025-10-23