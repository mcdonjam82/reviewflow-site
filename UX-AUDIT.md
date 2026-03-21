# Gleam Site UX Audit
**Audited:** March 21, 2026  
**Auditor:** Luke (CSO, LucraLab)  
**Target buyer:** Local business owner, 35–55, skeptical of tech, gut decision-maker, checks phone constantly  
**Site:** gleamreply.com  

---

## INDEX — gleamreply.com/

**Overall UX Score: 7/10**  
**Critical Issues (fix before showing to prospects):** 3  
**Nice-to-have improvements:** 5  

### Critical Issues

1. **Completely different design system from every other page** — index.html uses `Plus Jakarta Sans + Inter` fonts, `#131124` background, lighter component colors, and different CSS variable names. Every other page uses `Roboto`, `#0d0b1e` background, and the `--cyan/#07b9fd` token system. When a prospect clicks from index.html to dental.html or examples.html, it feels like a different company. This is a trust-killer for skeptical buyers. **Fix:** Unify the design system. Either migrate index.html to match the Roboto/dark palette of the other pages, or (if this is a deliberate rebrand) migrate ALL other pages to match index.html. Whichever direction — pick one and be consistent.

2. **Footer links use `/privacy` and `/terms` without `.html` extension** — `<a href="/privacy">` and `<a href="/terms">`. On GitHub Pages and most static hosts, these will 404. Every other page correctly uses `/privacy.html` and `/terms.html`. **Fix:** Change to `href="/privacy.html"` and `href="/terms.html"` in the index footer.

3. **Nav logo links to `href="#"`** — The nav-logo "GLEAM" has `href="#"` which scrolls to top instead of linking to the homepage. If someone navigates here from another page, clicking the logo doesn't work as expected. **Fix:** Change `href="#"` to `href="/"` or `href="/index.html"`.

### Nice-to-Have

1. **Primary CTA points to external `app.gleamreply.com/signup`** — Unlike all other pages which use an on-page form (reducing friction), index.html sends users off-site to a separate signup flow. For skeptical buyers, leaving the landing page to sign up feels like a big commitment. Consider embedding the email-first form here too.

2. **Inconsistent social proof number** — index.html says "500+ businesses"; dental.html footer says "200+ dental practices." Both can't be right without context. If 500+ is real, use it everywhere. If it's aspirational, don't use it at all. **Fix:** Align all pages on one verifiable number.

3. **"500+" appears in hero stat without source** — The "500+" businesses stat has no citation. The hero cite links (Harvard, ReviewTrackers) are good — apply the same standard to social proof claims.

4. **`cal.gleamreply.com` secondary CTA has no visual treatment** — The "Questions? Book a 15-min call →" link has no styling indicator that it's a link. Visually invisible to mobile users scrolling past it.

5. **No testimonials visible above fold** — Testimonials exist but are buried. For gut-decision buyers, social proof needs to be higher.

### Mobile Score: 7/10
Responsive grid works, but the tab interface in the nav on mobile needs checking. Buttons are sized appropriately. The animated blob in the hero is heavy on mobile CPUs.

### Desktop Score: 7/10
Good visual hierarchy, clear CTA in hero, stat bar builds credibility. Loses points for the off-site CTA and the design inconsistency with the rest of the site.

---

## DENTAL — gleamreply.com/dental

**Overall UX Score: 8/10**  
**Critical Issues (fix before showing to prospects):** 2  
**Nice-to-have improvements:** 4  

### Critical Issues

1. **Nav has no navigation links — only logo and CTA** — Dental prospects can't explore the site from this page. If they want to see examples or pricing before committing, they're stuck. Other pages (examples.html) don't even have a CTA, so there's no easy path between them. **Fix:** Add 2–3 nav links: "How It Works", "See Examples", and keep the CTA.

2. **Conflicting social proof: "Trusted by 200+ dental practices"** — This appears in the footer but the main site says "500+ businesses." Pick one source of truth. If Gleam genuinely has 200+ dental practices, that's a great specific stat — use it proudly throughout the dental page instead of hiding it in the footer.

### Nice-to-Have

1. **Backfill date examples are stale** — The backfill cards say "Jan 2025," "Mar 2025," etc. It's now 2026. These look like old screenshots. **Fix:** Update to 2025-2026 dates or make them generic ("3 months ago," "6 months ago").

2. **`btn-secondary` "Show me the sample report" competes with primary CTA** — Two equally-weighted buttons in the hero split attention. Secondary button should have less visual weight. **Fix:** Style it as a text link or smaller outlined button.

3. **No testimonials** — Index has testimonials from real (or named) customers. Dental page has none. Dentists are skeptical of AI — peer validation from another dentist would do heavy lifting here. **Fix:** Add 1–2 dental-specific testimonials near the pricing section.

4. **`href="#"` on nav logo** — Should link to homepage (`/`), not `#`.

### Mobile Score: 8/10
Grid collapses properly at 768px. Buttons stack. The new-features-grid correctly goes to 1 column with the dedicated media query. Steps collapse to 1 column. Font sizes use `clamp()` — solid. Tap targets are adequate.

### Desktop Score: 8/10
Strong hero with clear value prop. HIPAA angle addresses the biggest dental objection. Problem/solution flow is well structured. Stat bar provides instant credibility. Demo phone mockup is a nice touch.

---

## EXAMPLES — gleamreply.com/examples.html

**Overall UX Score: 6/10**  
**Critical Issues (fix before showing to prospects):** 2  
**Nice-to-have improvements:** 3  

### Critical Issues

1. **No CTA anywhere on the page** — This is the primary trust-building asset (60 real AI responses across 6 industries) but there is absolutely no call to action. Not in the nav, not in the header, not at the bottom. After scrolling through dozens of examples and getting convinced, users have nowhere to go. **Fix:** Add a sticky or bottom-of-page CTA: "Seen enough? Start your free trial →" with link to the signup form.

2. **Unfilled `[Contact Information]` placeholder in live HVAC example** — In the Pacific Air Systems 2-star reviews section (Donna W.'s review), the Gleam suggested response includes "Please reach out directly at [Contact Information]" — this is an obvious unfilled template placeholder. If a prospect sees this it immediately undermines the "professional AI responses" pitch. **Fix:** Replace `[Contact Information]` with "our office" or "us directly" — something generic and complete.

### Nice-to-Have

1. **Empty media query `@media(max-width:768px){}` in CSS** — Dead CSS that suggests this breakpoint was planned but not implemented. Tab overflow on small screens may be problematic. **Fix:** Either add proper 768px styles (wrap tabs, reduce font sizes) or remove the empty rule.

2. **Tab row scrolls horizontally on mobile without indicator** — 6 tabs on mobile require horizontal scrolling but there's no scroll indicator or arrow hint. **Fix:** Add `overflow-x:auto; -webkit-overflow-scrolling:touch` with a right-fade gradient to hint at scrollability.

3. **Nav has no CTA button** — Just the logo and a "Review Sandbox" badge. Users who arrive directly at this URL (from SEO, social, etc.) have no obvious path to the product. **Fix:** Add the same `nav-cta` button ("Start Free Trial") that appears on dental.html.

### Mobile Score: 5/10
Reviews grid collapses at 900px — good. But the tabs overflow without clear indication, and the `.gcard` content is dense at 320px widths. The SMS bubble monospace font (`SF Mono`) can render oddly small on Android.

### Desktop Score: 7/10
Very strong content. The four-step flow (review → SMS alert → edit/approve → posted) is visually clear and effectively demonstrates the product. Just needs a conversion path.

---

## NEGATIVE-REVIEW-DEMO — gleamreply.com/negative-review-demo.html

**Overall UX Score: 7/10**  
**Critical Issues (fix before showing to prospects):** 1  
**Nice-to-have improvements:** 3  

### Critical Issues

1. **Logo loads from absolute URL `https://gleamreply.com/logo.svg`** — If the site is accessed on staging, localhost, or a different domain (e.g., Netlify preview), the logo will either load from production or fail entirely. **Fix:** Change to a relative path `/logo.svg` like every other page.

### Nice-to-Have

1. **Font stack is different (`-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto`)** — Not a crisis since Roboto is in the fallback, but the primary font will render differently on Windows (Segoe UI) vs other pages. **Fix:** Match `font-family:'Roboto',sans-serif` with the Google Fonts preload like dental.html uses.

2. **Bottom CTA button has no visible destination indication** — `<a href="/" class="btn">` just says "Start your free trial" and links to `/`. This is correct but the button styling (`linear-gradient(135deg,#1f3b90,#7649ec)`) differs from the standard cyan CTA style. Not broken, but slightly off-brand. **Fix:** Standardize button gradient to match primary CTA style site-wide.

3. **`noindex,nofollow` means no organic discovery** — This is intentional, but worth revisiting. This page could rank for "how to respond to negative reviews" type queries. If it's useful for prospects, consider making it indexable with good title/description.

### Mobile Score: 7/10
The "how it works" strip collapses to column on mobile via the 640px media query — good. Review pairs and SMS bubbles reflow reasonably.

### Desktop Score: 8/10
Well-structured demo page. The 4-step "how" strip at the top is an excellent visual summary. Review pairs are realistic. Appropriate scope for a supporting/sales asset page.

---

## AUTO-REPLY — gleamreply.com/auto-reply.html

**Overall UX Score: 4/10**  
**Critical Issues (fix before showing to prospects):** 3  
**Nice-to-have improvements:** 2  

### Critical Issues

1. **Page is branded as "LucraLab" NOT "Gleam"** — The nav logo says "LucraLab," the footer says "LucraLab," and the title says "Auto-Reply — Never Lose a Missed Call Again | LucraLab." This is a completely different product (missed call auto-reply) that happens to live in the gleam-site directory. If accessed from gleamreply.com, a visitor sees "LucraLab" with no mention of Gleam in the nav — severely confusing. **Fix:** Either (a) move this page to a LucraLab domain, or (b) clearly brand it as a separate LucraLab product with a "← Back to Gleam" link, or (c) rebrand it under Gleam if it's part of the Gleam product suite.

2. **Nav logo `href="#"` — dead link** — Clicking the LucraLab logo scrolls to top instead of going anywhere useful. **Fix:** Link to the relevant homepage.

3. **CTA points to `https://app.gleamreply.com/signup`** — The auto-reply page CTA directs people to sign up for Gleam (review management). If these are separate products, this is wrong. If auto-reply is a Gleam feature, the page needs to say so. **Fix:** Clarify product relationship and route CTA appropriately.

### Nice-to-Have

1. **Stat bar shows "3-4 missed calls/day" without citation** — The number is specific but unattributed. Other stats on the site have citations. Add a source or soften the claim.

2. **No form on page** — All other primary pages have inline forms. This page only has a button CTA to app.gleamreply.com. For cold traffic, an inline email capture would convert better.

### Mobile Score: 6/10
Uses the same responsive patterns as dental.html. Grid collapses, buttons stack. Phone mockup shrinks. Nav padding reduces. Generally functional.

### Desktop Score: 5/10
The product itself (missed call auto-reply) is compelling copy. But the brand confusion makes it a liability. Decent visual design that matches the Gleam dark aesthetic, but the identity mismatch undermines everything.

---

## SUCCESS — gleamreply.com/success.html

**Overall UX Score: 8/10**  
**Critical Issues (fix before showing to prospects):** 1  
**Nice-to-have improvements:** 2  

### Critical Issues

1. **Support email is `support@lucralab.com` — conflicts with `hello@gleamreply.com` in index.html footer** — A new customer just signed up and is on the success page. The support email they see here (`support@lucralab.com`) is different from the contact email on the main site (`hello@gleamreply.com`). Creates confusion about who to contact. **Fix:** Standardize to one support email across all pages. Pick `hello@gleamreply.com` (more on-brand) or `support@gleamreply.com`.

### Nice-to-Have

1. **"Back to Gleam" button is redundant** — The user just signed up. They don't need to go back to the marketing site — they need to go to their onboarding email. This button could instead say "Check your email →" or just be removed. **Fix:** Replace with a link to a helpful "What to expect" resource or remove entirely.

2. **No tracking confirmation** — Good post-signup pages confirm the specific email address the user signed up with ("We sent your setup email to you@yourpractice.com"). This reduces anxiety. **Fix:** If Stripe/the API can pass the email to this page (via query param), display it here.

### Mobile Score: 9/10
Full-height centered card layout works perfectly on mobile. Minimal content. Clean and focused.

### Desktop Score: 8/10
Clean, confident, reassuring tone. The 3-step next-steps section is well written. Appropriate for a post-payment confirmation.

---

## SAMPLE-REPORT — gleamreply.com/sample-report.html

**Overall UX Score: 7/10**  
**Critical Issues (fix before showing to prospects):** 1  
**Nice-to-have improvements:** 3  

### Critical Issues

1. **Report is for "Cascade Home Services" (HVAC) — used on a general page** — The sample-report.html shows a home services company report. There is also `sample-report-dental.html` which dental.html correctly links to. If the general `sample-report.html` is accessible from index.html or other non-dental pages, it should show a more generic or multi-industry business. Currently it could confuse dental prospects who click a generic "see sample report" link and get an HVAC report. **Fix:** Link consistently — dental pages → sample-report-dental.html; general pages → sample-report.html. Verify the generic page header says "Home Services" clearly so visitors know this is a representative example.

### Nice-to-Have

1. **No CTA at bottom of report** — The sample report is excellent proof of value (clean, data-rich, professional). But after viewing it, there's only a nav link back to gleamreply.com and no "Start my free trial" button at the bottom. This is a high-intent moment — add a CTA. **Fix:** Add a footer CTA section: "Like what you see? Your practice gets this report every month → [Start Free Trial]"

2. **"← Back to Gleam" nav link is the only navigation** — Adequate but minimal. The nav bar is almost empty. At minimum, add the "Start Free Trial" button here.

3. **Email-table layout may look different in browser vs email client** — This page uses `<table>` email layout which renders well in browsers, but any tweaks to make it look better in browser may break email rendering. This is acceptable since it's being used as a static demo page, not an actual email. Just worth noting.

### Mobile Score: 7/10
Table-based email layout is generally mobile-friendly due to the max-width:600px container, but wide stat tables inside may clip on very narrow screens (320px). The three-column stat card table may squish uncomfortably.

### Desktop Score: 8/10
Excellent proof-of-value asset. The "Sample Report" banner at the top is clear and honest. Data presentation is clean and professional. This is one of the strongest sales assets on the site.

---

## TERMS — gleamreply.com/terms.html

**Overall UX Score: 8/10**  
**Critical Issues (fix before showing to prospects):** 0  
**Nice-to-have improvements:** 2  

### Nice-to-Have
1. **Fonts loaded synchronously** — Unlike other pages which use `preload` pattern for fonts, terms.html uses the blocking `<link href="...fonts.googleapis.com...">`. Minor performance issue. Not a conversion concern.
2. **No "Back to home" link in footer** — Legal pages should link back to the product. Add a simple footer link.

### Mobile Score: 8/10  
### Desktop Score: 8/10

---

## PRIVACY — gleamreply.com/privacy.html

**Overall UX Score: 8/10**  
**Critical Issues (fix before showing to prospects):** 0  
**Nice-to-have improvements:** 2  

### Nice-to-Have
1. **Same font loading issue as terms.html** — Blocking font load.
2. **SMS consent language references check** — The signup form on dental.html has detailed TCPA/SMS consent language. Verify privacy.html covers the SMS marketing program with equivalent specificity. The Twilio Compliance Report exists (`TWILIO-COMPLIANCE-REPORT.md`) — ensure this page stays synchronized with it.

### Mobile Score: 8/10  
### Desktop Score: 8/10

---

## CONSISTENCY AUDIT ACROSS ALL PAGES

| Element | index.html | dental.html | examples.html | negative-review-demo.html | auto-reply.html |
|---------|-----------|-------------|---------------|--------------------------|-----------------|
| Font | Plus Jakarta Sans + Inter | Roboto | System stack | System stack | Roboto |
| Background | `#131124` | `#0d0b1e` | `#0d0b1e` | `#0d0b1e` | `#0d0b1e` |
| Nav: sticky vs fixed | Fixed | Fixed | Sticky | None (just topbar) | Fixed |
| Nav CTA | "Start Free Trial" | "Protect My Reviews" | None | None | "Stop Losing Calls" |
| Logo links to | `#` (dead) | `/` | N/A | N/A | `#` (dead) |
| Footer links format | `/privacy` `/terms` | `/privacy.html` `/terms.html` | N/A | N/A | N/A |
| Support email | `hello@gleamreply.com` | N/A | N/A | N/A | N/A |
| Brand name in nav | GLEAM | Gleam (logo svg) | Gleam | Gleam (logo svg via absolute URL) | LucraLab |

**Verdict:** Significant inconsistencies exist. The site was built in layers at different times, and it shows. The index.html appears to be a newer redesign that was never propagated to the other pages.

---

## PRIORITY FIX LIST — Top 10 by Conversion Impact

### #1 — Unify design system across all pages ⚡ HIGHEST IMPACT
**Impact:** Every page-to-page navigation currently feels like a different product. Skeptical buyers need consistency to build trust.  
**Fix:** Migrate all pages to use a single CSS design token file. The dental.html system (Roboto, `#0d0b1e`, `--cyan/#07b9fd` tokens) is more polished and consistent — use it as the standard. Index.html needs the most work.  
**Effort:** High (3–5 hours)

### #2 — Add CTA to examples.html
**Impact:** Examples.html is the highest-intent asset on the site. Prospects who visit it are evaluating Gleam seriously. Right now there's no path to conversion.  
**Fix:** Add a sticky footer CTA banner: "Seen enough? Start your 14-day free trial →" (same inline form or link to dental.html/#get-started). Also add the `nav-cta` button to the nav.  
**Effort:** Low (30 min)

### #3 — Fix `[Contact Information]` placeholder in examples.html
**Impact:** This visible template placeholder directly undermines the core product promise ("professional AI responses"). If a prospect sees it, conversion is dead.  
**Fix:** Find-replace `[Contact Information]` with "our office directly" throughout examples.html.  
**Effort:** 5 minutes

### #4 — Fix footer links in index.html (`/privacy` → `/privacy.html`)
**Impact:** Legal link 404s are a trust signal. If the privacy and terms links are broken, prospects notice. Also kills TCPA compliance paper trail.  
**Fix:** In index.html footer, change `href="/privacy"` to `href="/privacy.html"` and `href="/terms"` to `href="/terms.html"`.  
**Effort:** 5 minutes

### #5 — Clarify auto-reply.html brand identity
**Impact:** A LucraLab-branded page living on gleamreply.com causes identity confusion. If this is currently linked anywhere from Gleam pages, it actively hurts Gleam's brand.  
**Fix option A:** Add a clear header: "A separate product by LucraLab — makers of Gleam" with a back link.  
**Fix option B:** Rebrand the page as a Gleam add-on with the Gleam visual system.  
**Effort:** 1–2 hours

### #6 — Standardize support email sitewide
**Impact:** Post-purchase trust. A new customer sees `support@lucralab.com` on success.html but `hello@gleamreply.com` on the main site. Inconsistency generates "did I sign up for the right thing?" anxiety.  
**Fix:** Decide on one address (recommend `support@gleamreply.com`). Update success.html, index footer, any email templates.  
**Effort:** 30 min

### #7 — Fix all `href="#"` logo links (index.html nav, auto-reply.html nav)
**Impact:** Broken nav logos are a basic UX failure. Skeptical buyers who try to go "back to the homepage" from a sub-page by clicking the logo will be confused when it does nothing.  
**Fix:** Change `href="#"` to `href="/"` on all logo links.  
**Effort:** 10 minutes

### #8 — Unify social proof numbers
**Impact:** "500+ businesses" (index) vs "200+ dental practices" (dental footer) creates distrust. Prospects who see both numbers in the same session will notice the discrepancy.  
**Fix:** Audit real customer count. Use the most honest/accurate number site-wide. If segmented (500 total, 200 dental), write it that way: "500+ local businesses, including 200+ dental practices."  
**Effort:** 30 min (copy change across 2 pages)

### #9 — Add CTA to sample-report.html bottom
**Impact:** Prospects who view the sample report are high-intent. They've done the mental work of imagining themselves receiving this report monthly. There's no "yes" button at the bottom.  
**Fix:** Add a bottom section after the report: blue card with headline ("This is what lands in your inbox every month") + "Start My Free 14-Day Trial" button.  
**Effort:** 1 hour

### #10 — Add dental testimonials to dental.html
**Impact:** Dentists specifically distrust AI. The highest objection-handler in the dental vertical is "another dentist trusts this." Zero testimonials on the dental page is a gap.  
**Fix:** Add 2–3 named testimonials from dental practice owners near the pricing section. If real testimonials aren't available yet, mark them as beta tester quotes. Format: headshot placeholder + name + practice name + city.  
**Effort:** 1 hour (content + markup)

---

## SUMMARY TABLE

| Page | Score | Critical | Nice-to-Have |
|------|-------|----------|--------------|
| index.html | 7/10 | 3 | 5 |
| dental.html | 8/10 | 2 | 4 |
| examples.html | 6/10 | 2 | 3 |
| negative-review-demo.html | 7/10 | 1 | 3 |
| auto-reply.html | 4/10 | 3 | 2 |
| success.html | 8/10 | 1 | 2 |
| sample-report.html | 7/10 | 1 | 3 |
| terms.html | 8/10 | 0 | 2 |
| privacy.html | 8/10 | 0 | 2 |

**Total critical issues across site: 13**  
**Most urgent: #3 (placeholder text) and #4 (broken links) — can be fixed in under 10 minutes**  
**Highest conversion impact: #1 (design unification) and #2 (examples.html CTA)**

---

*Audit produced by Luke (AI CSO, LucraLab) — March 21, 2026*
