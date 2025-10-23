# Quickstart Guide: Portfolio Website

## Prerequisites

- Node.js (v18.13.0 or later)
- npm (v9.0.0 or later) or yarn
- Angular CLI (v20.3.6 or later)
- Git

## Setup Instructions

### 1. Clone and Initialize
```bash
# Clone the repository
git clone <repository-url>
cd <repository-name>

# Install dependencies
npm install
# OR if using yarn
yarn install
```

### 2. Install Angular CLI (if not already installed)
```bash
npm install -g @angular/cli@latest
```

### 3. Install Bootstrap
```bash
npm install bootstrap@^5.3.8
```

### 4. Configure Bootstrap in Angular
Add Bootstrap to your `angular.json` file:

```json
{
  "projects": {
    "Portfolio": {
      "architect": {
        "build": {
          "builder": "@angular/build:application",
          "options": {
            "styles": [
              "node_modules/bootstrap/dist/css/bootstrap.min.css",
              "src/styles.css"
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

Or import Bootstrap in your `src/styles.css`:

```css
/* Import Bootstrap */
@import '~bootstrap/dist/css/bootstrap.min.css';

/* Your custom styles */
```

## Development Workflow

### 1. Start Development Server
```bash
ng serve
# The application will be available at http://localhost:4200
```

### 2. Add New Project Content
1. Create a new Markdown file in `src/assets/content/projects/`
2. Follow the structure with YAML frontmatter:

```yaml
---
title: "Project Name"
date: "2025-01-15"
slug: "project-name"
technologies:
  - "Technology 1"
  - "Technology 2"
images:
  - "/assets/images/project-thumb.jpg"
links:
  github: "https://github.com/username/project"
  demo: "https://project-demo.com"
featured: true
---
# Project Details

Detailed description of the project in Markdown format...
```

### 3. Update Developer Profile
Edit the profile information in `src/assets/content/profile.json`:

```json
{
  "name": "Your Name",
  "title": "Your Title",
  "bio": "Your bio...",
  "skills": ["Skill 1", "Skill 2", "Skill 3"],
  "experience": "Your experience...",
  "contactInfo": {
    "email": "your-email@example.com",
    "socialLinks": {
      "github": "https://github.com/your-profile",
      "linkedin": "https://linkedin.com/in/your-profile"
    }
  }
}
```

## Testing

### Run Unit Tests
```bash
ng test
```

### Run End-to-End Tests
```bash
ng e2e
```

### Accessibility Testing
```bash
# Using axe-core for accessibility testing
npm install --save-dev @axe-core/puppeteer
# Run the accessibility tests with your e2e suite
```

## Build for Production

```bash
ng build --configuration production
# Output will be in the dist/ folder
```

## Deployment

### Deploy to Netlify
1. Build the project: `ng build --configuration production`
2. The `dist/` folder contains the static files ready for deployment
3. Connect to Netlify through their UI or CLI

### Configure Environment Variables
If needed, create environment files:
- `src/environments/environment.ts` (development)
- `src/environments/environment.prod.ts` (production)

## Key Angular Components

### 1. Project Gallery Component
- Displays projects in a responsive grid
- Filters projects by technology
- Shows project details on click

### 2. Hero Section Component
- Displays the immersive background
- Includes navigation and title

### 3. About Section Component
- Displays developer profile information
- Shows skills and experience

### 4. Contact Component
- Provides contact methods via mailto links
- Includes social media links

## Content Management

### Adding New Projects
1. Create a new `.md` file in `src/assets/content/projects/`
2. Use the YAML frontmatter format
3. Add project images to `src/assets/images/`
4. The content service will automatically load the new project

### Updating Content
- Project content: Edit the corresponding `.md` file in `src/assets/content/projects/`
- Developer profile: Edit `src/assets/content/profile.json`
- Navigation: Update routes in `src/app/app.routes.ts`

This quickstart guide provides the essential steps to set up, develop, test, and deploy the portfolio website while maintaining accessibility and the Massively template aesthetic.