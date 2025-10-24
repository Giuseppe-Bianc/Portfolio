# Data Model: Portfolio Website

## Entities

### Portfolio Project
**Description**: A work sample that includes title, description, technologies used, images, and links to live demos or source code

**Fields**:
- `id` (string): Unique identifier for the project, generated from the slug field for internal routing and tracking purposes
- `title` (string): The project's display title, must be between 2-100 characters for proper display in gallery views and SEO purposes
- `date` (string, YYYY-MM-DD): The date of project completion, used for chronological ordering and timeline presentation
- `slug` (string): URL-friendly identifier for the project, must be unique and contain only alphanumeric characters and hyphens to ensure proper routing
- `description` (string): Brief description of the project, limited to 200 characters maximum for gallery display consistency
- `technologies` (string[]): Array of technologies used in the project, containing 1-10 items to provide meaningful technical context without overwhelming users
- `images` (string[]): Array of image paths for the project, referencing optimized image files in the assets directory for consistent loading performance
- `links` (object): Object containing links to external resources with the following properties:
  - `github` (string, optional): URL to GitHub repository, validated as a proper HTTPS URL format
  - `demo` (string, optional): URL to live demo, validated as a proper HTTPS URL format
  - `additional` (string[], optional): Array of additional resource URLs related to the project
- `featured` (boolean): Whether this project is featured on the homepage, defaults to false, used for highlighting priority projects
- `longDescription` (string): Detailed project description in Markdown format, allowing for rich text formatting while maintaining security through sanitization

**Validation Rules**:
- `title` must be 2-100 characters with no HTML tags to prevent injection and ensure display consistency
- `slug` must be URL-friendly (alphanumeric, hyphens only) and unique across all projects to prevent routing conflicts
- `technologies` array must contain 1-10 items with each technology name being 1-30 characters
- `featured` defaults to false but only one project should be featured at a time in specific contexts
- `images` must reference valid image file paths with proper extensions (.jpg, .png, .webp, .gif) that exist in the assets directory
- `date` must be in valid YYYY-MM-DD format and not in the future
- `description` must not exceed 200 characters and should be plain text without HTML formatting

### Developer Profile
**Description**: Information about the developer including bio, skills, experience, and contact information

**Fields**:
- `name` (string): The developer's full name, displayed prominently in the header and about section
- `title` (string): Professional title or role, used for professional identity and SEO purposes
- `bio` (string): Brief biographical information, optimized for 2-3 sentences to maintain visitor engagement
- `skills` (string[]): Array of professional skills, limited to 1-15 items to maintain visual balance and readability
- `experience` (string): Professional experience details in Markdown format, allowing for structured presentation of career history
- `contactInfo` (object): Contact information with nested properties for organized access:
  - `email` (string): Email address in proper RFC 5322 format for primary communication
  - `phone` (string, optional): Phone contact in international format, with proper formatting validation
  - `socialLinks` (object): Professional social media and networking links organized for easy access:
    - `github` (string, optional): GitHub profile URL in proper HTTPS format
    - `linkedin` (string, optional): LinkedIn profile URL in proper HTTPS format
    - `twitter` (string, optional): Twitter/X profile URL in proper HTTPS format
    - `other` (object, optional): Additional professional links with custom display labels

**Validation Rules**:
- `name` must be 2-50 characters to ensure proper display in navigation and headers
- `skills` array must contain 1-15 items with each skill name being 1-25 characters
- `email` must be a valid RFC 5322 email format to ensure contact functionality
- `bio` must be between 100-500 characters to provide sufficient information without overwhelming users
- `title` must be between 2-50 characters for professional presentation
- `socialLinks` URLs must be properly formatted HTTPS URLs with appropriate domain validation

### Contact Method
**Description**: Ways for visitors to reach out to the developer (email, social media links)

**Fields**:
- `email` (string): Primary email for contact, validated as a proper RFC 5322 email format
- `socialLinks` (object[]): Array of social media links with structured format for consistent presentation:
  - `platform` (string): Name of the platform (e.g., "github", "linkedin", "twitter", "codepen") for icon selection and accessibility
  - `url` (string): Validated URL to the profile, ensuring proper HTTPS protocol
  - `label` (string): Accessible label for the link that provides context for screen reader users
  - `icon` (string): CSS class name or path to icon for consistent visual presentation
  - `priority` (number): Display priority for contact methods, with lower numbers displayed first

**Validation Rules**:
- `email` must be a valid RFC 5322 email format with proper domain validation
- Each social link URL must be a valid HTTPS URL with proper domain structure
- `platform` must be one of the predefined valid platform names for consistent icon display
- `label` must be 5-50 characters to provide meaningful accessibility information
- `priority` must be a positive integer with lower values displayed first in the UI

## State Transitions

### Project Gallery
- **Loading State**: Gallery is initializing and content is being fetched from Markdown files; displays skeleton loading UI to maintain perceived performance and user engagement
- **Loaded State**: Gallery displays projects with thumbnails, titles, descriptions, and technologies using responsive grid layout; implements lazy loading for improved performance
- **Filtered State**: Gallery shows subset of projects based on filter criteria (technology tags, featured status, date range); maintains responsive behavior and preserves original layout patterns
- **Error State**: Gallery shows error message when content fails to load with appropriate fallback content; provides retry mechanism for failed requests
- **Empty State**: Gallery displays appropriate message when no projects match current filters; includes reset filter option and fallback display

### Navigation
- **Default State**: Navigation shows all available sections with proper active state indication; implements accessibility features for keyboard navigation
- **Active State**: Current section is highlighted in navigation with visual indicators; maintains focus management for accessibility
- **Mobile State**: Navigation is collapsed behind a hamburger menu on small screens, with slide-out functionality and proper focus trapping for accessibility
- **Sticky State**: Navigation becomes fixed at the top of the viewport during scrolling, with appropriate z-index management and CSS transitions

## Relationships

- A **Developer Profile** has many **Portfolio Projects**, creating a one-to-many relationship that organizes the portfolio content hierarchically
- Each **Portfolio Project** has associated **Contact Methods** for reaching the developer, providing multiple communication pathways
- **Portfolio Projects** may link to external resources (GitHub, live demos), creating external reference relationships while maintaining data integrity
- **Developer Profile** connects to external social platforms through **Contact Methods**, establishing the professional network integration

## Content Structure

### Project Content Files
Projects are stored as Markdown files with YAML frontmatter in the `src/assets/content/projects/` directory, following the Jekyll-style metadata format:

```yaml
---
title: "Project Title"
date: "2025-01-15"
slug: "project-title"
technologies:
  - "Angular"
  - "TypeScript"
  - "Bootstrap"
images:
  - "/assets/images/project/project1-thumb.webp"
  - "/assets/images/project/project1-full.jpg"
links:
  github: "https://github.com/username/project"
  demo: "https://project-demo.com"
featured: true
---
# Project Description

Detailed project description in Markdown format with support for headers, lists, code blocks, and emphasis formatting. The content is processed through a sanitization pipeline to prevent XSS vulnerabilities while preserving the rich text formatting capabilities that Markdown provides.
```

### Developer Profile Content
The developer profile information is stored in a JSON file at `src/assets/content/profile.json` with the following structure:

```json
{
  "name": "Developer Name",
  "title": "Senior Developer",
  "bio": "Brief biographical information with sufficient detail to establish professional credentials while maintaining concise presentation to user attention.",
  "skills": ["JavaScript", "TypeScript", "Angular", "React", "Node.js"],
  "experience": "Professional experience details in Markdown format, allowing for structured presentation of career history, major accomplishments, and professional achievements.",
  "contactInfo": {
    "email": "email@example.com",
    "phone": "+1-555-123-4567",
    "socialLinks": {
      "github": "https://github.com/username",
      "linkedin": "https://linkedin.com/in/username",
      "twitter": "https://twitter.com/username"
    }
  }
}
```

## CSS/SCSS Architecture

### Component Styling Pattern
- Each component uses CSS with Angular's encapsulation for local styles
- Global styles defined in main CSS files with Bootstrap 5.3+ integration
- Custom properties (CSS variables) for theme consistency and maintainability
- Responsive design implemented using Bootstrap grid system and custom media queries where needed
- Follows BEM methodology for class naming consistency

### Massively Template Customization
- Preserves original Massively template aesthetic through custom CSS
- Integrates with Bootstrap 5.3+ while maintaining visual identity
- Uses modern CSS features (Grid, Flexbox) for layout where appropriate
- Implements proper CSS encapsulation to prevent style bleeding between components