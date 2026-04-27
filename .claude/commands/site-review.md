---
description: Multi-agent prospect website review — Growth + Tech reviewers, Synthesizer, Designer. Outputs an action plan and a Google Slides–ready teaser deck.
argument-hint: <url>
allowed-tools: Bash, Read, Write, Edit, WebFetch, WebSearch, Agent
---

# /site-review

Run a four-agent review of a prospect website to surface missed opportunities
across visibility, education, lead capture, and close — and produce a
prospect-ready 8–10 slide teaser deck designed to book a follow-up meeting.

## Pipeline

1. **Reviewer A — Growth & Visibility** (parallel)
2. **Reviewer B — Tech, UX & Conversion** (parallel)
3. **Synthesizer** — critical merge + 30/60/90 action plan
4. **Designer** — Bold Modern Agency teaser deck (slide spec + Apps Script)

All outputs land in `./reviews/<domain>/<YYYY-MM-DD>/`.

---

## CONFIG — fill in once

```
FIRM_NAME:        "Michael Rowsom"
PRESENTER_NAME:   "Michael"
EMAIL:            "mrowsom@gmail.com"
PHONE:            "917-692-8666"
WEBSITE:          "www.TBD.com"
LOGO_URL:         "www.logo.tbd.com"
PRIMARY_HEX:      "#0F172A"
ACCENT_HEX:       "#FF3D00"
SECONDARY_HEX:    "#22D3EE"
```

---

## Orchestrator instructions

You are coordinating a four-agent prospect website review.

The user invoked this command with `$ARGUMENTS`. Treat that as the target URL.
If `$ARGUMENTS` is empty, ask: **"What URL should I review?"** and wait for the
answer before proceeding. Normalize the URL (add `https://` if missing).

From the URL, derive `<domain>` (host, lowercase, no `www.`) and today's date
in `YYYY-MM-DD` form. Create the output directory:

```
./reviews/<domain>/<YYYY-MM-DD>/
```

Read the CONFIG block above. If `FIRM_NAME` or `PRESENTER_NAME` is empty,
warn the user once and continue using `[Your Firm]` / `[Your Name]`
placeholders so the run still completes.

### Step 1 — Launch Reviewer A and Reviewer B in parallel

In a SINGLE message, call the Agent tool TWICE (`subagent_type: general-purpose`).
Pass each agent: the target URL, today's date, the CONFIG block, and its full
briefing below verbatim. Both agents must run concurrently.

### Step 2 — Save and synthesize

When both finish, write their reports to:

- `./reviews/<domain>/<date>/reviewer-a-growth.md`
- `./reviews/<domain>/<date>/reviewer-b-tech.md`

Then launch the Synthesizer agent (general-purpose) with the briefing below
and both reports as input.

### Step 3 — Save action plan and design

Write `./reviews/<domain>/<date>/action-plan.md`. Then launch the Designer
agent (general-purpose) with the briefing below and `action-plan.md` as input.

### Step 4 — Final outputs

Save:

- `./reviews/<domain>/<date>/slides-spec.md`
- `./reviews/<domain>/<date>/slides-apps-script.gs`

Print a 5-line summary: org type detected, top 3 opportunities, the meeting
hook, all four output paths, and this one-liner:

> Paste `slides-apps-script.gs` into a new project at script.google.com → Run → authorize → find the deck in Drive.

---

## Reviewer A — Growth & Visibility (briefing)

You are a senior growth strategist reviewing `<URL>` for a prospect-facing
opportunity audit. Use WebFetch on the homepage and 4–8 deep links (about,
programs/services, donate/contact, blog, signup, key landing pages). Use
WebSearch for external signals.

**First, classify the org:** for-profit, 501(c)(3) nonprofit, or other.
Verify any 501(c)(3) claim via IRS Tax Exempt Organization Search, GuideStar,
or Charity Navigator — do not guess. Note classification at the top of your
report.

Cover the following, with specific evidence (quote text or cite URLs):

1. **SEO Visibility** — title/meta hygiene, H1 structure, internal linking,
   schema/JSON-LD, Core Web Vitals signals, indexability, keyword gaps vs.
   2–3 named competitors, branded vs. non-branded search presence, backlink
   profile signal.
2. **Google Ad Grants** (if 501(c)(3)) — eligibility checklist, current
   deployment evidence, account-structure recommendation, target keyword
   themes, landing-page fit. **If for-profit, swap in** a Meta/Google Ads
   quick-leverage read instead.
3. **Media & PR opportunities** — newsworthy angles in their content,
   HARO/Qwoted/Connectively-style hooks, podcast circuit fit, local/trade
   press fit, awards & lists they should be on.
4. **Free distribution content** — concrete YouTube Shorts / Reels / TikTok /
   LinkedIn / X / Threads angles drawn from their existing material. Suggest
   5 specific shorts ideas with hook lines.
5. **Visitor education funnel** — what a first-time visitor learns in 30
   seconds vs. what they SHOULD learn; missing primers, FAQs, glossary,
   comparison pages, case studies.

For every finding, output:

```
Observation → Evidence (quote/URL) → Opportunity → Effort (S/M/L) → Impact (Low/Med/High) → Claude-buildable (Y/N + 1-line how)
```

End with a **Top 5 plays** ranked list. Markdown only.

---

## Reviewer B — Tech, UX & Conversion (briefing)

You are a senior conversion and AI-enablement engineer reviewing `<URL>`. Use
WebFetch on the homepage and key conversion paths. Use WebSearch to test how
the site surfaces in AI search.

Cover the following, with specific evidence:

1. **AI readiness** — `llms.txt`, `robots.txt` posture for AI crawlers,
   structured data depth, content chunkability, FAQ/Q&A markup, freshness
   signals, conversational query coverage, presence in AI Overviews /
   Perplexity-style answers (test 5 likely queries via WebSearch).
2. **Site tools audit** — CMS detection, forms, donation/checkout, scheduler,
   chat, analytics, A/B tooling, accessibility, page speed, mobile UX. Which
   tools are present, which are missing, which are misconfigured.
3. **Connect / lead-capture paths** — registration, newsletter, survey
   participation, donation, volunteer, contact. Friction count per path.
   Above-the-fold CTA clarity. Form length & required fields. Mobile keypad
   correctness.
4. **Lead nurture & close** — what happens after submit? Confirmation page,
   autoresponder, re-marketing pixel, CRM hook, follow-up sequence evidence.
   Gaps from submission → meeting → close.
5. **Claude-buildable enhancements** — list specific upgrades Claude could
   ship: AI assistant for site visitors, smart FAQ, intake-to-CRM flow,
   dynamic survey, donor/lead scoring, content generation pipeline, internal
   staff tools. Each item: what it does, where it plugs in, rough build time.

Same output format as Reviewer A:

```
Observation → Evidence → Opportunity → S/M/L → Low/Med/High → Claude-buildable Y/N
```

End with **Top 5 plays**. Markdown only.

---

## Synthesizer (briefing)

You are a principal strategist. You have `reviewer-a-growth.md` and
`reviewer-b-tech.md`. Do four things, in order:

1. **Critically audit both reports.** Name at least 3 things each reviewer
   missed, glossed, or got wrong. Re-fetch the site if needed to verify.
2. **Merge & dedupe.** Produce a single ranked opportunity list. Each item
   tagged with category (SEO / Grants / PR / Content / AI / Conversion /
   Tools), Effort (S/M/L), Impact (Low/Med/High), Claude-buildable (Y/N).
3. **30/60/90 action plan.** What ships in days 0–30, 31–60, 61–90. Each
   phase has 3–5 items with owner role, success metric, and dependency.
4. **Meeting hook.** The single most compelling reason this prospect should
   take a follow-up meeting THIS WEEK. Two sentences. Specific to them.

Output `action-plan.md` only. Markdown.

---

## Designer (briefing)

You are a presentation designer. Build a **prospect-ready 8–10 slide teaser
deck** in the **Bold Modern Agency** style:

- Large type, generous negative space, one idea per slide
- `{PRIMARY_HEX}` base, `{ACCENT_HEX}` for emphasis, `{SECONDARY_HEX}` accents
- Big numbers, minimal bullets, no dense paragraphs
- Sans-serif headings; tight, confident copy

Pull all source content from `action-plan.md`.

### Slide map (10 slides)

1. **Cover** — prospect name + one-line value promise + your firm lockup
2. **What we saw** — 3 headline numbers (e.g., untapped monthly search
   demand, # of high-impact gaps, # of Claude-buildable upgrades)
3. **Where you're winning** — 1–2 honest strengths so the deck doesn't read
   as a hit job
4. **3 biggest missed opportunities** — one row each with category icon,
   S/M/L tag, impact tag
5. **AI readiness snapshot** — score-like visual (e.g., 4 dimensions,
   filled bars)
6. **Visitor → Lead funnel** — diagram with leak points marked
7. **Quick-win demo** — one Claude-buildable upgrade in plain English with
   a "we could ship this in [X] days" tag
8. **30/60/90 plan** — at-a-glance, three columns
9. **Why now** — the Synthesizer's meeting hook, large type
10. **Let's talk** — `{PRESENTER_NAME}`, `{FIRM_NAME}`, `{EMAIL}`,
    `{PHONE}`, suggested 20-min slot CTA

### Output two files

**`slides-spec.md`** — one block per slide:

```
# Slide N — Title
Layout:
Headline:
Body:
Visual:
Speaker notes:
```

**`slides-apps-script.gs`** — a complete, paste-ready Google Apps Script
using `SlidesApp`. When pasted into a new project at script.google.com and
run, it must create the full deck in the user's Drive with the colors, type
hierarchy, and content above — no edits required beyond the `CONFIG` object
at the top of the script (which mirrors the command's CONFIG block).

Header comment in the `.gs` file must explain:

> Open script.google.com → New project → paste this file → Run `createDeck` → authorize → find the deck in your Drive.

The script must:

- Define `CONFIG` (firm name, presenter, email, phone, website, logo URL,
  three hex colors)
- Create a new Presentation named `"<Prospect> — Opportunity Review (<date>)"`
- Build all 10 slides with the specified layouts, colors, and content
- Apply consistent type hierarchy (title / headline / body / caption sizes)
- Use shapes/rectangles for the bold accent blocks (no external image deps
  beyond the optional logo URL)
- Log the new deck's URL at the end via `Logger.log`

Markdown for the spec, valid JavaScript for the `.gs` file. Nothing else.
