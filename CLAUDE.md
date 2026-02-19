# CLAUDE.md — HammerHub Website

Static marketing / landing page for **hammerhub.com**.

## Stack
- **Framework**: Astro 5 (static output)
- **Styling**: Tailwind CSS 4 (via `@tailwindcss/vite`, no config file — theme in `src/styles/global.css`)
- **Interactivity**: React (for components needing client-side state)
- **Package manager**: pnpm exclusively
- **Node**: v20
- **Hosting**: Netlify (auto-deploy from `dist/`)
- **Forms**: Netlify Forms (`data-netlify="true"`)

## Commands
```bash
pnpm dev      # Dev server on localhost:4322
pnpm build    # Production build → dist/
pnpm preview  # Preview production build
```

## Structure
```
src/
├── components/
│   ├── Nav.astro
│   ├── HeroSection.astro
│   ├── FeaturesSection.astro
│   ├── AlreadyLiveSection.astro
│   ├── GameSystemsSection.astro
│   ├── EmailSignupSection.astro
│   └── Footer.astro
├── layouts/
│   └── Layout.astro          # Base HTML, Inter font, GA
├── pages/
│   ├── index.astro            # Landing page
│   └── privacy.astro          # Privacy & Disclaimers
└── styles/
    └── global.css             # @theme (HammerHub palette), utility classes
```

## Design System
All brand colours defined in `src/styles/global.css` under `@theme`:

| Token | Value | Usage |
|-------|-------|-------|
| `hh-navy` | `#0f0f1a` | Page background |
| `hh-navy-soft` | `#1a1a2e` | Alternate section bg |
| `hh-surface` | `#1e1e35` | Card/surface bg |
| `hh-cyan` | `#00c8dc` | Primary accent / CTA |
| `hh-border` | `rgba(255,255,255,0.08)` | Default borders |
| `hh-border-cyan` | `rgba(0,200,220,0.3)` | Highlighted borders |
| `hh-text-muted` | `#94a3b8` | Body text |
| `hh-text-dim` | `#64748b` | Placeholder / helper text |

Utility classes: `.btn-cyan`, `.btn-ghost`, `.feature-card`, `.bg-grid` — see `global.css`.

## Environment Variables
```
PUBLIC_OWR_URL      # OWR app URL (default: https://oldworldrankings.com)
PUBLIC_GA_ID        # Google Analytics 4 measurement ID (optional)
```

## Netlify Forms
The email signup uses Netlify Forms. The form name is `notify`.
Submissions appear in the Netlify dashboard under Forms → notify.
The JS in `EmailSignupSection.astro` submits via fetch for a SPA-like experience,
with a fallback to native form submission on error.

## Deployment (Netlify)
1. Connect the repo in Netlify
2. Build command: `pnpm build`
3. Publish directory: `dist`
4. Node version: 20 (set in `netlify.toml` and `.node-version`)
5. Set env vars: `PUBLIC_OWR_URL`, optionally `PUBLIC_GA_ID`
