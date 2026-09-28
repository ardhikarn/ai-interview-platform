# Recruitment interface

This is an improvement of the existing React, Tailwind, and Radix interface. Keep assessment configuration, interview lifecycle, portfolio generation, overrides, exports, and hiring decisions on their existing service paths.

## Direction

Use neutral surfaces, quiet borders, compact controls, and teal for primary actions and active navigation. The references are [Cal.com on getdesign.md](https://getdesign.md/cal/design-md) for restrained navigation and hierarchy, and [Airtable on getdesign.md](https://getdesign.md/airtable/design-md) for structured data scanning. These are inspiration, not copied layouts.

## Foundation

- Colors live in `src/index.css` and are exposed through `tailwind.config.js`. Reuse background, surface, muted, foreground, border, primary, success, warning, destructive, and info tokens.
- Default controls are 36px tall; compact actions are 32px. Use 16px icons, 8px container radii, and 6px control radii. Reserve shadows for overlays.
- Page titles use 24px semibold text; body and controls use 14px; metadata uses 12px. Use a system font stack without a remote font dependency.
- Prefer 4/8/12/16/24/32px spacing. Use separators and headings before adding more nested cards.
- Desktop navigation is 224px wide. Forms are limited to 768px and report pages to 1024px. Navigation becomes horizontal on small screens.

## Shared components

- `ui/page.tsx`: PageHeader, ErrorState, EmptyState, TableLoading, SearchField, Pagination.
- `ui/resource-list.tsx`: API-paginated resource table, page-scoped search/filter/sort, retry, and empty states. Assessment and vacancy lists use this component.
- Existing Button, Input, Select, Card, and Badge primitives remain the component foundation. Badge includes neutral, success, warning, danger, and info variants.
- Candidate tables keep interview status separate from evaluation and hiring decisions. Do not infer a hiring decision from a score or interview completion.
- Label AI-generated summaries explicitly and retain the distinction between AI ratings and recruiter overrides.

## Interaction and accessibility

Use actual links for navigation, visible keyboard focus, associated input labels, unique radio IDs, descriptive icon-button names, and textual status labels. Keep errors separate from empty results. Retain entered values when an invitation or form submission fails. Confirm clipboard success only after the browser accepts the write. Respect reduced-motion preferences.

Tables may scroll inside their container on small screens; the page itself should not overflow. Wrap header actions and form controls rather than shrinking text.

## Verification and boundaries

- Production build and 18 Vitest tests pass, including API pagination, filter/reset behavior, load retry, invitation failure/retry, clipboard denial, unique skill radio labels, existing decision rules, and narrative attribution.
- Chromium checks used mocked API responses at 1440px and 390px for assessment lists, candidates, vacancies, assessment creation, vacancy editing, portfolio, fit/gap, and transcript. No document overflow or JavaScript errors were observed in those checks.
- Browser fixtures are test-only; no sample records were inserted into the application or backend.
- Assessment/vacancy search, filter, and sort operate on the current API page, explicitly labeled in the UI. Candidate filters operate on all sessions returned for that assessment.
- Live audio, real backend mutations, and AI generation were not exercised end to end during this UI verification.
