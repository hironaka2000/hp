# CLAUDE.md

This file provides guidance for AI assistants working on this repository.

## Project Overview

This is a **static HTML/CSS web hosting project** deployed via GitHub Pages. It serves as a public homepage portfolio containing multiple standalone single-page websites, all written in Japanese and English.

**Repository:** `hironaka2000/hp`
**Hosting:** GitHub Pages (auto-deployed from `master` branch)
**Live URL:** Deployed via GitHub Actions at the user's GitHub Pages endpoint

## Repository Structure

```
hp/
├── .github/
│   └── workflows/
│       └── static.yml          # GitHub Actions deployment pipeline
├── index.html                  # AI-in-Education presentation (Reveal.js)
├── coffee-shop-light.html      # Coffee shop website (SORA COFFEE)
├── seimei-gakuen-highschool.html  # High school institutional website
├── README.md                   # Minimal project description
└── Gemini_Generated_Image_atmtzeatmtzeatmt (1).png  # Image asset
```

## Pages / Sites

### 1. `index.html` — AI Education Presentation
- **Framework:** Reveal.js 5.0.4 (via CDN)
- **Topic:** "教育業界におけるAI活用" (AI Application in Education)
- **Format:** Multi-slide presentation with fragments and transitions
- **Language:** Japanese

### 2. `coffee-shop-light.html` — Coffee Shop Website
- **Name:** SORA COFFEE / そらコーヒー
- **Theme:** Modern dark design with warm orange/peach accents
- **Design features:** Fixed nav, hero animations, glassmorphism, CSS variables
- **Fonts:** Playfair Display, Noto Sans JP, Quicksand (Google Fonts)

### 3. `seimei-gakuen-highschool.html` — High School Website
- **Name:** 清明学園高等学校 (Seimei Gakuen High School)
- **Theme:** Professional light theme with navy blue and gold
- **Design features:** Fixed header, fade-in animations, responsive layout
- **Fonts:** Noto Serif JP, Zen Kaku Gothic New (Google Fonts)

## Technology Stack

- **Languages:** HTML5, CSS3 (inline in HTML files)
- **JavaScript:** Only via CDN (Reveal.js for presentations)
- **No build tools** — no npm, no webpack, no compilation step
- **No backend** — purely static
- **No testing framework**

## Development Workflow

### Local Preview
Since this is pure static HTML, open files directly in a browser:
```bash
open index.html
open coffee-shop-light.html
open seimei-gakuen-highschool.html
```
Or serve locally with any static server:
```bash
python3 -m http.server 8080
# Then visit http://localhost:8080
```

### Deployment
Deployment is fully automated via GitHub Actions:
- Push to `master` branch → triggers `.github/workflows/static.yml`
- Workflow uploads the entire repo root as a GitHub Pages artifact
- No manual deployment steps needed

### Branch Strategy
- `master` — production branch, auto-deploys to GitHub Pages
- Feature branches — use `claude/<description>` naming convention for AI-assisted work
- Merge feature branches into `master` via pull requests

## Code Conventions

### HTML
- Use double quotes for attributes
- Declare `charset="UTF-8"` and viewport meta tag in every HTML file
- Each HTML file is self-contained (styles inline in `<style>` tags)
- No external JavaScript files — CDN links only

### CSS (inline in `<style>` blocks)
- **CSS custom properties** for all colors and repeated values:
  ```css
  :root {
    --bg-dark: #0a0a0a;
    --accent-orange: #ff6b35;
  }
  ```
- **Naming conventions:** kebab-case for class names, semantic color names for variables
- **Layout:** CSS Grid and Flexbox preferred
- **Responsiveness:** Use `clamp()`, viewport units, and `@media` queries
- **Animations:** Define with `@keyframes`, apply via `animation` shorthand
- **Modern features allowed:** `backdrop-filter`, CSS variables, `clamp()`, custom properties

### Design Patterns
- Each standalone HTML file includes all its CSS inline in a `<style>` block
- No shared stylesheets — each page is fully independent
- Japanese-language content with occasional English headings/labels
- Responsive design with mobile-first approach

## CI/CD

**Workflow:** `.github/workflows/static.yml`

```
Trigger: push to master | manual dispatch
  → checkout repository
  → configure GitHub Pages
  → upload artifact (entire repo root)
  → deploy to GitHub Pages
```

**Permissions required:**
- `contents: read`
- `pages: write`
- `id-token: write`

**Concurrency:** Only one deployment runs at a time; in-progress runs complete before new ones start.

## Key Constraints

1. **No build pipeline** — Do not introduce npm packages, build tools, or compilation steps without explicit user request
2. **Self-contained files** — Each HTML file must work standalone; do not split CSS into separate files unless asked
3. **CDN-only dependencies** — External libraries must be loaded from CDNs (no local installs)
4. **Japanese content** — Content is primarily in Japanese; preserve Japanese text accurately
5. **No tests** — There is no testing infrastructure; do not add test runners without being asked
6. **Static only** — No server-side code, no databases, no APIs

## Common Tasks

### Adding a new page
1. Create a new `.html` file in the repo root
2. Include inline `<style>` with all required CSS
3. Add `charset="UTF-8"` and viewport meta tags
4. Use CSS custom properties for theme colors
5. Commit and push to `master` to deploy

### Modifying an existing page
1. Read the target HTML file fully before editing
2. Preserve existing CSS variable naming conventions
3. Test locally by opening in a browser
4. Commit with a descriptive message

### Updating the presentation (index.html)
- Reveal.js slides use `<section>` elements inside `<div class="slides">`
- Nested `<section>` elements create vertical slides
- Add `class="fragment"` for step-by-step reveals
- Reveal.js version is pinned at 5.0.4 via CDN
