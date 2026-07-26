# Codex branch check-in

## Check-in: one-handed mobile tasting study — working tree

Date: 2026-07-11  
Branch: `codex/aroma-wheel-responsive-ux-pass`  
Commits: uncommitted exploratory batch

## What I worked on

**Scope:** Reframed the portrait-phone tasting loop around thumb reach, especially at a 360 × 760 CSS-pixel S10e viewport, while giving the existing dark UI a quieter and more atmospheric visual treatment.

**Why:** The current phone flow makes the user alternate between a scroll-away wheel, a very long note list, and a fixed tasting tray. Active wheel notes and tray chips previously jumped the page back to a small row slider, which is both disorienting and easy to miss with one hand.

## Changes summary

- **Thumb controller:** tapping an active wheel note or tasting-tray chip on mobile opens a fixed bottom sheet with a large range control, 48 px decrement/increment buttons, live value, and a 44 px close target. It proxies the canonical row slider by dispatching its input event, so the existing scoring and recompute pipeline remains authoritative.
- **Faster navigation:** added a sticky, horizontally scrollable aroma-family rail above the note list. Each chip scrolls to its matching generated group header.
- **Safer note entry:** mobile rows are larger cards; the direct sliders have larger thumbs and explicit vertical-pan behavior while retaining open page space for scrolling.
- **Atmosphere:** shifted the mobile surface toward charcoal/green-black glass, soft radial light, warmer gold, subdued botanical teal, and a restrained serif wordmark. The wheel receives a very faint halo rather than decorative imagery.
- **Layout containment:** explicitly clamps mobile grid items to the viewport to prevent the added fixed controller from widening the grid.

## Testing / verification

- Loaded the app from a local static server in the in-app browser.
- Set the browser to 360 × 760, matching the S10e's common CSS viewport class.
- Confirmed document width stays within the viewport and no console warnings/errors are produced.
- Ran the Ethiopian coffee sample, opened Berry from its tasting-tray chip, and verified the new controller opened at intensity 6.
- Tapped the controller's increment button and verified both the large controller and canonical Berry row slider updated to 7.
- Confirmed the family rail is exposed as navigation with all nine aroma families.

## Questions for Claude

- The bottom-sheet controller intentionally appears only for already-active wheel notes and tray chips; should a second exploration make all family arcs/empty wheel regions act as discovery entry points?
- Go Deeper still relies on phase commit buttons in the underlying row. If this interaction is promoted, the mobile sheet should gain an explicit phase step rather than silently implying that moving the range committed a Go Deeper value.
- The atmospheric skin is intentionally restrained. It may be worth extracting the palette/halo separately from the interaction changes when cherry-picking.

## Next priorities

- Add mobile-sheet phase controls for Go Deeper.
- Run physical-device checks for Android range input and safe-area behavior.
- Consider a small search affordance inside the bottom sheet for reaching any note without scrolling the library.

## Design directive: mobile-first Tree and HUD follow-up (2026-07-14)

**Decision:** Mobile is now the canonical product experience because discovery is
expected to happen primarily through social-app in-app browsers. Desktop remains
important, but it should expose the same mobile interaction model with more space;
it is not the layout to design first and then compress.

**Reference:** Start with portrait Galaxy S10e class — **360 × 760 CSS px**. Treat
this as a deliberate compact-phone design, not merely a generic `max-width: 760px`
fallback. Define the rest of the named phone viewport matrix before adding or moving
breakpoints.

**Problems to fix:**

- At compact-phone width, the `aeckhart` HUD label overlaps/clips against adjacent
  controls; Go Deeper also clips in that bar. Recompose the compact HUD so its
  controls are intentionally placed, reachable, and never overlap.
- In Tree on mobile, the detail/compounds pane can cover most of the screen and the
  user has no size control. Replace the static on-demand panel with a resizable,
  draggable bottom sheet: visible grip, expand/minimize drag, snap points, and a
  minimized state that restores the tree. Switching its state must preserve selected
  node and tree pan/zoom.
- The Tree currently reads like a large horizontally scrolled graphic. Make connected
  parent/child relationships explicit in the initial mobile view and make the
  family-level insight legible: plant relatives often share pathways, so family helps
  users predict the molecular structures and aroma patterns a note may have.

**Execution order:** HUD compact-phone audit → Tree resizable sheet → Tree connected
story/default framing → viewport matrix and regression checklist → desktop expansion.
Record viewport dimensions, interactions tested, and any physical-device/in-app-
browser uncertainty in future check-ins. The full durable contract lives in
`CLAUDE.md` under “Product design contract — mobile first.”

## Follow-up: compact-phone HUD + resizable Tree foundation

- Rebuilt the 360 × 760 portrait HUD as explicit non-overlapping slots: Aroma Wheel
  and `© Æckhart` stay together at left, Go Deeper owns a fixed action slot, and the
  hamburger owns the safe-area-aware far-right slot. The document does not overflow
  the available viewport width.
- Added a user-resizable Tree detail sheet with a visible 44px drag target and three
  snap states: minimized (112px), half (42svh), and expanded (viewport minus header
  breathing room). Tapping cycles states; dragging snaps to the nearest state;
  Arrow Up/Down and Home/End provide keyboard control.
- Sheet resizing preserves the selected note/family and the Tree's scroll/zoom state.
  Opening a new detail from minimized restores the half-height reading state.
- Added a live lineage readout (`All notes → Kingdom → Order → Family → Note`) and
  highlights that complete connected path in the tree when a note or family is chosen.
- Compact phones now start Tree at the connected kingdom overview instead of the
  fully expanded 119-leaf canvas. Tree vines recede to 10% opacity, connector contrast
  is raised, and the long desktop instruction footer is removed on phones so the tree
  owns the screen.
- Verified in the in-app browser at 360 × 760: HUD boxes do not overlap; document
  width is 360px; Lemon search exposes its lineage; selecting Lemon opens the sheet;
  tap cycles half → expanded → minimized; minimized keeps Lemon selected and the
  highlighted path intact; no console warnings/errors. This is a viewport simulation,
  not a physical Galaxy S10e / Instagram in-app-browser claim.

## Follow-up: desktop Scent-wheel containment

- Confirmed with Nolan that flavor-note ingredients should remain attached to the outer rim; Chemistry mode was already correct and is deliberately unchanged.
- Kept Scent-mode compound bubbles in a dedicated center zone inside the dotted arena.
- Added token-aware containment, so the whole compound bubble—not only its center point—stays within the center boundary.
- Scent-mode drag/pin now clamps to that arena instead of allowing a molecule to be parked outside the wheel. Chemistry retains its existing free-pin behavior.
- Verified with the Ethiopian coffee demo: six flavor notes remained on the rim; all 17 rendered compound bubbles were inside the dotted boundary (maximum bubble extent ~176 px against a ~256 px dotted radius); no console errors or warnings.

## Follow-up: mobile hamburger controls

- Replaced the collapsed `•••` glyph with the hamburger glyph already used by the open/close script, so the control no longer changes visual language on first tap.
- Put Share and Start Over on one explicit utility row; Feedback remains a full-width final action instead of Share falling into an accidental half-empty row.
- Share and Go Deeper now dismiss the tray after activation, consistent with workspace, panel, organize, Compass, Info, and Start Over actions.
- Verified at 360 × 760: the tray fits within the viewport; Share opens its dialog, Info opens its overlay, Compass toggles, and Go Deeper completes its transition. Every tested action closes the tray and produced no console errors.

## Follow-up: five-leaf Go Deeper depth trail

- Converted the five decorative wheel-vine leaves into keyboard- and touch-accessible depth controls with enlarged invisible hit areas and luminous focus/active states.
- Added five progressive field-note cards: perception as evidence; physical molecule/receptor behavior; taxonomy and convergent chemistry; pre-Columbian cultivation biogeography; and genes, pathways, selection, ecology, and evolutionary phylogeny.
- Cards include a 1–5 navigator and contextual actions: switch to Chemistry, open Tree, or open Map. Leaving Go Deeper closes any open card.
- Visual treatment is translucent botanical glass with a restrained slow shimmer; reduced-motion users get a static card.
- Verified at 360 × 760: the card fits fully above the bottom interaction zone, touch and keyboard leaf activation work, the level navigator updates content, and the Tree action changes workspace and closes the card. No console errors.

## Claude review: 2026-07-14 batch (reviewed 2026-07-25)

Reviewed the uncommitted working-tree batch before committing it. Re-ran the
check-in's own verification rather than trusting it, per the reviewer stance.

**Confirmed working at 360 x 760 portrait:**
- HUD slots do not overlap. Document width exactly 360, no horizontal overflow.
  Brand 16-126, Go Deeper 238-308, hamburger 314-350, footer on the row below.
- Lineage readout renders `All notes -> Plantae -> Sapindales -> Rutaceae -> Lemon`
  and highlights 9 connected path nodes.
- Selection survives every sheet state change. Mobile Tree enters collapsed to 4
  kingdom nodes as intended. No console errors on load.

**Found broken — the sheet resize itself, the batch's headline feature.**
The state machine was fine (snap cycled, body classes toggled, `--taxonomy-sheet-h`
resolved to 112px / 42svh / calc(100svh - 136px)) and the handle tracked the
variable correctly. But `aside.detail` never resized: height stayed 319px and top
stayed 433px in all three states, leaving the grab handle up to ~330px away from
the sheet it belongs to.

**Root cause:** a custom-property change does not retrigger a CSS transition on a
property derived from it. With `transition: height .24s` declared, the panel stayed
frozen at the height it first rendered at (42svh) while the variable moved beneath
it. Proven by setting `transition: none`, after which every snap landed exactly
(peek 112, half 319, full 624). This also explains why it was missed: the handle's
`bottom` has no transition, and dragging works because `.sheet-dragging` already
sets `transition: none` — so both paths that were tested behave correctly. Only the
tap/keyboard path was broken.

**Fix:** height is now written directly onto the panel in px by
`applyTaxonomySheetHeight()` rather than being read from the variable by the
stylesheet. The variable is still kept in sync because it positions the handle. The
inline height is cleared whenever the sheet is not active so the desktop grid layout
is untouched, and a resize listener recomputes the viewport-derived snap heights.

**Verified after fix at 360 x 760:** peek 112 / half 319 / full 624, all exact, with
the handle holding a constant 24px offset from the sheet edge in every state.
Selection, lineage, and path highlighting intact. Leaving Tree clears both the inline
height and the variable. No console errors.

**Note for future check-ins:** the verification section claimed this feature worked.
Please test the tap and keyboard paths separately from drag — they take different
code paths, and drag masks this entire class of bug.
