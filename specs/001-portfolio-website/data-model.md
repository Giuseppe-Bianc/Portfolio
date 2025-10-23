# Data Model: Portfolio Website

## Entities

### Portfolio Project
**Description**: A work sample that includes title, description, technologies used, images, and links to live demos or source code

**Fields**:
- `id` (string): Unique identifier for the project
- `title` (string): The project's display title
- `date` (string, YYYY-MM-DD): The date of project completion
- `slug` (string): URL-friendly identifier for the project
- `description` (string): Brief description of the project
- `technologies` (string[]): Array of technologies used in the project
- `images` (string[]): Array of image paths for the project
- `links` (object): Object containing links to external resources
  - `github` (string, optional): URL to GitHub repository
  - `demo` (string, optional): URL to live demo
- `featured` (boolean): Whether this project is featured on the homepage
- `longDescription` (string): Detailed project description in Markdown format

**Validation Rules**:
- `title` must be 2-100 characters
- `slug` must be URL-friendly (alphanumeric, hyphens only)
- `technologies` array must contain 1-10 items
- `featured` defaults to false
- `images` must be valid image file paths

### Developer Profile
**Description**: Information about the developer including bio, skills, experience, and contact information

**Fields**:
- `name` (string): The developer's full name
- `title` (string): Professional title or role
- `bio` (string): Brief biographical information
- `skills` (string[]): Array of professional skills
- `experience` (string): Professional experience details
- `contactInfo` (object): Contact information
  - `email` (string): Email address
  - `socialLinks` (object): Social media and professional links
    - `github` (string, optional): GitHub profile URL
    - `linkedin` (string, optional): LinkedIn profile URL
    - `twitter` (string, optional): Twitter profile URL
    - `other` (string, optional): Other professional links

**Validation Rules**:
- `name` must be 2-50 characters
- `skills` array must contain 1-15 items
- `email` must be a valid email format

### Contact Method
**Description**: Ways for visitors to reach out to the developer (email, social media links)

**Fields**:
- `email` (string): Primary email for contact
- `socialLinks` (object[]): Array of social media links
  - `platform` (string): Name of the platform (e.g., "github", "linkedin")
  - `url` (string): URL to the profile
  - `label` (string): Accessible label for the link

**Validation Rules**:
- `email` must be a valid email format
- Each social link URL must be a valid URL format

## State Transitions

### Project Gallery
- **Loading State**: Gallery is initializing and content is being fetched
- **Loaded State**: Gallery displays projects with thumbnails, titles, descriptions, and technologies
- **Filtered State**: Gallery shows subset of projects based on filter criteria
- **Error State**: Gallery shows error message when content fails to load

### Navigation
- **Default State**: Navigation shows all available sections
- **Active State**: Current section is highlighted in navigation
- **Mobile State**: Navigation is collapsed behind a hamburger menu on small screens

## Relationships

- A **Developer Profile** has many **Portfolio Projects**
- Each **Portfolio Project** has associated **Contact Methods** for reaching the developer
- **Portfolio Projects** may link to external resources (GitHub, live demos)

## Content Structure

### Project Content Files
Projects are stored as Markdown files with YAML frontmatter in the `assets/content/projects/` directory:

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
  - "/assets/images/project1-thumb.jpg"
  - "/assets/images/project1-full.jpg"
links:
  github: "https://github.com/username/project"
  demo: "https://project-demo.com"
featured: true
---
# Project Description

Detailed project description in Markdown format...
```

### Developer Profile Content
The developer profile information is stored in a JSON file at `assets/content/profile.json`:

```json
{
  "name": "Developer Name",
  "title": "Senior Developer",
  "bio": "Brief biographical information...",
  "skills": ["JavaScript", "TypeScript", "Angular", "React"],
  "experience": "Professional experience details...",
  "contactInfo": {
    "email": "email@example.com",
    "socialLinks": {
      "github": "https://github.com/username",
      "linkedin": "https://linkedin.com/in/username",
      "twitter": "https://twitter.com/username"
    }
  }
}
```