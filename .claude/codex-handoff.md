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

## Follow-up: three-ingredient geography lens pilot (2026-07-26)

- Added mutually exclusive `Origin`, `Grown now`, and `Traditions` lenses to the
  existing world map. Only one mark system renders at a time so present production
  and cultural documentation cannot be mistaken for botanical origin.
- Limited the pilot to Coffee, Cacao / Chocolate, and Vanilla. The ingredient picker
  appears only in the two new lenses; the original search, family filters, marker
  selection, and pre-Columbian framing return unchanged in `Origin`.
- `Grown now` shows the five leading 2024 raw-crop producers for each pilot
  ingredient. Circle area is proportional to tonnes within the selected ingredient.
  Values and observation flags come from the FAOSTAT normalized bulk release dated
  31 December 2025; the legend states coverage of the world total and decodes flags.
- `Traditions` uses seven sourced attestations from UNESCO, Mexican government, and
  EU geographical-indication pages. The interface explicitly describes them as
  examples rather than a ranking, heatmap, or complete cultural inventory.
- New source records remain marked `UNVERIFIED_REFS`, consistent with the app's
  policy: agent-opened primary sources stay under human review until Nolan verifies
  them. Detail panels link directly to each source.
- At 360 x 760, production/tradition labels remain hidden until a marker is selected,
  avoiding collisions while retaining tap and keyboard access. At 1280 x 800, all
  labels remain visible. The map has no horizontal overflow at either viewport.
- Verified all three production datasets (15 markers), all three tradition datasets
  (7 markers), production and tradition detail panels, source badges, lens switching,
  ingredient switching, and restoration of the original Vanilla search (`1 match`).
  Browser console reported no warnings or errors.

### Displacement-distance follow-up

- `Grown now` now retains one contextual origin anchor and draws a restrained
  great-circle route from it to each of the five production markers. Routes wrap
  correctly at the dateline rather than crossing the long way through the map.
- Country labels, accessible marker names, and detail panels report the rounded
  anchor-to-anchor distance in kilometers. Selecting a marker emphasizes only its
  route; the detail guardrail says explicitly that this is an approximate geometric
  distance, not a reconstructed trade or crop-dispersal path.
- Production details now cite both the FAOSTAT record and the ingredient's existing
  human-verified origin source. The legend names the active origin region so the
  comparison baseline remains legible without switching lenses.
- Verified Coffee, Cacao, and Vanilla route sets at 360 x 760 and 1280 x 800,
  including the Pacific/dateline paths for Vanilla and Cacao. No horizontal overflow
  or browser console warnings/errors.

## Follow-up: family wheel blooms + directional map compass (2026-07-26)

- The large Tree remains the Kingdom → Order → Family overview. Selecting a family
  now replaces only the final leaf fan-out with a circular family wheel bloom, so the
  transition happens exactly where the large branching explanation stops being useful.
- Each bloom keeps the family at its center and arranges its supported notes around a
  dotted ring with group-colored dots and the wheel's existing note icons. Notes are
  keyboard-focusable and open the existing detail view without leaving the bloom.
- Added an explicit `← Full tree` return action. Returning clears all bloom SVG
  elements before restoring the hierarchy, preventing the two layouts from layering.
- At the compact-phone reference viewport (360 × 760), the bloom sizes to 325 × 325,
  has no horizontal document overflow, keeps every label inside the viewport, and
  automatically minimizes the existing Tree detail sheet to its peek state.
- Added a draggable and keyboard-movable compass to the Map's `Origin` lens. The
  compass converts its on-map position to a geographic anchor and plots up to eight
  active tasting-note origins by initial bearing and great-circle distance. Its
  caption and accessible label update as it moves; `Grown now` and `Traditions`
  intentionally hide it so the lenses remain mutually exclusive.
- Verified the bloom at 1280 × 800 and 360 × 760, including family → note selection,
  responsive sizing, peek-sheet behavior, and returning to the full tree. Verified
  the compass at 360 × 760 with the Ethiopian coffee sample, including Arrow-key
  repositioning and the resulting direction/anchor updates. Browser console reported
  no warnings or errors. These are browser viewport simulations, not physical-device
  or social in-app-browser claims.

### Coordination boundary

- Claude is concurrently handling the workspace view changer and a separate Go Deeper
  prompt-provenance archive. This batch does not alter either feature. The untracked
  `.claude/session-handoff-thesis-systems.md` file was left untouched.

## Follow-up: named lineage rings inside family discs (2026-07-27)

- Promoted two growth rings from decoration into taxonomy: the upper ring is labeled
  with the selected family's Order and the lower ring with its Kingdom. Family remains
  the center/heartwood and supported notes remain leaves on the living edge.
- The ring names are computed from the selected family node's real ancestors rather
  than duplicated taxonomy strings. The disc now carries its complete
  Kingdom → Order → Family lineage without requiring the breadcrumb above it.
- Reduced decorative-ring density around the named bands so the semantic ranks lead
  the composition. Compact discs receive thinner bands, smaller center typography,
  tighter leaf-label spacing, and a larger usable ring span.
- Added a concise accessible name to the disc that announces common family name,
  scientific family, Order, Kingdom, and note count. Existing keyboard-selectable
  note leaves remain unchanged.
- Verified Rutaceae at 1280 × 720 and Rutaceae/Rosaceae at 360 × 760. The compact
  Rosaceae disc (10 leaves) had no SVG or viewport overflow; Enter selected Strawberry
  while preserving both named rings and updating the existing detail pane. Returning
  to `← Full tree` removed the lineage SVG and its compact/accessibility state.
- Browser console reported no warnings or errors. These are simulated browser
  viewports, not physical-device or social in-app-browser claims.

### Coordination boundary

- Claude added separate uncommitted Map compass-centering work to `index.html` during
  this pass. It is intentionally excluded from this check-in; only the lineage-ring
  hunks and this handoff entry belong to Codex.

## Follow-up: clickable taxonomy rings + stationary Tree border vines (2026-07-27)

- Turned the family disc's named Order and Kingdom rings into keyboard- and
  pointer-accessible navigation. Family remains the center; selecting either
  ancestor now zooms the same circular visualization outward to that real rank.
- Added generated Order and Kingdom discs. Order shows its Family wedges and flavor
  notes around the living edge; Kingdom shows Order wedges, Family wedges, and all
  supported flavor-note endpoints. Any Family wedge returns to its family bloom, and
  any note endpoint opens the existing note detail.
- The hierarchy is generated from the existing taxonomy tree, including collapsed
  descendants. It does not invent intermediate clades that are absent from the
  dataset, and it excludes the explicitly non-taxonomic `(multiple families)` bucket
  from the biological Kingdom disc.
- Repaired the decorative Tree vines at the source of the reported overlap: the
  app-wide `svg { width:100%; height:100% }` rule was stretching each vine across the
  workspace. Explicit capped heights and automatic widths now keep them as stationary
  left/right border rails; the compact layout makes them smaller and fainter.
- Verified the complete Family → Order → Kingdom → Order → Family loop with pointer
  input and verified ancestor navigation with Enter. At 360 × 760, all three discs
  fit the Tree viewport, the detail sheet remains at its peek state, and the vines
  stay outside the central wheel. Also inspected Family, Order, and Kingdom at the
  normal 1280 × 720 browser viewport. These are browser simulations, not a
  physical-device or social in-app-browser claim.

### Coordination boundary

- This pass changes only Tree rendering/state and its decorative vines. Claude's Map
  work and the untracked `.claude/session-handoff-thesis-systems.md` file remain
  untouched.

## Follow-up: honest ring hit areas + flowering fiddlehead vines (2026-07-27)

- Reproduced the reported hover-without-navigation failure. The accessible SVG
  `g[role=button]` exposed a rectangular bounding box even though the visible control
  was circular, so an apparent click could land in empty center space owned by a
  different SVG sibling.
- Added an explicit transparent annular hit stroke to every named lineage ring and
  removed pointer capture from its decorative label/band. Pointer geometry now
  matches the highlighted ring; keyboard Enter/Space behavior remains unchanged.
- Replaced both Tree vines' delayed yellow endpoint dots with directional blooms.
  Each stem now grows through paired lavender florets and resolves into a curled
  fiddlehead fern tip. The lower-left bloom grows upward; the upper-right bloom hangs
  downward, preserving the side-border composition.
- Verified direct mouse clicks on the Family-disc Order ring and the Order-disc
  Kingdom ring at 1280 × 720, plus the Family-disc Order ring at 360 × 760. Each
  immediately rendered the requested taxonomy level. The resized vines remained
  outside the central disc at both viewports.

### Coordination boundary

- This follow-up remains Tree-only. It does not alter Claude's Map work or the
  untracked `.claude/session-handoff-thesis-systems.md` file.

## Follow-up: note-centered zoom + one stable upward path (2026-07-27)

- Changed family-leaf and rank-edge note activation from an aside-only update into
  an explicit radial zoom. Clicking a flavor note now replaces the current disc with
  a note-centered view carrying its real Family, Order, and Kingdom as named rings;
  the existing note detail still updates in parallel.
- Recast the single toolbar return control as consistent "up one level" navigation.
  Its position does not move and its label follows the current scope:
  `← Family` → `← Order` → `← Kingdom` → `← Full tree`.
- The same path works with pointer and keyboard activation. Named lineage rings
  remain available as direct shortcuts, but the toolbar now supplies one predictable
  route instead of making users infer different return positions.
- On compact phones, entering a note or family focus now leaves the detail sheet at
  its peek state. The selected-note detail remains available by dragging the sheet
  upward, while the wheel and all named rings stay unobstructed.
- Verified Lemon leaf → note focus → Family → Order → Kingdom → full dendrogram at
  1280 × 720. Verified Lemon leaf → note focus → Family at 360 × 760, including the
  stationary toolbar position and peek-sheet behavior.

### Coordination boundary

- This pass remains scoped to Tree visualization/navigation. The concurrent
  `CLAUDE.md` modification and untracked
  `.claude/session-handoff-thesis-systems.md` file were left untouched.

## Follow-up: circles become the Tree default; branches become optional (2026-07-27)

- Added a top-level circular taxonomy overview and made it the Tree workspace's
  initial state. Its center represents all 119 notes; four wedges honestly separate
  Plantae, Fungi, Animalia, and the non-biological Process bucket.
- Biological Kingdom wedges drill into the existing circular Kingdom → Order →
  Family → Note path. Returning from a Kingdom now uses `← Overview` and lands on
  the circular overview rather than unexpectedly opening the dendrogram.
- Added one stable `View branches` control. It toggles to `View circles` in the
  optional dendrogram, while `Expand all` and `Collapse to kingdoms` appear only in
  that branch view.
- Opening a Family from the optional dendrogram returns to the primary circular
  interaction automatically. Updated the Tree's explanatory copy to describe circles
  as the main path and branches as an optional organization diagram.
- Verified default circle → Plantae → Overview, circle → branches → circle, and
  branch-only control visibility at 1280 × 720. Verified the centered circular
  overview and branch toggle at 360 × 760.

### Coordination boundary

- This pass remains Tree-only. The concurrent `CLAUDE.md` modification and untracked
  `.claude/session-handoff-thesis-systems.md` file were not staged or changed.

## Follow-up: illustrated Kingdom buttons + coverage-led expansion (2026-07-27)

- Replaced the circular overview's tiny rotated labels with large upright category
  marks: sprout/Plantae, mushroom/Fungi, bee/Animalia, and alembic/Process. Each also
  shows its supported-note count; biological categories state that they open Orders.
- Biological category activation now visibly expands into the next represented ranks:
  an Order ring followed by the Families actually present in the tool.
- Orders and Families are sorted by descendant-note coverage so the categories that
  collect the most supported notes lead each Kingdom. Plantae therefore begins with
  Sapindales (14), Poales (10), and Rosales (10).
- Fixed a pre-existing honesty/count gap exposed by testing all Kingdom buttons:
  Mushroom belongs to Fungi but currently has no Order or Family fields. It now
  remains visible as an unplaced Kingdom-edge note instead of disappearing when the
  Fungi overview changed from 2 notes to its placed subset of 1.
- Verified the enlarged category marks and Plantae drill-down at 360 × 760. Verified
  Fungi exposes Saccharomycetales → Saccharomycetaceae plus Mushroom, and Animalia
  exposes Hymenoptera → Apidae → Honey.

### Coordination boundary

- This pass remains Tree-only. The concurrent `CLAUDE.md` modification and untracked
  `.claude/session-handoff-thesis-systems.md` file remain untouched.

## Follow-up: collapsed regional map glyphs (2026-07-29)

- Replaced the always-open colored boxes used for crowded map regions with one
  count-bearing circular glyph per region cluster. The resting map no longer
  presents a block of names whose ownership is unclear.
- Clicking or keyboard-activating the regional circle expands just that cluster.
  After direct screenshot feedback rejected even an unboxed stacked word list,
  the expanded state became a radial spider bloom: every member is its own
  colored circular satellite with an ingredient icon, its name immediately
  outside the circle, and one short hub-to-satellite spoke. There is no rectangle,
  shared label anchor, stacked word object, or crossed leader geometry. Activating
  the center circle again collapses it.
- The cluster glyph reports its member-note count, accessible expanded state, and
  full member list. Active-tasting dimming, search-hit behavior, map filtering,
  selection restoration, and sibling-origin jumps all understand collapsed
  clusters. Selecting a hidden member programmatically expands its cluster first.
- Added the new cluster glyph to the map pan-handler exclusion boundary. This is
  required because pointer capture on the map canvas otherwise retargets and
  swallows the cluster click—the same failure mode previously fixed for ordinary
  origin markers and taxonomy controls.
- Mobile keeps ordinary labels quiet but explicitly reveals every satellite label
  inside an expanded cluster. Clusters above eight members use a staggered second
  orbit. Circle size, count, summary, satellites, icons, labels, and spoke endpoints
  are recomputed with zoom so the interaction remains legible rather than scaling
  into tiny map geometry.
- Static verification: the single inline script compiles and `git diff --check`
  passes. The in-app browser control surface rejected DOM inspection of the open
  `file://` URL under its URL policy, so no visual/browser interaction result is
  claimed; the human will verify after refreshing their local tab.

### Coordination boundary

- This pass changes the origin-marker presentation only. It does not alter origin
  data, production/tradition lenses, or the wheel and taxonomy views. The concurrent
  `CLAUDE.md` modification and untracked
  `.claude/session-handoff-thesis-systems.md` file remain untouched.

## Follow-up: map-local clear tasting action (2026-07-29)

- Added a dedicated `Clear tasting · N` button beside `Only notes in my tasting`
  in the Origin legend. It reports the number of distinct entered notes, disables
  itself when the tasting is empty, and has a count-aware accessible label.
- Clearing removes every committed phase of every note and resets their slider
  values through the existing `setNotes([])` bulk path. It also closes the open
  origin detail, clears the selected marker, and collapses any regional bloom
  while preserving map zoom, filters, and the selected geography lens.
- If `Only notes in my tasting` is active, clearing performs the necessary full
  marker rebuild so the filtered map becomes honestly empty instead of retaining
  stale markers.
- Renamed the nearby map-visibility link from `toggle all` to `toggle groups` so
  it no longer reads like a tasting-data action.
- Static verification: the inline script compiles and `git diff --check` passes.

## Follow-up: family recognition bridges become first-class notes (2026-07-29)

- Added all seven human-approved continuity notes: Lychee, Cardamom, Walnut,
  Bay leaf, Olive, Lilac, and Beet / beetroot. Each is a top-level wheel note
  with a real genus, Family, Order, icon, descriptor vocabulary, chemistry
  edges, full aroma-literature reference, and a Map origin marker.
- The additions turn six previously single-note Families into visible pairings:
  Maple ↔ Lychee (Sapindaceae), Ginger ↔ Cardamom (Zingiberaceae),
  Pecan ↔ Walnut (Juglandaceae), Cinnamon ↔ Bay leaf (Lauraceae),
  Jasmine ↔ Lilac ↔ Olive (Oleaceae), and Quinoa ↔ Beet (Amaranthaceae).
- Rewrote those six Family diagnostics around the familiar plant parts that make
  the relationship memorable: maple sap / lychee fruit, ginger rhizome /
  cardamom pod, cinnamon bark / bay leaf, flowers / olive fruit, quinoa seed /
  beet root, and the two husked nuts.
- Reused supported chemistry wherever the literature allowed. Added only two
  genuinely necessary compounds: α-terpinyl acetate for cardamom and bay leaf,
  and (2E,4E,6Z)-nona-2,4,6-trienal, which combines with sotolon to reconstruct
  walnut aroma.
- Added full references and citation mappings for Feng et al. (2018), Mishra et
  al. (2022), Miao & Weng (2009), Stübner & Steinhaus (2023), Zhou et al.
  (2019), Gecer (2022), and Freidig & Goldman (2014).
- Static integrity check: 127 unique Notes, 94 Compounds, and 262 Edges; no
  duplicate Note or Compound ids; no Edge points to a missing Note or Compound;
  the inline script compiles and `git diff --check` passes.

### Coordination boundary

- After the human confirmed Claude was inactive, this pass also supplied minimal,
  explicitly approximate origin markers for the new notes (and Gardenia) so the
  shared note records do not become dead ends in Map view. It does not change the
  separate three-note geography pilot, production data, or tradition lenses.
- The concurrent `CLAUDE.md` modification and untracked
  `.claude/session-handoff-thesis-systems.md` file remain untouched.

## Follow-up: Gardenia as the Coffee-family recognition bridge (2026-07-29)

- Added Gardenia as a first-class Floral note rather than an explanatory name that
  appears only in Rubiaceae copy. It is placed at
  Plantae → Gentianales → Rubiaceae alongside Coffee / roast, so the Family disc
  now demonstrates the relationship with two supported notes.
- Gardenia uses three compounds already present in the library and measured in
  fresh `Gardenia jasminoides` flower headspace: linalool, β-caryophyllene, and
  methyl salicylate. Added the full Cai et al. (2025) Scientific Reports reference
  and citation mapping; also added Gardenia to the note icon map and the
  “What am I smelling?” floral vocabulary.
- Rewrote the Rubiaceae diagnostic around the intended recognition bridge:
  gardenia makes the flowering family visible, while the coffee “bean” is the seed
  inside that family's red coffee cherry.
- Audited every Family with only one supported note against its diagnostic copy.
  The strongest analogous continuity candidates are Lychee ↔ Maple (Sapindaceae),
  Cardamom ↔ Ginger (Zingiberaceae), Walnut ↔ Pecan (Juglandaceae), Bay leaf ↔
  Cinnamon (Lauraceae), Olive or Lilac ↔ Jasmine (Oleaceae), and Beet ↔ Quinoa
  (Amaranthaceae). These are findings only, not silently added scope.
- Static integrity check: 120 unique note records; Gardenia has three resolved
  edges; no Edge points to a missing Note or Compound; `git diff --check` passes.

### Coordination boundary

- Gardenia work changes only the wheel/taxonomy data and this handoff. No Map origin
  record was added while Claude owns Map work. The concurrent `CLAUDE.md`
  modification and untracked `.claude/session-handoff-thesis-systems.md` remain
  untouched.

## Follow-up: all four overview wedges act; every radial label stays upright (2026-07-27)

- Removed the special non-interactive treatment from Process. All four overview
  wedges now share hover, focus, pointer, and keyboard behavior.
- Process opens a dedicated circular group containing all 13 non-organism notes.
  Selecting one opens a visible note-centered disc with an honest
  `GROUP · Process / non-organism` ring; `← Process` and `← Overview` preserve the
  same stable upward navigation used by biological ranks.
- Extended note focus to honestly unplaced biological notes. Mushroom can now open a
  Fungi-centered note disc without inventing an Order or Family; moving up returns
  to Fungi.
- Replaced rotated rim labels with screen-horizontal labels anchored around the
  circle. Applied the same treatment to internal Order/Family wedge labels, removing
  the upside-down Family names found in the Sapindales check.
- Verified a real coordinate mouse click on the Process wedge at 360 × 760, all 13
  Process note controls, Process → Smoky → Process, and the full Process circle with
  upright labels at 1280 × 720 and 360 × 760. Also verified Sapindales Family labels
  and its 14 note labels remain upright.

### Coordination boundary

- This pass remains Tree-only. The concurrent `CLAUDE.md` modification and untracked
  `.claude/session-handoff-thesis-systems.md` file were left untouched.

## Follow-up: pointer-capture fix for radial controls (2026-07-27)

- Reproduced the reported symptom from its cursor clue: Tree's empty-space
  drag-to-pan handler treated every newer radial control as empty space because it
  exempted only legacy `g.tx-node` branch nodes.
- On pointer-down it set pointer capture and the grabbing cursor; per pointer-event
  semantics that retargeted the eventual click to the scroll container. The wedge
  could flash its hover treatment but never receive activation.
- Expanded the panning exclusion boundary to all semantic SVG button groups plus
  native buttons, inputs, and links. Empty Tree space still starts drag-to-pan;
  interactive controls now retain their own complete pointer sequence.
- Verified with real coordinate mouse input at 1280 × 720: Process wedge → 13-note
  Process circle, Smoky rim control → focused Smoky disc, and Animalia wedge →
  Kingdom/Order/Family disc. These checks deliberately did not use synthetic
  `dispatchEvent` or role-button activation.

### Coordination boundary

- This pass changes only Tree pointer handling and its handoff record. The concurrent
  `CLAUDE.md` modification and untracked
  `.claude/session-handoff-thesis-systems.md` file remain untouched.

## Follow-up: species lineage hitboxes + functional-language threshold (2026-07-29)

- Individual biological note discs now carry three concentric lineage controls:
  Family and Kingdom are always directly clickable; Order is clickable only when
  the represented dataset contains more than one Family inside that Order.
- A one-Family Order remains named for context but is darkened and removed from the
  tab/click path. Moving up from its Family skips the redundant Order view and goes
  directly to Kingdom. The same rule is applied to the Family wreath's named Order
  ring and top Up control.
- The exact multi-Family Orders represented by the current notes are Sapindales
  (3 Families), plus Poales, Asparagales, Lamiales, Solanales, Myrtales, Fagales,
  Malpighiales, and Zingiberales (2 each). The other 20 represented Orders currently
  contain one Family and therefore use the inactive/skip behavior.
- Separated cross-lineage functional words from biological descent in the Plantae
  disc with a soft gray transition annulus labeled `FUNCTIONAL WORDS · NOT LINEAGE`.
  Berry, Green, and Anise now occupy that threshold instead of being mixed into the
  same living edge as taxonomically placed notes.
- A focused functional word gets its own gray fog boundary. Where the data provides
  concrete examples, the outer ring becomes clickable Family sectors rather than a
  false parent: Berry spans Rosaceae/Rosales, Ericaceae/Ericales,
  Grossulariaceae/Saxifragales, and Lythraceae/Myrtales. Its outer Kingdom ring
  returns directly to Plantae.
- Per the human's request, this final additive pass was not browser-tested; they
  are checking it in their own live tab. `git diff --check` passes.

### Coordination boundary

- This pass remains Tree-only. The concurrent `CLAUDE.md` modification and untracked
  `.claude/session-handoff-thesis-systems.md` file remain untouched.
