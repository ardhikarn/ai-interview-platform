# UI refinement audit — 23 September 2026

Primary reference: `DESIGN.md` in this directory. The root Cal.com reference informs restraint and hierarchy; the recruitment-specific system retains teal actions, compact controls, and structured tables.

## Gaps and changes

| Area | Gap found | Incremental refinement |
| --- | --- | --- |
| Filters | Native selects differed from form selects | Reusable `FilterSelect` using the installed Radix primitives; original values, callbacks, filter scope, sorting, and pagination preserved |
| Select overlays | Inconsistent selection feedback and unbounded positioning | Trigger minimum width, viewport bounds, collision padding, scroll controls, visible checked/highlighted states, stable chevrons, and 150ms transitions |
| Inputs and search | Strong offset focus rings; browser-specific clear control | Quiet focus treatment, error and disabled surfaces, explicit accessible search-clear action that restores input focus |
| Dialogs | Edge-to-edge mobile width, no height constraint, heavy backdrop | Mobile gutters, viewport height limit, internal scrolling, quieter backdrop, larger close target, and disabled close during invitation submission |
| Menus and tooltips | Overlay bounds and tooltip clipping risk | Collision padding, viewport constraints, menu scrolling, portalled tooltip, and explicit transition timing |
| Tabs and radio controls | Inconsistent radii, focus, and selected treatment | Teal selection, consistent control radius, restrained focus and hover states, wrapped tabs, no tab shadow |
| Skill picker | Fetch failure appeared as no results | Separate loading/error/empty states, retry preserving query, accessible search name and dialog description, stale request protection |
| Content | Tight card headings, duplicate form separator, tiny skill icon targets | Readable heading line height, single action separator, 32px drag/remove targets, and specific remove-button names |

Existing 24px page titles, 14px body text, system fonts, flat cards, 224px sidebar, horizontal mobile navigation, form/report widths, table scanning structure, and semantic status distinctions remain intact. No new application UI library was added. Backend services, hiring rules, and navigation flows were not changed.

## Verification

- Production build passed; 22 Vitest tests passed. Added interaction coverage for selection, Escape/focus restoration, disabled filters, and skill taxonomy failure/retry. Updated existing filter tests to operate the Radix controls.
- Chromium checks at 1440px and 390px: assessment list, candidate invitation dialog, and assessment creation. Checked filter/reset behavior, keyboard opening/dismissal, focus restoration, popup bounds, dialog gutters, and document overflow. No JavaScript errors observed.
- Browser-only component fixture: keyboard option selection, long option wrapping, disabled option/trigger/input/button states, invalid input treatment, search clear/focus, menu dismissal, tab arrow navigation, tooltip display, and reduced-motion animation suppression.
- Reviewed desktop/mobile screenshots and component states. Default, hover, focus, open/active, selected, disabled, and error treatments were checked where applicable; loading and retry were exercised for the skill picker.
- Browser API responses were mocked. The component fixture and runner stayed outside the application source; no sample records were inserted. Live audio, real backend mutations, and AI generation were not exercised end to end in this pass.

The broader report-page checks described in `DESIGN.md` predate this pass; this pass concentrated browser verification on the changed shared controls and their recruitment flows.
