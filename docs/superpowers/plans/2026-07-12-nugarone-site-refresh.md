# Nugarone Site Refresh Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Rewrite `index.html` (content, hierarchy, and visual polish) per `docs/superpowers/specs/2026-07-12-nugarone-site-refresh-design.md`, fix broken file paths, and keep the whole project a single drag-and-drop-to-Netlify folder.

**Architecture:** One static `index.html` with inline `<style>` and inline `<script>` — no build step, no framework, no dependencies. All changes are direct edits to `index.html`, plus a small number of file renames/copies in `images/` and the root.

**Tech Stack:** Plain HTML5 + CSS3 + vanilla JS. Fonts via Google Fonts CDN (already wired up, untouched).

## Global Constraints

- No fabricated content: no fake testimonials, no invented placement numbers, no city-specific coverage claims. Pre-launch honesty per the spec.
- Calendly (`https://calendly.com/abanjoko-nugaronevending`) is the single primary CTA everywhere it appears. Email/phone are secondary, footer-only.
- Every internal link and asset path must use forward slashes and no spaces (works both locally on Windows and once deployed to Netlify's case-sensitive Linux filesystem).
- This project has **no git repository**. Steps below do not include `git commit` — if you want version history, run `git init` and an initial commit before starting Task 1.
- Verification for each task is manual/visual (open `index.html` in the Browser pane, since there's no test framework for a static marketing page) — not automated tests.

---

### Task 1: Technical fixes — file renames and broken paths

**Files:**
- Rename: `images/Logo 1.png` → `images/logo.png`
- Create: `images/machine.png` (copied from `C:\Users\adenu\Downloads\H8eb7e44b0b754b82b8126b210202916es.png`)
- Rename: `privacy policy.html` → `privacy-policy.html`
- Modify: `index.html:11-14` (favicon/manifest links), `index.html:583` (logo `<img>`), `index.html:782` (privacy policy link)

**Interfaces:**
- Produces: `images/logo.png` and `images/machine.png` as the asset paths every later task's HTML references.

- [ ] **Step 1: Rename the logo file**

```bash
mv "images/Logo 1.png" "images/logo.png"
```

- [ ] **Step 2: Copy the machine product photo into the project**

```bash
cp "/c/Users/adenu/Downloads/H8eb7e44b0b754b82b8126b210202916es.png" "images/machine.png"
```

- [ ] **Step 3: Rename the privacy policy file**

```bash
mv "privacy policy.html" "privacy-policy.html"
```

- [ ] **Step 4: Fix favicon/manifest link paths**

In `index.html`, replace:

```html
<link rel="apple-touch-icon" sizes="180x180" href="favicon_io\apple-touch-icon.png">
<link rel="icon" type="image/png" sizes="32x32" href="favicon_io\favicon-32x32.png">
<link rel="icon" type="image/png" sizes="16x16" href="favicon_io\favicon-16x16.png">
<link rel="manifest" href="/site.webmanifest">
```

with:

```html
<link rel="apple-touch-icon" sizes="180x180" href="favicon_io/apple-touch-icon.png">
<link rel="icon" type="image/png" sizes="32x32" href="favicon_io/favicon-32x32.png">
<link rel="icon" type="image/png" sizes="16x16" href="favicon_io/favicon-16x16.png">
<link rel="manifest" href="favicon_io/site.webmanifest">
```

- [ ] **Step 5: Fix the logo `<img>` path**

Replace:

```html
<div class="logo"><a href="#top"><img src="images\Logo 1.png" alt="Nugarone Logo" width="110" height="50"/></a></div>
```

with:

```html
<div class="logo"><a href="#top"><img src="images/logo.png" alt="Nugarone Logo" width="110" height="50"/></a></div>
```

- [ ] **Step 6: Fix the privacy policy footer link**

Replace:

```html
<a href="privacy policy.html" target="_blank" >Privacy Policy</a>
```

with:

```html
<a href="privacy-policy.html" target="_blank" >Privacy Policy</a>
```

- [ ] **Step 7: Verify in browser**

Open `index.html` in the Browser pane (navigate to the local file path). Confirm:
- The logo image renders in the nav (not a broken-image icon).
- No 404s in the console for `favicon_io/*` or `images/logo.png` (check `read_console_messages` and `read_network_requests`).
- Clicking "Privacy Policy" in the footer opens `privacy-policy.html` successfully.

---

### Task 2: SEO title and meta description

**Files:**
- Modify: `index.html:6-7`

- [ ] **Step 1: Replace title and meta description**

Replace:

```html
    <meta name="description" content="Discover how nugarone helps UK venues earn passive income with sleek, fully managed vending machines. No cost, no hassle, just revenue." />
    <title>"nugarone" vending – Passive Income for UK Venues</title>
```

with:

```html
    <meta name="description" content="Nugarone installs free perfume vending machines in UK nightclubs, bars and gyms — zero cost, fully managed, and you earn a share of every sale." />
    <title>Nugarone Vending | Perfume Vending Machines for UK Nightclubs, Bars & Gyms</title>
```

- [ ] **Step 2: Verify in browser**

Reload `index.html` in the Browser pane. Confirm the browser tab title reads "Nugarone Vending | Perfume Vending Machines for UK Nightclubs, Bars & Gyms" (use `read_page` or check the tab via `tabs_context`).

---

### Task 3: Nav + Hero rewrite

**Files:**
- Modify: `index.html:128-135` (`.hero p` CSS block, to insert `.hero-tag` after it), `index.html:584-589` (nav links), `index.html:594-601` (hero section)

**Interfaces:**
- Produces: `#faq` nav anchor, which Task 6 must land a matching `id="faq"` section for.

- [ ] **Step 1: Add `.hero-tag` CSS**

Replace:

```css
        .hero p {
            font-size: 1.25rem;
            color: #666;
            max-width: 900px;
            margin: 0 auto 40px;
            line-height: 1.5;
        }
```

with:

```css
        .hero p {
            font-size: 1.25rem;
            color: #666;
            max-width: 900px;
            margin: 0 auto 24px;
            line-height: 1.5;
        }

        .hero-tag {
            font-size: 1rem;
            font-weight: 600;
            color: #0049ff;
            margin-bottom: 32px;
        }
```

- [ ] **Step 2: Add the FAQ nav link**

Replace:

```html
            <ul class="nav-links">
                <li><a href="#features">Features</a></li>
                <li><a href="#specs">Specs</a></li>
                <li><a href="#Profit">Profit Share</a></li>
                <li><a href="#contact">Contact</a></li>
            </ul>
```

with:

```html
            <ul class="nav-links">
                <li><a href="#features">Features</a></li>
                <li><a href="#specs">Specs</a></li>
                <li><a href="#Profit">Profit Share</a></li>
                <li><a href="#faq">FAQ</a></li>
                <li><a href="#contact">Contact</a></li>
            </ul>
```

- [ ] **Step 3: Rewrite the hero section**

Replace:

```html
    <section class="hero" id="top">
        <div class="hero-badge">✨ Now Available</div>
        <h1>Effortless Revenue.</h1>
        <p>Enhance your customer experience and unlock a new income stream — all without lifting a finger. Nugarone installs sleek, compact vending machines stocked with luxury scents, fully managed and maintained for you. It’s plug-in profit with zero overhead.</p>
        <a href="#steps" target="_blank" class="hero-cta">
            Discover More →
        </a>
    </section>
```

with:

```html
    <section class="hero" id="top">
        <div class="hero-badge">✨ Now onboarding UK venues</div>
        <h1>Effortless Revenue.</h1>
        <p>Nugarone installs a sleek, fully managed perfume vending machine in your venue — at zero cost to you. We handle stocking, maintenance and repairs; you earn a share of every sale.</p>
        <p class="hero-tag">Perfect for: Nightclubs · Bars · Gyms</p>
        <a href="https://calendly.com/abanjoko-nugaronevending" target="_blank" class="hero-cta">
            Book a Free Call →
        </a>
    </section>
```

- [ ] **Step 4: Verify in browser**

Reload in the Browser pane. Confirm the hero shows the new badge, headline, tightened paragraph, the blue "Perfect for: Nightclubs · Bars · Gyms" line, and that the hero CTA button is labeled "Book a Free Call →". Click it and confirm it opens Calendly in a new tab (check `tabs_context` for the new tab, or `read_network_requests`/console — Calendly may be blocked by the preview sandbox, which is fine as long as the `href` is correct via `read_page`).

---

### Task 4: Features grid copy tightening

**Files:**
- Modify: `index.html:605-640`

- [ ] **Step 1: Replace the six feature cards**

Replace:

```html
            <div class="feature-card">
                <div class="feature-icon">💡</div>
                <h3>No Cost to You</h3>
                <p>Installed and managed at zero expense. You get why we call it effortless revenue now?</p>
            </div>
            
            <div class="feature-card">
                <div class="feature-icon">💰</div>
                <h3>Profit Share Model</h3>
                <p>You earn passive income per sale. Sharing is caring!</p>
            </div>
            
            <div class="feature-card">
                <div class="feature-icon">🔌</div>
                <h3>Compact & Sleek Design</h3>
                <p>Our machines fit neatly in restrooms, salons, or lounges.</p>
            </div>
            
            <div class="feature-card">
                <div class="feature-icon">🛠</div>
                <h3>24-Hour Repair Guarantee</h3>
                <p>Fast support and minimal downtime. Less downtime, more profits right?</p>
            </div>

            <div class="feature-card">
                <div class="feature-icon">🧴</div>
                <h3>Premium Perfume Refills</h3>
                <p>Rotating selection of top-selling scents</p>
            </div>

            <div class="feature-card">
                <div class="feature-icon">🔋</div>
                <h3>Cashless Payments</h3>
                <p>Supports contactless/tap via card or phone</p>
            </div>
```

with:

```html
            <div class="feature-card">
                <div class="feature-icon">💡</div>
                <h3>No Cost to You</h3>
                <p>Installed, stocked and maintained at zero cost — you never pay for equipment, install, or upkeep.</p>
            </div>
            
            <div class="feature-card">
                <div class="feature-icon">💰</div>
                <h3>Profit Share Model</h3>
                <p>Earn a share of every sale, paid out automatically — no admin on your end.</p>
            </div>
            
            <div class="feature-card">
                <div class="feature-icon">🔌</div>
                <h3>Compact & Sleek Design</h3>
                <p>Wall-mounted and space-saving — fits neatly in restrooms, salons, or lounges.</p>
            </div>
            
            <div class="feature-card">
                <div class="feature-icon">🛠</div>
                <h3>24-Hour Repair Guarantee</h3>
                <p>Any fault is fixed within 24 hours, so the machine is rarely out of action.</p>
            </div>

            <div class="feature-card">
                <div class="feature-icon">🧴</div>
                <h3>Premium Perfume Refills</h3>
                <p>A rotating selection of top-selling scents, restocked regularly.</p>
            </div>

            <div class="feature-card">
                <div class="feature-icon">🔋</div>
                <h3>Cashless Payments</h3>
                <p>Supports contactless card, Apple Pay and Google Pay.</p>
            </div>
```

- [ ] **Step 2: Verify in browser**

Reload in the Browser pane, scroll to the Features section, use `get_page_text` and confirm none of the old rhetorical lines ("You get why we call it effortless revenue now?", "Sharing is caring!", "Less downtime, more profits right?") remain.

---

### Task 5: Machine showcase section (replaces the fake comparison table)

**Files:**
- Modify: `index.html:279-367` (`.comparison`/`.comparison-table` CSS block → replaced with `.showcase`/spec-list CSS)
- Modify: `index.html:536-539` and `540-548` (mobile media query rules for `.comparison`/`.table-header`/`.table-row`)
- Modify: `index.html:686-738` (the `<section class="comparison" id="specs">` HTML)

**Interfaces:**
- Consumes: `images/machine.png` (produced by Task 1).

- [ ] **Step 1: Replace the comparison CSS block with showcase CSS**

Replace:

```css
        /* Comparison Table */
        .comparison {
            padding: 100px 40px;
            max-width: 1200px;
            margin: 0 auto;
        }

        .comparison h2 {
            font-size: 2.5rem;
            font-weight: 800;
            color: #1a1a1a;
            text-align: center;
            margin-bottom: 24px;
            letter-spacing: -0.02em;
        }

        .comparison-subtitle {
            text-align: center;
            color: #666;
            font-size: 1.1rem;
            margin-bottom: 60px;
        }

        .comparison-table {
            background: white;
            border-radius: 16px;
            overflow: hidden;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
            border: 1px solid #e9ecef;
        }

        .table-header {
            background: #f8f9fa;
            display: grid;
            grid-template-columns: 2fr 1fr 1fr 1fr;
            padding: 24px;
            border-bottom: 1px solid #e9ecef;
            font-weight: 700;
            color: #1a1a1a;
        }

        .table-row {
            display: grid;
            grid-template-columns: 2fr 1fr 1fr 1fr;
            padding: 20px 24px;
            border-bottom: 1px solid #f1f3f4;
            align-items: center;
        }

        .table-row:last-child {
            border-bottom: none;
        }

        .product-name {
            font-weight: 700;
            color: #1a1a1a;
        }

        .product-name.highlight {
            color: #1a1a1a;
            position: relative;
        }

        .product-name.highlight::after {
            
            position: absolute;
            top: -8px;
            right: -80px;
            background: #1a1a1a;
            color: white;
            padding: 4px 8px;
            border-radius: 4px;
            font-size: 10px;
            font-weight: 500;
        }

        .feature-status {
            color: #666;
        }

        .feature-status.good {
            color: #22c55e;
            font-weight: 600;
        }

        .feature-status.bad {
            color: #ef4444;
            font-weight: 600;
        }
```

with:

```css
        /* Machine Showcase */
        .showcase {
            padding: 100px 40px;
            max-width: 1200px;
            margin: 0 auto;
        }

        .showcase h2 {
            font-size: 2.5rem;
            font-weight: 800;
            color: #1a1a1a;
            text-align: center;
            margin-bottom: 24px;
            letter-spacing: -0.02em;
        }

        .showcase-subtitle {
            text-align: center;
            color: #666;
            font-size: 1.1rem;
            margin-bottom: 60px;
        }

        .showcase-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 60px;
            align-items: center;
        }

        .showcase-photo img {
            width: 100%;
            height: auto;
            border-radius: 16px;
        }

        .spec-list {
            display: flex;
            flex-direction: column;
            gap: 24px;
        }

        .spec-item {
            padding-bottom: 24px;
            border-bottom: 1px solid #e9ecef;
        }

        .spec-item:last-child {
            border-bottom: none;
            padding-bottom: 0;
        }

        .spec-label {
            font-weight: 700;
            color: #1a1a1a;
            margin-bottom: 6px;
        }

        .spec-value {
            color: #666;
            font-size: 15px;
        }
```

- [ ] **Step 2: Update the mobile media query**

Replace:

```css
            .comparison {
                padding: 80px 20px;
            }
            
            .table-header,
            .table-row {
                grid-template-columns: 1fr;
                gap: 12px;
            }
            
            .table-header {
                display: none;
            }
```

with:

```css
            .showcase {
                padding: 80px 20px;
            }
            
            .showcase-grid {
                grid-template-columns: 1fr;
                gap: 32px;
            }
```

- [ ] **Step 3: Replace the comparison section HTML with the showcase section**

Replace:

```html
    <section class="comparison" id="specs">
        <h2>Machine Specifications</h2>
        <p class="comparison-subtitle">Our machines are compact, secure, and built for high-traffic environments — making them the perfect low-maintenance solution for your venue.</p>
        
        <div class="comparison-table">
            <div class="table-header">
                <div>Specification Details</div>
            </div>
            
            <div class="table-row">
                <div class="product-name highlight">Maintainance Access</div>
                <div class="feature-status">Rear panel access</div>
                <div class="feature-status">Quick weekly refills</div>
                <div class="feature-status">No staff needed</div>
            </div>
            
            <div class="table-row">
                <div class="product-name">Power Requirements</div>
                <div class="feature-status">Standard UK plug (230V)</div>
                <div class="feature-status">Low energy usage</div>
                <div class="feature-status">Plug-and-play setup</div>
              <!--  <div class="feature-status bad">Restricts customization</div>//-->
            </div>
            
            <div class="table-row">
                <div class="product-name">Capacity</div>
                <div class="feature-status">30–50 sprays</div>
                <div class="feature-status">Compact refill system</div>
                 <!--  <div class="feature-status bad">No AI assistance</div>//-->
                <div class="feature-status">1–2 week stock</div>
            </div>

            <div class="table-row">
                <div class="product-name">Payment Options</div>
                <div class="feature-status">Contactless cards</div>
                <div class="feature-status">Apple/Google Pay</div>
                <div class="feature-status">Coins Accepted</div>
            </div>

            <div class="table-row">
                <div class="product-name">Locking Mechanism</div>
                <div class="feature-status">Steel-reinforced casing</div>
                <div class="feature-status">Tamper-proof access</div>
                <div class="feature-status">Dual lock system</div>
            </div>
            <div class="table-row">
                <div class="product-name highlight">Mounting Options</div>
                <div class="feature-status">Space-saving design</div>
                <div class="feature-status">Wall or floor mount</div>
                <div class="feature-status">Non-invasive install</div>
            </div>
        </div>
    </section>
```

with:

```html
    <section class="showcase" id="specs">
        <h2>See the Machine</h2>
        <p class="showcase-subtitle">Compact, secure, and built for high-traffic venues — here's what's inside.</p>

        <div class="showcase-grid">
            <div class="showcase-photo">
                <img src="images/machine.png" alt="Nugarone perfume vending machine" width="1024" height="1024" loading="lazy" />
            </div>

            <div class="spec-list">
                <div class="spec-item">
                    <div class="spec-label">Maintenance</div>
                    <div class="spec-value">Rear panel access, quick weekly refills, no staff needed</div>
                </div>
                <div class="spec-item">
                    <div class="spec-label">Power</div>
                    <div class="spec-value">Standard UK plug (230V), low energy usage, plug-and-play setup</div>
                </div>
                <div class="spec-item">
                    <div class="spec-label">Capacity</div>
                    <div class="spec-value">30–50 sprays per fill, 1–2 week stock per refill</div>
                </div>
                <div class="spec-item">
                    <div class="spec-label">Payment</div>
                    <div class="spec-value">Contactless card, Apple Pay / Google Pay, coins accepted</div>
                </div>
                <div class="spec-item">
                    <div class="spec-label">Security</div>
                    <div class="spec-value">Steel-reinforced casing, tamper-proof dual lock system</div>
                </div>
                <div class="spec-item">
                    <div class="spec-label">Mounting</div>
                    <div class="spec-value">Wall or floor mount, non-invasive install</div>
                </div>
            </div>
        </div>
    </section>
```

- [ ] **Step 4: Verify in browser**

Reload in the Browser pane, scroll to the "See the Machine" section (`#specs`). Confirm the product photo renders (no broken image icon, check `read_network_requests` for a 200 on `images/machine.png`), the six spec rows display as clean label/value pairs, and there is no leftover "highlight" badge artifact. Resize to mobile width (`resize_window` with `preset: "mobile"`) and confirm the photo and spec list stack vertically.

---

### Task 6: FAQ section (replaces the fabricated testimonial)

**Files:**
- Modify: `index.html:369-397` (`.testimonial` CSS block → `.faq` CSS)
- Modify: `index.html:550-552` (mobile media query `.testimonial` rule)
- Modify: `index.html:740-746` (`<section class="testimonial">` HTML)

**Interfaces:**
- Produces: `id="faq"` section matching the `#faq` nav link added in Task 3.

- [ ] **Step 1: Replace the testimonial CSS with FAQ CSS**

Replace:

```css
        /* Testimonial */
        .testimonial {
            background: #0049ff;
            color: white;
            padding: 100px 40px;
            text-align: center;
        }

        .testimonial-container {
            max-width: 800px;
            margin: 0 auto;
        }

        .testimonial-quote {
            font-size: 1.5rem;
            line-height: 1.5;
            margin-bottom: 32px;
            font-style: italic;
        }

        .testimonial-author {
            font-weight: 700;
            margin-bottom: 4px;
        }

        .testimonial-title {
            color: #b9b8b8;
            font-style: bold;
        }
```

with:

```css
        /* FAQ */
        .faq {
            background: #0049ff;
            color: white;
            padding: 100px 40px;
        }

        .faq-container {
            max-width: 800px;
            margin: 0 auto;
        }

        .faq h2 {
            font-size: 2.5rem;
            font-weight: 800;
            text-align: center;
            margin-bottom: 60px;
            letter-spacing: -0.02em;
        }

        .faq-item {
            border-bottom: 1px solid rgba(255, 255, 255, 0.2);
            padding: 24px 0;
        }

        .faq-item:last-child {
            border-bottom: none;
        }

        .faq-item h4 {
            font-size: 1.1rem;
            font-weight: 700;
            margin-bottom: 12px;
        }

        .faq-item p {
            color: rgba(255, 255, 255, 0.85);
            line-height: 1.6;
        }
```

- [ ] **Step 2: Update the mobile media query**

Replace:

```css
            .testimonial {
                padding: 80px 20px;
            }
```

with:

```css
            .faq {
                padding: 80px 20px;
            }
```

- [ ] **Step 3: Replace the testimonial section with the FAQ section**

Replace:

```html
    <section class="testimonial">
        <div class="testimonial-container">
            <p class="testimonial-quote">"I was hesitant at first, but having the Nugarone vending machine in our venue has been a game-changer. It takes up barely any space, requires no effort from our team, and generates extra income week after week. The entire process was smooth, and the guests love it."</p>
            <div class="testimonial-author">Sarah Thompson</div>
            <div class="testimonial-title">Venue Manager, The Avenue Bar</div>
        </div>
    </section>
```

with:

```html
    <section class="faq" id="faq">
        <div class="faq-container">
            <h2>Common Questions</h2>

            <div class="faq-item">
                <h4>Will it disrupt my staff or take up their time?</h4>
                <p>No. We handle delivery, install, stocking, and repairs ourselves. Your team doesn't need to do anything — refills and maintenance happen without any input from your staff.</p>
            </div>

            <div class="faq-item">
                <h4>What if it doesn't sell?</h4>
                <p>There's no cost or commitment either way — you only earn when it sells, and you're never charged for machine time that doesn't convert. If a venue isn't the right fit, we'll say so upfront.</p>
            </div>

            <div class="faq-item">
                <h4>Who owns the stock and machine?</h4>
                <p>Nugarone owns and stocks the machine. You're simply hosting it and earning a share of the revenue it generates — no purchase, no inventory risk on your side.</p>
            </div>

            <div class="faq-item">
                <h4>Can we cancel?</h4>
                <p>Yes. There's no long-term contract — if it's not working for your venue, we'll remove the machine at no cost to you.</p>
            </div>
        </div>
    </section>
```

- [ ] **Step 4: Verify in browser**

Reload in the Browser pane, click the nav "FAQ" link, confirm it scrolls to the new blue FAQ section with 4 questions and no leftover testimonial text (`get_page_text` should contain "Common Questions" and none of "Sarah Thompson"/"The Avenue Bar").

---

### Task 7: Profit Share section — swap CTA to Calendly, add coverage line

**Files:**
- Modify: `index.html:472-477` (`.final-cta:hover` block, to insert `.coverage-note` after it)
- Modify: `index.html:748-775` (`<section class="cta-section" id="Profit">` HTML)

- [ ] **Step 1: Add `.coverage-note` CSS**

Replace:

```css
        .final-cta:hover {
            background: #333;
            transform: translateY(-2px);
            box-shadow: 0 10px 40px rgba(0, 0, 0, 0.2);
        }
```

with:

```css
        .final-cta:hover {
            background: #333;
            transform: translateY(-2px);
            box-shadow: 0 10px 40px rgba(0, 0, 0, 0.2);
        }

        .coverage-note {
            margin-top: 20px;
            font-size: 14px;
            color: #999;
        }
```

- [ ] **Step 2: Update the section subtitle and CTA**

Replace:

```html
    <section class="cta-section" id="Profit">
        <div class="cta-container">
            <h2>Our Profit Share Model</h2>
            <p>Schedule a quick call to learn how you can earn passive income with zero hassle, cost, or commitment.</p>
            
            <div class="steps">
                <div class="step">
                    <div class="step-number">01</div>
                    <h4>We Handle the Sales</h4>
                    <p>Customers use the machine — we track every purchase digitally in real time.</p>
                </div>
                
                <div class="step">
                    <div class="step-number">02</div>
                    <h4>You Earn Automatically</h4>
                    <p>You receive a percentage of every sale, paid out monthly — no admin, no effort.</p>
                </div>
                
                <div class="step">
                    <div class="step-number">03</div>
                    <h4>Transparent Reporting</h4>
                    <p>You get a clear monthly report showing sales and your earnings, so you’re always in the loop.</p>
                </div>
            </div>
            
            <a href="mailto:abanjoko@nugaronevending.co.uk?subject=Interested%20in%20Hosting%20a%20Vending%20Machine" class="final-cta">Connect with us</a>
        </div>
    </section>
```

with:

```html
    <section class="cta-section" id="Profit">
        <div class="cta-container">
            <h2>Our Profit Share Model</h2>
            <p>Book a free call to see exactly how much you could earn — no cost, no commitment.</p>
            
            <div class="steps">
                <div class="step">
                    <div class="step-number">01</div>
                    <h4>We Handle the Sales</h4>
                    <p>Customers use the machine — we track every purchase digitally in real time.</p>
                </div>
                
                <div class="step">
                    <div class="step-number">02</div>
                    <h4>You Earn Automatically</h4>
                    <p>You receive a percentage of every sale, paid out monthly — no admin, no effort.</p>
                </div>
                
                <div class="step">
                    <div class="step-number">03</div>
                    <h4>Transparent Reporting</h4>
                    <p>You get a clear monthly report showing sales and your earnings, so you’re always in the loop.</p>
                </div>
            </div>
            
            <a href="https://calendly.com/abanjoko-nugaronevending" target="_blank" class="final-cta">Book a Free Call</a>
            <p class="coverage-note">Currently onboarding venues UK-wide.</p>
        </div>
    </section>
```

- [ ] **Step 3: Verify in browser**

Reload in the Browser pane, scroll to the Profit Share section, confirm the subtitle is tightened, the button now reads "Book a Free Call" and its `href` points to the Calendly URL (check via `read_page`), and the grey "Currently onboarding venues UK-wide." note appears beneath it.

---

### Task 8: Final full-page verification pass

**Files:** None (verification only — no edits)

- [ ] **Step 1: Full click-through in the Browser pane**

Open `index.html` fresh. For each nav link (Features, Specs, Profit Share, FAQ, Contact) click it and confirm it scrolls to the matching section (`#features`, `#specs`, `#Profit`, `#faq`, `#contact`).

- [ ] **Step 2: Check console and network for errors**

Run `read_console_messages` (onlyErrors: true) and `read_network_requests` — confirm zero errors and zero 404s across `images/logo.png`, `images/machine.png`, `favicon_io/*`, and `privacy-policy.html`.

- [ ] **Step 3: Confirm no leftover fabricated content**

Run `get_page_text` on the full page and confirm none of these strings remain anywhere: "Sarah Thompson", "The Avenue Bar", "Discover More", "You get why we call it", "Sharing is caring", "Less downtime, more profits right".

- [ ] **Step 4: Mobile check**

Run `resize_window` with `preset: "mobile"`, reload, and visually confirm the hero, features grid, showcase (photo + specs stacked), FAQ, and profit-share sections all render without horizontal overflow or overlapping text.

- [ ] **Step 5: Confirm every primary CTA points to Calendly**

Using `read_page`, confirm the nav CTA, hero CTA, and profit-share CTA all have `href="https://calendly.com/abanjoko-nugaronevending"`, and that the only `mailto:`/`tel:` links remaining are in the footer.
