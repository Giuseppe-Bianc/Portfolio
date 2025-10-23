# Portfolio Project - QWEN Context

## Project Overview

The Portfolio project is an Angular application built with Angular CLI version 20.3.6. It's a web-based portfolio application that serves as a platform to showcase personal or professional work. The project uses modern Angular features including component-based architecture, reactive programming with RxJS, and follows Angular's best practices.

## Key Technologies

- **Angular 20.3.0**: The primary frontend framework
- **TypeScript**: Strongly typed programming language that compiles to JavaScript
- **Bootstrap 5.3.8**: CSS framework for responsive design
- **RxJS**: Reactive programming library for handling asynchronous operations
- **Angular CLI**: Command line tool for managing the Angular project

## Folder Structure

```
Portfolio/
├── src/                    # Source files
│   ├── app/               # Main application components
│   │   ├── app.ts         # Main application component
│   │   ├── app.html       # Application template
│   │   ├── app.css        # Application styles
│   │   ├── app.config.ts  # Application configuration
│   │   ├── app.routes.ts  # Application routes
│   │   └── app.spec.ts    # Application tests
│   ├── index.html         # Main HTML file
│   ├── main.ts            # Application entry point
│   └── styles.css         # Global styles
├── public/                # Public assets
├── angular.json           # Angular CLI configuration
├── package.json           # Project dependencies and scripts
├── tsconfig.json          # TypeScript configuration
├── tsconfig.app.json      # TypeScript app-specific configuration
└── tsconfig.spec.json     # TypeScript testing configuration
```

## Building and Running

### Development Server
To run the development server:
```bash
npm start
# or
ng serve
```
The application will be available at `http://localhost:4200/` and automatically reloads when source files are modified.

### Production Build
To build the project for production:
```bash
npm run build
# or
ng build
```
Build artifacts are stored in the `dist/` directory with optimizations for performance.

### Additional Scripts
- Watch mode: `npm run watch`
- Unit tests: `npm run test` or `ng test`
- End-to-end tests: `ng e2e` (requires additional setup)

## Development Conventions

### Code Scaffolding
Generate new components using:
```bash
ng generate component component-name
```

Other available schematics include:
- Components: `ng generate component <name>`
- Services: `ng generate service <name>`
- Pipes: `ng generate pipe <name>`
- Directives: `ng generate directive <name>`

### TypeScript Configuration
The project uses strict TypeScript settings:
- Strict type checking enabled
- Experimental decorators enabled
- Target: ES2022
- Import helpers enabled

### Styling
- Global styles in `src/styles.css`
- Component-specific styles in component files
- Bootstrap CSS framework included for responsive design
- Modern CSS features (CSS Grid, Flexbox, custom properties)

### Testing
The project includes:
- Jasmine for unit testing
- Karma test runner
- Code coverage reporting
- Angular's testing utilities

## Routing
The application uses Angular's router with:
- Configured in `app.routes.ts`
- Router outlet in the main template
- Lazy loading capabilities for feature modules

## Architecture
- Component-based architecture
- Signal-based state management (Angular's new reactivity system)
- Reactive programming with RxJS
- Modular application structure
- Dependency injection for services