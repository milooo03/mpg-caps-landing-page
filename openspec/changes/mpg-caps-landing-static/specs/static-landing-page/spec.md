# Static Landing Page Specification

## Purpose

Define one semantic, responsive MPG-CAPS landing page rebuilt from the explored Stitch direction using only `index.html`, `styles.css`, and minimal `script.js`.

## Requirements

### Requirement: Section Structure and Copy

The page MUST render a single document with these sections in order: navbar, hero, product explanation, video placeholder, benefits, testimonials, contacts, and footer. The navbar SHALL expose brand identity and in-page navigation; the hero SHALL present primary headline, supporting copy, and CTA emphasis; the product explanation SHALL clarify the offer; the video placeholder SHALL reserve media space; the benefits and testimonials sections SHALL communicate value and trust; the contacts section SHALL expose contact actions; and the footer SHALL close the page with secondary navigation or brand information. Visible marketing copy MUST remain in English and follow the Stitch source of truth.

#### Scenario: All required sections exist
- GIVEN the page loads successfully
- WHEN a reviewer scans the document outline
- THEN each required section appears once in the expected order

#### Scenario: Copy remains authoritative
- GIVEN the Stitch reference provides English text
- WHEN implementation content is reviewed
- THEN section headings, CTA labels, and body copy remain in English

### Requirement: Responsive Layout

The layout MUST remain usable across four responsive ranges representing desktop, laptop, tablet, and mobile. Multi-column areas SHALL collapse progressively, navigation SHALL remain reachable on narrow screens, and placeholder media blocks MUST preserve composition without overflowing or collapsing.

#### Scenario: Desktop and laptop presentation
- GIVEN a wide viewport
- WHEN the page is viewed above tablet width
- THEN hero and card-based sections may use multiple columns with balanced spacing

#### Scenario: Tablet and mobile presentation
- GIVEN a narrow viewport
- WHEN the page is viewed at tablet or mobile widths
- THEN columns stack or simplify, text stays readable, and no horizontal scrolling is introduced

### Requirement: Allowed Interactions

The page MUST limit interactivity to standard anchor/navigation behavior, lightweight hover states for buttons, links, and cards, and minimal progressive enhancement such as mobile navigation toggling. The page MUST remain understandable if JavaScript is absent.

#### Scenario: Minimal enhancement
- GIVEN JavaScript is unavailable
- WHEN the page is loaded
- THEN content and anchor navigation still work as a static landing page

#### Scenario: Hover-only affordances
- GIVEN a pointer-capable device
- WHEN a user hovers an interactive element
- THEN a visible hover state appears without triggering animation-heavy behavior

### Requirement: Accessibility and Semantics

The document MUST use semantic HTML landmarks and heading hierarchy appropriate for a landing page. Interactive elements MUST be keyboard reachable, placeholders MUST expose meaningful text alternatives or be explicitly decorative, and color usage SHOULD preserve readable contrast in the dark theme.

#### Scenario: Semantic navigation
- GIVEN a reviewer inspects the markup
- WHEN landmarks and headings are checked
- THEN header, nav, main, section, and footer semantics support page understanding

#### Scenario: Keyboard access
- GIVEN a keyboard-only user
- WHEN tabbing through the page
- THEN links, CTAs, and any mobile navigation control are reachable and operable

### Requirement: Visual Fidelity

Styling MUST reflect the explored Stitch direction: dark automotive atmosphere, charcoal-dominant surfaces, orange accent emphasis, strong typographic hierarchy, card-based grouping, and intentional spacing. Local/system font stacks MAY approximate the reference, but the page SHALL NOT depend on hosted external fonts.

#### Scenario: Design direction is preserved
- GIVEN the implemented page is compared to the explored Stitch reference
- WHEN atmosphere, hierarchy, and section composition are reviewed
- THEN the page clearly matches the intended dark automotive visual identity

### Requirement: Explicit Non-Requirements

The page MUST NOT introduce extra pages, forms backend behavior, analytics, CMS editing, frameworks, build tooling, external libraries, scrolling animations, autoplay media, or heavy interactive effects beyond the stated scope.

#### Scenario: Scope remains tight
- GIVEN the delivered files are reviewed
- WHEN included features and dependencies are checked
- THEN only the single static landing page scope is present
