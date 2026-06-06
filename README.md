# Appeal-IQ — Landing Page

**Status:** Phase 1 — Coming-soon / waitlist page. MVP not started.

> From denial chaos to appeal-ready clarity.

Appeal-IQ is an AI-assisted appeal-preparation workspace for legal-medical teams
handling health insurance denials. This repository contains the landing page.

---

## Project Overview

**Product:** Appeal-IQ
**Stage:** Pre-launch / coming soon
**URL:** https://appealiq.ngengwe.com
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
| DNS         | Cloudflare (appealiq.ngengwe.com)   |

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
appeal_iq/
├── public/
│   └── favicon.svg
├── src/
│   ├── layouts/
│   │   └── Layout.astro          # HTML shell, meta tags, global CSS
│   ├── pages/
│   │   └── index.astro           # Main page (assembles all sections)
│   └── components/
│       ├── NavBar.astro           # Fixed top navigation
│       ├── Hero.astro             # Hero section
│       ├── Problem.astro          # The challenge / pain points
│       ├── Product.astro          # Intake-to-appeal workflow
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
git init
git add .
git commit -m "feat: initial landing page"
git remote add origin https://github.com/YOUR_USERNAME/appealiq.git
git push -u origin main
```

### Step 2: Connect to Cloudflare Pages

1. Log in to [Cloudflare Pages](https://pages.cloudflare.com)
2. Create a new project → Connect to GitHub → Select `appealiq`
3. Set build configuration:
   - **Framework preset:** Astro
   - **Build command:** `npm run build`
   - **Output directory:** `dist`
4. Deploy

### Step 3: Custom Domain

1. In Cloudflare Pages → Custom Domains → Add domain: `appealiq.ngengwe.com`
2. In Cloudflare DNS → Add CNAME:
   - Name: `appealiq`
   - Target: `<your-pages-project>.pages.dev`
3. Cloudflare auto-provisions SSL — no additional config needed.

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

**Option B — Netlify Forms:**
Add `data-netlify="true"` to the `<form>` element (works only on Netlify).

**Option C — Custom API:**
Implement a POST endpoint (e.g., Cloudflare Worker or Next.js API route)
and update the fetch URL in the form's submit handler.

---

## Environment Variables

None required for the current landing page.

For future MVP features, create `.env` (excluded from git via `.gitignore`):
```
# Form endpoint (if using custom API)
PUBLIC_FORM_ENDPOINT=https://...

# Future: intake API, auth, etc.
```

---

## MVP Extension Points

The landing page is structured for clean incremental extension:

- Each section is a self-contained Astro component — add or reorder easily
- The `Layout.astro` global CSS design tokens (`--navy-dark`, `--teal`, etc.)
  carry through any new pages or UI components automatically
- Future MVP pages (intake form, case workspace, appeal builder) can be added
  as new files under `src/pages/`
- The Astro static output can be replaced with `output: 'server'` + an adapter
  (e.g., `@astrojs/cloudflare`) when server-side features are needed

**Planned MVP modules (do not build yet):**
- [ ] Secure patient intake form
- [ ] Denial letter upload and parsing
- [ ] AI-assisted interview / transcript
- [ ] Medical/legal fact extraction workspace
- [ ] Appeal-strength classifier
- [ ] Missing support detector
- [ ] Attorney review workspace
- [ ] Appeal package builder / export

---

## Branding Notes

- Product name: **Appeal-IQ** (hyphenated)
- Entity: HK Clearway LLC, powered by becomiNG
- Colors: Deep navy `#0A1628`, Teal `#1A8EA8`, Ivory `#F8F7F4`
- Fonts: DM Serif Display (headings) + Inter (body)
- Tagline: *From denial chaos to appeal-ready clarity.*

---

*Appeal-IQ does not provide legal, medical, or insurance advice.
All appeal materials require attorney or licensed professional review.*
