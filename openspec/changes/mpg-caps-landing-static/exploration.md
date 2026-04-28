## Exploration: mpg-caps-landing-static

### Current State
The repository has no website implementation yet; it currently contains only SDD scaffolding and project skills. The source of truth for the landing page lives in Stitch as the `MPG-CAPS Landing Page` screen plus its associated dark automotive design system. The exported screen already defines the single-page structure, English marketing copy, placeholder media blocks, and the overall charcoal/orange visual direction.

### Affected Areas
- `openspec/changes/mpg-caps-landing-static/exploration.md` — exploration artifact for this change.
- `index.html` — will hold the full single-page semantic structure: navbar, hero, product explanation, video placeholder, benefits, testimonials, contacts, and footer.
- `styles.css` — will hold the full visual system, responsive layout, card treatments, placeholders, hover states, and breakpoint behavior.
- `script.js` — should stay minimal; likely limited to mobile navigation toggling and tiny progressive enhancement only.
- `openspec/config.yaml` — confirms there is no existing app/runtime stack, no test runner, and no build tooling to integrate with.

### Approaches
1. **Semantic rebuild from Stitch source** — Recreate the landing page manually in plain HTML/CSS/JS using the Stitch screen, design tokens, and visible copy as the implementation reference.
   - Pros: Clean static output, easy to maintain, responsive structure can be intentional, fits the `index.html` / `styles.css` / `script.js` constraint exactly.
   - Cons: Requires interpretation of spacing and layout details instead of copying raw generated DOM.
   - Effort: Medium

2. **Port the exported Stitch HTML literally** — Start from the generated HTML structure and strip it down until it behaves like a clean static site.
   - Pros: Faster initial parity with the screen.
   - Cons: Likely carries noisy markup, weak semantics, brittle responsiveness, and harder long-term maintenance.
   - Effort: Medium-High

### Recommendation
Use **Semantic rebuild from Stitch source**. This de-risks the final deliverable because the project wants a real static website, not a preserved AI export. The best implementation is a section-based page with reusable patterns for CTA buttons, content cards, benefit items, testimonial cards, contact actions, and placeholder media blocks, all driven by a small set of CSS tokens for colors, spacing, radius, and type scale.

### Risks
- The source brief originated in Spanish, but the Stitch screen copy currently appears in English; proposal/spec should explicitly declare which copy is authoritative.
- The Stitch design references `Space Grotesk` and `Inter`; without external font loading, final typography will need fallback stacks or a later self-hosting decision.
- Placeholder image/video/product blocks must preserve composition with fixed aspect ratios, or the page will collapse visually on smaller screens.
- The hero and multi-card sections need deliberate breakpoint rules so the automotive visual weight survives tablet/mobile without becoming cramped.

### Ready for Proposal
Yes — the change is sufficiently de-risked. The next phase should lock the semantic section map, declare the copy source of truth, and specify the responsive/static implementation plan for `index.html`, `styles.css`, and `script.js`.
