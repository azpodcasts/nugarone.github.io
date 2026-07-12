# Nugarone Vending — One-Page Site Refresh

## Context

Pre-launch perfume vending machine company (nightclubs, bars, gyms in the UK). Existing site is a single `index.html` with inline CSS, no build step, hosted via drag-and-drop to Netlify. Prior audit (see conversation) flagged technical bugs, weak credibility signals, competing CTAs, no FAQ, and repetitive tone. Business has no installed machines yet — no real testimonials, photos-in-venue, or placement numbers exist.

## Constraints

- Stays a single-page site: one `index.html` + `images/` + `favicon_io/` + `privacy-policy.html`. No build tooling, no framework — must remain a plain drag-and-drop-to-Netlify folder.
- No fabricated social proof (no fake numbers, fake venue names, fake photos-in-venue). Pre-launch honesty over inflated credibility.
- One product photo is available: a clean render of the machine on white background (shows the 4-step customer usage flow: choose perfume → pay → guide hand to nozzle → press button).

## Technical fixes

- `images/Logo 1.png` → `images/logo.png`
- `privacy policy.html` → `privacy-policy.html` (and update the footer link)
- Add product photo as `images/machine.png`
- Fix backslash path references (`favicon_io\...` → `favicon_io/...`) — backslashes are a Windows-local artifact that can break on real servers/case-sensitive hosts.
- Fix `<link rel="manifest" href="/site.webmanifest">` → point at `favicon_io/site.webmanifest` (file exists there, not at root).
- Fix the "Machine Specifications" table markup bug: header row currently has 1 column div while each data row has 4 — replaced entirely by the new spec-list layout (see below), so the mismatch is moot.

## Page structure (single page, anchor nav)

1. **Nav** — logo, anchors to Features / Specs / Profit Share / FAQ / Contact, Calendly as the single nav CTA.
2. **Hero** — "Effortless Revenue." headline retained. Subhead tightened to concrete language. Adds a "Perfect for: Nightclubs · Bars · Gyms" tag line to self-qualify visitors. Single Calendly CTA (drops the old "Discover More →" scroll-anchor CTA competing for attention).
3. **Features grid** — existing 6 cards, copy tightened (no rhetorical asides, "no cost, no hassle" said once clearly rather than repeated in variant phrasing).
4. **Machine showcase (NEW)** — product photo alongside a redesigned two-column spec list (label → value: maintenance access, power requirements, capacity, payment options, locking mechanism, mounting options). Replaces the old fake "comparison table" styling (there is nothing being compared against, so the comparison framing and the unused "badge" pseudo-element are dropped).
5. **4-Step Onboarding Process** — existing content (intro call → site visit → install & stock → earn), light copy tightening only.
6. **Profit Share** — existing 3-step earnings explanation (sales tracked digitally → paid monthly → transparent reporting) + Calendly CTA.
7. **FAQ (NEW)** — replaces the old fabricated testimonial section. Addresses real objections drawn from existing in-person pitch language: noise/staff involvement, "what if it doesn't sell", who owns the stock, cancellation terms.
8. **Final CTA** — Calendly as primary action; includes "Currently onboarding venues UK-wide" line (honest framing — no specific city claims since there's no placement history yet).
9. **Footer** — email, phone, fixed privacy policy link.

## CTA strategy

Calendly (`https://calendly.com/abanjoko-nugaronevending`) is the single primary CTA, repeated at consistent visual weight in nav, hero, and final CTA section. Email (`mailto:abanjoko@nugaronevending.co.uk`) and phone remain available but demoted to footer-only, secondary weight. No contact form (Netlify Forms) — Calendly serves as the single low-friction first step per the user's choice.

## Copy tone

Punchy, confident headlines retained (e.g. "Effortless Revenue."). Sub-copy and body text tightened to be concrete and factual rather than rhetorical ("You get why we call it effortless revenue now?" and similar asides removed). No invented stats, testimonials, or placement claims anywhere on the page.

## SEO

Update `<title>` and meta description to work in targeted, natural keyword phrases: "perfume vending machine UK", "nightclub vending machine", "gym vending machine income" — integrated into hero/feature copy rather than only stuffed into meta tags.

## Out of scope

- Contact form / Netlify Forms (explicitly declined in favor of single Calendly CTA).
- Any real testimonial, venue photo-in-situ, or placement statistic (none exist yet; to be added post-launch).
- Multi-page structure, blog, or CMS — stays a single static HTML file.
