# Validation record

Checked on 2026-10-26 (America/Managua), Windows, Node 24.22.1, Astro 7.4.2, three.js 0.160.0.

| Check | Observed result |
| --- | --- |
| `npm run check` | 0 errors |
| `npm test` | Localized paths |
| `npm run build` | 3 pages: `/`, `/en/`, `404` |
| `npm run test:build` | Generated links and language alternatives resolve |
| `npm run budget` | 3D chunk 143,059 gzip bytes / 160 KiB; other JS 17,007 / 80 KiB; CSS 13,167 / 60 KiB |
| `npm run test:e2e` | 16 passed (Chromium desktop and mobile): metadata, overflow, axe A/AA (except color-contrast, below), script boot with the animated journey in both locales, theme persistence, menu scrolling, blocked storage, no-script content |
| `npm audit --omit=dev` | 0 reported vulnerabilities |
| CSP | No violations in captures of both locales at 1440 and 375 px |
| Visual review | Both locales captured section by section at 1440 and 375 px, dark and light, and compared with the previous static page: no visible differences |

## Known accessibility findings (color contrast, light theme)

axe reports these against WCAG AA 4.5:1. They predate the migration and need a design decision before changing colours:

| Element | Ratio | Where |
| --- | --- | --- |
| `.btn-ops` (dark text on teal) | 2.92:1 | Works, Toolkit action |
| `.danger` (white on red) | 3.91:1 | Playground, Delete button |
| `.ok.pill` (green on pale green) | 4.01:1 | Works, status pills |
| `.pill.ops` (teal on pale teal) | 4.03:1 | Hero card (English) |
| `.pill.ds` (blue on pale blue) | 4.24–4.36:1 | Hero card, Projects |
| `#wordmark` | 1.09:1 | Finale decorative wordmark (`aria-hidden`), intentionally faint |

The browser tests disable only the `color-contrast` rule until these are resolved.
