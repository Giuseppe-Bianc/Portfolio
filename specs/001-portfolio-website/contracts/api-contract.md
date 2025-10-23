# API Contract: Portfolio Website

## Overview
The portfolio website is a static site that loads content from local JSON/Markdown files. There is no backend API server required, as all content is served statically. The contract defines the interface between the Angular application and the static content files, specifying the expected format and structure of data assets, and outlining the patterns for component styling with CSS/SCSS integration.

## Content Endpoints (Static Asset Contracts)

### GET /assets/content/profile.json
**Purpose**: Retrieve developer profile information with comprehensive details for about section

**Response Format**:
```json
{
  "name": "string (2-50 chars)",
  "title": "string (2-50 chars)", 
  "bio": "string (100-500 chars, Markdown format)",
  "skills": ["string (1-25 chars)"],
  "experience": "string (Markdown format)",
  "contactInfo": {
    "email": "string (RFC 5322 valid email)",
    "phone": "string (optional, international format)",
    "socialLinks": {
      "github": "string (optional, HTTPS URL)",
      "linkedin": "string (optional, HTTPS URL)",
      "twitter": "string (optional, HTTPS URL)",
      "other": "object (optional, custom links with labels)"
    }
  }
}
```

**Validation Requirements**:
- All email addresses must pass RFC 5322 validation
- Skills array must contain 1-15 items
- Name must be 2-50 characters
- Bio must be 100-500 characters (plain text)

### GET /assets/content/projects/{slug}.md
**Purpose**: Retrieve a specific project's markdown content with YAML frontmatter, providing rich content for project detail views

**Response Format**:
Raw markdown content with YAML frontmatter containing:
- `title`: string (2-100 chars, no HTML)
- `date`: string (YYYY-MM-DD format, not in future)
- `slug`: string (URL-friendly with alphanumeric and hyphens)
- `technologies`: array of strings (1-10 items, 1-30 chars each)
- `images`: array of image paths (valid asset references)
- `links`: object with `github`, `demo` URLs (HTTPS format)
- `featured`: boolean (defaults to false)
- `longDescription`: markdown content (sanitized HTML)

**Validation Requirements**:
- All dates must be in the past
- Technologies array must have 1-10 items
- All URLs must be valid HTTPS links
- Slug must be unique across projects

### GET /assets/content/projects/
**Purpose**: Retrieve list of all projects with metadata for gallery display, enabling dynamic project listing

**Response Format**:
Array of project metadata objects:
```json
[
  {
    "id": "string (generated from slug)",
    "title": "string (2-100 chars)",
    "date": "string (YYYY-MM-DD)",
    "slug": "string (URL-friendly)",
    "description": "string (max 200 chars, plain text)",
    "technologies": ["string"],
    "featured": "boolean",
    "images": ["string (image paths)"]
  }
]
```

**Validation Requirements**:
- Each project must have a unique slug
- All dates must be in the past
- Technology counts must be 1-10 items per project

## Client-Side Services Interface

### ContentService Contract
**Purpose**: Define the interface for loading and parsing content from markdown/json files with proper error handling and caching

**Methods Specification**:

#### getProfile(): Promise<DeveloperProfile>
- **Purpose**: Load developer profile information from static JSON file
- **Success Response**: DeveloperProfile object matching the schema above
- **Error Handling**: Returns default profile object if content fails to load, logs error for observability
- **Caching**: Implements in-memory caching after initial load to optimize performance
- **Validation**: Validates all fields according to schema requirements before returning

#### getProjects(): Promise<Project[]>
- **Purpose**: Load all projects for gallery display and navigation
- **Success Response**: Array of Project objects with complete metadata
- **Error Handling**: Returns empty array if content fails to load, with appropriate fallback behavior
- **Caching**: Implements in-memory caching with TTL mechanism for performance optimization
- **Sorting**: Returns projects sorted by date (newest first) as default ordering

#### getProject(slug: string): Promise<Project>
- **Purpose**: Load specific project by slug for detail views
- **Success Response**: Single Project object with full content including longDescription
- **Error Handling**: Returns 404-like error object if project not found, with navigation fallback
- **Caching**: Leverages in-memory cache mechanism for improved performance
- **Content Processing**: Sanitizes Markdown content to prevent XSS while preserving formatting

#### getFeaturedProjects(): Promise<Project[]>
- **Purpose**: Load only featured projects for homepage highlighting
- **Success Response**: Array of Project objects marked with featured: true
- **Error Handling**: Returns empty array if content fails to load, with appropriate UI fallback
- **Validation**: Ensures no more than 3 projects are returned as featured by default

### AccessibilityService Contract
**Purpose**: Manage accessibility features and WCAG 2.1 AA compliance with user preferences and system capabilities

**Methods Specification**:

#### setHighContrastMode(enabled: boolean): void
- **Purpose**: Toggle high contrast mode for users with visual impairments
- **Implementation**: Adds/removes CSS class for high contrast theme
- **Persistence**: Saves user preference to localStorage for consistency
- **Validation**: Ensures sufficient color contrast ratios (≥4.5:1 for normal text, ≥3:1 for large text)

#### getCurrentContrastMode(): boolean
- **Purpose**: Get current contrast mode state from user preferences
- **Implementation**: Reads contrast preference from localStorage
- **Default**: Returns false if no preference is set
- **Accessibility**: Updates ARIA attributes based on current mode

#### setKeyboardNavigation(enabled: boolean): void
- **Purpose**: Manage keyboard navigation enhancements for accessibility
- **Implementation**: Updates focus indicators and navigation patterns
- **Default Behavior**: Enabled by default for accessibility compliance
- **Focus Management**: Ensures logical tab order and proper focus indicators

#### announce(message: string): void
- **Purpose**: Provide screen reader announcements for dynamic content updates
- **Implementation**: Uses live regions for non-visual alerts
- **Accessibility**: Follows ARIA best practices for screen reader notifications
- **Timing**: Implements appropriate delays for reliable announcement delivery

## CSS/SCSS Integration Contract

### Component Styling Standards
**Purpose**: Define the contract for CSS/SCSS usage following Angular and Bootstrap 5.3+ integration patterns

#### Component SCSS Structure
- **Encapsulation**: Each component uses Angular's view encapsulation to maintain local styles
- **File Naming**: Component SCSS files follow the pattern `component-name.component.scss`
- **BEM Methodology**: Class names follow Block__Element--Modifier pattern for consistency
- **Custom Properties**: CSS variables for theme consistency defined as `--component-name-property`
- **Bootstrap Integration**: Components use Bootstrap utility classes where appropriate for consistency

#### Global Styling Standards
- **Custom Properties**: Global CSS variables defined in `src/styles.scss` with `--global-` prefix
- **Responsive Design**: Follow Bootstrap 5.3+ breakpoints (xs, sm, md, lg, xl, xxl) in media queries
- **Modern CSS Features**: Utilize CSS Grid and Flexbox for complex layouts with fallbacks
- **Accessibility Colors**: Color values maintain WCAG 2.1 AA contrast ratios
- **Massively Aesthetic**: Custom overrides preserve the original Massively template visual identity

#### Style Validation Requirements
- **Naming Consistency**: Class names follow kebab-case convention
- **No Inline Styles**: All styling implemented through CSS/SCSS files, not inline styles
- **Responsive Behavior**: All components adapt appropriately to different screen sizes
- **Accessibility Compliance**: Color contrast ratios and focus indicators meet WCAG 2.1 AA standards
- **Performance**: CSS is optimized for minimal size and efficient rendering

## Error Handling Contracts

### Content Loading Errors
- If content fails to load, display appropriate fallback content with graceful degradation
- For missing images, show placeholder with alt text and proper dimensions to prevent layout shift
- For missing profile data, show default values while maintaining layout integrity
- All error states must be accessible and provide clear user feedback for navigation

### HTTP Status Considerations (for hosting)
- 200: Content loaded successfully with proper validation
- 404: Content not found (should handle gracefully with fallback and user guidance)
- 500: Server error (for hosted content, though static sites rarely encounter this)

## Validation Rules Contract

### Profile Validation
- `name` must be 2-50 characters to ensure proper display in navigation and headers
- `email` must be valid RFC 5322 email format to ensure contact functionality
- `skills` array must contain 1-15 items to maintain visual balance and readability
- All content must pass sanitization to prevent XSS while preserving intended formatting

### Project Validation
- `title` must be 2-100 characters with no HTML tags to prevent injection and ensure display consistency
- `slug` must be URL-friendly (alphanumeric, hyphens only) and unique across all projects
- `technologies` array must contain 1-10 items with each technology name being 1-30 characters
- `images` must reference valid image file paths with proper extensions (.jpg, .png, .webp, .gif)
- `date` must be in valid YYYY-MM-DD format and not in the future

### Security Validation
- All Markdown content must be sanitized using DOMPurify to prevent XSS attacks
- URL validation must ensure proper HTTPS protocol for external links
- File paths must be validated to prevent directory traversal vulnerabilities
- All user-facing content must be properly encoded for safe display in HTML

## Request/Response Format
All requests and responses follow standard HTTP protocols with appropriate MIME types. Markdown files are served with `text/markdown` content-type during development, while the Angular application processes them to `text/html` with proper sanitization. JSON files use `application/json` with UTF-8 encoding. CSS/SCSS is compiled to CSS following modern browser compatibility standards.

## Cross-Origin Resource Sharing (CORS)
Since this is a static site, CORS policies depend on the hosting provider. For development, ensure assets can be loaded from the same origin.

## Caching Strategy
- ContentService implements in-memory caching with TTL for all content loaded from static files
- Cache invalidation occurs on application reload or explicitly when content is updated
- Fallback mechanisms ensure availability when cache is cleared or unavailable
- Performance optimization through caching must not compromise content freshness requirements

## Observability Integration
- Content loading errors must be reported to observability tools as specified in FR-010
- Performance metrics for content loading times must be captured and reported
- User interaction events related to content consumption must be tracked for analytics
- Accessibility usage patterns should be monitored to improve the user experience
- CSS/SCSS performance metrics tracked through Web Vitals and Lighthouse scores