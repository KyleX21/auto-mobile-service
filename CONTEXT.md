# CONTEXT.md — Business & Project Context

> This file provides the business domain knowledge, brand guidelines, and strategic context that informs every technical decision. Read this alongside `CLAUDE.md` before making any changes.

---

## The Business

**Auto Mobile Service (AMS)** is a single-owner auto electrical diagnostics and car repair operation based in Garsfontein, Pretoria East, Gauteng, South Africa.

### Owner

- **Name**: Thomas Dreyer
- **Experience**: 30+ years in the trade
- **Reputation**: Thousands of satisfied, loyal clients built through word-of-mouth over three decades
- **Approach**: Honest diagnostics, affordable pricing, no upselling, no shortcuts

### Operations

- **Location**: 532 Borzoi Street, Garsfontein, Pretoria (X10 extension)
- **Postal**: PO Box 39501, Garsfontein, 0042
- **Phone**: 082 894 3559
- **Hours**: Mon–Fri 07:30–17:00, Sat 08:00–13:00, Sun Closed
- **Capacity**: Very limited premises — maximum 4-5 vehicles on-site at any time
- **Workshop**: No formal workshop. Operations run from the premises and via mobile field service.
- **Coverage**: Any make, any model, any year. No body/panel work.

### Current Marketing

- **Zero online presence** — no website, no Google Business Profile, no social media
- **Current marketing**: Physical business cards and printed flyers (see brand assets below)
- **Client acquisition**: 100% word-of-mouth referrals over 30 years
- **WhatsApp**: Used informally for booking — SA market standard

---

## Strategic Goals

### Immediate (this project)

1. **Establish online discoverability** — when someone in Pretoria East searches "mechanic near me" or "car diagnostic Garsfontein", AMS must appear
2. **Create a professional, branded web presence** that converts visitors into phone calls or WhatsApp messages
3. **Service catalog** that Thomas can request updates to easily — initially via config file edits, later via a simple admin UI
4. **Trust signalling** — surface 30+ years of experience, client testimonials, and eventually TrustPilot/Google ratings

### Medium-Term

5. **Google Business Profile** — claim and verify, link from website, drive review collection
6. **TrustPilot integration** — establish profile, embed widget, use as social proof
7. **Simple booking flow** — WhatsApp deep link initially, then a form that emails Thomas
8. **Analytics** — understand where traffic comes from and what converts

### Long-Term Vision

9. **Business expansion** — hire qualified/certified mechanics, establish a proper workshop
10. **Scale the website** — team profiles, expanded service catalog, potential CMS
11. **Process optimisation** — job tracking, simple invoicing, client follow-ups

---

## Brand Identity

### Origin

The brand identity is derived from Thomas's existing physical marketing materials — a business card and advertising flyer that have been in circulation for years. The website must feel like a **digital extension of these materials**, not a generic template.

### Colour Palette

| Token | Hex | Usage | Source |
|-------|-----|-------|--------|
| `--ams-navy` | `#102B6A` | Primary brand colour — headers, logo mark, key UI | Blue banner on business card |
| `--ams-navy-deep` | `#0A1D4A` | Footer, dark backgrounds | Deepened navy |
| `--ams-navy-light` | `#1A3D8F` | Hover states, lighter accents | Lightened navy |
| `--ams-red` | `#CC2029` | CTA buttons, accent highlights, phone number | Red phone number on card/flyer |
| `--ams-red-dark` | `#A8171F` | Hover state for red buttons | Darkened red |
| `--ams-white` | `#FFFFFF` | Backgrounds, text on dark surfaces | Card background |
| `--ams-off-white` | `#F5F6FA` | Section backgrounds, subtle separation | — |

### Logo Treatment

There is no formal vector logo. The brand mark is text-based:

1. **"AMS" abbreviated mark** — white text on navy blue rectangular background. Mimics the blue banner at the top of the business card. Used in nav and footer.
2. **"AUTO MOBILE SERVICE" full name** — set in `Barlow Condensed` 800 weight, uppercase, navy blue. This is the primary brand text.
3. **Subline**: "Electronic Diagnostics & Repair" — smaller, grey, uppercase, letter-spaced.

### Typography

- **Display/Headlines**: `Barlow Condensed` (weights 600–800) — bold, industrial, automotive feel
- **Body/UI**: `Barlow` (weights 400–700) — clean, readable, pairs naturally with Condensed variant
- These fonts were chosen to match the bold, uppercase, no-nonsense aesthetic of the existing flyer

### Voice & Tone

- **Direct and honest** — no marketing fluff. "We fix cars. We do it right. We've been doing it for 30 years."
- **Approachable** — Thomas is a person, not a corporation. First-name basis.
- **Local** — this is a Garsfontein business serving Pretoria East. Speak to that community.
- **Confident but not arrogant** — let the track record speak. No "best mechanic in Pretoria" claims.

---

## Service Catalog (Current)

These are the services AMS currently offers, as listed on the flyer and business card:

| # | Service | Description | Notes |
|---|---------|-------------|-------|
| 1 | **Electronic Diagnostics** | Full OBD-II and manufacturer-level fault code scanning for all makes/models | Core differentiator — "Electronic Diagnostic Car Service" is the primary tagline |
| 2 | **Auto Electrical Repairs** | Wiring harnesses, fuse boxes, shorts, circuit troubleshooting | Listed on flyer as "General Auto Electrical Repairs" |
| 3 | **Starters & Alternators** | Repair and replacement | Explicitly listed on flyer |
| 4 | **Rewiring** | Full or partial vehicle rewiring for damaged/corroded looms | Explicitly listed on flyer |
| 5 | **Car Servicing** | Scheduled maintenance — oil, filters, fluids, inspections | Listed as "Services" on flyer |
| 6 | **Aircon Re-Gas** | AC re-gas, leak detection, compressor diagnostics | Listed as "Car Aircon Re-Gas" on flyer |
| 7 | **Breakdown Assistance** | Emergency mobile field service — home, office, roadside | Listed as "Breakdowns" + "Field Service" on flyer |
| 8 | **Battery Testing & Replacement** | Load testing, terminal cleaning, same-day fitting | Implied by electrical services — common customer need |

**Important**: This catalog must be easily expandable. Thomas may add services like brake repairs, suspension work, or fleet maintenance as the business grows. The technical implementation must make adding a service as simple as adding an object to an array.

---

## Competitive Landscape (Pretoria East)

AMS competes with:
- **Franchise dealerships** (expensive, impersonal, long wait times)
- **Chain workshops** (Formula 1, Midas, Supa Quick — generic, variable quality)
- **Other independent mechanics** (most have no/poor online presence)

AMS's advantages:
- 30+ years experience (longer than most competitors have existed)
- Personal service from the owner — you deal with Thomas directly
- Mobile/field service capability — most competitors require you to come to them
- Electronic diagnostics expertise — not all independents have this
- Affordable rates — no dealership markup

The website must make these advantages immediately obvious.

---

## Target Audience

### Primary: Vehicle owners in Pretoria East

- **Demographics**: Adults 25-65, own 1-2 vehicles, middle-income to affluent (Garsfontein, Moreleta Park, Waterkloof, Faerie Glen, Lynnwood, Menlo Park, Ashlea Gardens)
- **Trigger moments**: Check engine light, car won't start, AC not blowing cold, scheduled service due, breakdown
- **Search behaviour**: "mechanic near me", "car service Garsfontein", "auto electrician Pretoria", "check engine light Pretoria"
- **Decision drivers**: Trust (reviews, years in business), proximity, price, availability
- **Preferred contact**: Phone call or WhatsApp (SA standard). NOT online forms or email.

### Secondary: Referral sources

- Existing clients who recommend Thomas to friends/family
- The website gives them something to share ("check out his website")

---

## Technical Constraints

1. **Budget**: Minimal. Free-tier Azure SWA, free Google Fonts, no paid APIs initially.
2. **Maintenance**: Thomas is not technical. Any content changes will be handled by the developer (the project owner) or eventually through a simple admin UI.
3. **Performance**: Must load fast on mobile data (many SA users are on limited data plans). Target < 100KB initial page load.
4. **Connectivity**: SA mobile networks can be slow. Progressive enhancement — content must be readable before JS executes.
5. **No backend initially**: Static site only. Any dynamic features (forms, reviews) will be added incrementally via Azure Functions.

---

## Review Strategy

### Phase 1 (Launch)

- Hardcoded testimonials from real clients (collect quotes from Thomas's existing customers)
- "Leave a Review" CTA linking to Google Business Profile (once claimed)

### Phase 2

- Google Business Profile reviews — embed widget or pull via Places API
- TrustPilot profile — establish and link. TrustPilot allows business owners to flag/report unreasonable reviews (important requirement from Thomas).

### Phase 3

- Aggregate review scores in hero/trust bar from live data
- Review collection follow-up (automated WhatsApp message after service)

---

## Google Business Profile — Setup Notes

This is the #1 priority action after website launch:

1. **Claim the listing** at [business.google.com](https://business.google.com)
2. **Verify** via postcard to 532 Borzoi Street (takes ~5 days in SA)
3. **Complete profile**: business name, category (Auto Electrician / Auto Repair Shop), address, phone, hours, website URL, photos
4. **Review link**: Once verified, generate the direct review URL: `https://search.google.com/local/writereview?placeid=PLACE_ID`
5. **Embed on website**: Update the hero stat card and testimonials section with live data once reviews accumulate

---

## File Reference: Existing Assets

| Asset | Description | Location |
|-------|-------------|----------|
| Business card photo | Front of card — brand treatment, address, phone, services | Provided to Claude (image in conversation) |
| Flyer/advertisement photo | Service listing, phone number, "30 years experience" | Provided to Claude (image in conversation) |
| Current HTML prototype | Single-file SPA with full design | `auto-mobile-service.html` in project outputs |

---

## Decision Log

| Date | Decision | Rationale |
|------|----------|-----------|
| 2026-04-20 | React + Vite + TypeScript stack | TS for type safety and maintainability; Vite for fast builds; React for component architecture and future feature development |
| 2026-04-20 | Azure Static Web Apps for hosting | Aligns with owner's Azure preference; free tier covers needs; built-in CI/CD, HTTPS, custom domains |
| 2026-04-20 | CSS Modules over Tailwind | Smaller bundle, no build-time dependency, design tokens via CSS custom properties are framework-agnostic |
| 2026-04-20 | No backend/database at launch | Overkill for current needs. Static config files are sufficient. Backend comes later with Azure Functions when forms/booking are needed |
| 2026-04-20 | Barlow / Barlow Condensed fonts | Matches the bold, industrial, uppercase aesthetic of existing print materials. Free via Google Fonts |
| 2026-04-20 | WhatsApp as primary CTA (alongside phone) | SA market standard. WhatsApp has higher engagement than email or web forms in this demographic |
| 2026-04-20 | No blog | Thomas doesn't have capacity to produce content. Thin blog pages would hurt SEO more than help |
| 2026-04-20 | SEO-first approach | Zero current online presence means organic search is the biggest growth lever. Every technical decision optimises for this |

---

## Glossary

| Term | Meaning |
|------|---------|
| **OBD-II** | On-Board Diagnostics (standard port in all vehicles since ~1996) — Thomas plugs into this to read fault codes |
| **Re-gas** | Refilling the air conditioning refrigerant (common SA term) |
| **Field service** | Thomas travels to the client's location to diagnose/repair — not all mechanics offer this |
| **Azure SWA** | Azure Static Web Apps — Microsoft's hosting service for static/SPA sites |
| **SPA** | Single Page Application — one HTML page, sections scroll or route internally |
| **Structured data** | JSON-LD markup that tells Google exactly what the business is, where it is, and what it does |
