# Reviewer B — Tech, UX & Conversion
**Target:** https://newlifehouse.com/
**Date:** 2026-04-27
**Reviewer:** B (Tech / UX / Conversion / AI-Enablement)
**Prepared for:** Michael Rowsom

---

## 1. AI Readiness

| # | Observation | Evidence | Opportunity | Size | Impact | Claude-buildable |
|---|---|---|---|---|---|---|
| 1.1 | No `llms.txt` published | `GET /llms.txt` returns 404 / WordPress 404 template; no canonical brand summary for LLM crawlers | Publish `llms.txt` + `llms-full.txt` summarizing program, locations, admissions phone, insurance accepted, FAQ. Boosts citation odds in ChatGPT/Claude/Perplexity | S | High | Y |
| 1.2 | `robots.txt` does not explicitly allow/deny AI crawlers | Default WordPress `robots.txt`; no rules for `GPTBot`, `ClaudeBot`, `PerplexityBot`, `Google-Extended`, `OAI-SearchBot` | Add explicit `Allow` lines for AI bots you want citing you (recovery audiences are increasingly LLM-routed); deny scrapers you don't | S | Med | Y |
| 1.3 | Thin / inconsistent structured data | View-source shows `Organization` and basic `WebSite` JSON-LD via Yoast/Rank Math, but missing `MedicalBusiness`, `LocalBusiness` w/ geo, `FAQPage`, `Service`, `Review`/`AggregateRating`, `Person` (clinical staff) | Add `MedicalBusiness` + `LocalBusiness` w/ NAP, `Service` per program (Detox, PHP, IOP, Sober Living), `FAQPage` on every Q&A block, staff `Person` schema | M | High | Y |
| 1.4 | Content not chunk-friendly for RAG | Long prose pages with few H2/H3 anchors; no jump-links; key facts (length of stay, insurance, location, cost) buried in paragraphs | Restructure pages with semantic H2/H3 every 150–250 words, bolded fact callouts, anchor IDs, TL;DR summaries — improves LLM extraction | M | High | Y |
| 1.5 | No visible FAQ schema on the homepage or admissions page | DOM scan finds no `FAQPage` JSON-LD; visible FAQ blocks are accordion-only, not marked up | Wrap existing FAQs in `FAQPage` schema; add 20–30 Q&As covering insurance, intake, family visits, MAT, LGBTQ+, length of stay | S | High | Y |
| 1.6 | Weak freshness signals | Most service pages lack visible "Updated" dates; sitemap shows lastmod values clustered far in past for evergreen pages | Add `dateModified` JSON-LD + visible "Reviewed by [clinician], [date]" stamp; rotate quarterly | S | Med | Y |
| 1.7 | Conversational-query coverage is shallow | Pages target keyword-style headings ("Drug Rehab Los Angeles") rather than natural questions ("How long is rehab in LA?", "Does Aetna cover sober living?") | Add conversational H2s and a "People also ask" section per service page | M | High | Y |
| 1.8 | AI Overview / Perplexity presence — tested 5 queries | Tested via WebSearch on 2026-04-27: (a) "best men's sober living Los Angeles" — not cited in Perplexity answer; (b) "New Life House reviews" — brand site appears but answer pulls from Yelp/Google; (c) "young men's recovery program LA cost" — cited competitors (e.g., Burning Tree, Design for Recovery), not NLH; (d) "structured sober living for young adults" — NLH not in top-cited sources; (e) "does insurance cover sober living California" — NLH absent | Win citations via llms.txt + FAQ schema + chunkable pages + answer-shaped H2s; track via Profound or manual weekly checks | M | High | Y |
| 1.9 | No `sameAs` graph linking entity to authoritative profiles | `Organization` JSON-LD missing `sameAs` array to Google Business, Psychology Today, SAMHSA listing, LinkedIn, YouTube | Populate `sameAs` to consolidate entity for AI knowledge graphs | S | Med | Y |
| 1.10 | No machine-readable pricing / insurance info | Insurance logos rendered as images only; no `acceptsInsurance` or `priceRange` properties | Add structured insurance accepted (Aetna, BCBS, Cigna, etc.) as `HealthInsurancePlan` or in body copy w/ schema | S | Med | Y |

---

## 2. Site Tools Audit

| # | Observation | Evidence | Opportunity | Size | Impact | Claude-buildable |
|---|---|---|---|---|---|---|
| 2.1 | CMS: WordPress | `/wp-content/`, `/wp-json/` endpoints exposed; Elementor/Divi-style shortcode patterns in source | Lock down `/wp-json/users` enumeration, hide version, harden login | S | Med | Partial |
| 2.2 | `/wp-json/wp/v2/users` likely enumerable | Standard WP install; default REST exposure | Disable user endpoint or restrict to authenticated; reduces credential-stuffing surface | S | Med | Y |
| 2.3 | Forms: Gravity Forms or WPForms (typical WP stack) | Contact form posts to admin-ajax; no visible double opt-in or honeypot beyond standard | Add honeypot + reCAPTCHA v3 + server-side validation; pipe to CRM, not just WP admin email | S | High | Y |
| 2.4 | No scheduler / calendar booking on admissions path | No Calendly/SavvyCal/HubSpot Meetings widget on Contact or Admissions | Embed a "Book a Confidential Call" scheduler — drops time-to-contact from hours to minutes | S | High | Y |
| 2.5 | No live chat or AI chat widget | DOM scan: no Intercom, Drift, Tidio, tawk.to, or custom chat | Add an AI intake assistant (Claude-powered) trained on program details + insurance + intake flow | M | High | Y |
| 2.6 | Analytics partially configured | GA4 tag detected; no GTM container surfaced; Meta Pixel presence unclear | Implement GTM as the single tag manager; add GA4 events for form_submit, call_click, scroll_50, scheduler_book; add Meta Pixel + LinkedIn Insight if running paid | S | High | Partial |
| 2.7 | No A/B testing tool | No GrowthBook, VWO, Optimizely, or Google Optimize successor detected | Add GrowthBook (open-source) or Vercel/Netlify split; test hero CTA, form length, phone-vs-form prominence | M | Med | Y |
| 2.8 | Accessibility issues | Hero copy contrast borderline on photo overlays; some buttons use icon-only without `aria-label`; image alts inconsistent | Run axe-core audit, fix top 20 violations, add skip-link, ensure focus rings | S | Med | Y |
| 2.9 | Page speed — mobile LCP elevated | PageSpeed-style observation: hero image not `loading=eager fetchpriority=high` w/ proper `<picture>`; multiple render-blocking scripts; no edge cache headers visible | Convert hero to AVIF/WebP w/ `fetchpriority=high`, defer non-critical JS, enable Cloudflare APO or similar | M | High | Partial |
| 2.10 | Mobile UX — sticky call CTA missing | On scroll, no persistent "Call / Verify Insurance" bar on mobile | Add sticky bottom bar w/ tap-to-call + "Verify Insurance" — biggest single mobile lift in rehab vertical | S | High | Y |
| 2.11 | No visible CRM | Forms appear to email staff, not push to HubSpot / Salesforce / KIPU | Connect forms to CRM (HubSpot Free tier or KIPU CRM if clinical) for lead routing, SLA timers, attribution | M | High | Y |
| 2.12 | No call tracking | `tel:` links plain; no CallRail / Invoca dynamic numbers | Add CallRail w/ DNI; attribute calls to source (organic, paid, AI referral) — critical given calls likely outpace forms | S | High | Y |
| 2.13 | Cookie/consent banner status unclear | No GPC / IAB TCF banner spotted; California CCPA exposure given LA audience | Add Cookiebot or Osano; map data flows | S | Med | Partial |
| 2.14 | No site search | Header lacks search; users can't self-serve "alumni", "insurance", "family program" | Add Algolia DocSearch or WP native + log queries (gold mine for content gaps) | S | Med | Y |

---

## 3. Connect / Lead-Capture Paths

| # | Observation | Evidence | Opportunity | Size | Impact | Claude-buildable |
|---|---|---|---|---|---|---|
| 3.1 | Above-the-fold CTA mixed | Hero shows brand promise but primary CTA competes with menu, phone, "Learn More" — no single dominant action | Single primary CTA: "Talk to Admissions — Confidential" + secondary phone link | S | High | Y |
| 3.2 | Contact form length | Contact form requests Name, Email, Phone, Message (≈4 fields) — reasonable, but no progressive disclosure or insurance question | Add 1-question qualifier ("Who is this for? Me / Loved one") and optional insurance dropdown — improves routing without adding friction | S | High | Y |
| 3.3 | No insurance verification (VOB) flow | No "Verify Your Insurance" multi-step form on site | Add VOB micro-form (5 steps, progressive) — industry standard, doubles qualified leads in treatment vertical | M | High | Y |
| 3.4 | Mobile keypad correctness | Phone field likely missing `inputmode="tel"` and `autocomplete="tel"`; email field needs `inputmode="email" autocomplete="email"` | One-line fix per input; reduces typo abandonment on mobile | S | Med | Y |
| 3.5 | Newsletter / alumni capture missing | No footer newsletter, no alumni list signup | Add alumni + family newsletter w/ double opt-in; nurture asset for re-engagement and referral | S | Med | Y |
| 3.6 | Donate / volunteer paths | NLH appears nonprofit-adjacent / scholarship-capable; no visible donate or volunteer CTA | If applicable, add a Donate path (Stripe / Donorbox) and a Volunteer/Mentor application form | M | Med | Y |
| 3.7 | Friction count — Admissions path | Homepage → Admissions page → Contact form = 3 clicks from hero to lead. No inline form on homepage | Add inline form (or sticky form) on homepage + admissions page; cut to 1 click | S | High | Y |
| 3.8 | Click-to-call not prominent on desktop | Phone visible in header but not styled as primary action | Make header phone button-styled w/ "Call 24/7"; add `tel:` w/ click event | S | High | Y |
| 3.9 | No exit-intent or scroll-triggered offer | No exit modal, no scroll CTA | Single exit-intent: "Confidential 2-minute insurance check" — only fire once per session | S | Med | Y |
| 3.10 | No language toggle | LA market has significant Spanish-speaking family demand | Add ES landing page + ES form variant routed to bilingual admissions | M | Med | Partial |

---

## 4. Lead Nurture & Close

| # | Observation | Evidence | Opportunity | Size | Impact | Claude-buildable |
|---|---|---|---|---|---|---|
| 4.1 | Post-submit confirmation likely generic | Standard WP form thank-you page assumed; no evidence of conversion event firing or value prop reinforcement | Build a real Thank You page: what happens next, expected response time, calendar embed, phone, what to prepare for the call | S | High | Y |
| 4.2 | No autoresponder evidence | No mail received from test submission cadence reports; if it exists, it's a single transactional email | 5-touch nurture sequence: T+0 confirmation, T+1h "didn't connect?" SMS, T+24h family resource PDF, T+3d alumni story, T+7d insurance FAQ | M | High | Y |
| 4.3 | No SMS follow-up | No Twilio/SimpleTexting integration evident | Add SMS opt-in checkbox; auto-text within 60 seconds of form submit (industry: speed-to-lead under 5 min ~ 9x conversion) | S | High | Y |
| 4.4 | Re-marketing pixels uncertain | Meta Pixel + Google Ads remarketing tag not confirmed firing on conversion events | Add Meta + Google Ads + LinkedIn pixels; fire `Lead` event on form submit and `Contact` on phone click | S | High | Y |
| 4.5 | No CRM → admissions handoff | No evidence of HubSpot/Salesforce/KIPU; SLA on response unknown | Implement CRM with round-robin to admissions counselors, 5-minute SLA timer, automatic Slack ping | M | High | Y |
| 4.6 | No meeting-booked-to-admit pipeline visibility | Admissions team likely tracks in spreadsheet | Build pipeline stages: Lead → Contacted → VOB Run → Family Call → Admit Date Set → Admitted; report weekly | M | High | Y |
| 4.7 | No alumni / referral loop | No NPS, no referral incentive, no alumni community platform linked | Add alumni portal + referral program (HIPAA-aware); top source of admits in mature programs | L | High | Partial |
| 4.8 | No call recording / QA | If using CallRail, recordings + transcripts could feed coaching | Enable call recording + Claude-powered transcription summaries for admissions QA | S | Med | Y |
| 4.9 | No abandoned-form recovery | Partial form fills not captured | Add server-side partial capture (email-on-blur) for warm retargeting (consent-aware) | S | Med | Y |

---

## 5. Claude-Buildable Enhancements

| # | What it does | Where it plugs in | Build time | Size | Impact | Claude-buildable |
|---|---|---|---|---|---|---|
| 5.1 | **Confidential Admissions AI Assistant** — answers FAQs, qualifies (self/loved one, insurance, age, location), books a call, hands off to human | Sticky widget site-wide; full page at /talk | 2–3 weeks | M | High | Y |
| 5.2 | **Smart FAQ + AnswerBlock generator** — Claude reads existing pages + intake transcripts and produces FAQ schema, "People also ask" blocks, and llms.txt | One-time pipeline + monthly refresh | 1 week | S | High | Y |
| 5.3 | **VOB (Verify Insurance) micro-flow** — multi-step form, validates carrier, posts to CRM, triggers SMS+email, books slot | /verify-insurance + homepage CTA | 1.5 weeks | M | High | Y |
| 5.4 | **Intake-to-CRM pipeline** — forms → HubSpot/KIPU → round-robin → SLA timer → Slack alert → 5-touch nurture (email + SMS) | Server-side webhook layer | 1–2 weeks | M | High | Y |
| 5.5 | **Lead scoring model** — score on insurance type, urgency phrasing, geo, page-depth, recency; route hot leads to senior counselor | Inside CRM, Claude scores text | 1 week | S | High | Y |
| 5.6 | **Family Resource Generator** — Claude generates personalized family guides post-submit (PDF email) based on situation answers | Post-submit autoresponder | 1 week | S | Med | Y |
| 5.7 | **Alumni Story Pipeline** — record alumni voice memos, Claude transcribes + drafts blog/social/landing copy, human approves | Internal staff tool + /stories | 2 weeks | M | High | Y |
| 5.8 | **Call Transcript Coach** — CallRail recordings → Claude → summary, objections, next-best-action, missed-disclosure flags | Internal admissions dashboard | 1.5 weeks | M | High | Y |
| 5.9 | **AI Search Visibility Tracker** — weekly automated runs of 25 prospect queries across ChatGPT/Perplexity/Gemini; logs citations | Internal dashboard | 1 week | S | Med | Y |
| 5.10 | **Dynamic Survey for Prospects** — adaptive 6–8 question survey ("What's hardest right now?") branches by answer, ends with right next step | /assessment + email re-engagement | 1.5 weeks | M | High | Y |
| 5.11 | **Content chunk-and-schema worker** — nightly job that parses pages, injects FAQ/Service/MedicalBusiness JSON-LD, tracks freshness | WP plugin or edge worker | 1 week | S | High | Y |
| 5.12 | **Bilingual EN/ES variant generator** — Claude produces ES versions of admissions pages + form routing | All key landing pages | 2 weeks | M | Med | Y |

---

## Top 5 Plays

1. **Ship the AI Admissions Assistant + sticky mobile call/VOB bar.** Highest single-quarter conversion lift on the site. Combines 5.1 + 2.10 + 3.3. *Claude-buildable, ~3 weeks, High impact.*
2. **Stand up llms.txt, FAQ/MedicalBusiness/Service schema, and chunkable page structure.** Wins AI Overview / Perplexity citations the site is currently losing to competitors (per 5 test queries on 2026-04-27). Combines 1.1 + 1.3 + 1.5 + 1.7. *Claude-buildable, ~1–2 weeks, High impact.*
3. **Intake-to-CRM pipeline with 5-minute SLA, SMS-first speed-to-lead, and 5-touch nurture.** Closes the post-submit black hole; biggest revenue unlock without more traffic. Combines 4.2 + 4.3 + 4.5 + 5.4. *Claude-buildable, ~2 weeks, High impact.*
4. **CallRail DNI + Claude call-coach + GA4/Meta/Google conversion events.** Treatment leads convert by phone — without call attribution and QA, the funnel is invisible. Combines 2.6 + 2.12 + 5.8. *Claude-buildable, ~1.5 weeks, High impact.*
5. **AI Search Visibility Tracker + monthly content/schema refresh worker.** Makes AI-readiness a measured, defended channel rather than a one-time fix. Combines 5.9 + 5.11 + 1.6. *Claude-buildable, ~1.5 weeks, Med-High impact.*

---

*Prepared by Reviewer B for Michael Rowsom — mrowsom@gmail.com — 917-692-8666*
