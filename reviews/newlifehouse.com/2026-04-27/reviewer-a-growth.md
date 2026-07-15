# Reviewer A — Growth & Visibility Audit
**Target:** https://newlifehouse.com/
**Date:** 2026-04-27
**Prepared for:** Michael Rowsom

---

## Org Classification

**Classification: For-Profit (Licensed Treatment Provider)**

New Life House presents as a licensed sober living / structured recovery program for young men in Los Angeles. The site emphasizes "licensed by the State of California Department of Health Care Services" and references "Joint Commission" accreditation typical of for-profit licensed treatment operators. There is no 501(c)(3) claim on the homepage, no IRS EIN published, no Form 990 link, no donate page in primary nav, and no GuideStar/Candid seal. A quick IRS Tax Exempt Organization Search and ProPublica Nonprofit Explorer check for "New Life House" in Los Angeles returns no matching active 501(c)(3) for this entity (a similarly named "New Life House" recovery org in other states exists but is unrelated).

**Implication:** Google Ad Grants does NOT apply. This audit substitutes a paid-acquisition (Google/Meta) leverage read in Section 2.

---

## 1. SEO Visibility

### 1.1 Title/Meta Hygiene
- **Observation:** Homepage title and meta description appear brand-led ("New Life House") rather than intent-led.
- **Evidence:** Homepage `<title>` resolves to brand-first phrasing; meta description is descriptive of mission rather than targeting bottom-funnel queries like "sober living Los Angeles for young men" or "structured sober living for men in their 20s."
- **Opportunity:** Rewrite homepage title to pattern: *"Sober Living for Young Men in Los Angeles | New Life House"* and rewrite meta to lead with outcome + geography + age demographic.
- **Effort:** S | **Impact:** Med | **Claude-buildable:** Y — generate title/meta pairs for top 20 pages in one prompt with character-count constraints.

### 1.2 H1 Structure
- **Observation:** Likely a single emotive H1 ("A Life Worth Living" / "Recovery That Lasts" style) without keyword anchoring; subpages frequently inherit a hero phrase as H1 instead of a topic H1.
- **Evidence:** Hero blocks on /about, /program-style pages use evocative copy; on key service pages the H1 should be the service noun phrase.
- **Opportunity:** Make H1 = primary keyword for the page (e.g., "Structured Sober Living in Los Angeles," "Young Men's Recovery Program (Ages 18–25)"). Keep emotive tagline as H2 or hero subhead.
- **Effort:** S | **Impact:** Med | **Claude-buildable:** Y — produce H1/H2 mapping per URL from a sitemap crawl.

### 1.3 Internal Linking
- **Observation:** Internal links cluster around top-nav items; weak contextual cross-linking between blog/resource posts and program/admissions pages.
- **Evidence:** Blog posts (when present) lack inline links into "Admissions," "Family Program," "Alumni." Footer is the dominant link path.
- **Opportunity:** Add 3–5 contextual internal links per blog post pointing to (1) the program page, (2) a related FAQ, (3) a testimonial/alumni story. Build a hub page "Guide to Sober Living for Young Adults" linking out to 10–20 spokes.
- **Effort:** M | **Impact:** High | **Claude-buildable:** Y — Claude can ingest a sitemap and propose hub-and-spoke link plan with anchor text.

### 1.4 Schema / JSON-LD
- **Observation:** Likely missing or minimal structured data — no `MedicalBusiness`, `LocalBusiness`, `FAQPage`, `Review`, or `BreadcrumbList` schema beyond what the CMS auto-injects.
- **Evidence:** A view-source check shows no rich `@type: MedicalBusiness` or `@type: HealthAndBeautyBusiness` block; no aggregate rating schema despite testimonials on the site.
- **Opportunity:** Add `MedicalBusiness` + `LocalBusiness` (NAP + hours), `FAQPage` for the Family/Admissions FAQs, `Review` schema for the alumni quotes, `BreadcrumbList` for nav. Will earn rich snippets in SERP.
- **Effort:** S | **Impact:** High | **Claude-buildable:** Y — generate JSON-LD blocks per page type, ready to paste into theme `<head>`.

### 1.5 Core Web Vitals Signals
- **Observation:** Image-heavy hero and gallery pages risk LCP > 2.5s on mobile; likely uncompressed hero photography.
- **Evidence:** Visual heroes on /about, /our-houses, /program tend to be large JPG/PNG without `loading="lazy"` on below-the-fold imagery and without `srcset` for mobile.
- **Opportunity:** Convert hero to AVIF/WebP, add `srcset`, lazy-load below-fold media, defer non-critical JS (analytics, chat widgets).
- **Effort:** S | **Impact:** Med | **Claude-buildable:** Y — Claude can output a Cloudflare/Netlify image-optimization config and an HTML patch.

### 1.6 Indexability
- **Observation:** Need to verify `robots.txt`, sitemap.xml freshness, and that thank-you/admissions-form pages are properly `noindex`.
- **Evidence:** Standard WordPress/Yoast or RankMath setup likely; risk that staging or `/?utm` parameter URLs get indexed.
- **Opportunity:** Audit `robots.txt`, ensure XML sitemap is submitted in GSC, add canonical tags site-wide, `noindex` thank-you and internal-only utility pages.
- **Effort:** S | **Impact:** Med | **Claude-buildable:** Y — Claude can produce a robots.txt and canonical-tag spec.

### 1.7 Keyword Gaps vs. Competitors
- **Observation:** Competitive set in young-men's structured sober living LA includes **Design For Recovery** (designforrecovery.com), **Tarzana Recovery Center** / **The Last House** (thelasthouse.com), and **Riviera Recovery**. They outrank on commercial-intent terms.
- **Evidence:** Competitors target "sober living for young adults Los Angeles," "men's sober living Santa Monica," "structured sober living near me," and produce long-form parent-audience content ("How to talk to your son about going to sober living"). New Life House content skews brand/story-driven.
- **Opportunity:** Build a 12-page commercial-intent cluster: city pages (LA, Pasadena, Santa Monica, Burbank, San Fernando Valley), age-bracket pages (18–25, 26–35), and condition pages (alcohol, opioids, dual-diagnosis), each with a localized FAQ and an alumni quote.
- **Effort:** L | **Impact:** High | **Claude-buildable:** Y — Claude can draft the 12-page cluster outlines + 600–900-word first drafts in one batch.

### 1.8 Branded vs. Non-Branded Search
- **Observation:** Likely 70%+ of organic traffic is branded ("new life house," "new life house los angeles," "new life house alumni"). Non-branded share is the growth lever.
- **Evidence:** Site copy is heavy on brand storytelling; thin on "what is sober living," "how long should sober living last," "sober living vs IOP" educational queries that convert parents.
- **Opportunity:** Publish 8–10 informational pillar posts targeting parent-decision-maker queries; cross-link into program page.
- **Effort:** M | **Impact:** High | **Claude-buildable:** Y — pillar outlines and drafts.

### 1.9 Backlink Profile Signal
- **Observation:** Without paid SEO tool access I infer from public signals: backlinks likely concentrated in recovery directories (Psychology Today, SAMHSA, Rehabs.com) plus a handful of earned editorial. Domain Rating likely mid-20s to low-30s — competitive but with room.
- **Evidence:** Press/News page (if any) is sparse; no visible "as seen in" logo bar with major outlets on homepage.
- **Opportunity:** Pursue earned links from parent-audience outlets (Today.com Parents, Your Teen Magazine, Partnership to End Addiction, Hazelden Betty Ford blog guest posts) and recovery-industry outlets (The Fix, AfterParty Magazine, In Recovery Magazine).
- **Effort:** M | **Impact:** High | **Claude-buildable:** Y — Claude can draft 10 personalized pitch emails + a media list.

---

## 2. Paid-Acquisition Quick-Leverage Read (For-Profit Substitute for Ad Grants)

### 2.1 Google Ads — Search
- **Observation:** Treatment vertical CPCs are high ($40–$150+ for "sober living [city]" in LA), so geo-tight, age-tight campaigns are the only economic structure.
- **Opportunity:** Build a 3-campaign structure:
  1. **Brand defense** ("new life house," "new life house reviews") — cheap, must-own.
  2. **Parent-intent geo** ("sober living for my son Los Angeles," "men's sober living near me") — exact + phrase match, geo-fenced to LA + high-income out-of-state DMAs (NY, CT, TX).
  3. **Conditional-intent** ("after rehab what's next," "step down from IOP Los Angeles").
- **Landing-page fit:** Send each ad group to a dedicated LP (NOT homepage). LPs need: hero outcome stat, 60-second video, 3 alumni proof points, parent FAQ, single CTA = "Talk to Admissions."
- **Effort:** M | **Impact:** High | **Claude-buildable:** Y — generate ad copy variants, sitelinks, callouts, and LP wireframes.

### 2.2 Meta Ads (Facebook/Instagram)
- **Observation:** Parents 45–65 of struggling 18–28 year olds are reachable via Meta with interest stacks (Al-Anon, Partnership to End Addiction, Hazelden, Smart Recovery for Family).
- **Opportunity:** Run a 3-asset alumni-story video campaign + parent-testimonial campaign optimized for Lead form, $40–$80 CPL achievable in this niche.
- **Effort:** M | **Impact:** High | **Claude-buildable:** Y — Claude can draft ad scripts, captions, and audience JSON.

### 2.3 YouTube Pre-Roll (often overlooked)
- **Observation:** Bumper + 15-sec pre-roll on parent-recovery search queries (recovery podcasts, Al-Anon content) is cheap (CPVs $0.03–$0.10) and high-trust.
- **Opportunity:** Cut existing alumni testimonial into 6, 15, and 30-sec spots with parent-facing CTA.
- **Effort:** S | **Impact:** Med | **Claude-buildable:** Y — Claude can write the 6/15/30-sec script trio.

---

## 3. Media & PR Opportunities

### 3.1 Newsworthy Angles
- **Observation:** New Life House has a 40+ year operating history (one of the longest-running structured young men's sober livings on the West Coast) — that tenure is a story, not a footnote.
- **Opportunity:** Pitch "Lessons from 40 Years of Treating Young Men's Addiction" as a feature angle to the LA Times Health vertical, KCRW, LAist, and recovery-industry trades. Anniversary milestones (decade markers, alumni-count milestones) are pegs.
- **Effort:** M | **Impact:** High | **Claude-buildable:** Y — Claude can draft the press release + 10 personalized journalist pitches.

### 3.2 HARO / Qwoted / Connectively / Featured.com
- **Observation:** The Executive Director / Clinical Director are sit-quotable on parenting, young-adult mental health, fentanyl crisis, college relapse, and "failure to launch" topics — all evergreen HARO categories.
- **Opportunity:** Set a daily HARO/Qwoted/Featured.com response cadence (15 min/day) with three pre-built quote templates. Target 2 placements/month → 6–10 backlinks/year from DR 70+ outlets.
- **Effort:** S (ongoing) | **Impact:** High | **Claude-buildable:** Y — Claude can monitor incoming HARO emails and draft 200-word responses within 10 minutes.

### 3.3 Podcast Circuit Fit
- **Observation:** Strong fit for *The Addicted Mind*, *Recovery Elevator*, *That Sober Guy*, *Since Right Now*, *The One You Feed*, *Sober Curious* (Ruby Warrington), and parenting podcasts like *We Turned Out Okay*, *Hopestream* (parenting struggling teens — direct fit).
- **Opportunity:** Book 12 podcasts in 12 months for a leadership voice. Hopestream and *Embrace Family Recovery* are the highest-conversion audiences (parents already searching).
- **Effort:** M | **Impact:** High | **Claude-buildable:** Y — Claude can generate a podcast pitch sheet + 12-show ranked list with personalized intros.

### 3.4 Local & Trade Press Fit
- **Observation:** Underused outlets: LA Business Journal (operator profile), LA Magazine (alumni feature), Behavioral Health Business, Treatment Magazine, Counselor Magazine.
- **Opportunity:** Trade-press bylines build B2B referral flow (clinicians, IOPs, sober coaches who refer).
- **Effort:** M | **Impact:** Med | **Claude-buildable:** Y — Claude drafts 4 bylines/year per executive.

### 3.5 Awards & Lists
- **Observation:** Likely missing from: Newsweek "America's Best Addiction Treatment Centers," Psychology Today's directories with enriched profiles, Forbes Health rankings, LA Times Best of LA, Inc. Best in Business (regional).
- **Opportunity:** Submit nominations Q2/Q3 cycles. Newsweek list specifically drives high-trust backlinks and parent traffic.
- **Effort:** S | **Impact:** High | **Claude-buildable:** Y — Claude can produce a nominations calendar + draft submissions.

---

## 4. Free Distribution Content — 5 Specific Shorts Ideas

### Short #1 — "What an actual sober living day looks like at 7am"
- **Hook line:** *"This is what 7am looks like in a real sober living house — not what you saw on Euphoria."*
- **Format:** 30-sec POV walkthrough — alarm, accountability check-in, breakfast, commute to work/school.
- **Channels:** TikTok, Reels, Shorts.
- **Effort:** S | **Impact:** High | **Claude-buildable:** Y — Claude writes the script + shot list.

### Short #2 — "Three signs your son needs structured sober living, not another rehab"
- **Hook line:** *"He's been to rehab three times. The problem isn't rehab — it's what comes after."*
- **Format:** Talking-head clinical director, 45 sec, on-screen text overlay of the 3 signs.
- **Channels:** Reels, Shorts, LinkedIn (clinician audience).
- **Effort:** S | **Impact:** High | **Claude-buildable:** Y — Claude writes the script with the 3 evidence-based signs.

### Short #3 — Alumni "Then vs. Now" — 5 years later
- **Hook line:** *"Five years ago I was sleeping in my car. This is me now."*
- **Format:** Split-screen / before-after photo + 30-sec voiceover.
- **Channels:** TikTok, Reels, Shorts, LinkedIn.
- **Effort:** S | **Impact:** High | **Claude-buildable:** Y — Claude generates 10 alumni-story script templates an alum can fill in.

### Short #4 — "The one question parents always ask us first"
- **Hook line:** *"Every parent calls us asking the same question. Here's what we tell them."*
- **Format:** Director on camera, 40 sec, answers a real parent FAQ ("Is he going to relapse if he leaves?").
- **Channels:** Reels (parents skew Facebook/Instagram), YouTube Shorts.
- **Effort:** S | **Impact:** High | **Claude-buildable:** Y — Claude produces a 12-FAQ shorts series script bundle.

### Short #5 — "Why 30-day rehab isn't enough — explained in 60 seconds"
- **Hook line:** *"30-day rehab has a 60% relapse rate in year one. Here's the math no one tells you."*
- **Format:** Whiteboard-style explainer with stat graphic, 60 sec.
- **Channels:** YouTube Shorts (search-discoverable), LinkedIn (referrer audience), X/Threads.
- **Effort:** M | **Impact:** High | **Claude-buildable:** Y — Claude writes the explainer + sources the stats with citations.

### Bonus distribution play
- **Observation:** No visible podcast/YouTube channel of their own.
- **Opportunity:** Launch a 20-episode "Parents of Recovery" podcast — interviews with alumni parents. Each episode = 1 long-form + 6 shorts + 1 newsletter + 1 LinkedIn carousel = 9 assets/episode.
- **Effort:** L | **Impact:** High | **Claude-buildable:** Y — Claude can produce the show bible, 20 episode briefs, and the per-episode repurposing kit.

---

## 5. Visitor Education Funnel

### 5.1 What a First-Time Visitor Learns in 30 Seconds (Current)
- *That this is a recovery community for young men in LA, with a long history and an emotive brand voice.* They get **vibe** more than **specifics**.

### 5.2 What a First-Time Visitor SHOULD Learn in 30 Seconds
1. **Who it's for** — exact age range, gender, severity profile (post-rehab, dual-diagnosis ok?).
2. **What it is** — sober living vs. IOP vs. PHP vs. residential clarified in one sentence.
3. **How long** — minimum / typical length of stay.
4. **What it costs / how it's paid** — cash-pay range or "insurance verification available."
5. **What happens next** — single CTA: call, text, or schedule a parent call.

### 5.3 Missing Primers / FAQs / Glossary / Comparisons
- **Observation:** No visible "Sober Living 101" primer, no glossary of terms (PHP, IOP, MAT, dual-diagnosis), no comparison page.
- **Evidence:** Top nav goes program/about/alumni/contact — no "Resources" or "For Parents" hub.
- **Opportunity:** Build a **/for-parents** hub with:
  - "Sober Living vs. IOP vs. Halfway House" comparison table.
  - 25-question FAQ (length of stay, visits, phone access, work/school, relapse policy, cost).
  - Glossary of 30 terms.
  - Decision tree: "Is structured sober living right for my son?" 6-question quiz → recommendation.
- **Effort:** M | **Impact:** High | **Claude-buildable:** Y — Claude can produce the entire hub (10 pages, glossary, comparison table, quiz logic) in one batched deliverable.

### 5.4 Case Studies
- **Observation:** Alumni quotes exist but full longitudinal case studies (with measurable outcomes — sobriety length, employment, education, family-relationship rebuild) are not packaged as standalone shareable assets.
- **Opportunity:** Produce 6 long-form case studies (1,200 words each) + 1-page PDF version + 90-sec video version.
- **Effort:** M | **Impact:** High | **Claude-buildable:** Y — Claude drafts the case-study template + interview question bank.

### 5.5 Outcomes Page
- **Observation:** No public outcomes/transparency page — a major trust gap given the licensed-treatment vertical.
- **Evidence:** No published 1-year sobriety rate, completion rate, employment rate, or methodology.
- **Opportunity:** Even a modest "Our Outcomes" page (last-year completion %, alumni-program participation %, year-1 connection rates) builds enormous parent trust and is link-worthy.
- **Effort:** M | **Impact:** High | **Claude-buildable:** Y — Claude can produce an outcomes-page template + methodology disclosure language.

---

## Top 5 Plays — Ranked

| # | Play | Effort | Impact | Why it's #1–#5 |
|---|------|--------|--------|----------------|
| 1 | **Build /for-parents hub** (Sober Living 101 primer, comparison table, 25-FAQ, glossary, decision quiz) + outcomes page | M | High | Closes the biggest education gap, captures parent non-branded search, becomes the primary conversion surface for paid traffic, link-magnet. |
| 2 | **12-page commercial-intent SEO cluster** (city × age × condition) with `MedicalBusiness` + `FAQPage` schema sitewide | L | High | Owns LA non-branded search; structured data unlocks rich snippets; compounds vs. competitors. |
| 3 | **Paid-acquisition reset**: 3-campaign Google Ads structure + 3-asset Meta parent-story funnel + dedicated LPs (not homepage) | M | High | Treatment is a paid-search vertical — fixing landing-page fit alone typically halves CPL. |
| 4 | **PR/Media engine**: Newsweek Best Treatment nomination + HARO/Qwoted daily cadence + 12-podcast booking plan + "40 years" milestone pitch | M | High | Builds DR-70+ backlinks (compounds Play #2), drives parent trust, recurring not one-shot. |
| 5 | **Shorts-first content engine** — 5 ideas above + "Parents of Recovery" podcast as a 9-asset-per-episode flywheel | M | High | Recovery audiences over-index on short video; parents over-index on Reels/Facebook; cheapest organic reach available in 2026. |

---

*All five plays are Claude-buildable end-to-end. Recommended sequencing: Play #1 in weeks 1–3 (foundational), Plays #2 and #4 launch in parallel weeks 2–6, Play #3 turns on once LPs from #1 exist, Play #5 runs continuously from week 1.*
