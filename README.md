# Meadowside Clinic — Twickenham

**Live site:** <https://alexswabey.github.io/meadowside-clinic/> *(served from the `main` branch)*

Responsive website for **Meadowside Clinic**, a fictional Twickenham osteopathic clinic led by Lydia Selby, M.Ost. — seven content pages plus a branded `404.html` — built with semantic HTML5, custom CSS variables, and Bootstrap `5.3.9` using zero custom JavaScript.

---

## Table of Contents

- [Website Purpose & User Value](#website-purpose--user-value)
- [Features & User Benefits](#features--user-benefits)
- [User Stories & Acceptance Criteria](#user-stories--acceptance-criteria)
- [Design Tokens & Typography](#design-tokens--typography)
- [Deployment & Local Preview](#deployment--local-preview)
- [Screenshots](#screenshots)
- [Validation & Testing Status](#validation--testing-status)
- [Bugs & Quirks Resolved](#bugs--quirks-resolved)
- [Attribution & Licences](#attribution--licences)
- [AI Use & Reflection](#ai-use--reflection)
- [Planned Future Updates](#planned-future-updates)

---

## Website Purpose & User Value

Meadowside Clinic gives local Twickenham and St Margarets residents a calm, plain-English overview before attending a first osteopathic appointment:

- **Lowers first-visit uncertainty:** Explains what happens during a 90-minute Initial Consultation and a 45-minute Follow-Up Session before visitors arrive.
- **Keeps patient experience front and centre:** Foregrounded comfort, step-free access, and continuous one-to-one practitioner care while keeping GOsC registration and qualifications clear in the background.
- **Accessible across devices:** Readable `17px` body copy, `>= 44px` touch controls, high-contrast Mineral Teal and Rosewood palette, keyboard focus rings, and zero horizontal overflow down to `320px` viewports.

---

## Features & User Benefits

- **Global Sticky Header & Mobile Offcanvas Drawer:** Uses Bootstrap `.navbar-expand-lg` and `.offcanvas-lg.offcanvas-end` so desktop navigation stays inline and mobile viewports get an accessible slide-over menu without custom JavaScript, with the tap-to-call number inline in the desktop nav and as a full row in the mobile drawer.
- **Fee Transparency:** Session fees (£200 initial consultation, £100 follow-up) appear on the home-page session badges, the treatments comparison table, and the booking pre-visit card, so visitors know the cost before they book — added on explicit client request.
- **Appointment Switcher & Stay-Open FAQ (`treatments.html`):** Bootstrap `.nav-pills` tabs separate **Initial Consultation · 90 mins** from **Follow-Up Session · 45 mins**, paired with a boxed FAQ `.accordion` intentionally omitting `data-bs-parent` so visitors can compare multiple answers simultaneously.
- **Location Diagram & Step-Free Access Switcher (`visiting.html`):** Pairs a custom line-drawing SVG street diagram (`twickenham-map.svg`) and Google Maps link with `.nav-pills` travel tabs (*Rail & Bus*, *By Car & Parking*, *Step-Free Access*).
- **Online Booking Hub (`booking.html`):** Embeds a live Koalendar scheduling calendar (`?embed=true` zero-JS `<iframe>`) alongside pre-visit reassurance, direct enquiry/telephone options, and a Bootstrap `.collapse` quick visit checklist.
- **Native Contact Validation & Confirmation Flow (`contact.html` & `thank-you.html`):** Uses HTML5 constraint attributes (`required`, `minlength`, `type="email"`, `inputmode`, `autocomplete`) plus CSS `:user-invalid` styling so inline error hints stay quiet until field blur, routing via `method="get"` to a static `thank-you.html` confirmation page with fictional-practice disclosure.

---

## User Stories & Acceptance Criteria

The site is verified against three visitor journeys, each documented with step-by-step walkthroughs and per-page acceptance criteria in [`TESTING.md` §2](TESTING.md):

- **Nervous first-timer:** Arrives unsure what osteopathy involves and how much it costs; should leave with the session steps, the session fees, and a confident path to booking.
- **Local resident checking logistics:** Verifies parking, step-free access, and the clinic phone number (header on desktop, drawer on mobile) before committing to a visit.
- **Returning patient with a question:** Sends the validated enquiry form and immediately sees a confirmation with next steps and the fictional-practice disclosure.

---

## Design Tokens & Typography

Custom properties in `assets/css/style.css` override Bootstrap `--bs-*` root and component tokens using a two-layer architecture:

- **Palette:** Mineral Teal (`#12525E` / `#0C3C45`), Porcelain (`#FAFCFD`), Sea-Glass Mist (`#EAF3F5` / `#F3F8F9`), Warm Linen (`#F5F2ED`), Deep Pine ink (`#14282C`), and Rosewood accents (`#8A3C54` / `#6E2C40`).
- **Typography:** `Literata` (optical serif at weights `400` and `600`) for display headings and patient reflections, paired with `Source Sans 3` (`400`, `600`, `700`) at `1.0625rem` (`17px`) for body copy and UI controls.

---

## Deployment & Local Preview

### Local Preview

Serve the repository over HTTP (or open via VS Code Live Server) rather than `file://` so responsive WebP `srcset`, relative assets, and form navigation behave identically to production:

```sh
python3 -m http.server 8000
```

Then visit `http://127.0.0.1:8000/index.html`.

### GitHub Pages Deployment

1. Push the updated `main` branch (`git push origin main`).
2. In the GitHub repository settings under **Pages**, deploy from branch **`main`** and folder **`/ (root)`**.
3. Open `https://alexswabey.github.io/meadowside-clinic/` and verify navigation links, images, interactive Bootstrap tabs/accordions, and form confirmation parity with the local build.

---

## Screenshots

Desktop (`1440x900`) and mobile (`390x844`) captures for all eight pages are stored in `docs/screenshots/`:

| Page | Purpose & User Value | Desktop (`1440x900`) | Mobile (`390x844`) |
| --- | --- | --- | --- |
| Home (`index.html`) | Calm first impression, Lydia introduction, and clear pathway to treatments and booking | [Desktop](docs/screenshots/desktop/index.png) | [Mobile](docs/screenshots/mobile/index.png) |
| About (`about.html`) | Care philosophy pillars, patient reflections, and quiet background credentials | [Desktop](docs/screenshots/desktop/about.png) | [Mobile](docs/screenshots/mobile/about.png) |
| Treatments (`treatments.html`) | Session comparison table, `.nav-pills` switcher, and stay-open FAQ accordion | [Desktop](docs/screenshots/desktop/treatments.png) | [Mobile](docs/screenshots/mobile/treatments.png) |
| Visiting (`visiting.html`) | Custom Twickenham Green SVG map, travel tabs, and step-free access details | [Desktop](docs/screenshots/desktop/visiting.png) | [Mobile](docs/screenshots/mobile/visiting.png) |
| Booking (`booking.html`) | Live Koalendar scheduling embed, fallback contact options, and `.collapse` visit checklist | [Desktop](docs/screenshots/desktop/booking.png) | [Mobile](docs/screenshots/mobile/booking.png) |
| Contact (`contact.html`) | Native HTML5 validated enquiry form with direct clinic details | [Desktop](docs/screenshots/desktop/contact.png) | [Mobile](docs/screenshots/mobile/contact.png) |
| Thank You (`thank-you.html`) | Immediate enquiry confirmation with next steps and fictional-practice notice | [Desktop](docs/screenshots/desktop/thank-you.png) | [Mobile](docs/screenshots/mobile/thank-you.png) |
| 404 (`404.html`) | Branded not-found page with the same header, tone, and navigation as every other page | [Desktop](docs/screenshots/desktop/404.png) | [Mobile](docs/screenshots/mobile/404.png) |

### Validation & Lighthouse Proof

| Check | Result | Screenshot |
| --- | --- | --- |
| W3C Nu HTML Validator (`vnu 26.11.20`) | `0` errors / `0` warnings across all 8 HTML files | [W3C Nu HTML](docs/screenshots/validation/w3c-nu-html.png) |
| W3C Jigsaw CSS Validator (`css3svg`, `warning=1`) | `0` errors / `0` warnings on `assets/css/style.css` | [W3C Jigsaw CSS](docs/screenshots/validation/w3c-jigsaw-css.png) |
| Lighthouse (`13.6.0`) — Home (`index.html`, Desktop) | **100** Performance · **100** Accessibility · **100** Best Practices · **100** SEO | [Lighthouse Desktop](docs/screenshots/validation/lighthouse-index-desktop.png) |
| Lighthouse (`13.6.0`) — Home (`index.html`, Mobile) | **99** Performance · **100** Accessibility · **100** Best Practices · **100** SEO | [Lighthouse Mobile](docs/screenshots/validation/lighthouse-index-mobile.png) |
| Lighthouse (`13.6.0`) — Booking (`booking.html`, Desktop) | **100** Performance · **100** Accessibility · **100** Best Practices · **100** SEO | [Lighthouse Booking](docs/screenshots/validation/lighthouse-booking-desktop.png) |
| Lighthouse (`13.6.0`) — Booking (`booking.html`, Mobile) | **98** Performance · **100** Accessibility · **100** Best Practices · **100** SEO | [Lighthouse Booking Mobile](docs/screenshots/validation/lighthouse-booking-mobile.png) |

*Mobile Performance scores land at `98–99` from sub-second LCP/FCP variance under `4×` CPU throttling against the local preview server; GitHub Pages serves the identical assets from its global CDN with long cache lifetimes. `style.css` is deliberately unminified (readable-code requirement) and the bulk of the unmodified CDN Bootstrap CSS is unused by design.*

---

## Validation & Testing Status

Headline results: W3C Nu HTML & Jigsaw CSS `0` errors / `0` warnings, `0` `axe-core` WCAG 2.1 A/AA violations (WebKit & Chromium across desktop, tablet, and mobile breakpoints, static + interactive states), `Linkinator` `0` broken links, and the Lighthouse scores in the table above. Test environments, user-story walkthroughs, the `18`-row test matrix, and per-command automated evidence live in [`TESTING.md`](TESTING.md).

---

## Bugs & Quirks Resolved

- **Bootstrap 5.3 link colour regression (`#0d6efd`):** Defining `--bs-link-color` alone left compiled links Bootstrap-blue; overriding `--bs-link-color-rgb` (`18, 82, 94`) and `--bs-link-hover-color-rgb` (`12, 60, 69`) restored compliant Mineral Teal link contrast across all surfaces.
- **Bootstrap theme-attribute specificity:** Compiled Bootstrap component tokens are declared on theme-scoped selectors (e.g. `.navbar[data-bs-theme="light"]`), which outrank plain custom class selectors—theme overrides must repeat the `data-bs-theme` attribute in the selector to win the cascade (applied to the header's navbar colour/toggler tokens).
- **Nu HTML ARIA validation on responsive `.offcanvas-lg`:** Added `role="group"` to `#clinicNav` so `aria-labelledby="clinicNavLabel"` remains valid before Bootstrap JS promotes the drawer to `role="dialog"` on mobile toggle.
- **WebKit `:user-invalid` hint reveal:** An early `:has()` fallback was added for hint reveal, then removed once `qa:full` confirmed the plain sibling combinator works alone — the shipped rule is only `main form .form-control:user-invalid + .clinic-error-hint`, with hints revealing consistently on blur in both WebKit and Chromium.
- **Hidden Bootstrap `.tab-pane` image verification:** Updated the automated Playwright runner to skip `scrollIntoViewIfNeeded()` on `display: none` tab images during initial load and explicitly verify `#followup-pane` `.webp` decoding after clicking `#followup-tab`.
- **iCloud Drive sync overwrites (workflow):** Storing the workspace inside iCloud Drive caused macOS file-sync conflicts to overwrite uncommitted local edits earlier in the project. Resolved by committing small, frequent checkpoints and using GitHub `main` as the canonical sync source.
- **FAQ `.accordion` corner tapering:** Splitting the outer border between `.accordion` (`border-left`/`border-right` only) and `.accordion-item` (`border-top`/`border-bottom`) caused browsers to taper the `1px` border to `0px` at the rounded corners. Resolved by moving the full `1px` border onto `.accordion` and keeping only internal `border-top` dividers on `.accordion-item`.
- **`65ch` prose cap clipping `.list-group-item` dividers:** Setting `max-width: 65ch` on `main li` also constrained `.list-group-item` rows inside cards, stopping horizontal dividers short on the right. Resolved by adding `main .list-group-item { max-width: none; }`.
- **Curved corner "horns" on `<aside>` callouts:** Applying `border-left: 4px` directly alongside `border-radius: 0.9rem` curved the accent bar into dark hooks at the left corners. Resolved with an `overflow: hidden` clipped `::before` `border-left` accent bar (preserving Windows Forced Colors visibility).

---

## Attribution & Licences

### Photography (Responsive `.webp` Sets in `assets/images/`)

| Slot | Page | Files (`w` × `h`) | Creator / Source | Licence / Disclosure |
| --- | --- | --- | --- | --- |
| Hero treatment room | `index.html` | `hero-treatment-room-640.webp` (`640x480`), `-800.webp` (`800x600`), `-1200.webp` (`1200x900`) | Kimiya Sabbaghan | [Unsplash](https://unsplash.com/photos/a-white-room-with-a-bed-and-a-desk-o4OJfrmMC0o) · Unsplash License |
| Clinic waiting room opener | `about.html` | `clinic-waiting-room-800.webp` (`800x450`), `clinic-waiting-room-1440.webp` (`1440x810`) | Raphael (Ajani Kamali Akio) | [Unsplash](https://unsplash.com/photos/modern-living-room-with-three-sofas-and-coffee-table-LacQuwrta3I) · Unsplash License |
| Meet Lydia portrait | `index.html` | `lydia-portrait-640.webp` (`640x480`), `-800.webp` (`800x600`), `-1200.webp` (`1200x900`) | AI-generated editorial suite | Generated specifically for this fictional clinic so practitioner identity, clothing, and daylight room palette remain cohesive across pages; converted to responsive `.webp` |
| Initial consultation card | `index.html` | `consultation-conversation-480.webp` (`480x360`), `consultation-conversation-960.webp` (`960x720`) | AI-generated editorial suite | Consistent Lydia Selby consultation scene matching the clinic palette |
| Follow-up session card | `index.html` | `osteopathic-lumbar-care-480.webp` (`480x360`), `osteopathic-lumbar-care-960.webp` (`960x720`) | AI-generated editorial suite | Clothed hands-on osteopathic care detail matching the clinic's "loose, comfortable clothing" guidance |
| Initial consultation tab | `treatments.html` | `initial-assessment-640.webp` (`640x480`), `-800.webp` (`800x600`), `-1200.webp` (`1200x900`) | AI-generated editorial suite | Consistent Lydia Selby consultation scene in the sunlit clinic room |
| Follow-up session tab | `treatments.html` | `followup-thoracic-care-640.webp` (`640x480`), `-800.webp` (`800x600`), `-1200.webp` (`1200x900`) | AI-generated editorial suite | Clothed hands-on osteopathic care detail matching the clinic palette |
| Clinic exterior frontage | `visiting.html` | `twickenham-shopfront-640.webp` (`640x480`), `-800.webp` (`800x600`), `-1200.webp` (`1200x900`) | AI-generated editorial suite | Fictional Meadowside Clinic frontage at 14 The Green with mineral teal timberwork and flush step-free entry |

### Custom Graphics, Framework & Web Fonts

- **Custom SVGs:** `assets/images/brand-mark.svg` and `assets/images/twickenham-map.svg` were authored specifically for Meadowside Clinic.
- **Bootstrap `5.3.9`:** Front-end grid, components, and interactive bundle loaded via jsDelivr CDN ([MIT License](https://github.com/twbs/bootstrap/blob/main/LICENSE)).
- **Google Fonts:** `Literata` and `Source Sans 3` loaded via Google Fonts API v2 ([SIL Open Font License 1.1](https://scripts.sil.org/OFL)).

---

## AI Use & Reflection

- **Code creation:** AI assisted with scaffolding the Bootstrap `5.3.9` layout across eight HTML files, dual-layer `--bs-*` token architecture, and declarative zero-JS controls (offcanvas menu, `.nav-pills` tabs, stay-open accordion, native `:user-invalid` form validation), enabling cleaner structural separation than earlier custom CSS iterations.
- **Debugging & validation:** AI-assisted contrast audits and cross-engine Playwright + `axe-core` scripts identified `#0d6efd` token leakage, dark navbar specificity collisions, Nu HTML ARIA requirements on `.offcanvas-lg`, and WebKit `:user-invalid` repaint gaps prior to deployment.
- **Performance & UX optimisation:** Guided responsive `.webp` multi-width `srcset`/`sizes` generation, LCP `fetchpriority="high"` vs lazy/low-priority hints on non-critical or hidden-tab images, trimming unused Google Fonts italic axes, editorial `Literata` + `Source Sans 3` typography selection, and generating a cohesive AI editorial photography suite so practitioner identity, clothed care, and the Twickenham frontage stay visually consistent across every page.
- **Workflow impact:** Separating project state docs and automated QA scripts (`twickenham-osteopath-project-state`) from static site output kept commits auditable and made visual, validator, and accessibility regressions rapid to catch and resolve.

---

## Planned Future Updates

- Connect `contact.html` (`method="get"`) to a live form handler endpoint for production deployment beyond static GitHub Pages.
