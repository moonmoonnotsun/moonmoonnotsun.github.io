# iOS Apps Landing Pages

This repository hosts landing pages for all iOS mobile apps, accessible via subdirectories on the main domain.

## Structure

```
.
├── index.html              # Main hub page listing all apps
├── metronome/              # Metronome app landing page
│   └── index.html
├── assets/                 # Shared assets
│   ├── css/
│   │   ├── main.css        # Shared styles
│   │   └── app-page.css    # App page specific styles
│   └── images/             # Shared images (App Store badges, etc.)
└── README.md
```

## Setup Instructions

### 1. GitHub Pages Configuration

1. Go to your repository **Settings** > **Pages**
2. Under **Source**, select your branch (typically `main` or `master`)
3. Under **Custom domain**, enter your domain (e.g., `company.com`)
4. Enable **Enforce HTTPS**

### 2. DNS Configuration

To point your custom domain to GitHub Pages:

**For Apex Domain (`company.com`):**
- Add these `A` records pointing to GitHub's IP addresses:
  - `185.199.108.153`
  - `185.199.109.153`
  - `185.199.110.153`
  - `185.199.111.153`

**For `www` Subdomain (`www.company.com`):**
- Add a `CNAME` record pointing to `moonmoonnotsun.github.io`

### 3. CNAME File

GitHub will automatically create a `CNAME` file when you set the custom domain. If you need to create it manually:

```
company.com
```

## Adding a New App

1. Create a new folder for your app (e.g., `app2/`)
2. Create an `index.html` file in that folder
3. Copy the structure from `metronome/index.html` as a template
4. Update the content, app name, description, and features
5. Add the app card to the root `index.html` in the `apps-grid` section

### Example App Card

```html
<a href="/app2" class="app-card">
    <div class="app-icon">📱</div>
    <h2 class="app-name">App 2</h2>
    <p class="app-description">Description of your app</p>
    <span class="app-link">View App →</span>
</a>
```

## App Store Badge

To add an App Store download badge:

1. Download the official App Store badge from Apple's Marketing Resources
2. Save it as `assets/images/app-store-badge.svg` (or `.png`)
3. Update the image path in your app's `index.html` if needed

## Customization

### Colors

Edit CSS variables in `assets/css/main.css`:

```css
:root {
    --primary-color: #007AFF;
    --primary-dark: #0051D5;
    /* ... */
}
```

### Styling

- `assets/css/main.css` - Shared styles for all pages
- `assets/css/app-page.css` - Styles specific to individual app pages

## Accessing Your Pages

After setup and DNS propagation:

- Main hub: `https://company.com/`
- Metronome app: `https://company.com/metronome`
- Future apps: `https://company.com/app-name`

## Notes

- DNS changes can take up to 24 hours to propagate
- GitHub Pages automatically builds and deploys on push to the main branch
- All pages are mobile-responsive
- HTTPS is enforced by default on GitHub Pages

