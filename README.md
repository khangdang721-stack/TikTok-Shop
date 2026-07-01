# ZLP Design Prototype

Lightweight static HTML/CSS prototype workspace for ZLP design review and mobile flow iteration.

Current prototype: **2 landing concepts in one phone-frame prototype**.

## Source Reference

- `PROTOTYPE_RULES.md` was used as the setup source of truth.
- Visual references: `Ref/Landing concept 1.png` and `Ref/Landing concept 2.png`.
- Source assets: `Assets/[new] Nav bar.png`, `Assets/Banner.png`, Coincard layer assets, Section Nhận hoàn xu layer assets, and `Assets/Body.png`.
- No Spek export is currently included.

## Preview

Open with VS Code Live Server:

1. Open this folder in VS Code.
2. Right-click `index.html`.
3. Select **Open with Live Server**.

You can also preview with a simple static server:

```bash
python3 -m http.server 5500
```

Then open `http://localhost:5500`.

Inside the prototype:

- Use the floating `Concept 1` / `Concept 2` switcher to move between concepts.
- `Concept 1` tracks claimed xu into `Xu đã hoàn`.
- `Concept 2` tracks claimed xu into `Xu chờ nhận`.

## Responsive Behavior

- Desktop browser widths show a centered 375px phone-like frame.
- Mobile and device emulation use the full viewport width.
- Supported mobile widths: 320px, 360px, 375px, 390px, 414px, and 430px.
- The prototype is set up to avoid horizontal scrolling.

## Reusable Patterns

Minimal starter CSS patterns were created for:

- phone frame
- screen container
- card
- button
- fixed nav
- image-based landing sections

No full design system, framework, build tool, npm setup, or external library was added.

## Main Interactions

- The nav is fixed at the top and overlays the banner.
- The prototype now contains 2 tabs with independent interaction state.
- Clicking any available `Nhận xu` CTA hides that reward row for that concept and updates its relevant xu summary.
- `Concept 1`: only the first reward row is claimable in v1 and its xu amount updates `Xu đã hoàn`.
- `Concept 2`: all 3 reward rows remain claimable and their xu amounts update `Xu chờ nhận`.
- The first successful claim in each concept switches milestone `1-locked` to `1-done`.
- In `Concept 2`, after all 3 reward cards are claimed, milestone `3-locked` switches to `3-done` and the reward section swaps to `Assets/Group - card -done.png`.
- Number changes in `Xu chờ nhận` and `Xu đã hoàn` use the `animate-text` `top-down-letters` pattern with a per-character downward swap.
- Clicking the Coincard `History` icon opens a full-screen `Lịch sử hoàn xu` screen that is fed by real claim interactions from the active concept.
- New history entries created from landing claims appear in `Chờ hoàn` with a random `Nhận sau x ngày` label from 1 to 10.
- The claim interaction is one-time per page load and resets on refresh.

## Assumptions

- Assets are used directly from the existing `Assets/` folder.
- The reference image is 1125px wide, treated as a 3x export for a 375px mobile baseline.
- Coincard and Section Nhận hoàn xu are assembled from the requested source layers instead of using only the full composite PNGs.
- The reward list is rebuilt as HTML/CSS so all 3 claim buttons can be interactive while still using the provided `Buttons.png` asset.
- `Xu chờ nhận` is rebuilt as a small HTML block so the pending xu total can update dynamically in `Concept 2`.
- The history screen follows the `History 1a` layout direction, but only `Chờ hoàn` entries are mapped in v1; `Đã hoàn` and `Thu hồi` use empty states.
- `Concept 1` keeps two static countdown rows (`Còn 2 ngày`, `Còn 10 ngày`) and does not auto-switch them in this v1.
- Future screens should continue using static HTML, CSS, and small vanilla JavaScript only when interaction is needed.
