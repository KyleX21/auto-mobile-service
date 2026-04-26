# CLAUDE.md — Auto Mobile Service (AMS) Website

## Project Overview

Single-page application website for **Auto Mobile Service**, a 30+ year auto electrical diagnostics and car repair business in Garsfontein, Pretoria. The site serves as the company's first online presence — its primary job is **local discoverability** (SEO), **trust signalling** (reviews, experience), and **conversion** (phone call / WhatsApp).

## Tech Stack

| Layer | Choice | Rationale |
|-------|--------|-----------|
| **Framework** | React 18+ with Vite | Fast builds, excellent TS support, SPA-native |
| **Language** | TypeScript (strict mode) | Type safety for content management, future features |
| **Styling** | CSS Modules + CSS Custom Properties | Scoped styles, design token system, zero runtime cost |
| **Hosting** | Azure Static Web Apps | Free tier sufficient, custom domain + HTTPS, CI/CD via GitHub Actions |
| **Build** | Vite | Sub-second HMR, optimised production bundles |
| **Package Manager** | npm | Standard, Azure SWA compatible |

## Architecture

```
ams-website/
├── CLAUDE.md                    # This file — project instructions
├── CONTEXT.md                   # Business context and requirements
├── .github/
│   └── workflows/
│       └── azure-swa-deploy.yml # CI/CD pipeline
├── staticwebapp.config.json     # Azure SWA routing + headers config
├── package.json
├── tsconfig.json
├── vite.config.ts
├── index.html                   # Vite entry point
├── public/
│   ├── favicon.ico
│   ├── robots.txt
│   └── sitemap.xml
└── src/
    ├── main.tsx                 # React entry
    ├── App.tsx                  # Root component + section routing
    ├── styles/
    │   ├── tokens.css           # Design tokens (colours, spacing, typography)
    │   └── global.css           # Reset + base styles
    ├── config/
    │   ├── services.ts          # SERVICE CATALOG — the owner edits this
    │   ├── testimonials.ts      # Client testimonials data
    │   ├── business.ts          # Business details (address, phone, hours)
    │   └── seo.ts               # Meta tags, structured data config
    ├── components/
    │   ├── Nav/
    │   │   ├── Nav.tsx
    │   │   └── Nav.module.css
    │   ├── Hero/
    │   ├── TrustBar/
    │   ├── Services/
    │   ├── WhyAMS/
    │   ├── Testimonials/
    │   ├── Contact/
    │   ├── Footer/
    │   └── common/
    │       ├── Button.tsx
    │       ├── SectionHeader.tsx
    │       └── Icon.tsx          # SVG icon system
    ├── hooks/
    │   ├── useScrollReveal.ts   # Intersection Observer hook
    │   └── useScrollShadow.ts   # Nav shadow on scroll
    ├── utils/
    │   └── seo.ts               # Schema.org JSON-LD generator
    └── types/
        └── index.ts             # Shared TypeScript interfaces
```

## Design System

### Brand Tokens (extracted from business card/flyer)

```css
/* Primary — navy blue banner from business card */
--ams-navy: #102B6A;
--ams-navy-deep: #0A1D4A;
--ams-navy-light: #1A3D8F;

/* Accent — red from phone number/CTA */
--ams-red: #CC2029;
--ams-red-dark: #A8171F;
--ams-red-light: #E8333C;

/* Neutrals */
--ams-white: #FFFFFF;
--ams-off-white: #F5F6FA;
--ams-grey-100 through --ams-grey-800;
--ams-text: #1A1E2A;
```

### Typography

- **Display**: `Barlow Condensed` (800 weight) — headlines, stats, section titles
- **Body**: `Barlow` (400/500/600/700) — paragraphs, UI elements
- Load via Google Fonts with `display=swap`

### Design Rules

1. All colours MUST reference CSS custom properties — never hardcode hex values
2. Spacing uses a 4px base grid (`--sp-1` through `--sp-24`)
3. Border radius: `--radius-sm: 4px`, `--radius-md: 8px`, `--radius-lg: 12px`
4. Single easing curve throughout: `cubic-bezier(0.22, 1, 0.36, 1)`
5. The blue/red/white palette is non-negotiable — it IS the brand
6. The navy `AMS` logo mark replicates the blue banner from the physical business card

## Content Management

### Service Catalog (`src/config/services.ts`)

This is the **most important file for the business owner**. It must remain a simple, flat TypeScript array that non-developers can understand with minimal guidance:

```typescript
export const SERVICE_CATALOG: Service[] = [
  {
    id: "electronic-diagnostics",
    title: "Electronic Diagnostics",
    description: "Full OBD-II and manufacturer-level fault code scanning...",
    icon: "diagnostic",
    featured: true
  },
  // ... add/remove/reorder entries here
];
```

**Rules:**
- One file, one export, flat array
- No nested configs, no imports from other files
- Icon keys map to the `Icon` component's SVG registry
- The `featured` flag can be used for homepage prominence (future)
- Descriptions should be 1-2 sentences max, written for the customer not the mechanic

### Testimonials (`src/config/testimonials.ts`)

Same pattern — flat array, easy to edit:

```typescript
export const TESTIMONIALS: Testimonial[] = [
  {
    name: "Johan van der Merwe",
    text: "Thomas has been servicing our family cars for over 15 years...",
    rating: 5,
    meta: "Loyal client since 2009"
  },
];
```

### Business Details (`src/config/business.ts`)

Single source of truth for all contact info, hours, and address. Referenced by components and SEO structured data.

## SEO Requirements — Critical

SEO is the primary driver of ROI for this site. Every decision must consider search ranking.

### Must-Haves

1. **Schema.org structured data** — `AutoRepair` type with full address, geo coordinates, opening hours, aggregate rating. Generated from `business.ts` config.
2. **Meta tags** — title, description, geo tags (`geo.region`, `geo.placename`, `geo.position`, `ICBM`), Open Graph, canonical URL.
3. **Semantic HTML** — proper heading hierarchy (`h1` > `h2` > `h3`), `<nav>`, `<main>`, `<section>`, `<footer>`, `<address>`.
4. **`robots.txt`** — allow all crawlers.
5. **`sitemap.xml`** — single-page sitemap with lastmod.
6. **Performance** — Lighthouse score 95+ across all categories. No render-blocking resources. Font preconnect. Lazy-load map iframe.
7. **Mobile-first** — Google indexes mobile-first. Every component must be responsive.

### Target Keywords

Primary: `auto electrician Garsfontein`, `car diagnostic Pretoria`, `car service Garsfontein`
Secondary: `mobile mechanic Pretoria`, `auto electrical repairs Pretoria East`, `aircon regas Pretoria`, `car breakdown Garsfontein`, `electronic car diagnostics`
Long-tail: `mechanic near me Pretoria East`, `affordable car service Garsfontein`, `alternator repair Pretoria`

### Pre-rendering for SEO

Azure SWA serves static files — Vite's build output is pre-rendered HTML + JS. For a single-page site this is fine since all content is in the initial HTML. However, ensure `index.html` contains the full meta tags and structured data BEFORE React hydration (use Vite's `index.html` template, not client-side injection).

**Critical:** Meta tags, `<title>`, and JSON-LD structured data MUST be in the static `index.html` — not injected by React at runtime. Search crawlers may not execute JS.

## Azure Static Web Apps Deployment

### `staticwebapp.config.json`

```json
{
  "navigationFallback": {
    "rewrite": "/index.html",
    "exclude": ["/assets/*", "/favicon.ico", "/robots.txt", "/sitemap.xml"]
  },
  "globalHeaders": {
    "X-Content-Type-Options": "nosniff",
    "X-Frame-Options": "DENY",
    "X-XSS-Protection": "1; mode=block",
    "Referrer-Policy": "strict-origin-when-cross-origin",
    "Permissions-Policy": "camera=(), microphone=(), geolocation=()",
    "Cache-Control": "public, max-age=3600"
  },
  "mimeTypes": {
    ".json": "application/json",
    ".xml": "application/xml"
  }
}
```

### GitHub Actions Pipeline (`.github/workflows/azure-swa-deploy.yml`)

Trigger on push to `main`. Steps:
1. Checkout
2. Setup Node 20
3. `npm ci`
4. `npm run build`
5. Deploy to Azure SWA using `Azure/static-web-apps-deploy@v1`

The `app_location` is `/`, `output_location` is `dist`.

### Environment Variables

- `VITE_GOOGLE_MAPS_EMBED_URL` — Google Maps embed URL (can be hardcoded for now)
- `VITE_WHATSAPP_NUMBER` — `27828943559`
- `VITE_SITE_URL` — canonical URL once domain is registered

## Development Workflow

### Getting Started

```bash
npm create vite@latest ams-website -- --template react-ts
cd ams-website
npm install
npm run dev
```

### Scripts

| Command | Purpose |
|---------|---------|
| `npm run dev` | Local development server |
| `npm run build` | Production build to `dist/` |
| `npm run preview` | Preview production build locally |
| `npm run lint` | ESLint check |
| `npm run typecheck` | `tsc --noEmit` type validation |

### Quality Gates

Before any PR merge:
1. `npm run typecheck` passes with zero errors
2. `npm run lint` passes
3. `npm run build` succeeds
4. Lighthouse audit: Performance ≥ 95, Accessibility ≥ 95, SEO ≥ 95
5. Mobile viewport tested (375px, 768px, 1200px)

## Component Development Rules

1. **One component per directory** — `ComponentName/ComponentName.tsx` + `ComponentName.module.css`
2. **Props interfaces** — every component defines its props interface in the same file or imports from `types/`
3. **No `any`** — TypeScript strict mode, no escape hatches
4. **CSS Modules for scoping** — global styles only in `tokens.css` and `global.css`
5. **SVG icons** — inline SVGs via the `Icon` component, not image files. Keeps bundle tiny.
6. **Lazy-load the map iframe** — use `loading="lazy"` attribute
7. **Intersection Observer** — use `useScrollReveal` hook for all section entrance animations
8. **No external JS dependencies** — this site must remain ultra-lightweight. No animation libraries, no UI frameworks. Pure CSS animations + React.

## Future Roadmap (in priority order)

1. **Google Business Profile integration** — claim profile, add review link CTA, potentially pull live reviews via Places API
2. **TrustPilot widget** — embed once profile is established
3. **Admin panel** — simple authenticated page (Azure AD B2C or static password) where Thomas can edit the service catalog and testimonials via a form UI, which writes to an Azure Blob Storage JSON file
4. **Booking form** — simple appointment request form that sends an email via Azure Functions (no database needed initially)
5. **Multi-language** — Afrikaans/English toggle (Garsfontein is bilingual market)
6. **Analytics** — Azure Application Insights or Plausible (privacy-friendly)
7. **Expansion** — if the business grows to multiple mechanics/workshop, the site scales to include team profiles, gallery, and a proper CMS

## What NOT to Build

- No backend API (static site only, for now)
- No database
- No user authentication (for now)
- No blog (not enough content to sustain it — would hurt SEO with thin pages)
- No chatbot
- No complex animations or parallax effects — keep it fast and honest
- No third-party CSS frameworks (Tailwind, Bootstrap) — the design token system is sufficient and keeps the bundle minimal
