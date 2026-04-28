# Design: MPG-CAPS Landing Static

## Technical Approach

Build a single semantic static document from the Stitch landing page direction, not from exported/generated markup. `index.html` owns accessible content and landmarks; `styles.css` owns all visual system tokens, layout, responsive behavior, and hover states; `script.js` is optional progressive enhancement only. This maps directly to the spec: ordered sections, responsive ranges, minimal interaction, accessibility, dark automotive visual fidelity, and no frameworks/build tooling/external libraries.

## Architecture Decisions

| Decision | Choice | Alternatives considered | Rationale |
|---|---|---|---|
| Source translation | Semantic rebuild from Stitch | Ship raw Stitch HTML or heavily edit export | Cleaner DOM, better headings/landmarks, intentional responsiveness, and easier maintenance under the three-file constraint. |
| Page architecture | One `index.html` with `header`, `main`, ordered `section`s, `footer` | Componentized framework or multiple pages | The scope is one static landing page; native HTML is enough and avoids banned dependencies. |
| CSS architecture | Token-first stylesheet with reusable classes | One-off per-section CSS or utility-only sprawl | Tokens preserve the charcoal/orange system; reusable cards/buttons/placeholders reduce drift while keeping CSS understandable. |
| Typography | Local/system stacks approximating Space Grotesk/Inter: headline `"Aptos Display", "Segoe UI", system-ui, sans-serif`; body `"Aptos", "Segoe UI", system-ui, sans-serif` | Google Fonts, self-hosted fonts, Arial-only | External fonts are banned. System stacks keep performance/dependency risk low while preserving a modern geometric feel. |
| JS behavior | Only mobile nav toggle and optional anchor polish | Scroll animations, carousels, form logic | Spec requires static usability without JS and bans heavy interactions. |

## Data Flow

Static browser load only:

    index.html content/anchors
          │
          ├── styles.css tokens, layout, hover states, breakpoints
          └── script.js progressive nav enhancement

No API, state store, build pipeline, analytics, or runtime data migration.

## File Changes

| File | Action | Description |
|---|---|---|
| `index.html` | Create | Document metadata, skip link, header/nav, hero, product explanation, video placeholder, benefits, testimonials, contacts, footer, and script/style references. |
| `styles.css` | Create | CSS custom properties for colors/spacing/type/radius/shadows, base reset, layout primitives, buttons, cards, placeholder blocks, responsive grids, focus/hover states. |
| `script.js` | Create | Small DOM-ready enhancement for mobile navigation: toggle `aria-expanded`, menu visibility class, close on in-page link selection/Escape if implemented. |

## Interfaces / Contracts

Recommended DOM contract:

- `body > .site-header + main + footer.site-footer`
- Main sections in exact order: `#hero`, `#product`, `#video`, `#benefits`, `#testimonials`, `#contact`
- Reusable classes: `.container`, `.section`, `.eyebrow`, `.button`, `.button--primary`, `.button--secondary`, `.card`, `.media-placeholder`, `.grid`, `.stack`
- Placeholders remain black visual blocks with stable aspect ratios (`16 / 9` for video, product/media ratios as composition requires) and accessible labels such as `aria-label="Product media placeholder"` unless decorative.

CSS token groups:

- Color: page black, charcoal surfaces, muted borders, orange accent, off-white text, subdued copy.
- Spacing: fluid section padding via `clamp()`, container max width, consistent grid gaps.
- Layering: subtle borders, dark gradients, restrained shadows; no animated scroll effects.

Breakpoints: mobile-first default, `480px` compact phones, `768px` tablet, `1024px` laptop, `1280px` desktop. Hero/product/contact become two-column at laptop; card grids move from one column to two at tablet and three at laptop/desktop where content fits. Navigation collapses below tablet/laptop threshold without hiding anchor access.

## Testing Strategy

| Layer | What to Test | Approach |
|---|---|---|
| Static review | Required section order, English copy, file constraint | Manual source inspection; no test runner exists. |
| Responsive | No horizontal overflow; readable typography; placeholders keep ratios | Browser resize at mobile/tablet/laptop/desktop widths. |
| Accessibility | Landmarks, heading order, keyboard nav, focus states, contrast | Manual keyboard pass and browser accessibility tree inspection. |

## Migration / Rollout

No migration required. Add the three root static files and keep OpenSpec artifacts under `openspec/changes/mpg-caps-landing-static/`.

## Open Questions

- [ ] None blocking. Final implementation should use Stitch as copy/composition reference and keep black placeholder blocks until assets are provided.
