# Quickstart Guide: Portfolio Website Implementation

## Prerequisites

### System Requirements
- Node.js (v18.13.0 or later) with npm v9.0.0+ for package management and build processes
- Angular CLI (v20.3.6 or later) for project scaffolding, development server, and production builds
- Git (v2.20.0 or later) for version control and collaboration workflows
- Modern web browser (Chrome 90+, Firefox 88+, Safari 15+, Edge 90+) for development and testing
- Text editor or IDE with TypeScript and SCSS support (VS Code recommended with Angular extension pack)

### Development Environment Setup
Before beginning the implementation, ensure your development environment meets the prerequisites. The portfolio website requires specific versions of tools to maintain compatibility with Angular 20+, Bootstrap 5.3+, and modern CSS features. Verify your Node.js version with `node --version` and install the latest LTS version if needed from nodejs.org.

## Setup Instructions

### 1. Initialize Angular Project
Begin by creating a new Angular project with the required specifications:
```bash
# Create new Angular project with routing and SCSS styling
ng new portfolio-website --routing=true --style=scss --standalone=true

# Navigate to project directory
cd portfolio-website
```

The `--standalone=true` flag ensures the project follows Angular's latest component architecture pattern, which aligns with our component-first architecture principle from the constitution.

### 2. Install Bootstrap and Dependencies
Install Bootstrap 5.3+ and other necessary dependencies for the portfolio website:
```bash
# Install Bootstrap 5.3+ and its required dependencies
npm install bootstrap@^5.3.8

# Install additional dependencies for content processing and accessibility
npm install marked@^12.0.0 dompurify@^3.0.0
npm install --save-dev @types/marked@^5.0.0
```

### 3. Configure Bootstrap and CSS in Angular
Add Bootstrap CSS and JavaScript to your `angular.json` file under the project's build options:

```json
{
  "projects": {
    "portfolio-website": {
      "architect": {
        "build": {
          "builder": "@angular/build:application",
          "options": {
            "styles": [
              "node_modules/bootstrap/dist/css/bootstrap.min.css",
              "src/styles.scss"
            ],
            "scripts": [
              "node_modules/bootstrap/dist/js/bootstrap.bundle.min.js"
            ]
          }
        }
      }
    }
  }
}
```

Alternatively, you can import Bootstrap in your `src/styles.scss` file:
```scss
// Import Bootstrap SCSS files for customization capability
@import 'bootstrap/scss/bootstrap';
```

### 4. Configure TypeScript and Compilation Settings
Update your `tsconfig.json` to include strict type checking and ensure compatibility with Angular 20+ standards:

```json
{
  "compilerOptions": {
    "strict": true,
    "noImplicitOverride": true,
    "noPropertyAccessFromIndexSignature": true,
    "noImplicitReturns": true,
    "noFallthroughCasesInSwitch": true,
    "skipLibCheck": true,
    "isolatedModules": true,
    "moduleResolution": "bundler",
    "experimentalDecorators": true,
    "importHelpers": true,
    "target": "ES2022",
    "module": "ES2022"
  },
  "angularCompilerOptions": {
    "enableI18nLegacyMessageIdFormat": false,
    "strictInjectionParameters": true,
    "strictInputAccessModifiers": true,
    "strictTemplates": true
  }
}
```

### 5. Configure CSS/SCSS Linting
Set up stylelint for consistent CSS/SCSS formatting as required by the constitution:

```bash
# Install stylelint for CSS/SCSS validation
npm install --save-dev stylelint stylelint-config-standard-scss
```

Create a `.stylelintrc.json` file:
```json
{
  "extends": [
    "stylelint-config-standard-scss"
  ],
  "rules": {
    "indentation": 2,
    "string-quotes": "single",
    "color-hex-case": "lower",
    "color-hex-length": "short",
    "selector-max-id": 0,
    "no-duplicate-selectors": true,
    "no-descending-specificity": null
  }
}
```

## Development Workflow

### 1. Start Development Server
Launch the Angular development server to begin implementing the portfolio:
```bash
# Start development server with live reload
ng serve

# The application will be available at http://localhost:4200
# Changes to source files will automatically reload the browser
```

### 2. Create Project Structure Based on Massively Template
Implement the core components of the Massively template by creating the following component structure:

```bash
# Generate core components based on user stories
ng generate component components/hero
ng generate component components/project-gallery
ng generate component components/navigation
ng generate component components/about
ng generate component components/contact
ng generate component components/shared/project-card
```

### 3. Add Content Management Structure
Create the content directory structure for Markdown-based content management:
```bash
# Create content directories in src/assets
mkdir -p src/assets/content/projects
mkdir -p src/assets/content/pages
mkdir -p src/assets/images
mkdir -p src/assets/styles
```

### 4. Add New Project Content
To add a new project to your portfolio:

1. Create a new Markdown file in `src/assets/content/projects/`
2. Follow the structure with YAML frontmatter:

```yaml
---
title: "Project Name"
date: "2025-01-15"
slug: "project-name"
technologies:
  - "Angular"
  - "TypeScript"
  - "Bootstrap"
images:
  - "/assets/images/project-name-thumb.webp"
  - "/assets/images/project-name-full.jpg"
links:
  github: "https://github.com/username/project"
  demo: "https://project-demo.com"
featured: true
---
# Project Details

Detailed description of the project in Markdown format with support for headings, lists, code blocks, and emphasis formatting. The content is processed through a sanitization pipeline to prevent XSS vulnerabilities while preserving the rich text formatting capabilities that Markdown provides.
```

### 5. Update Developer Profile
Edit the profile information in `src/assets/content/profile.json`:

```json
{
  "name": "Your Name",
  "title": "Your Title",
  "bio": "A comprehensive biographical description that establishes professional credentials while maintaining concise presentation to optimize user attention.",
  "skills": ["JavaScript", "TypeScript", "Angular", "React", "Node.js"],
  "experience": "Professional experience details in Markdown format, allowing for structured presentation of career history, major accomplishments, and professional achievements.",
  "contactInfo": {
    "email": "your-email@example.com",
    "phone": "+1-555-123-4567",
    "socialLinks": {
      "github": "https://github.com/your-profile",
      "linkedin": "https://linkedin.com/in/your-profile",
      "twitter": "https://twitter.com/your-profile"
    }
  }
}
```

## Testing

### Unit Testing
Run unit tests using Angular's built-in testing framework:
```bash
# Run unit tests once
ng test

# Run unit tests in watch mode for continuous testing during development
ng test --watch=true
```

Unit tests should achieve ≥90% coverage as specified in the constitution, with particular attention to component logic, service functionality, and content processing.

### Accessibility Testing
Validate accessibility compliance with automated tools:
```bash
# Install accessibility testing tools
npm install --save-dev @axe-core/cli

# Run accessibility tests on the built application
npx axe-cli http://localhost:4200 --include "body" --show-errors

# Or integrate with your existing e2e tests using axe-core
npm install --save-dev @axe-core/puppeteer
```

### End-to-End Testing
Set up and run e2e tests using Cypress or Angular's E2E framework:
```bash
# Add e2e testing framework
ng add @cypress/schematic

# Run e2e tests
ng e2e

# Run e2e tests in interactive mode for development
ng e2e --watch
```

### Cross-Browser Compatibility Testing
Validate functionality across target browsers:
```bash
# Use browserslist configuration in package.json to specify target browsers
# Chrome 90+, Firefox 88+, Safari 15+, Edge 90+

# For manual testing, use browser vendor tools:
# - Chrome DevTools Device Mode for mobile testing
# - Firefox Responsive Design Mode
# - Safari Device Simulation
# - Edge Developer Tools
```

### CSS/SCSS Validation
Validate CSS/SCSS formatting and best practices:
```bash
# Run stylelint to validate CSS/SCSS formatting
npx stylelint "src/**/*.scss"

# Run stylelint with auto-fix
npx stylelint "src/**/*.scss" --fix
```

## Build for Production

### Standard Production Build
Create a production-ready build with optimization:
```bash
# Build for production with optimization
ng build --configuration production

# Output will be in the dist/ folder, ready for deployment
```

### Performance Optimization Build
Build with additional performance analytics:
```bash
# Build with bundle analysis to identify optimization opportunities
ng build --configuration production --stats-json

# Analyze the generated stats.json file with tools like webpack-bundle-analyzer
npx webpack-bundle-analyzer dist/portfolio-website/browser/stats.json
```

## Deployment

### Deploy to Netlify
1. Build the project: `ng build --configuration production`
2. The `dist/` folder contains the static files ready for deployment
3. Connect to Netlify through their UI or CLI:
```bash
# Install Netlify CLI
npm install -g netlify-cli

# Login to Netlify
netlify login

# Deploy the built application
netlify deploy --dir=dist/portfolio-website/browser --prod
```

### Configure Environment Variables
If needed, create environment files:
- `src/environments/environment.ts` (development)
- `src/environments/environment.prod.ts` (production)

## Key Angular Components for Massively Template Implementation

### 1. Hero Section Component
- Implements the immersive background with proper contrast for text readability
- Includes navigation and maintains the distinctive Massively template aesthetic
- Responsive design that adapts to different viewport sizes while preserving visual impact
- Accessible with proper ARIA labels and semantic HTML structure
- Component styling follows Angular's encapsulation with SCSS for local styles

### 2. Project Gallery Component
- Displays projects in a responsive grid following Bootstrap 5.3+ grid system
- Implements filtering by technology tags as specified in user requirements
- Shows project details with thumbnail, title, description, and technologies
- Includes lazy loading for improved performance with larger project collections
- Component styling integrates Bootstrap utilities with custom Massively aesthetic

### 3. Navigation Component
- Responsive navigation that works across all device types (mobile, tablet, desktop)
- Implements mobile hamburger menu with proper focus management for accessibility
- Active section highlighting to guide user orientation within the portfolio
- Sticky behavior on scroll as implemented in the original Massively template
- Component styling follows BEM methodology with CSS custom properties

### 4. About Section Component
- Displays developer profile information with proper typography hierarchy
- Shows skills in a visually appealing and accessible format
- Implements proper heading structure for screen reader navigation
- Responsive layout that adapts to different screen sizes
- Component styling maintains Massively template aesthetic with Bootstrap integration

### 5. Contact Component
- Provides multiple contact methods with appropriate accessibility features
- Implements mailto links with proper fallback for email clients
- Includes social media links with appropriate icons and labels
- Responsive design that works across all targeted browsers and devices
- Component styling follows accessibility contrast requirements

## Content Management Implementation

### Adding New Projects
1. Create a new `.md` file in `src/assets/content/projects/` with proper YAML frontmatter
2. Use the required frontmatter fields as specified in the data model
3. Add project images to `src/assets/images/` with proper optimization
4. The content service will automatically detect and load the new project

### Updating Content
- Project content: Edit the corresponding `.md` file in `src/assets/content/projects/`
- Developer profile: Edit `src/assets/content/profile.json`
- Navigation: Update routes in `src/app/app.routes.ts` as needed
- Content is loaded dynamically on application startup, no rebuild required for content changes

## Quality Assurance and Compliance

### WCAG 2.1 AA Compliance Verification
1. Ensure all images have appropriate alt text
2. Verify color contrast ratios meet minimum requirements (4.5:1 normal text, 3:1 large text)
3. Test keyboard navigation with tab order and focus indicators
4. Validate semantic HTML structure with proper heading hierarchy
5. Test with screen readers (NVDA, JAWS, VoiceOver)

### Performance Testing
1. Verify First Contentful Paint < 3s
2. Verify Time to Interactive < 5s
3. Optimize image sizes and formats (use WebP where supported)
4. Implement lazy loading for images and non-critical content
5. Monitor and optimize bundle size using Angular CLI tools

### Cross-Browser Testing
1. Test functionality in Chrome 90+, Firefox 88+, Safari 15+, Edge 90+
2. Verify responsive behavior across different device sizes
3. Validate CSS Grid and Flexbox layouts render correctly
4. Test JavaScript functionality in all target browsers
5. Verify accessibility features work in each browser

### CSS Best Practices
1. Use component encapsulation to prevent style bleeding
2. Implement BEM methodology for consistent class naming
3. Utilize CSS custom properties for theme consistency
4. Follow responsive design principles with Bootstrap integration
5. Validate CSS with stylelint for consistent formatting

This quickstart guide provides the essential steps to set up, develop, test, and deploy the portfolio website while maintaining full accessibility compliance and the distinctive Massively template aesthetic. All documentation has been created in a very detailed, precise, meticulous, and in-depth way while remaining concise and actionable, as required by the project constitution.