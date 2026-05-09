# OilCert — Ads & SEO Integration Guide

This is the playbook for paid acquisition and organic SEO on oilcert.co.uk. The site already
ships with the Utilities Combined GTM, Google Ads and Microsoft Clarity tags inherited from
Electricert — those need swapping out for OilCert-specific IDs (see `SETUP-CHECKLIST.md`).

---

## Quick Setup Checklist

### 1. Google Tag Manager (recommended over individual tags)
- Create a new GTM container at https://tagmanager.google.com
- Replace `GTM-MPGJV5DC` in `index.html` and every page in `pages/` with the new container ID
- Inside GTM, configure tags for: GA4, Google Ads remarketing, Google Ads conversion, optional Meta Pixel

### 2. Google Analytics 4
- Create a new property for oilcert.co.uk at https://analytics.google.com
- Connect via GTM (recommended) or paste the Measurement ID into a hard-coded gtag block

### 3. Google Ads
- Create / re-use the Utilities Combined Google Ads account at https://ads.google.com
- Replace `AW-18046002549` in every page with the new conversion ID (see `SETUP-CHECKLIST.md`)
- Configure conversion actions:
  - **Primary**: Booking form submission (`#bookingForm` submit)
  - **Secondary**: Phone clicks (`tel:+441442601383`)
  - **Secondary**: WhatsApp clicks (any `wa.me/441442601383` link)

### 4. Microsoft Clarity
- Create a project at https://clarity.microsoft.com
- Replace the placeholder `XXXXXXXXXX` Clarity ID across `index.html` and every page in `pages/`

### 5. Google Search Console
- Verify oilcert.co.uk via DNS TXT record (Namecheap → Advanced DNS → TXT)
- Submit `https://oilcert.co.uk/sitemap.xml`

### 6. Google Business Profile
- If a UC GBP already exists, add OilCert as an additional service category and link the website to oilcert.co.uk
- Otherwise create a new GBP listing — same NAP (name, address, phone) as Utilities Combined

---

## Google Ads Campaign Recommendations

Oil heating is a high-intent, low-volume niche compared with electrical or gas. Budgets stretch
further than you'd expect because there are fewer competing advertisers. Start small (£10–20/day
per campaign), watch search-term reports weekly, and add negatives aggressively.

### Campaign 1: Search — Annual Service & Safety (highest intent)
**Budget**: £15–25/day
**Bid Strategy**: Maximise conversions

**Ad Group: Annual Oil Boiler Service**
Keywords (all phrase or exact match — broad match wastes spend on this niche):
- oil boiler service hertfordshire
- oftec engineer near me
- oftec registered engineer hertfordshire
- oil boiler servicing
- annual oil boiler service
- oil boiler service near me
- cd/10 certificate
- cd 10 oil certificate
- oil boiler service st albans
- oil boiler service watford
- oil boiler service berkhamsted
- oil boiler service tring

Sample ad:
```
Headline 1: OFTEC Oil Boiler Service
Headline 2: CD/10 In 24 Hours
Headline 3: Hertfordshire & Surrounds
Description 1: OFTEC registered engineers servicing oil-fired boilers, ranges and tanks across Hertfordshire. Annual services, landlord certificates and emergency callouts.
Description 2: 5/5 from Google Reviews. Part of Utilities Combined Group. Book online or call 01442 601 383.
```

**Ad Group: AGA / Rayburn / Stanley**
Range cookers are a sub-niche with very specific search intent and almost no competition.
Worth its own ad group with bespoke copy.

Keywords:
- aga service hertfordshire
- rayburn service hertfordshire
- stanley range service
- aga oil service near me
- rayburn oil service
- aga deep clean
- rayburn nozzle change

Sample ad:
```
Headline 1: AGA & Rayburn Oil Service
Headline 2: OFTEC Registered
Headline 3: 2-3hr Deep Service
Description 1: Specialist AGA, Rayburn and Stanley range servicing across Hertfordshire. Burner strip, flueway clean, combustion re-set.
Description 2: OFTEC engineers. CD/10 in 24 hours. Book at oilcert.co.uk
```

### Campaign 2: Search — Landlord Compliance
**Budget**: £10–15/day

Keywords:
- landlord oil safety record
- landlord oil boiler certificate
- oil heating landlord compliance
- landlord oftec certificate
- annual oil safety check landlord

Sample ad:
```
Headline 1: Landlord Oil Safety Record
Headline 2: Annual Check & CD/10
Headline 3: Multi-Property Discounts
Description 1: Keep evidence of an annual safety check on the appliance and tank for every let property. OFTEC registered, fully insured.
Description 2: Multi-property pricing. Reminder service. Book your landlord oil safety check today.
```

### Campaign 3: Search — Tank Inspections (sale-driven)
**Budget**: £8–12/day. Lower volume but very high commercial intent (buyers, sellers, surveyors).

Keywords:
- oil tank inspection
- oil tank survey
- bs 5410 tank inspection
- oil tank condition report
- pre purchase oil heating inspection
- oil tank survey for house sale
- single skin oil tank replacement
- bunded oil tank assessment

### Campaign 4: Search — Emergency Callout
**Budget**: £5–10/day. Cold mornings spike search volume — set ad scheduling for 6am–10am
on October–March mornings when demand peaks.

Keywords:
- oil boiler not working
- oil boiler keeps locking out
- oil boiler emergency
- oil boiler engineer near me
- no heat oil boiler
- oil boiler stops firing

### Campaign 5: Performance Max
- Use a small set of high-quality images (oilcert hero image, the gear+drop logo, OFTEC engineer shots once available)
- Geographic target: Hertfordshire + 20-mile radius (catches Bucks, Beds, Essex)
- Let Google optimise across Search, Display, YouTube, Gmail
- Feed the same conversion actions as the search campaigns

---

## Negative Keywords (apply at account level)

Save spend by excluding these from every campaign:
- gas boiler / gas boiler service / gas safe
- electric / electrical / electrician
- biomass / pellet / wood pellet
- LPG (different fuel — separate niche)
- DIY / how to / yourself / replace nozzle yourself
- jobs / vacancy / training / oftec course
- prices / cost / how much (low conversion intent — let landlord/sale ads convert these)

---

## Facebook & Instagram Ads

Oil heating buyers skew older (40–75) and rural. Targeting works best by interest +
geographic + behaviour.

### Campaign 1: Awareness — Annual Service Reminder
**Objective**: Lead generation
**Audience**: Homeowners 40–75 in Hertfordshire, Beds, Bucks, Essex; interests:
"oil heating", "rural property", "country living", "AGA Living", "off-grid heating"
**Budget**: £8–12/day

Ad creative ideas:
- Before/after photos from real CD/10 jobs (once you have them — see Real Findings page)
- A "9 signs your oil boiler is overdue a service" carousel
- 30-second video of a burner strip-down (engineer on camera, OFTEC badge visible)

Sample copy:
```
Did you know a missed oil boiler service can void your manufacturer warranty?

Grant, Worcester Bosch, Firebird and Warmflow all expect annual servicing by an OFTEC engineer.

Skip a year, and the manufacturer can refuse to honour a £4,000+ boiler warranty.

OFTEC registered. CD/10 within 24 hours. 5/5 from Google Reviews.

Book at oilcert.co.uk
```

### Campaign 2: Landlord Compliance
**Objective**: Conversions
**Audience**:
- Interest: "Property management", "Buy to let", "Landlord"
- Location: Hertfordshire + adjacent counties
- Behaviour: Small business owner
**Budget**: £8–12/day

Sample copy:
```
Landlords with oil-heated properties:

Insurers are starting to ask whether the boiler has had an annual safety check
and whether the tank meets BS 5410. A missing record can refuse a claim after a leak
or a CO event.

We provide landlord oil safety records, annual servicing and tank condition reports
across Hertfordshire — multi-property discounts available.

oilcert.co.uk
```

### Campaign 3: Retargeting
**Objective**: Conversions
**Audience**: Site visitors who didn't book (requires Meta Pixel — see `SETUP-CHECKLIST.md`)
**Budget**: £4–8/day

---

## Integrating with Utilities Combined (utilitiescombined.co.uk)

### Cross-Linking Strategy
1. Add an "Oil Heating" service link in the Utilities Combined services dropdown pointing to oilcert.co.uk
2. Add a card on the UC homepage promoting OilCert alongside Electricert and Plumcert (the three sister brands)
3. The OilCert footer already cross-links to utilitiescombined.co.uk and the two sister brands
4. Share the GA4 property across UC, OilCert, Electricert and Plumcert for one unified reporting view

### Unified Google Ads Account
- Run all four sites under one Google Ads MCC account
- Shared remarketing audience: anyone who hits any UC-family domain
- Cross-promote: show OilCert ads to UC, Electricert and Plumcert visitors and vice versa
- One conversion tracking tag, multiple conversion actions per brand

---

## SEO Already Implemented

- Semantic HTML5 with proper heading hierarchy
- Schema.org `LocalBusiness` structured data with `OfferCatalog` of all five services
- Schema.org `FAQPage` covering CD/10, service intervals, AGA timing and tank inspection
- Open Graph and Twitter Card meta on the homepage (og:image points at the hero)
- `theme-color` meta for mobile browser chrome (charcoal #1F2937)
- Descriptive `<title>` and `<meta description>` on every page
- Canonical URLs
- XML sitemap at `/sitemap.xml`
- `robots.txt` allows all (admin panel is hidden by obscurity, not by robots — see SETUP)
- Real Findings page is `noindex, nofollow` and omitted from sitemap until photos are uploaded
- Mobile-responsive, no heavy frameworks, accessible (skip-link, ARIA, semantic elements)

### Additional SEO Actions

1. **Google Search Console**: verify oilcert.co.uk, submit sitemap, monitor coverage weekly
2. **Google Business Profile**: ensure GBP shows OFTEC accreditation; same NAP as UC
3. **Local directories**: list on Checkatrade, Yell, TrustATrader, the OFTEC "find an engineer" tool
4. **Sister-brand backlinks**: a single in-content link from electricert.co.uk and plumcert.co.uk to oilcert.co.uk (and vice-versa) materially improves crawlability and topical authority
5. **Blog content** (longer-term — `/pages/blog/`):
   - "How often should an oil boiler be serviced?"
   - "What is on a CD/10 certificate?"
   - "BS 5410 oil tank fire-separation distances explained"
   - "Should I replace my single-skin oil tank?"
   - "AGA vs Rayburn servicing — what is different?"
   - "Landlord oil heating compliance 2026"
   - "Why is my oil boiler locking out?"

---

## Performance Targets (first 90 days)

Conservative targets for a niche brand on a £30/day blended ads budget:
- 30–50 paid clicks/day
- 8–15% conversion to lead (form, phone or WhatsApp)
- 4–8 leads/day
- £15–30 cost per lead (target — oil heating CPLs run lower than gas/electrical)
- 50%+ leads convert to booked jobs at the call-back stage
- Organic traffic should overtake paid by month 6 if you publish 1–2 blog posts per month
