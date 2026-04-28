# Proposal: MPG-CAPS Landing Static

## Intent

Convert the explored Stitch `MPG-CAPS Landing Page` into a real, maintainable static website. The Stitch screen, its dark automotive design system, and its English copy are the authoritative source of truth. A semantic rebuild is preferred over raw Stitch markup so the final page has clean structure, intentional responsiveness, and no generated DOM noise.

## Scope

### In Scope
- Build one responsive landing page using only `index.html`, `styles.css`, and `script.js`.
- Recreate the Stitch page sections semantically: navigation, hero, product explanation, media/product placeholders, benefits, testimonials, contact actions, and footer.
- Preserve English design text and allow image/video/product placeholders to remain empty black blocks.
- Add only lightweight hover states and minimal progressive JS, likely mobile navigation.

### Out of Scope
- Frameworks, build tooling, external libraries, or hosted font dependencies.
- Multi-page routing, CMS/content editing, forms backend, analytics, SEO expansion, or production media assets.
- Scrolling animations, heavy interactions, or behavior not visible/required by the Stitch landing page.

## Capabilities

### New Capabilities
- `static-landing-page`: Defines the single-page MPG-CAPS static landing experience, responsive behavior, source-of-truth copy, placeholder media policy, and interaction boundaries.

### Modified Capabilities
- None

## Approach

Implement a section-based semantic page from the Stitch reference instead of copying exported markup. Use CSS design tokens for charcoal/orange colors, spacing, type scale, radii, cards, placeholders, and breakpoints. Keep `script.js` minimal and non-essential so the page remains usable without complex runtime behavior.

## Affected Areas

| Area | Impact | Description |
|------|--------|-------------|
| `index.html` | New | Semantic single-page content and section structure. |
| `styles.css` | New | Visual system, responsive layout, placeholders, and hover states. |
| `script.js` | New | Minimal mobile navigation/progressive enhancement only. |
| `openspec/changes/mpg-caps-landing-static/` | Modified | SDD artifacts for proposal/spec/design/tasks. |

## Risks

| Risk | Likelihood | Mitigation |
|------|------------|------------|
| Visual drift from Stitch | Medium | Treat Stitch screen/design metadata as source of truth during spec/design. |
| Typography mismatch without external fonts | Medium | Define local fallback stacks and avoid external dependencies. |
| Responsive layouts feel cramped | Medium | Specify breakpoints and placeholder aspect ratios before implementation. |

## Rollback Plan

Remove the three static site files and revert this change folder/artifacts; no runtime migration or data rollback is needed.

## Dependencies

- Existing Stitch exploration artifact and referenced Stitch screen/design system.

## Success Criteria

- [ ] Static site exists only as `index.html`, `styles.css`, and `script.js`.
- [ ] Page matches the Stitch structure, atmosphere, and English copy within static-site constraints.
- [ ] Layout is usable across desktop, laptop, tablet, and mobile.
- [ ] No frameworks, build tools, external libraries, scrolling animations, or heavy interactions are introduced.
