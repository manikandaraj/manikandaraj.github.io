# 🍋 Hugo Blogging Site - `mango` Theme

You are a **Hugo theme developer**. Your task is to build a **production-ready, dark-themed, fully responsive** Hugo theme called **`mango`** for the site owner **Manikandaraj Srinivasan**. The site will be built using **GitHub Actions** and deployed to **GitHub Pages** without requiring local Hugo installation. All layout and configuration must be driven from `hugo.toml`.

---

## 🎨 Desktop Layout Requirements

- **Header**
  - Width: 100%, Height: 5%
  - Fixed top bar
  - Displays site title and menu (from `[menu.main]`)

- **Left Sidebar**
  - Width: 15%, Height: 90%
  - Displays vertical list of social links from `[params.social]`
    - GitHub, LinkedIn, Twitter, StackOverflow, YouTube, Instagram, Email

- **Main Content Area**
  - Width: 70%, Height: 90%
  - Displays `.Content` from Markdown
  - Conditionally display `.TableOfContents` for content-heavy pages

- **Right Sidebar**
  - Width: 15%, Height: 90%
  - Contains an `<iframe>` that displays dynamic content (ads or other pages)
  - The iframe URL must be configurable via `params.iframeURL` or `params.ads.iframe`

- **Footer**
  - Width: 100%, Height: 5%
  - Displays dynamic copyright:
    ```html
    © 2021–{{ now.Year }} Manikandaraj Srinivasan
    ```
  - Text should be configurable via `params.footerCopyright`

---

## 📱 Mobile Layout Requirements

- Hide left & right sidebars and top menu by default
- Add a hamburger menu in the header
- On tap, the menu should slide in from the left side (collapsible)
- Ensure responsive styling across all screen sizes

---

## ⚙ Configurable via `hugo.toml`

| Key | Description |
|-----|-------------|
| `theme` | Must be `"mango"` |
| `[menu.main]` | Menu with 7 items: Home, About, Contact, Blog, Resume, My Projects, Referral Links |
| `[params.social]` | Social links listed above |
| `[params]` |
| `author.name` | Name of the site owner |
| `author.email` | Email ID |
| `googleAnalyticsID` | Google Analytics tracking ID (conditionally included) |
| `iframeURL` or `ads.iframe` | Iframe URL for right sidebar |
| `fontFamily` | Font to use across site (e.g., `"Inter, sans-serif"`) |
| `themeMode` | Set to `"dark"` |
| `footerCopyright` | Footer text, includes year range |

---

## 🚀 GitHub Actions Deployment

### GitHub Actions Workflow
Create `.github/workflows/hugo.yaml` with the following configuration:

```yaml
name: Deploy Hugo site to Pages

on:
  push:
    branches:
      - main
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: false

defaults:
  run:
    shell: bash

jobs:
  build:
    runs-on: ubuntu-latest
    env:
      DART_SASS_VERSION: 1.89.2
      HUGO_VERSION: 0.148.0
      HUGO_ENVIRONMENT: production
      TZ: America/Los_Angeles
    steps:
      - name: Install Hugo CLI
        run: |
          wget -O ${{ runner.temp }}/hugo.deb https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_extended_${HUGO_VERSION}_linux-amd64.deb
          sudo dpkg -i ${{ runner.temp }}/hugo.deb
      - name: Install Dart Sass
        run: |
          wget -O ${{ runner.temp }}/dart-sass.tar.gz https://github.com/sass/dart-sass/releases/download/${DART_SASS_VERSION}/dart-sass-${DART_SASS_VERSION}-linux-x64.tar.gz
          tar -xf ${{ runner.temp }}/dart-sass.tar.gz --directory ${{ runner.temp }}
          mv ${{ runner.temp }}/dart-sass/ /usr/local/bin
          echo "/usr/local/bin/dart-sass" >> $GITHUB_PATH
      - name: Checkout
        uses: actions/checkout@v4
        with:
          submodules: recursive
          fetch-depth: 0
      - name: Setup Pages
        id: pages
        uses: actions/configure-pages@v5
      - name: Install Node.js dependencies
        run: "[[ -f package-lock.json || -f npm-shrinkwrap.json ]] && npm ci || true"
      - name: Cache Restore
        id: cache-restore
        uses: actions/cache/restore@v4
        with:
          path: |
            ${{ runner.temp }}/hugo_cache
          key: hugo-${{ github.run_id }}
          restore-keys:
            hugo-
      - name: Configure Git
        run: git config core.quotepath false
      - name: Build with Hugo
        run: |
          hugo \
            --gc \
            --minify \
            --baseURL "${{ steps.pages.outputs.base_url }}/" \
            --cacheDir "${{ runner.temp }}/hugo_cache"
      - name: Cache Save
        id: cache-save
        uses: actions/cache/save@v4
        with:
          path: |
            ${{ runner.temp }}/hugo_cache
          key: ${{ steps.cache-restore.outputs.cache-primary-key }}
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: ./public

  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

### Hugo Configuration for GitHub Pages
Add this to your `hugo.toml`:

```toml
[caches]
  [caches.images]
    dir = ':cacheDir/images'
```

## 📁 Expected Project Structure

```plaintext
myblog/
├── .github/
│   └── workflows/
│       └── hugo.yaml
├── themes/
│   └── mango/
│       ├── LICENSE
│       ├── README.md
│       ├── theme.toml
│       ├── archetypes/
│       │   └── default.md
│       ├── assets/
│       │   ├── css/main.css
│       │   └── js/main.js
│       ├── static/
│       │   └── favicon.ico
│       └── layouts/
│           ├── _default/
│           │   ├── baseof.html
│           │   ├── single.html
│           │   ├── home.html
│           │   └── list.html
│           └── partials/
│               ├── head/
│               │   ├── head.html
│               │   ├── css.html
│               │   └── js.html
│               ├── header.html
│               ├── menu.html
│               ├── footer.html
│               └── terms.html
├── content/
├── hugo.toml
└── README.md
```

---

## 🧾 Archetype - `archetypes/default.md`

```markdown
---
title: "{{ replace .Name "-" " " | title }}"
date: {{ .Date }}
draft: true
summary: ""
tags: []
categories: []
---
```

---

## 🌙 Styling – `assets/css/main.css`

```css
:root {
  --header-bg-color: #1a1a1a;
  --footer-bg-color: #1a1a1a;
  --page-bg-color: #121212;
  --font-family: 'Inter', sans-serif;
}

/* Global Styles */
body {
  background-color: var(--page-bg-color);
  color: #f0f0f0;
  font-family: var(--font-family);
}
```

---

## 📊 Google Analytics

- Use `params.googleAnalyticsID` to inject the GA4 script inside `layouts/partials/head/head.html`
- Conditionally render script only if ID is present

---

## ✍ Content Notes

- Pages like `Resume`, `Projects`, `About` must display `.TableOfContents`
- Blog List Page and Project List Pages must iterate and link to individual posts
- Blog posts: Title should render as:
  ```
  {{ .Title }} - {{ site.Params.author.name }}
  ```

---

## 🔧 GitHub Pages Setup Steps

1. **Repository Setup**:
   - Create a GitHub repository (public for free GitHub Pages)
   - Enable GitHub Pages in repository settings
   - Set source to "GitHub Actions"

2. **Repository Structure**:
   - Push your Hugo site code to the repository
   - Include the `.github/workflows/hugo.yaml` file
   - Theme should be in `themes/mango/` directory

3. **Configuration**:
   - Ensure `hugo.toml` includes cache configuration
   - Set theme to `"mango"`
   - Configure all parameters as specified above

4. **Deployment**:
   - Push to main branch triggers automatic build and deployment
   - No local Hugo installation required
   - Site builds and deploys via GitHub Actions

## ✅ Final Goal

Develop the `mango` Hugo theme adhering to:
- Hugo's best practices
- Clean, modular layout
- Dark theme with responsive design
- Driven completely from `hugo.toml`
- **GitHub Actions deployment pipeline**
- **Automatic GitHub Pages hosting**
- **No local Hugo installation required**
