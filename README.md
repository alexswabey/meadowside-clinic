# Meadowside Clinic — Twickenham

**Live site (`main`):** <https://alexswabey.github.io/meadowside-clinic/> *(Bootstrap `5.3.9` rebuild promoted to local `main`)*

Responsive seven-page website for **Meadowside Clinic**, a fictional Twickenham osteopathic clinic led by Lydia Selby, M.Ost., built with semantic HTML5, custom CSS variables, and Bootstrap `5.3.9` using zero custom JavaScript.

---

## Table of Contents

- [Website Purpose & User Value](#website-purpose--user-value)
- [Features & User Benefits](#features--user-benefits)
- [Design Tokens & Typography](#design-tokens--typography)
- [Deployment & Local Preview](#deployment--local-preview)
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

- **Global Sticky Header & Mobile Offcanvas Drawer:** Uses Bootstrap `.navbar-expand-lg` and `.offcanvas-lg.offcanvas-end` so desktop navigation stays inline and mobile viewports get an accessible slide-over menu without custom JavaScript.
- **Appointment Switcher & Stay-Open FAQ (`treatments.html`):** Bootstrap `.nav-pills` tabs separate **Initial Consultation · 90 mins** from **Follow-Up Session · 45 mins**, paired with a boxed FAQ `.accordion` intentionally omitting `data-bs-parent` so visitors can compare multiple answers simultaneously.
- **Location Diagram & Step-Free Access Switcher (`visiting.html`):** Pairs a custom line-drawing SVG street diagram (`twickenham-map.svg`) and Google Maps link with `.nav-pills` travel tabs (*Rail & Bus*, *By Car & Parking*, *Step-Free Access*).
- **Embed-Ready Booking Hub (`booking.html`):** Concentrates clear next steps (Send Booking Enquiry or Call `020 8555 0142`) while preparing space for a future online scheduling calendar.
- **Native Contact Validation & Confirmation Flow (`contact.html` & `thank-you.html`):** Uses HTML5 constraint attributes (`required`, `minlength`, `type="email"`, `inputmode`, `autocomplete`) plus CSS `:user-invalid` styling so inline error hints stay quiet until field blur, routing via `method="get"` to a static `thank-you.html` confirmation page with fictional-practice disclosure.

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

1. Push the updated `main` branch (`git push origin main` — the previous custom-CSS release `f7103b9` remains archived on `archive/v4-custom-css`).
2. In the GitHub repository settings under **Pages**, deploy from branch **`main`** and folder **`/ (root)`**.
3. Open `https://alexswabey.github.io/meadowside-clinic/` and verify navigation links, images, interactive Bootstrap tabs/accordions, and form confirmation parity with the local build.

---

## Validation & Testing Status

Automated QA checks live in the sibling governance repository (`../twickenham-osteopath-project-state` via `npm run qa:full`) alongside industry linters and Lighthouse:

- **Colour contrast:** All 34 palette text (`>= 4.5:1`) and UI/focus boundary (`>= 3.0:1`) pairs verified by `check_contrast.py`.
- **HTML & CSS compliance:** Passed `html-validate` (`0` errors across all 7 HTML files), W3C Jigsaw CSS Validator (`css3svg`, `warning=1`: `0` errors / `0` warnings), and `modern-web-guidance legacy-scan` (`0` findings). *(W3C Nu HTML previously passed `0/0`; a final post-polish Nu re-check hit W3C's `HTTP 429` rate limit and is queued once clear.)*
- **Cross-engine browser & accessibility QA:** Passed **WebKit** and **Chromium** Playwright checks (`1440x900`, `390x844`, `320x700`, offcanvas drawer fit, pill tabs, stay-open FAQ, `:user-invalid` contact feedback, forced-colors, reduced-motion, `0` `axe-core` WCAG 2.1 A/AA violations), plus `Pa11y` (`WCAG2AA`: `0` issues on `index`, `treatments`, `visiting`, `contact`) and `Linkinator` (`0` broken links).
- **Lighthouse (`13.6.0`):** Desktop `index.html` scored **100 / 100 / 100 / 100**; Mobile audits scored **98–99** Performance (`98` Home/Treatments/Visiting, `99` About/Contact) and **100 / 100 / 100** across Accessibility, Best Practices, and SEO.
- **Remaining before final coursework submission:** Push `main`, choose and wire a zero-JS booking tool into `booking.html` if desired, and embed final desktop/mobile, W3C Nu/Jigsaw, and Lighthouse screenshots.

---

## Bugs & Quirks Resolved

- **Bootstrap 5.3 link colour regression (`#0d6efd`):** Defining `--bs-link-color` alone left compiled links Bootstrap-blue; overriding `--bs-link-color-rgb` (`18, 82, 94`) and `--bs-link-hover-color-rgb` (`12, 60, 69`) restored compliant Mineral Teal link contrast across all surfaces.
- **Dark navbar specificity:** Bootstrap's `.navbar[data-bs-theme=dark]` selector outranked `.clinic-navbar`; raising specificity via `.clinic-navbar[data-bs-theme="dark"]` fixed contrast across active, hover, and toggler tokens.
- **Nu HTML ARIA validation on responsive `.offcanvas-lg`:** Added `role="group"` to `#clinicNav` so `aria-labelledby="clinicNavLabel"` remains valid before Bootstrap JS promotes the drawer to `role="dialog"` on mobile toggle.
- **WebKit `:user-invalid` repaint on textarea:** Paired `:user-invalid` sibling combinators with `.clinic-form div:has(> .form-control:user-invalid) > .clinic-error-hint` so validation hints reveal consistently on Tab blur in both WebKit and Chromium.
- **Hidden Bootstrap `.tab-pane` image verification:** Updated the automated Playwright runner to skip `scrollIntoViewIfNeeded()` on `display: none` tab images during initial load and explicitly verify `#followup-pane` `.webp` decoding after clicking `#followup-tab`.

---

## Attribution & Licences

### Photography (Responsive `.webp` Sets in `assets/images/`)

| Slot | Page | Files (`w` × `h`) | Photographer | Source & Licence |
| --- | --- | --- | --- | --- |
| Hero treatment room | `index.html` | `hero-treatment-room-640.webp` (`640x480`), `-800.webp` (`800x600`), `-1200.webp` (`1200x900`) | Kimiya Sabbaghan | [Unsplash](https://unsplash.com/photos/a-white-room-with-a-bed-and-a-desk-o4OJfrmMC0o) · Unsplash License |
| Meet Lydia portrait | `index.html` | `lydia-portrait-640.webp` (`640x480`), `-800.webp` (`800x600`), `-1200.webp` (`1200x900`) | Vitaly Gariev | [Unsplash](https://unsplash.com/photos/woman-with-short-blonde-hair-smiles-against-colorful-wall-ZwNj7w0BnwA) · Unsplash License |
| Initial consultation card | `index.html` | `consultation-conversation-480.webp` (`480x360`), `consultation-conversation-960.webp` (`960x720`) | Vitaly Gariev | [Unsplash](https://unsplash.com/photos/two-women-talking-in-a-modern-office-setting-QxkvMblcaJ0) · Unsplash License |
| Follow-up session card | `index.html` | `osteopathic-lumbar-care-480.webp` (`480x360`), `osteopathic-lumbar-care-960.webp` (`960x720`) | Benjamin Wedemeyer | [Unsplash](https://unsplash.com/photos/persons-hand-on-white-textile-pN140LY8wn8) · Unsplash License |
| Clinic waiting room opener | `about.html` | `clinic-waiting-room-800.webp` (`800x450`), `clinic-waiting-room-1440.webp` (`1440x810`) | Raphael (Ajani Kamali Akio) | [Unsplash](https://unsplash.com/photos/modern-living-room-with-three-sofas-and-coffee-table-LacQuwrta3I) · Unsplash License |
| Initial consultation tab | `treatments.html` | `initial-assessment-640.webp` (`640x480`), `-800.webp` (`800x600`), `-1200.webp` (`1200x900`) | Vitaly Gariev | [Unsplash](https://unsplash.com/photos/a-woman-sitting-in-a-chair-talking-to-another-woman-CGCXJJlkpOQ) · Unsplash License |
| Follow-up session tab | `treatments.html` | `followup-thoracic-care-640.webp` (`640x480`), `-800.webp` (`800x600`), `-1200.webp` (`1200x900`) | Benjamin Wedemeyer | [Unsplash](https://unsplash.com/photos/person-in-black-and-white-striped-long-sleeve-shirt-t_29wZLpYwg) · Unsplash License |
| Twickenham shopfront parade | `visiting.html` | `twickenham-shopfront-640.webp` (`640x480`), `-800.webp` (`800x600`), `-1200.webp` (`1200x900`) | Michael Dibb *(originally contributed via [geograph.org.uk](https://www.geograph.org.uk/photo/7042211))* | *"St Margarets buildings (1)"* via [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:St_Margarets_buildings_(1)_-_geograph.org.uk_-_7042211.jpg) · [CC BY-SA 2.0](https://creativecommons.org/licenses/by-sa/2.0/). **Modifications:** downscaled and re-encoded to responsive `.webp`; derived image files remain licensed under CC BY-SA 2.0. |

### Custom Graphics, Framework & Web Fonts

- **Custom SVGs:** `assets/images/brand-mark.svg` and `assets/images/twickenham-map.svg` were authored specifically for Meadowside Clinic.
- **Bootstrap `5.3.9`:** Front-end grid, components, and interactive bundle loaded via jsDelivr CDN ([MIT License](https://github.com/twbs/bootstrap/blob/main/LICENSE)).
- **Google Fonts:** `Literata` and `Source Sans 3` loaded via Google Fonts API v2 ([SIL Open Font License 1.1](https://scripts.sil.org/OFL)).

---

## AI Use & Reflection

- **Code creation:** AI assisted with scaffolding the seven-page Bootstrap `5.3.9` layout, dual-layer `--bs-*` token architecture, and declarative zero-JS controls (offcanvas menu, `.nav-pills` tabs, stay-open accordion, native `:user-invalid` form validation), enabling cleaner structural separation than earlier custom CSS iterations.
- **Debugging & validation:** AI-assisted contrast audits and cross-engine Playwright + `axe-core` scripts identified `#0d6efd` token leakage, dark navbar specificity collisions, Nu HTML ARIA requirements on `.offcanvas-lg`, and WebKit `:user-invalid` repaint gaps prior to deployment.
- **Performance & UX optimisation:** Guided responsive `.webp` multi-width `srcset`/`sizes` generation, LCP `fetchpriority="high"` vs lazy/low-priority hints on non-critical or hidden-tab images, trimming unused Google Fonts italic axes, and editorial `Literata` + `Source Sans 3` typography selection.
- **Workflow impact:** Separating project state docs and automated QA scripts (`twickenham-osteopath-project-state`) from static site output kept commits auditable and made visual, validator, and accessibility regressions rapid to catch and resolve.

---

## Planned Future Updates

- Wire `booking.html` to a live third-party clinic scheduling embed once an integration is selected.
- Connect `contact.html` (`method="get"`) to a live form handler endpoint for production deployment beyond static GitHub Pages.
- Capture and link post-merge desktop/mobile screenshots, W3C validation proof, and Lighthouse audit reports under `docs/screenshots/`.
