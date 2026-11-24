# Testing — Meadowside Clinic

How the site was verified before submission. This document covers **how** we tested: environments, user-story walkthroughs, and the test matrix. What the site does and the headline validation summary live in [`README.md`](README.md); the automated scripts live in the sibling project-state repository (`twickenham-osteopath-project-state`) and run via `npm run qa:fast | qa:full | qa:links | qa:lighthouse | qa:w3c`.

---

## 1. Test Environments

| Layer | Setup |
| --- | --- |
| Automated browsers | Playwright **WebKit** (headless) + **Chromium**, both engines run for every check |
| Viewports | Core Bootstrap breakpoints: `1440x900` (desktop), `768x1024` (tablet `md`), `390x844` (phone), `320x568` (minimum mobile width) |
| Accessibility | `axe-core` WCAG 2.1 A/AA (both engines, static + interactive states) |
| Validation | W3C Nu HTML (`vnu 26.11.20`), W3C Jigsaw CSS (`profile=css3svg`, `warning=1`), `html-validate`, `Stylelint` |
| Link integrity | `linkinator` across all 8 pages (same-origin links, `#fragment` targets, CSS `url()`, no redirects) |
| Performance | `Lighthouse 13.6.0` (mobile + desktop presets) against a local HTTP preview of the exact `main` tree |
| Cross-device spot checks | Safari 18 (macOS 15), Chrome (macOS 15), iPhone-class 390x844, Windows High Contrast via `forced-colors: active` emulation |

---

## 2. User Story Walkthroughs

Each story was walked end-to-end in WebKit and Chromium at `1440x900` and `390x844`. Acceptance criteria are listed per page.

### US-1 — A nervous first-timer learns what to expect, then books

**Scenario:** A Twickenham resident has never seen an osteopath. They are anxious about what happens, what it costs, and whether they need a GP referral.

1. Land on **Home** — calm room photo, short introduction to Lydia, and the two appointment pathways side by side with duration **and fee** (`£200` / `£100`).
2. Open **Treatments** — compare the sessions in the table (time, fee, focus, clothing, referral), then switch between the two tab panes and read the FAQ with more than one answer open at once.
3. Read the *What happens in a session* three-step roadmap (conversation → explained treatment → aftercare).
4. Open **Booking** — choose a slot in the calendar, or fall back to *Send Booking Enquiry* / *Call*.

**Acceptance criteria**

- Home: both fees visible without scrolling to Treatments; both cards keyboard-reachable.
- Treatments: table row *Fee* reads `£200` / `£100`; FAQ accordion keeps earlier answers open; no content hidden behind a referral requirement.
- Booking: calendar interactive, or the two fallback actions reachable; phone number tap-to-call.

### US-2 — A local resident checks how to get there and finds the phone number fast

**Scenario:** A St Margarets resident is driving a relative in. They need parking info and want to call ahead—without hunting through the site.

1. Open **Visiting** — read the address, open the Google Maps link, and check the Twickenham Green line-drawing map.
2. Switch to the *Car & Parking* tab, then *Step-Free Access*.
3. Locate the phone number: inline in the header on desktop, full row inside the drawer on mobile—tap/click to call.

**Acceptance criteria**

- Visiting: all three travel tabs switch; SVG map renders with legible labels; Google Maps link opens in a new context.
- Header: number visible without opening the menu at `≥ 992px`; drawer row fits at `320x568` without clipping; `tel:+442085550142` well-formed on all 8 pages.

### US-3 — A returning patient sends an enquiry and gets a confirmation

**Scenario:** A patient is between follow-ups and wants to ask a question or rearrange.

1. Open **Contact** — fill Name, Email, Message (Phone optional; pick a preferred reply method).
2. Submit with a too-short message — the inline hint appears **only after** the field is interacted with, never on page load.
3. Submit a valid form — the **Thank You** page confirms receipt, lists next steps, and shows the fictional-practice educational disclosure.

**Acceptance criteria**

- Contact: no error hints visible before interaction; hints appear on blur (`:user-invalid`) in both engines; `maxlength` caps the message at 300 characters.
- Thank You: reachable via `method="get"` on static GitHub Pages; return CTAs and disclosure present.

---

## 3. Test Matrix

Desktop = `1440x900`, Mobile = `390x844` (tablet `768x1024` and minimum-width `320x568` also covered by the automated suite).

| # | Feature | Steps | Desktop | Mobile | Expected | Result |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | Primary navigation | Click each nav link; check active state | ✅ | ✅ | All links resolve; active page shows hairline (desktop) / underline (drawer) | PASS (automated link + active-state checks) |
| 2 | Mobile drawer | Tap toggler; focus moves into drawer; Escape closes | — | ✅ | Drawer fits viewport, traps focus, closes on Escape/backdrop | PASS (offcanvas fit check, both engines) |
| 3 | Skip link | First `Tab` press | ✅ | ✅ | Link becomes visible at top-left; Enter jumps to `#main-content` | PASS (focus check) |
| 4 | Session switcher (Treatments) | Click *Follow-Up Session* tab | ✅ | ✅ | Pane swaps; hidden-pane image decodes on activation | PASS (pill + image-decode check) |
| 5 | Stay-open FAQ (Treatments) | Open two items simultaneously | ✅ | ✅ | Both stay open (no `data-bs-parent`) | PASS (FAQ check) |
| 6 | Travel tabs + map (Visiting) | Switch *Rail* / *Car* / *Step-Free*; inspect SVG | ✅ | ✅ | Tabs switch; map renders, labels legible | PASS (pill + zero-sized-SVG check) |
| 7 | Visit checklist (Booking) | Toggle *Quick visit checklist* | ✅ | ✅ | `.collapse` expands/closes, `aria-expanded` tracks state | PASS (collapse check) |
| 8 | Form validation (Contact) | Leave fields empty / type 5 chars in message; blur | ✅ | ✅ | No hints on load; hints appear only via `:user-invalid` after interaction | PASS (`:user-invalid` check, both engines) |
| 9 | Enquiry flow (Contact → Thank You) | Submit valid form | ✅ | ✅ | `thank-you.html` shown with next steps + disclosure | PASS (GET action; live-site check) |
| 10 | Tap-to-call | Click/tap header + body `tel:` links | ✅ | ✅ | Dialer invoked on mobile; number never wraps mid-digit (`&nbsp;` joins) | PASS (link check + html-validate `tel-non-breaking`) |
| 11 | Branded 404 | Visit unknown URL on the live site | ✅ | ✅ | GitHub Pages serves `404.html` (home / book / contact CTAs + phone) | PASS (live-site check) |
| 12 | Focus rings | `Tab` through nav, buttons, form fields | ✅ | ✅ | 3px Rosewood outline, `≥ 3:1` against Porcelain/Mist/white | PASS (focus-visible check) |
| 13 | Windows High Contrast | Emulate `forced-colors: active` | ✅ | ✅ | Card/button/nav borders and focus outlines render in system colours | PASS (emulated media check) |
| 14 | Reduced motion | Emulate `prefers-reduced-motion: reduce` | ✅ | ✅ | No transforms/transitions; smooth scroll becomes `auto` | PASS (emulated media check) |
| 15 | Horizontal overflow | Measure at all 4 breakpoints (`1440`, `768`, `390`, `320`) | ✅ | ✅ | `scrollWidth == clientWidth` on every page | PASS (overflow check, both engines) |
| 16 | Anchor clearance | Load `treatments.html#faq`, `visiting.html#accessibility` | ✅ | ✅ | Target section clears the sticky header (~23px gap, no occlusion) | PASS (clearance check) |
| 17 | axe-core WCAG 2.1 A/AA | Audit static + interactive states, both engines | ✅ | ✅ | 0 violations | PASS (`qa:full`) |
| 18 | Imagery | Inspect every `<img>` / SVG | ✅ | ✅ | No broken images, all `alt` present, no zero-sized SVGs, no `#0d6efd` default-blue leaks | PASS (asset checks, both engines) |

---

## 4. Automated Evidence (2026-11-24)

| Command (project-state repo) | Scope | Result |
| --- | --- | --- |
| `npm run qa:css` (Stylelint) | `assets/css/style.css` token/specificity/no-`!important` hygiene | `0` errors |
| `npm run qa:html` (html-validate) | All 8 HTML files, offline | `0` errors |
| `npm run qa:links` (linkinator) | All 8 pages as crawl starts: same-origin links, `#fragment` targets, CSS `url()`, `redirects: "error"` | `32` OK, `0` broken |
| `npm run qa:fast` | Stylelint + html-validate + Chromium/`axe-core` quick pass | PASS |
| `npm run qa:full` | Stylelint + html-validate + `linkinator` + WebKit & Chromium Playwright/`axe-core` (4 breakpoints + interactive states) | PASS, `0` violations |
| `npm run qa:w3c` | W3C Nu HTML + Jigsaw CSS (live validators) | `0` errors / `0` warnings across all 8 HTML files + CSS |
| `npm run qa:lighthouse` | Lighthouse `13.6.0`, milestone preset: `index.html` + `booking.html` × mobile + desktop | Mobile `99` / `98` Perf, `100` A11y/BP/SEO · Desktop `100/100/100/100` (see §5) |

Screenshots of every page (desktop `1440x900`, mobile `390x844`) and the validator/Lighthouse reports are stored in [`docs/screenshots/`](docs/screenshots/).

---

## 5. Known Limitations & Deliberate Trade-offs

- **Lighthouse runs against a local static-server preview** (no cache headers, single machine) — `lighthouse_qa.mjs` serves the exact `main` tree and reuses Playwright's Chromium binary. GitHub Pages serves the same assets from a global CDN with long `max-age` values, so production Core Web Vitals should be at least as good. Mobile Performance scores `98–99` due to sub-second LCP/FCP timing variance under Lighthouse's 4× CPU throttling; desktop scores `100`.
- **`style.css` is intentionally not minified** (Lighthouse's `unminified-css` insight). Readable, commented code is a course requirement; the file is ~16 kB.
- **~90% of CDN Bootstrap CSS is unused** (Lighthouse's `unused-css-rules` insight). Inherent to the locked decision to ship unmodified Bootstrap 5.3.9 via CDN rather than a custom build.
- **Home session cards use a compact thumbnail + text layout below `768px`.** Stacking two full-width 4:3 photos back-to-back on a phone buries the fees and CTAs, so on mobile each card shows a column-width photo beside the text instead.
- **The booking calendar is a third-party embed** (`<iframe>`); its internals are outside axe/overflow/validator reach. The page's own markup, fallback actions, and checklist are fully covered.
- **The contact form uses `method="get"`** so it works on static GitHub Pages without a 405; field values therefore appear in the `thank-you.html` URL. This is covered by the educational disclosure on that page; a live handler is a planned production upgrade (see README).
