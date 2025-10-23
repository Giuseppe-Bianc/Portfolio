<!-- 
SYNC IMPACT REPORT:
Version change: N/A initial creation → 1.0.0
Modified principles: None (initial creation)
Added sections: All principles and sections (initial constitution)
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

### I. Component-First Architecture
Every feature starts as a self-contained Angular component; Components must be independently testable and reusable; Clear separation of concerns required - no tightly coupled business logic.

### II. Responsive Design First
All UI elements must be designed mobile-first with Bootstrap 5.3+ responsive utilities; Design must work on screen sizes from 320px to 1920px; Accessibility and usability on mobile devices is non-negotiable.

### III. Test-First (NON-NEGOTIABLE)
TDD mandatory: Unit tests written → Tests fail → Then implement; Component tests with Angular Testing Library required; Red-Green-Refactor cycle strictly enforced for all features.

### IV. Accessibility-First Development
All features must comply with WCAG 2.1 AA standards from initial development; ARIA attributes and semantic HTML required; Keyboard navigation and screen reader compatibility mandatory for all interactive elements.

### V. Performance & Observability
All features must meet performance targets: First Meaningful Paint < 3s, Time to Interactive < 5s; Google Analytics and basic RUM metrics required for user journey tracking; Bundle size optimization and image loading strategies mandatory.

## Additional Constraints

### Technology Stack Requirements
- Angular 20+ with TypeScript 5.9+ as the primary framework
- Bootstrap 5.3+ for CSS framework and responsive utilities
- RxJS 7.8+ for reactive programming patterns
- Markdown files with YAML frontmatter for content management
- Static site deployment with global CDN (Netlify or equivalent)

### Quality Standards
- Code coverage must be ≥80% for all components and services
- All components must pass axe-core accessibility tests
- Cross-browser compatibility: Chrome 90+, Firefox 88+, Safari 15+, Edge 90+
- All code must pass ESLint and Prettier formatting standards

## Development Workflow

### Code Review Process
- All pull requests require at least one peer review
- Review must verify compliance with accessibility standards
- Performance impact must be validated before approval
- Code must pass all automated tests before merging

### Quality Gates
- Component tests must pass (≥80% coverage)
- Accessibility tests must pass (zero violations for WCAG 2.1 AA)
- Performance metrics must meet targets
- Cross-browser testing must validate functionality

## Governance

All pull requests and code reviews must verify compliance with these principles. New features must align with the component-first architecture and accessibility-first approach. Complexity must be justified with clear user value. Use QWEN.md for runtime development guidance.

**Version**: 1.0.0 | **Ratified**: 2025-10-23 | **Last Amended**: 2025-10-23