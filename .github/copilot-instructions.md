# Copilot Instructions for Daria Portfolio

This document provides comprehensive guidance for coding agents working on this repository to minimize exploration time and avoid common pitfalls.

## High-Level Repository Information

### Summary
This is a personal portfolio website for Daria Kafler, a Junior Web Developer. The website showcases her projects, technical skills, and background. It's designed as a static website with modern responsive design, focusing on accessibility and clean presentation.

### Repository Details
- **Type**: Static portfolio website
- **Size**: Small (~20 files, minimal codebase)
- **Languages**: HTML5, CSS3, Vanilla JavaScript (ES6)
- **Target Runtime**: Modern web browsers, served via GitHub Pages
- **Framework**: None - pure HTML/CSS/JS
- **Dependencies**: Minimal (only shelljs for potential build scripts)
- **Deployment**: GitHub Pages with custom domain (dariakafler.com)

## Build and Validation Instructions

### Environment Setup
**Prerequisites**:
- Node.js v20.19.4+ and npm 10.8.2+
- Any modern web browser for testing
- Python 3 (for local development server)

**Always run these commands in order**:
1. `npm install` - Install minimal dependencies (takes ~6 seconds)
2. Validate your changes with HTML/CSS linters as described below

### Development Workflow
**Local Development**:
```bash
# Start local development server
python3 -m http.server 8000
# OR use any static file server
npx serve .
```
- Access the site at `http://localhost:8000`
- No build step required - changes are immediately visible on refresh
- No hot reload - manual refresh needed

### Validation Commands
**ALWAYS run these validation steps before committing**:

1. **HTML Validation** (Critical - fixes required):
```bash
npx htmlhint index.html
```
**Known Issues to Fix**:
- HTML tag names must be lowercase (H1 → h1)
- Duplicate class attributes on project sections
- Alt attributes must use double quotes, not single quotes
- Unclosed section tags
- SVG namespace elements may trigger warnings (safe to ignore)

2. **CSS Validation**:
```bash
npx stylelint "styles/*.css" --config-basedir .
```
Note: Requires stylelint config file for validation. Default validation may fail without config.

3. **Basic Syntax Check**:
```bash
# Check for common issues
grep -r "TODO\|FIXME\|HACK" --exclude-dir=node_modules .
```

### Deployment
- **No build process required** - static files are served directly
- Deployment is automatic via GitHub Pages when pushing to main branch
- Custom domain configured via CNAME file
- **Time**: Deployment takes 1-3 minutes after push

### Common Issues and Workarounds

1. **npm install warnings**: You'll see deprecation warnings for inflight and glob packages. These are safe to ignore as they come from shelljs dependency.

2. **HTML validation errors**: The current index.html has 16 validation errors that should be fixed:
   - Convert `<H1>` to `<h1>` (2 instances)
   - Remove duplicate `class` attributes on project sections (4 instances)  
   - Fix single quotes in alt attributes
   - Close unclosed `</section>` tag

3. **CSS Issues**: The CSS is generally clean but uses modern CSS features. Test in older browsers if broad compatibility is needed.

4. **JavaScript**: Minimal JS is embedded in HTML. The external scripts/app.js is mostly commented out and not used.

## Project Layout and Architecture

### Directory Structure
```
/
├── .github/
│   └── copilot-instructions.md  # This file
├── styles/
│   ├── assets/               # Images, icons, screenshots
│   │   ├── *.jpg, *.png     # Project screenshots and photos
│   │   └── *.svg            # Social media icons
│   └── style.css            # Main stylesheet (~800 lines)
├── scripts/
│   └── app.js              # Minimal JS (mostly unused)
├── index.html              # Main HTML file (~420 lines)
├── package.json            # Dependencies (minimal)
├── CNAME                   # GitHub Pages custom domain
├── README.md               # Brief project description
└── yarn.lock              # Dependency lock file
```

### Key Source Files

**index.html** (Main file - 420 lines):
- Self-contained HTML with embedded navigation JavaScript
- Responsive design with mobile-first approach  
- Semantic HTML structure: header, nav, sections for about/tech/projects/contact
- Inline SVG logo artwork
- JavaScript functions: `openNav()`, `closeNav()`, `backToTop()`, `scrollFunction()`

**styles/style.css** (800+ lines):
- CSS custom properties for consistent theming
- Mobile-first responsive design using clamp() functions
- Main color scheme: `--main-accent-color: #29F9FF`, `--secondary-accent-color: #FF0051`
- Flexbox and modern CSS layouts
- Font: 'Roboto Slab' from Google Fonts

### Architecture Notes
- **No bundling/compilation**: Files are served directly to browsers
- **No state management**: Static content only
- **No API calls**: All content is embedded in HTML
- **CSS organization**: Single file with organized sections by component
- **Assets**: All images are static files, no dynamic loading

### Validation Pipeline
**No formal CI/CD pipeline exists**, but you should manually run:
1. HTML validation (critical)
2. CSS syntax checking
3. Visual testing in browser
4. Check responsive design at different screen sizes

### Key Dependencies
- **shelljs**: Only dependency, likely unused (can be removed)
- **No build tools**: No webpack, vite, or similar
- **No test framework**: No automated tests exist
- **No linting config**: Would benefit from eslint/prettier setup

### Important File Locations
- **Main content**: All in `index.html`
- **Styling**: `styles/style.css` (imports Google Fonts)
- **Images**: `styles/assets/` (project screenshots, icons, profile images)
- **Configuration**: `package.json` (minimal), `CNAME` (domain config)

### GitHub Pages Configuration
- Serves from root directory
- Custom domain: dariakafler.com
- No Jekyll processing (plain HTML)
- Direct file serving - no build step

### Best Practices for Changes
1. **Always test locally** before committing
2. **Fix HTML validation errors** - they're actual issues, not false positives  
3. **Maintain responsive design** - test on mobile and desktop
4. **Preserve existing CSS custom properties** for consistency
5. **Keep dependencies minimal** - this is intentionally a simple static site
6. **Use semantic HTML** - important for accessibility
7. **Optimize images** before adding new assets (existing ones are well-optimized)

### Performance Considerations
- Site loads quickly as it's static HTML/CSS
- Images are dithered/optimized
- Minimal JavaScript footprint
- External dependencies: only Google Fonts

---

**Trust these instructions**: The information above is comprehensive and tested. Only search for additional information if you find errors in these instructions or need details not covered here.