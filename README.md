# ClearIQ — Landing Page

**Status:** Phase 1 — Coming-soon / waitlist page. MVP not started.

> From pre-authorization to final payment.

ClearIQ is an authorization and reimbursement platform for OBL owners, cardiologists,
and the billing teams managing their procedure pipeline — from pre-certification filing
through denial detection, appeal generation, and reimbursement recovery.

---

## Project Overview

**Product:** ClearIQ (formerly Appeal-IQ)
**Stage:** Pre-launch / coming soon
**URL:** https://cleariq.ngengwe.com
**Entity:** HK Clearway LLC (powered by becomiNG)

---

## Tech Stack

| Layer       | Technology                          |
|-------------|-------------------------------------|
| Framework   | [Astro](https://astro.build) v4     |
| Output      | Static HTML (no JS framework)       |
| Styling     | Scoped CSS inside Astro components  |
| Fonts       | Inter + DM Serif Display (Google)   |
| Deployment  | Cloudflare Pages                    |
| DNS         | Cloudflare (cleariq.ngengwe.com)    |

---

## Local Development

```bash
# Install dependencies
npm install

# Start dev server at http://localhost:4321
npm run dev

# Build for production (outputs to dist/)
npm run build

# Preview production build locally
npm run preview
```

---

## Project Structure

```
cleariq/
├── public/
│   └── favicon.svg
├── src/
│   ├── layouts/
│   │   └── Layout.astro          # HTML shell, meta tags, global CSS
│   ├── pages/
│   │   ├── index.astro           # Main page (assembles all sections)
│   │   ├── discovery.astro       # Internal — pre-launch decision framework (noindex)
│   │   └── stakeholders.astro    # Internal — stakeholder briefing (noindex)
│   └── components/
│       ├── NavBar.astro           # Fixed top navigation
│       ├── Hero.astro             # Hero section
│       ├── Problem.astro          # Authorization pain points
│       ├── Scenario.astro         # Before/after Tuesday morning scenario
│       ├── Product.astro          # 9-step pipeline walkthrough
│       ├── PaymentEngine.astro    # Recovery & Reimbursement Engine
│       ├── NotJustAI.astro        # Product differentiation
│       ├── Features.astro         # Feature cards (6 modules)
│       ├── WhoFor.astro           # Personas / target users
│       ├── EarlyAccess.astro      # Waitlist form
│       └── Footer.astro           # Footer
├── astro.config.mjs
├── package.json
├── tsconfig.json
└── README.md
```

---

## Deployment — Cloudflare Pages

### Step 1: Push to GitHub

```bash
git add .
git commit -m "your message"
git push
```

Cloudflare Pages auto-deploys on push to `main`.

### Custom Domain

Domain `cleariq.ngengwe.com` is configured via Cloudflare DNS → CNAME to the Pages project.

---

## Form Configuration

The waitlist form in `EarlyAccess.astro` currently shows a client-side success state
only (no data is sent). To wire up a real backend:

**Option A — Formspree (recommended for quick setup):**
1. Create account at formspree.io
2. Create a form → get your form ID
3. In `EarlyAccess.astro`, replace the TODO block with:
   ```js
   const res = await fetch('https://formspree.io/f/YOUR_FORM_ID', {
     method: 'POST',
     body: new FormData(form),
     headers: { Accept: 'application/json' },
   });
   ```

**Option B — Cloudflare Workers:**
Implement a POST endpoint as a Worker and update the fetch URL.

---

## Branding Notes

- Product name: **ClearIQ**
- Entity: HK Clearway LLC, powered by becomiNG
- Colors: Deep navy `#0A1628`, Teal `#1A8EA8`, Ivory `#F8F7F4`
- Fonts: DM Serif Display (headings) + Inter (body)
- Tagline: *From pre-authorization to final payment.*

---

*ClearIQ does not provide legal, medical, or insurance advice.
All appeal materials require licensed professional review before use.*
