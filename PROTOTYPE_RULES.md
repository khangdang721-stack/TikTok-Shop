# ZLP Prototype Rules

## Purpose

Build interactive browser prototypes for design review, user flow validation, and stakeholder demo.

The prototype should prioritize:

1. Visual accuracy
2. Fast iteration
3. Designer-editable code
4. Lightweight implementation
5. Reliable mobile responsiveness
6. Clear visual QA reporting

This repo is for prototype work, not production engineering.

---

## Default technology

Use static HTML, CSS, and vanilla JavaScript by default.

Do not use:

- React
- Next.js
- Vite
- npm
- TypeScript
- TSX
- build tools
- external UI libraries

unless explicitly requested by the user.

The prototype must open directly in browser with VS Code Live Server or a simple static server.

---

## Output

Create or update:

- `index.html`
- `README.md`
- `assets/` only if needed
- `spek-export/` only when Spek output is provided

The default prototype should work with:

```text
Right click index.html → Open with Live Server
```

or:

```bash
python3 -m http.server 5500
```

Do not create unnecessary files.

If the prototype becomes large, only then split into:

- `index.html`
- `styles.css`
- `script.js`
- `assets/`
- `spek-export/`

Do not split files prematurely.

---

## Default response after edits

After every edit, provide a short summary with:

- Files changed
- What was changed
- What was intentionally left unchanged
- Any remaining uncertainty or mismatch

Keep the summary concise.

---

## Prototype behavior

Use mock data only.

Do not connect real APIs.

Do not add authentication.

Do not store real user data.

Do not use localStorage/sessionStorage unless explicitly requested.

Keep the prototype lightweight and easy for designers to edit.

---

## Default edit behavior

For every follow-up edit request, treat the request as a targeted patch by default.

Unless the user explicitly asks for a full rebuild, redesign, refactor, or technology change, always follow these rules:

- Only edit the specific areas requested by the user.
- Do not rebuild the whole page.
- Do not restructure the entire prototype.
- Do not change unrelated sections.
- Do not change existing logic or interactions unless the request requires it.
- Do not change technology stack.
- Do not add React, Next.js, Vite, npm, TypeScript, TSX, routing libraries, or build tools.
- Preserve the current visual structure as much as possible.
- Preserve existing responsive behavior unless the request is about responsiveness.
- Preserve existing desktop phone-frame behavior unless the request is about desktop preview.
- Preserve existing interactions unless the request is about interaction logic.
- Make the smallest safe HTML/CSS/JS change that solves the issue.
- If the requested fix may affect other areas, report the risk before or after the change.
- After editing, summarize what changed and mention anything uncertain.

This applies to all small UI fixes, asset replacements, spacing fixes, responsive fixes, interaction fixes, text changes, and visual QA fixes.

---

## Rebuild and refactor permission rule

Do not perform a full rebuild, broad refactor, or technology migration unless the user explicitly says one of the following:

- rebuild the whole page
- refactor the structure
- restructure the prototype
- convert to React
- use TSX
- use Vite
- create a new architecture
- rebuild from scratch
- regenerate the prototype

If the user only says "fix", "adjust", "update", "make this closer", "replace this asset", or "change this interaction", treat it as a targeted patch.

---

## Figma source of truth

Use Figma MCP/integration as the visual source of truth when a Figma frame link is provided.

Before coding, inspect the Figma frame and summarize:

- frame name
- frame size
- main sections
- colors
- typography
- repeated components
- important layout observations

If Figma cannot be accessed, do not guess from the URL.

Ask for screenshot/export or state the limitation clearly.

---

## Spek-first implementation rule

If a `spek-export/` folder exists, Codex must treat it as the primary design source before making or editing UI.

Codex must not start implementation from visual guessing, screenshots, or self-created approximations before inspecting Spek.

Before any build or UI edit, Codex must scan and use relevant files from:

1. `spek-export/manifest.yaml`
2. `spek-export/README.md`
3. `spek-export/specs_document/`
4. `spek-export/components/`
5. `spek-export/styles/`
6. `spek-export/images/`
7. `spek-export/icons/`
8. `spek-export/vectors/`
9. `spek-export/ellipses/`
10. `spek-export/previews/`

Codex must summarize which Spek files or folders were checked before making changes.

If a relevant asset, icon, vector, style, component, or preview exists in `spek-export/`, Codex must use it or follow it.

Codex must not recreate UI elements manually when an equivalent Spek source exists.

Examples:

- If a banner image exists in `spek-export/images/`, use that image instead of rebuilding the banner with HTML/CSS.
- If an icon exists in `spek-export/icons/`, use the icon file instead of drawing it with CSS or inline SVG.
- If a vector exists in `spek-export/vectors/`, inspect it before approximating the shape.
- If typography exists in `spek-export/styles/`, use it before inventing font sizes or weights.
- If fills, strokes, gradients, or effects exist in `spek-export/styles/`, use those values before approximating colors, borders, or shadows.
- If a component spec exists in `spek-export/components/`, follow its structure before creating a new static pattern.
- If a preview exists in `spek-export/previews/`, use it for final visual QA.

Only use approximation when Spek does not provide enough information or the relevant Spek asset is missing/broken.

---

## No self-invented UI rule

Do not invent, redraw, or approximate UI elements when a Spek source is available.

Avoid these behaviors unless explicitly required:

- recreating exported images with HTML/CSS
- redrawing icons with CSS
- manually writing inline SVG paths
- inventing gradients from screenshots
- approximating shadows when Spek effects exist
- creating new colors when Spek fills exist
- creating new typography values when Spek typography exists
- creating new layout structure when Spek component or screen specs exist
- replacing exported assets with emoji, CSS shapes, or placeholder drawings
- simplifying complex vectors without checking Spek vectors first

If Codex chooses not to use a Spek source, it must explain why.

Valid reasons include:

- relevant Spek file is missing
- asset file is corrupted or cannot render
- SVG export is broken and needs PNG fallback
- Spek spec conflicts with explicit user instruction
- Spek preview does not match the requested visual target
- user explicitly asks for a custom/manual implementation

Otherwise, Codex must use the Spek source.

---

## Spek usage report rule

After every build or edit where `spek-export/` exists, Codex must include a short Spek usage report.

Use this format:

### Spek sources checked

- `spek-export/...`
- `spek-export/...`

### Spek sources used

- `spek-export/...`

### Manual approximations

- List any element that was manually recreated or approximated.
- Explain why Spek was not used for that element.

### Missing or risky Spek sources

- List any missing, broken, unclear, or risky assets/specs.

If no manual approximation was used, state:

- No manual approximation. Used available Spek sources where relevant.

---



---

## Spek as design spec source

If a `spek-export/` folder exists, use it as the primary design specification source.

Priority order:

1. Explicit user instruction
2. `PROTOTYPE_RULES.md`
3. `spek-export/`
4. local `assets/`
5. Figma screenshot or preview
6. reasonable prototype defaults

Use Spek to understand:

- screen hierarchy
- layout structure
- spacing and padding
- typography
- fills
- strokes
- effects
- shadows
- gradients
- component variants
- repeated UI patterns
- asset references
- icons
- images
- vectors
- preview references

Use screenshots mainly for final visual QA.

If Spek and screenshot conflict, report the conflict before making assumptions.

---

## Spek export reading rule

If a `spek-export/` folder is available, inspect it before coding.

Read in this order when available:

1. `spek-export/manifest.yaml`
2. `spek-export/README.md`
3. `spek-export/specs_document/`
4. `spek-export/styles/`
5. `spek-export/components/`
6. `spek-export/images/`
7. `spek-export/icons/`
8. `spek-export/vectors/`
9. `spek-export/ellipses/`
10. `spek-export/previews/`

Use the Spek export to determine:

- screen structure
- component hierarchy
- repeated patterns
- exact style values
- asset usage
- image/icon/vector references
- preview image for visual QA

Prefer Spek styles over screenshot color guessing.

Prefer Spek asset references over recreating visuals with HTML/CSS.

Prefer Spek component structure over inventing new UI patterns.

Keep the final prototype static HTML, CSS, and vanilla JavaScript unless explicitly requested otherwise.

Do not create React, TSX, npm, Vite, Next.js, or build tools unless explicitly requested.

---

## Spek responsive interpretation rule

Spek export is usually based on a fixed Figma frame width, such as 375px.

When implementing Spek specs:

- Use Spek values as the base design reference.
- Do not blindly hard-code every frame width from Spek.
- Convert the main screen and major sections into responsive containers.
- Preserve visual proportions from Spek at 375px.
- Adapt layout fluidly for 320px–430px mobile widths.
- Keep fixed sizes only for icons, small buttons, badges, and controls.
- Let banners, cards, list items, and main content expand with the viewport.
- Use Spek preview or screenshot at 375px for visual accuracy.
- Then verify responsiveness at all supported widths.

Spek helps with visual accuracy.

Responsive rules ensure the prototype works across real mobile devices.

---

## Spek asset rule

When Spek exports icons, images, vectors, ellipses, or previews, Codex must inspect and prefer those sources before creating visual elements manually.

Asset priority:

1. Explicit user-provided asset instruction
2. Spek exported image/icon/vector/ellipse
3. Local `assets/`
4. Figma screenshot or preview
5. Manual HTML/CSS approximation

Use exported assets when available:

- `spek-export/images/` for banners, illustrations, complex visual blocks, screenshots, and image-based sections
- `spek-export/icons/` for icon assets
- `spek-export/vectors/` for vector shapes
- `spek-export/ellipses/` for ellipse/circle assets or decorative shapes
- `spek-export/previews/` for visual QA reference

Do not recreate exported images, icons, or vectors with HTML/CSS if a usable Spek asset exists.

Do not inline or rewrite SVG unless explicitly requested.

Do not modify SVG paths, viewBox, masks, clipPaths, gradients, or filters unless fixing a confirmed export issue.

For prototype visual accuracy:

- Use SVG through `<img>` for simple icons.
- Use PNG/JPEG/WebP for complex visual blocks.
- Use PNG fallback if an SVG renders incorrectly.
- Preserve aspect ratio.
- Do not stretch assets.
- Do not crop assets unless the design requires it.

---

## Spek conflict rule

If Spek spec, local assets, Figma preview, and screenshot do not match:

- Do not silently guess.
- Report the mismatch.
- Prefer explicit user instruction first.
- Prefer Spek spec for layout, structure, spacing, and style values.
- Prefer exported image assets for complex visuals.
- Prefer screenshot/Figma preview for final visual appearance.
- Make the safest implementation choice and document the assumption in `README.md`.

Examples:

- If Spek says a banner is an exported image, use the image instead of rebuilding it with HTML/CSS.
- If Spek spacing differs slightly from screenshot, preserve the screenshot appearance only if it clearly matches the visual reference better.
- If an asset is missing, implement a safe placeholder and report the missing asset.

---

## Codex bootstrap mode

This prototype repo may start with no existing components, no design tokens, and no shared UI system.

When the repo does not contain reusable components yet, bootstrap only the minimum structure needed to build the requested prototype.

Do not ask the designer to provide:

- component map
- design token file
- frontend specification
- React component structure
- production-level architecture

unless explicitly requested.

The designer may provide only:

- a Figma frame link
- Spek export
- screenshot/reference image
- optional assets
- a short description of the intended flow

Infer and build a lightweight prototype from these inputs.

---

## Bootstrap component rules

If no reusable components exist yet, create simple prototype-level patterns only when clearly useful.

Prioritize creating these only if needed by the current screen or flow:

- button
- header
- card
- bottom CTA area
- input
- list item
- modal
- bottom sheet
- toast
- empty state
- loading state
- badge
- progress indicator

Do not create a full design system.

Do not create unused components.

Do not create complex abstractions.

Do not create framework-style component architecture.

If a UI element is used only once, keep it local in the HTML/CSS structure for that screen.

If a UI pattern appears multiple times in the same prototype, create a reusable CSS class or lightweight HTML pattern.

For static HTML prototypes, prefer reusable CSS classes over JavaScript-driven components.

---

## Static interpretation of Spek components

This repo uses static HTML, CSS, and vanilla JavaScript by default.

When Spek references components or variants, translate them into reusable static patterns instead of TSX components.

Examples:

- `Button/Primary` → `.zlp-button .zlp-button--primary`
- `Button/Secondary` → `.zlp-button .zlp-button--secondary`
- `Button/Disabled` → `.zlp-button .zlp-button--disabled`
- `Card/Product` → `.zlp-card .zlp-card--product`
- `Input/Search` → `.zlp-input .zlp-input--search`
- `BottomCTA` → `.zlp-bottom-cta`
- `Badge/Coin` → `.zlp-coin-badge`
- `Progress/Milestone` → `.zlp-progress .zlp-progress--milestone`

Do not create React, TSX, npm, Vite, or Next.js unless explicitly requested.

---

## Static component pattern rules

Because this repo uses static HTML, CSS, and vanilla JavaScript by default, reusable components should be implemented as HTML/CSS patterns, not React or TSX components.

Do not create `.tsx`, React components, npm setup, Vite, or Next.js unless explicitly requested.

For reusable UI elements, create:

- clear HTML block comments
- reusable CSS classes
- predictable class naming
- small vanilla JavaScript helpers only when interaction is needed

Use this naming convention:

- `.zlp-app`
- `.zlp-screen`
- `.zlp-section`
- `.zlp-header`
- `.zlp-button`
- `.zlp-button--primary`
- `.zlp-button--secondary`
- `.zlp-button--disabled`
- `.zlp-card`
- `.zlp-bottom-cta`
- `.zlp-badge`
- `.zlp-coin-badge`
- `.zlp-task-card`
- `.zlp-progress`
- `.zlp-modal`
- `.zlp-toast`
- `.zlp-icon-button`
- `.zlp-tabs`

Each reusable pattern should be easy for a designer to copy into another screen.

If a pattern is used two or more times in the same prototype, convert it into a reusable CSS class.

If a pattern is likely to be reused in future screens, add a short note in `README.md` under “Reusable patterns”.

---

## Component promotion rule

Use this rule to decide whether something should become reusable:

- Used once: keep it local.
- Used two or more times: create a reusable CSS class or HTML pattern.
- Used across multiple screens: document it briefly in `README.md`.
- Requires behavior: keep JavaScript small and readable.

Do not promote screen-specific UI into reusable patterns too early.

Do not create a component map at the beginning of a new prototype repo.

After 3–5 screens are built, summarize repeated UI patterns and suggest what should become reusable.

---

## Layout rules

The prototype must be fluid across mobile widths.

The Figma/Spek frame width of 375px is only the visual reference baseline, not the final fixed screen width.

Use 375px to preserve visual proportion, spacing rhythm, typography hierarchy, and component scale.

Do not treat 375px as a hard-coded viewport width.

---

### Supported mobile viewport widths

The prototype must support these mobile widths:

- 320px
- 360px
- 375px
- 390px
- 414px
- 430px

The layout must adapt fluidly between 320px and 430px.

---

### Mobile layout behavior

On real mobile viewport or browser device emulation:

- The app must use the full available viewport width.
- The main screen must be `width: 100%`.
- The main screen must not be fixed to `375px`.
- The main screen must not be centered inside a fixed 375px wrapper.
- There must be no unintended white/blank side gutters on 390px, 414px, or 430px.
- Long pages must scroll vertically.
- Horizontal scrolling is not allowed.

Correct:

```css
.zlp-app {
  width: 100%;
  min-height: 100vh;
  overflow-x: hidden;
}

.zlp-screen {
  width: 100%;
  min-height: 100vh;
}
```

---

Sau đó cũng nên thay section **Responsive device rules** hiện tại bằng bản ngắn hơn, để tránh trùng và mâu thuẫn:

```md
## Responsive device rules

The prototype must be built mobile-fluid first.

Do not implement the page as a fixed 375px canvas.

Use 375px only as the baseline for visual matching.

The implementation must adapt from 320px to 430px.

Required behavior:

- `html`, `body`, app root, and screen root use `width: 100%`.
- Major sections use `width: 100%`.
- Cards and content blocks use `width: 100%`.
- Side padding uses responsive values such as `clamp()`.
- Banners and full-width images expand with the viewport.
- Small icons and controls keep fixed sizes.
- No horizontal scroll.
- No unintended side gutters on 390px, 414px, or 430px.

Recommended global CSS baseline:

```css
* {
  box-sizing: border-box;
}

html,
body {
  width: 100%;
  min-height: 100%;
  margin: 0;
  overflow-x: hidden;
}

body {
  -webkit-font-smoothing: antialiased;
}

.zlp-app {
  width: 100%;
  min-height: 100vh;
  overflow-x: hidden;
}

.zlp-screen {
  width: 100%;
  min-height: 100vh;
  background: var(--zlp-screen-bg);
}

.zlp-section {
  width: 100%;
  padding-left: clamp(16px, 5vw, 24px);
  padding-right: clamp(16px, 5vw, 24px);
}

.zlp-card,
.zlp-list,
.zlp-banner,
.zlp-content-block {
  width: 100%;
}

img {
  max-width: 100%;
}
```
## Desktop preview vs mobile responsive rule

The prototype must behave differently on desktop browser and mobile/device emulation.

### Desktop browser behavior

On desktop browser widths, the prototype must appear inside a centered mobile phone-like frame.

Desktop browser should not stretch the mobile UI to full page width.

Use desktop preview shell when viewport width is larger than 768px.

Recommended behavior:

- Body background can be dark or neutral.
- The prototype is centered horizontally.
- The mobile screen width should be fixed for preview.
- Default desktop preview width should be 375px.
- Optional desktop preview max width can be 430px only when testing larger mobile devices.
- The mobile UI must not expand to full desktop browser width.
- Bottom navigation must stay inside the mobile frame.
- Long mobile pages should scroll inside the phone frame or page shell, not stretch across the desktop.

Recommended CSS pattern:

```css
html,
body {
  width: 100%;
  min-height: 100%;
  margin: 0;
  overflow-x: hidden;
}

body {
  background: #2f2f2f;
}

.zlp-app {
  width: 100%;
  min-height: 100vh;
}

.zlp-device-shell {
  width: 100%;
  min-height: 100vh;
}

.zlp-screen {
  width: 100%;
  min-height: 100vh;
  background: var(--zlp-screen-bg);
}

/* Desktop preview shell */
@media (min-width: 768px) {
  body {
    background: #2f2f2f;
  }

  .zlp-app {
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: flex-start;
    padding: 24px 0;
  }

  .zlp-device-shell {
    width: 375px;
    max-width: 375px;
    min-height: 812px;
    background: var(--zlp-screen-bg);
    overflow: hidden;
    border-radius: 40px;
    box-shadow: 0 24px 80px rgba(0, 0, 0, 0.24);
  }

  .zlp-screen {
    width: 100%;
    max-width: 100%;
    min-height: 812px;
  }
}
```
---

## Reference-based implementation rules

When building from a Figma frame, Spek preview, screenshot, or exported reference, prioritize visual accuracy in this order:

1. Overall layout structure
2. Main content hierarchy
3. Fixed header or bottom CTA behavior
4. Asset size and placement
5. Spacing rhythm
6. Typography hierarchy
7. Color matching
8. Shadows, blur, gradients, and decorative effects
9. Responsive behavior across supported widths

Do not chase pixel-perfect accuracy by adding fragile absolute positioning unless the prototype specifically requires it.

Use absolute positioning only for decorative or highly specific visual elements.

Use normal document flow, flexbox, or grid for most layout.

---

## Screenshot-only limitation

If only a screenshot or exported image is provided, do not assume perfect design metadata.

You may infer layout, spacing, color, and typography, but clearly state uncertain assumptions.

When information is missing, prefer reasonable prototype defaults:

- width: 375px as base reference
- visible viewport: 375x812
- supported responsive range: 320px–430px
- spacing grid: 4px
- common spacing: 8, 12, 16, 20, 24, 32
- border radius: 8, 12, 16, 24
- font family: system font unless specified by Figma or Spek
- object-fit: contain for non-photo assets

Do not block implementation because exact values are missing.

Make the best reasonable prototype and list the assumptions afterward.

---

## Asset inspection rules

Before coding, inspect all provided assets.

For each important asset, summarize:

- file name
- file type
- actual pixel size, if available
- intended display size, if inferable from Figma, Spek, or screenshot
- whether it appears to have transparent padding
- whether it should be rendered as image, inline SVG, background image, or CSS shape

Asset rendering rules:

- Preserve aspect ratio.
- Do not stretch icons, logos, or illustrations.
- Use `object-fit: contain` for icons, logos, and illustrations.
- Use `object-fit: cover` only for photo-like banners or thumbnails.
- Do not crop assets unless the design clearly requires it.
- If an asset export seems wrong, report the issue before trying to compensate with layout hacks.

If the visual mismatch is caused by a bad export, state it clearly instead of over-adjusting the code.

---

## Typography rules

Use Spek typography values when available.

If typography is not specified:

- Use system font.
- Preserve visual hierarchy from the reference.
- Avoid browser default typography.
- Use consistent font weights.
- Avoid over-bold text unless the design clearly uses it.
- Preserve line-height and text wrapping as closely as possible.

Responsive typography:

- Keep key headings visually close to the 375px reference.
- Use `clamp()` only when text needs to adapt across 320px–430px.
- Avoid font scaling that makes text too large on 430px devices.
- Prevent CTA labels and short labels from wrapping unexpectedly.

---

## Color, gradient, and effect rules

Use Spek style values when available.

Prefer exact values from:

- `styles/fills`
- `styles/gradients`
- `styles/effects`
- `styles/strokes`
- `styles/typography`

Do not approximate gradients, shadows, or effects from screenshots if Spek provides exact values.

If a complex gradient or visual effect is exported as an image, prefer using the image asset.

For shadows:

- Keep shadows subtle and close to reference.
- Avoid overly heavy shadows unless explicitly shown.
- Do not add new glow/bloom effects unless present in design.

---

## Interaction implementation

Implement only the interactions requested in the user flow.

Keep interactions simple, visible, and reviewable.

Do not add hidden interactions.

Do not add extra flows.

Do not connect real APIs.

Add a desktop-only Reset button only if it helps demo the flow.

For state-based interactions:

- Keep state logic in small vanilla JavaScript functions.
- Use readable class toggles.
- Avoid complex state management.
- Do not introduce framework-like patterns.

---

## SVG icon rendering rules

When Spek or Figma exports SVG icons, use the original SVG files directly whenever possible.

Preferred rendering method:

```html
<img class="zlp-icon" src="spek-export/icons/icon-name.svg" alt="" />
```

---

## Designer-friendly feedback rule

The designer should be able to give visual feedback without writing frontend instructions.

Accept feedback such as:

- icon is too large
- CTA is too close to the bottom
- card feels too wide
- title is too bold
- spacing should feel closer to Figma
- illustration looks stretched
- shadow is too heavy
- section hierarchy is not clear enough
- the UI has too much blank space on 430px
- the card should expand on larger mobile devices
- the banner should fill the width
- the page should not have side gutters

Translate designer feedback into HTML/CSS/JS changes.

Do not require the designer to provide exact CSS values unless they want to.

---

## Code organization

Keep the file structure simple.

Default output:

- `index.html`
- `README.md`
- `assets/`
- `spek-export/`

Do not introduce npm, bundlers, preprocessors, or framework conventions unless explicitly requested.

For CSS:

- Use clear section comments.
- Use reusable CSS classes only when helpful.
- Keep class names readable for designers.
- Avoid deeply nested selectors.
- Avoid hard-to-edit generated CSS.
- Prefer CSS variables for repeated colors, spacing, radius, and shadows.
- Avoid fragile pixel-perfect absolute layouts unless necessary.

For JavaScript:

- Use plain, readable JavaScript.
- Keep interactions close to the elements they affect.
- Avoid complex state management.
- Avoid unnecessary libraries.
- Keep event handlers easy to understand.

---

## README update rule

After building or updating the prototype, update `README.md` with:

- prototype purpose
- source reference used
- Spek export used, if available
- supported screen width
- supported responsive widths
- main interactions
- how to preview with Live Server
- how to deploy to Vercel, if relevant
- known visual mismatches or assumptions
- asset issues found
- reusable patterns created, if any

Keep README short and useful for design review.

---

## Visual QA with Spek

After implementation, compare the prototype against:

1. Spek spec
2. Figma preview or screenshot
3. User-stated requirements
4. Supported mobile widths

Before finishing, provide a short Visual QA Report.

Use this format:

### Matched

- What is close to Spek/reference.

### Mismatches

Group by:

- Layout
- Responsive behavior
- Spacing
- Typography
- Color
- Asset rendering
- Component pattern
- Interaction

### Responsive QA

Report checks at:

- 320px
- 360px
- 375px
- 390px
- 414px
- 430px

For each width, mention only important issues.

### Likely causes

Mention whether the mismatch likely comes from:

- Spek spec ambiguity
- missing asset
- bad asset export
- browser rendering difference
- implementation approximation
- responsive conversion from fixed 375px design

### Safe fixes applied

- List what was fixed.

### Remaining issues

- List what needs better asset export, Figma clarification, Spek re-export, or designer decision.

---

## Acceptance criteria

Before finishing, verify:

- `index.html` opens directly
- main flow is clickable
- layout matches the source at 375px width
- layout works at 320px, 360px, 375px, 390px, 414px, and 430px widths
- no unintended blank side gutters on wider mobile devices
- main content uses full available mobile viewport width
- cards, banners, and sections expand fluidly within the supported device width
- icons and small controls keep stable fixed sizes
- images preserve aspect ratio across all supported widths
- long pages scroll vertically
- desktop phone frame works
- mobile full viewport works
- no horizontal scroll
- no real API/auth/storage is used
- README explains how to preview and deploy
- assets preserve aspect ratio
- Spek assets are used when relevant
- visual mismatches are reported
- responsive mismatches are reported
- bootstrap components are minimal and not over-engineered

---

## Prompt behavior expectations

When the user asks to build a prototype:

1. Read `PROTOTYPE_RULES.md`.
2. Check whether `spek-export/` exists.
3. If Spek exists, inspect Spek before implementation.
4. Use Spek as the primary design spec.
5. Build static HTML/CSS/vanilla JS.
6. Preserve visual accuracy at 375px.
7. Make the layout responsive from 320px to 430px.
8. Use exported assets when available.
9. Avoid React/npm/TSX unless explicitly requested.
10. Provide a Visual QA Report before finishing.

When the user asks for small UI fixes:

1. Do not rebuild the whole page.
2. Only fix the requested areas.
3. Preserve existing interactions.
4. Preserve 375px visual accuracy.
5. Re-check responsive behavior if layout width, cards, banners, or sections changed.

When the user asks for responsive fixes:

1. Audit fixed widths.
2. Convert large containers to fluid widths.
3. Preserve small control sizes.
4. Remove unintended side gutters.
5. Check 320px, 360px, 375px, 390px, 414px, 430px.
6. Do not change unrelated visual details.