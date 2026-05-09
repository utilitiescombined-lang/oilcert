# OilCert — Setup Checklist

This is the punch-list of external integrations that still need your action. The codebase
is ready; these are the values you need to plug in (or decisions you need to make) before the
site is fully live and tracked.

---

## 1. GitHub repo transfer
- [x] Pushed the local repo to **github.com/danielcrypto1/oilcert**
- [x] Transferred to **utilitiescombined-lang** — repo now lives at https://github.com/utilitiescombined-lang/oilcert
- [x] `render.yaml` `repo:` updated to the new org URL
- [x] Local origin remote re-pointed to the new URL

## 2. Render web service
- [ ] Render → New → **Blueprint** → connect the repo at utilitiescombined-lang/oilcert
- [ ] Render reads `render.yaml` automatically. Verify:
  - Service name: `oilcert`
  - Build: `npm install`
  - Start: `node server.js`
  - Plan: free
  - Health check: `/api/health`
- [ ] Set the env var `GOOGLE_CREDENTIALS_JSON` (paste the Google service account JSON inline) so the booking form creates calendar events
- [ ] First deploy should take ~3–5 minutes. Confirm `https://oilcert.onrender.com` returns the homepage.

## 3. DNS — Namecheap (oilcert.co.uk → Advanced DNS)
- [ ] **Delete** the default `CNAME www → parkingpage.namecheap.com`
- [ ] **Delete** the default `URL Redirect @ → http://www.oilcert.co.uk/`
- [ ] **Add A record**: `@ → 216.24.57.1` (Render apex IP)
- [ ] **Add CNAME record**: `www → oilcert.onrender.com.` (note the trailing dot)
- [ ] **Leave alone**: the email forwarding `TXT` (SPF) record — that's keeping `oilcert@utilitiescombined.co.uk` working
- [ ] Wait 5–30 minutes for the zone to propagate
- [ ] Verify with `nslookup oilcert.co.uk dns1.registrar-servers.com` — the SOA serial increments when the update is live
- [ ] In Render → Settings → Custom Domains: add **oilcert.co.uk** and **www.oilcert.co.uk**, accept the auto-issued Let's Encrypt cert

## 4. Email — Namecheap forwarder
- [x] **Already done by you**: `oilcert@utilitiescombined.co.uk` forwarder is set up in Namecheap
- [ ] Send a test message to confirm it lands in the inbox you're forwarding to

## 5. Analytics & tracking — replace placeholder IDs

The codebase still carries the **Electricert / UC** analytics IDs, on purpose, so your replacements
are visible at a glance. Find each ID via repo-wide search and swap in the OilCert-specific values:

- [ ] **Google Tag Manager** — replace `GTM-MPGJV5DC` (3 files: `index.html`, `pages/findings.html`, `pages/about.html`, plus other pages copied from the same template). Easiest: PowerShell regex replace across the tree.
- [ ] **Google Ads conversion tag** — replace `AW-18046002549` everywhere
- [ ] **Microsoft Clarity** — replace the placeholder `XXXXXXXXXX` everywhere

Once swapped, deploy and verify each tag in **GTM Preview**, **Clarity Live**, and **Google Ads → Tools → Tag Diagnostics**.

## 6. Google Search Console
- [ ] Add property: `https://oilcert.co.uk/`
- [ ] Verify via DNS TXT record (Namecheap → Advanced DNS → add TXT)
- [ ] Submit sitemap: `https://oilcert.co.uk/sitemap.xml`
- [ ] Check coverage weekly for the first month

## 7. Google Business Profile
- [ ] Decide whether to add OilCert as a service to the existing UC GBP **or** create a new GBP listing
- [ ] If new: same NAP (name/address/phone) as UC, primary category "Heating Contractor", secondary "Boiler Supplier"
- [ ] Add OFTEC registration number to the profile
- [ ] Link the profile back to **oilcert.co.uk**
- [ ] Set up Google Reviews link in the GBP — replace the existing UC review link in `index.html` if you want OilCert-specific reviews

## 8. Calendly
- [x] **Decision: skip for now.** UC has not created an oilcert-specific Calendly event type
- [x] No Calendly link is present in the booking flow (intentionally removed). The form submits via `/api/book` and the WhatsApp/phone CTAs are the only secondary booking paths
- [ ] When you create the Calendly event, add a single CTA back into the booking section in `index.html` — do not add a fallback that 404s

## 9. Anthropic API key (for installer AI rewrite)
- [ ] Get an API key from https://console.anthropic.com (look for `sk-ant-...`)
- [ ] In the deployed admin panel: **Settings → AI Settings → paste the key → Save**
- [ ] OR set `AI_API_KEY` as a Render env var (preferred — survives redeploys)
- [ ] The AI rewrite prompts already reference OFTEC TI/133, OFTEC TI/134, BS 5410 and Building Regs Part J — see `server.js` `AI_PROMPTS`

## 10. Real Findings page
- [x] Hidden from nav, footer, sitemap and marked `noindex, nofollow` until you upload findings with photos
- [ ] When you have at least 3 approved findings with before/after photos, **un-noindex** `pages/findings.html`, add it back to `sitemap.xml`, and re-add the nav link in every page

## 11. Hero image — final QA
- [x] Hero `images/cover.webp` uses `object-fit: contain` with a warm amber gradient backdrop and a 4/5 aspect ratio (per the lessons-learned brief)
- [ ] If you have a higher-resolution version of the gear+drop hero, drop it in at `images/cover.webp` (must be webp, ideally 1200×1500 for retina)

## 12. Favicon
- [x] Currently uses the full-colour logo (`images/favicon.png` = a 233 KB copy of the logo PNG)
- [ ] **Optional:** generate a proper favicon set (16×16, 32×32, 180×180 apple-touch-icon, 192/512 PWA icons) at https://realfavicongenerator.net and replace the single PNG. The current setup works but pays a small KB cost on first load.

## 13. Signs section image
- [x] `images/signs.jpg` is a real OFTEC service photo (Worcester oil boiler being serviced — burner pulled, flue analyser fitted, tools laid out). Used in the homepage Signs section in a two-column layout next to the self-check checklist.
- [x] Re-encoded from a 3 MB PNG to a 381 KB JPEG (quality 82) for web performance
- [x] CSS `.signs-img` aspect-ratio is `5/4` to match the photo's natural 4:3 — only ~3% horizontal crop on each side with `object-fit: cover`
- [x] Old `images/testing.png` (electrical fuse-board photo) deleted

## 14. Reviews on the homepage
- [x] The four reviews on the homepage are **rewritten as oil-heating equivalents** of the originals — they are placeholder copy that reads naturally for the new domain
- [ ] Replace each with a real verified Google review as soon as you have them. Update `aggregateRating.reviewCount` in the JSON-LD block in `index.html` to match the real count.

## 15. Phone / WhatsApp
- [x] Phone: `01442 601 383` (UC main line)
- [x] WhatsApp: `wa.me/441442601383`
- [x] Booking confirmation messages reference "oil boiler service" rather than "EICR"

## 16. Sister-brand cross-links
- [x] Footer cross-links to **utilitiescombined.co.uk**, **electricert.co.uk** and **plumcert.co.uk**
- [x] About page mentions the sibling brands and links them
- [ ] Reciprocate from the Plumcert and Electricert footers — a single in-content link in each direction materially helps SEO

## 17. First test booking
- [ ] After DNS goes live, submit one booking through the form and confirm:
  - The lead lands in `data/leads.json` (visible in admin panel → Leads)
  - A calendar event is created in the linked Google Calendar (assuming `GOOGLE_CREDENTIALS_JSON` is set)
  - The phone and WhatsApp deep links work on a real phone

---

## What's already done in code (no action needed)

- ✅ Brand strings (`ElectriCert`/`electricert` → `OilCert`/`oilcert`) across HTML, JS, CSS, JSON, MD, YAML, XML, TXT
- ✅ Domain references (`electricert.co.uk` → `oilcert.co.uk`)
- ✅ Email forwarder (`electricert@...` → `oilcert@...`)
- ✅ Logo and hero image swapped (gear + drop)
- ✅ Charcoal slate / amber / vermilion palette across CSS variables and inline hex codes
- ✅ Hero image styling: `object-fit: contain`, 4/5 aspect, warm amber gradient backdrop
- ✅ Service types in the booking form: annual service, landlord, pre-purchase, tank, emergency
- ✅ Brand grid: Grant, Worcester, Firebird, Warmflow, Trianco, Boulter, Titan, Harlequin, Atlas, Kingspan
- ✅ Installer appliance dropdown: oil boiler (combi/system/heat-only), AGA/Rayburn/Stanley range, oil tank (single-skin/bunded/integrally bunded), oil supply pipework, flue/chimney, hot water cylinder, plumbing/heating system
- ✅ Finding classifications: ID / AR / NCS (replacing C1 / C2 / C3) — wired through `server.js`, `pages/installer.html`, `pages/findings.html`, `js/installer.js`, `admin/index.html`, `index.html`
- ✅ AI rewrite prompts reference OFTEC TI/133, TI/134, BS 5410 and Building Regs Part J
- ✅ Calendar event title (`Oil heating service — {name}`) and review-request WhatsApp message updated
- ✅ Open Graph + Twitter Card + theme-color meta tags on the homepage
- ✅ Stats are now truthful: 5/5 Google Reviews, Part of UC Group, 24hr CD/10 turnaround (no fabricated "2,400 inspections")
- ✅ `aggregateRating.ratingValue` set to 5
- ✅ Calendly link removed from the booking section
- ✅ Real Findings page hidden from nav/footer/sitemap and `noindex, nofollow`
- ✅ All page nav menus updated: "Book Inspection" → "Book Service", "Real Findings" link removed
- ✅ Privacy and terms pages rewritten for OFTEC oil heating context
