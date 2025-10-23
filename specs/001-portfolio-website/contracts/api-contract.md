# API Contract: Portfolio Website

## Overview
The portfolio website is a static site that loads content from local JSON/Markdown files. There is no backend API server required, as all content is served statically.

## Content Endpoints

### GET /assets/content/profile.json
**Purpose**: Retrieve developer profile information

**Response**:
```json
{
  "name": "string",
  "title": "string",
  "bio": "string",
  "skills": ["string"],
  "experience": "string",
  "contactInfo": {
    "email": "string",
    "socialLinks": {
      "github": "string (optional)",
      "linkedin": "string (optional)",
      "twitter": "string (optional)"
    }
  }
}
```

### GET /assets/content/projects/{slug}.md
**Purpose**: Retrieve a specific project's markdown content with YAML frontmatter

**Response**:
Raw markdown content with YAML frontmatter containing:
- title: string
- date: string (YYYY-MM-DD)
- slug: string
- technologies: array of strings
- images: array of image paths
- links: object with github and demo URLs
- featured: boolean
- body: markdown content

### GET /assets/content/projects/
**Purpose**: Retrieve list of all projects (via directory listing)

**Response**:
Array of project metadata objects:
```json
[
  {
    "title": "string",
    "date": "string (YYYY-MM-DD)",
    "slug": "string",
    "technologies": ["string"],
    "featured": "boolean"
  }
]
```

## Client-Side Services

### ContentService
**Purpose**: Load and parse content from markdown/json files

**Methods**:
- `getProfile(): Promise<Profile>` - Load developer profile
- `getProjects(): Promise<Project[]>` - Load all projects
- `getProject(slug: string): Promise<Project>` - Load specific project
- `getFeaturedProjects(): Promise<Project[]>` - Load only featured projects

### AccessibilityService
**Purpose**: Manage accessibility features and WCAG compliance

**Methods**:
- `setHighContrastMode(enabled: boolean): void` - Toggle high contrast mode
- `getCurrentContrastMode(): boolean` - Get current contrast mode
- `setKeyboardNavigation(enabled: boolean): void` - Manage keyboard navigation
- `announce(message: string): void` - Screen reader announcements

## Error Handling

### Content Loading Errors
- If content fails to load, display appropriate fallback content
- For missing images, show placeholder with alt text
- For missing profile data, show default values

### HTTP Status Codes for Static Assets
- 200: Content loaded successfully
- 404: Content not found (should handle gracefully with fallback)
- 500: Server error (for hosted content, though static sites rarely encounter this)

## Validation Rules

### Profile Validation
- `name` must be 2-50 characters
- `email` must be valid email format
- `skills` array must contain 1-15 items

### Project Validation
- `title` must be 2-100 characters
- `slug` must be URL-friendly
- `technologies` array must contain 1-10 items
- `images` must be valid image file paths
- `featured` defaults to false

## Request/Response Format
All requests and responses use standard HTTP protocols with appropriate MIME types. Markdown files are served with `text/markdown` content-type, while JSON files use `application/json`.

## Cross-Origin Resource Sharing (CORS)
Since this is a static site, CORS policies depend on the hosting provider. For development, ensure assets can be loaded from the same origin.