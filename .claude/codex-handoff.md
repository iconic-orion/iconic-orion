# Codex branch check-in

## Codex follow-up: Go Deeper Wheel-to-HUD morph + compound gravity (2026-08-05)

- Go Deeper's existing canopy-to-soil descent now hands off to the actual workspace
  navigation instead of simply making Map and Tree appear. After the soil overlay clears, a
  gold outline traces the live Wheel rim, holds for one readable beat, then contracts into a
  temporary visual copy of the real `Wheel / Map / Tree` HUD switch and crossfades to that
  interactive control.
- The morph uses the rendered Wheel radius and the HUD switch's live client rectangle, so it
  lands on the genuine target after desktop header wrapping. On phones it opens the HUD tray
  immediately before the contraction, waits two animation frames for the grid to settle, then
  targets the visible three-option switch. Escape ends the flourish at the usable menu.
- Reduced-motion mode skips both the descent and geometric morph: it opens the phone HUD if
  needed and gives the final workspace switch a static attention outline.
- Scent-mode compounds now obey a support-count gravity rule. One unique active note keeps a
  compound in an outer 72-88% parent-gravity band. At two active notes the compound crosses
  into shared Wheel space; further unique notes add inward momentum. Evidence strength still
  differentiates radius inside each band and continues to control token size/opacity.
- Support counting follows the current tasting, group visibility, and the comparison model's
  culinary-varietal inheritance. Each entered varietal remains a unique source even when it
  reaches a shared compound through its culinary parent. Chemistry organization is unchanged.
- Compound controls now report support count in their accessible label and expose a hover title
  naming either the source-note gravity relationship or every active note in the shared orbit.
  The expanded Wheel hint explains the same visual law in plain language.

### Verification

- Chrome localhost at 1440x1000: the post-warp highlight measured about 688x671 around the
  rendered Wheel and contracted onto the 219x29 desktop HUD switch. The settled state exposes
  Wheel, Map, and Tree, restores full target opacity, and leaves the temporary overlay hidden.
- Chrome localhost at 360x760: the 244px Wheel highlight targets the open HUD's 231x46 workspace
  switch at x=12/y=69. The HUD remains open on the real three-option menu after the crossfade;
  page overflow remains zero.
- Desktop Lemon at intensity 8 gives Limonene one source and a 108.8px outer home. Adding Orange
  changes Limonene to two named sources and a 43.43px shared-space home; the remaining one-source
  Linalool target stays at 117.01px. The rendered shared compound settles inside the single-source
  compound rather than merely changing metadata.
- At 360x760 the same threshold moves Limonene from a 41.23px one-source home to 16.46px with
  Lemon + Orange, while the one-source compound remains at least 44.34px out. Both states have
  zero horizontal overflow and the tooltip names `Lemon, Orange` as the shared support.

## Codex follow-up: Wheel-local controls + Go Deeper explorer reveal (2026-08-05)

- Moved `Organize · Scent / Chemistry` and the Radar toggle out of the
  global HUD and into a compact frosted toolbar inside `main.wheel`. Map and Tree hide
  that toolbar with the Wheel itself, so neither control lingers as an inert global setting.
- Renamed the Wheel aroma-profile tool to `Radar`, reserving `compass` exclusively for Map.
  Map's independent control now identifies itself in its title, SVG description, and live accessible
  label as the `Map bearing compass` / geographic tasting-note bearings.
- Phone placement accounts for the empty-state nudge, compound-label toggle, context hint,
  and saved-lap ribbon. An expanded lap ribbon temporarily hides the Wheel toolbar; a collapsed
  non-empty ribbon shifts the toolbar and its following helpers down together.
- Map and Tree now follow Go Deeper's progressive-disclosure hierarchy. Before Go Deeper,
  Wheel is the sole visible workspace choice; opening Go Deeper reveals Map and Tree. Entering
  either explorer enforces the deeper state, while collapsing Go Deeper from an explorer returns
  to Wheel before hiding those choices.
- Added a compass, hierarchical-tree, and sparkle glyph cluster directly beside the
  `Go Deeper` label. The glyphs are inline line-art rather than separate controls and remain
  visible beside the label at the compact-phone breakpoint.

### Verification

- Chrome localhost at 360x760: the Wheel toolbar is 329x52 inside the 345px content width;
  Scent/Chemistry and Radar fit without horizontal overflow. The
  empty-state nudge begins four pixels below it, and the active-state compound toggle/context
  hint occupy separate rows. The open mobile HUD contains neither moved control.
- At 360x760 the Go Deeper button is 124x44 with all three glyphs, does not intersect the
  110px brand or 44px menu target, and introduces zero page overflow. Go Deeper reveals all
  three workspace choices in a 231px-wide HUD group.
- Chrome localhost at 1440x1000: the Wheel toolbar is 389x41 at the visualization's upper-left;
  Radar opens beneath it with its own title. Map hides the Wheel and
  toolbar while retaining its large cardinal-direction bearing compass.
- Interaction check: initial workspace visibility is Wheel / hidden Map / hidden Tree; Go Deeper
  changes that to all three visible. Collapsing Go Deeper while Map is active returns to Wheel,
  clears Map/Tree mode, and restores Wheel as the sole visible workspace entry.

## Codex follow-up: comparison compound definitions in-place (2026-08-05)

- Every compound emitted by the two-note comparison now carries a plain-language sensory anchor
  from the compound library, including the shared-compound cards and both chart orientations.
- Compound names in the overlap chips and weighted graph are underlined, keyboard-accessible
  definition controls. Selecting one opens an evidence card inside the comparison pane instead
  of sending the user away to the separate Results panel.
- The in-place card reuses the Results detail model: common name / chemical class, sensory
  description, intensity and confidence scores, odor threshold with source, aroma-graph carrier
  notes, and the full contributing-note literature evidence list with formatted citations.
- Escape closes the evidence card before it closes or contracts the comparison itself. Expanded
  desktop uses a 760px, two-column evidence surface; phone uses one column constrained to the
  visible pane and retains internal scrolling.

### Verification

- Chrome localhost at 1440x1000: Lemon / Orange -> Linalool displayed 16 evidence rows, the
  expected floral-citrus sensory description, threshold source, and citations in a 760x848 card
  with no horizontal overflow.
- Chrome localhost at 360x760: the same Linalool card measured 327px client and scroll width,
  stayed within x=1..345 and y=68..748, and rendered all 16 evidence rows in one column.
- Compact comparison was also checked at 858px: sensory descriptions remain visible and the
  comparison panel has no horizontal overflow.

## Codex follow-up: comparison highlight precision (2026-08-05)

- Removed the broad wheel-group shortcut from comparison affinity. Sharing a navigation family
  such as `Fruity` no longer keeps two choices bright; a note must share a compound or a genuine
  culinary parent/varietal umbrella.
- Reproduced with Apple / pear and Bergamot: they have no shared compound and no shared culinary
  parent, but both previously stayed bright solely because both are Fruity. Bergamot now sorts
  into the dimmed/unrelated block.

### Verification

- Chrome localhost at 1440x1000: Apple has 24 bright choices, all with shared-compound reasons;
  Bergamot is unrelated and begins after the related block. Console warnings/errors were empty.
- Chrome localhost at 360x760: Bergamot remains dimmed/unrelated and the comparison panel has no
  horizontal overflow (327px scroll width and client width).

## Codex follow-up: Constellation aroma-overlap spectrum (2026-08-05)

- Constellation's default side panel is now a full 127-note bar graph ranked from the
  strongest graph-wide compound connectedness to notes with zero known overlap. Each note's
  connectedness is the sum of its weighted-Jaccard scores against every other note, normalized
  to the top note; varietals use the comparison tool's same inherited culinary-parent profile.
- Every bar reports how many other notes share at least one compound and names its strongest
  individual match with that pair's exact weighted-overlap percentage. Bar color retains the
  note's culinary aroma family. Notes active in the current tasting receive a bordered row.
- The seven current zero-overlap notes appear in an explicit final section with empty tracks:
  Arugula, Buttery, Carrot, Celery, Garlic, Skunky, and Taro. Copy frames zero as the current
  evidence graph's state rather than proof that the notes are chemically unique.
- Selecting any spectrum row now opens a complete overlap profile for that note: every matching
  note, ranked by weighted overlap, with an exact percentage and the full list of shared compound
  names. Each relationship row pivots selection to that note; `Overlap spectrum` returns to the
  full graph. The profile persists while changing Chemistry/Taxonomy/Geography/Embodied lenses.

### Verification

- Chrome localhost at 1440x1000: 127 bars render in a 317px side pane with no horizontal
  overflow; 120 are connected and seven isolated. The top bar is Red currant with 26 links.
  The graph header remains sticky while scrolling to the separated zero-overlap section.
- Red currant drill-down shows all 26 relationships. Berry ranks first at 98% through five named
  compounds; selecting it pivots the selected star and redraws Berry's full 26-note list. The
  relationship panel remains intact after switching to the Taxonomy lens.
- Chrome localhost at 360x760: the graph uses the existing 258px scrollable Constellation side
  region with all 127 rows, no horizontal overflow, and two readable leading rows beneath the
  sticky explanation. Drill-down also fits without sideways overflow. No browser console
  warnings or errors were observed at either viewport.

## Codex follow-up: mobile Branches + expanded comparison legibility (2026-08-05)

- Mobile and portrait navigation no longer redirects a Branches Kingdom click into the
  square Order directory. Plantae and Fungi now remain in the actual curved SVG tree; Orders
  grow their Family florets in place. `View circles` remains available only as an explicit
  alternate view.
- The full-window desktop comparison now defaults to a vertical compound contribution graph.
  Shared compounds and lower-confidence unmatched compounds occupy separately labelled groups;
  paired orange/blue columns display exact A/B evidence weights and use up to 430px of viewport
  height. A `Horizontal / Vertical` control switches chart orientation without losing the pair.
- Expanded desktop typography and hit areas are substantially larger across the note pickers,
  overlap summary, compound chips, chart labels, explanation, and all six cross-workspace cards.
  The compact HUD card keeps its dense footprint, and phone expansion continues to use the
  horizontal chart so narrow screens do not inherit the desktop column layout.

### Verification

- Chrome localhost at 360x760: Tree opens in Branches (`View circles` is the offered action).
  Plantae expands to 28 Order nodes with zero directory cards; Rosales then renders its real
  Rosaceae floret, 10 note petals, and 13 curved links while remaining in Branches.
- Chrome localhost at 1440x1000: expanded Coffee / Chocolate fills the 1440x932 area beneath
  the HUD. Eight vertical compound items render with 380px plotting height; result text is
  14px, chart labels 13px, and context cards 12.5px. Horizontal mode restores all eight
  mirrored rows.
- Expanded comparison at 360x760 begins at the 56px HUD and ends at the viewport bottom. It
  forces the horizontal graph, hides the desktop orientation switch, and has no horizontal
  panel or picker overflow. Browser console warnings/errors were empty at both viewports.

## Codex follow-up: culinary two-note aroma comparison (2026-08-05)

Added a persistent `A ⇄ B Compare notes` tool to the global header for exploring two
culinary notes from Wheel, Map, or Tree. The result deliberately distinguishes evidence
overlap from relationship: the Tree's orange/blue marks identify two observations without
drawing a causal branch, while each workspace adds only the context it can support.

- Both selectors use the complete note vocabulary, including culinary umbrellas, hidden
  varietals, and process descriptors; the feature is not limited to botanical Tree leaves.
- Shared compounds come from the existing evidence graph. A hidden `subOf` varietal inherits
  its culinary parent's base aroma profile, while its own direct compound edges override
  duplicate parent edges.
- The overlap percentage is a weighted Jaccard comparison: shared evidence uses the lower of
  the two note weights and the total uses the higher weight for each linked compound.
- Shared-compound chips display both evidence weights and open the existing compound detail,
  so users can inspect literature-linked contributing notes instead of treating the score as
  a causal claim.
- After either note is chosen, the other selector reorders itself: notes with a shared
  compound or culinary aroma-group relationship remain bright and sort first; choices with
  no known link move below them, render dimmer, and remain selectable for honest 0% checks.
- A mirrored contribution graph sits at the result's lower right on desktop and below the
  explanation on a phone. Shared compounds align first in bright A/B bars; unmatched edges
  sit beneath a divider at lower contrast. Bar length is explicitly labelled as this model's
  literature-linked evidence weight, not measured concentration.
- `Expand analysis` promotes the compact card into the only full-workspace takeover in the
  app: it covers every pixel beneath the persistent HUD, edge to edge, while preserving the
  active Wheel/Map/Tree state behind it. `Compact view`, Escape, or the HUD control restores
  the compact card without losing either selected note; the HUD can close either state.
- The expanded compound graph grows to 12px bars / 26px rows on desktop and adds exact A/B
  evidence weights beneath every compound name. Six cross-tool context cards appear below:
  Compounds, Culinary, Taxonomy, Origins & culture, Production / economy, and Climate. The
  active workspace's card is highlighted automatically when moving among Wheel, Tree, and Map.
- Quantitative dimensions keep separate scales. The production pilot adds mirrored bars for
  shared current top-five countries, normalized within each note's displayed five markers;
  its copy explicitly says tonnes are not price, value, or market importance. Climate and
  economic-value claims remain marked as awaiting sourced data rather than being inferred.
- Tree adds the most specific represented botanical link available (genus, family, then
  Order), or explicitly says none is represented. It never converts that context into a
  causal claim.
- Map adds the great-circle distance between the two represented historical-origin points
  and draws a dashed A-to-B arc with colored endpoints. For the three-note geography pilot,
  it also reports shared current top-five production countries and exact shared documented
  cultural markers when present.
- Tree-note clicks and search results fill the two slots while compare mode is active; swap
  and clear controls are included. Selecting a third Tree note rolls the pair forward.

### Verification

- Chrome localhost desktop: Berry / Cranberry renders a 5-shared/1-unmatched mirrored graph
  in a 340px right column with no panel overflow. Lemon / Orange reports 73% weighted overlap
  through Limonene and a represented Citrus/Rutaceae genus link in Tree.
- Expanded desktop Coffee / Chocolate: pane measured 1,987x1,235 beneath a 69px HUD and covered
  the complete remaining viewport. The graph grew to 744px in the initial bounded check and
  wider again after the edge-to-edge takeover; eight rows rendered at 26px, all six layer cards
  appeared, and Indonesia rendered as the shared production-bar dimension.
- Chrome localhost at 360x760: Berry / Cranberry reports 78%, five shared compounds, and the
  culinary parent/varietal context. The full global comparison and six-row contribution graph
  fit in a 377px panel with no internal overflow; Tree retains a separate 330px ceiling.
- Expanded 360x760 Coffee / Chocolate: the dedicated pane begins exactly at the 56px HUD and
  ends at the viewport bottom, with a 314px graph and six scroll-reachable context cards. The
  mobile HUD opened above the pane and closed the comparison successfully; no state or console
  errors were observed.
- Selector guidance checked with Lemon: 48 related choices sort first, followed by 79 dimmed
  no-known-link choices; both groups remain alphabetical and selectable.
- Map checked with Lemon / Orange: a dashed two-endpoint overlay and `2,473 km between
  represented origins` label render, matching the textual origin context. Coffee / Chocolate
  reports Indonesia as a shared present-day production marker and a 14,504 km origin distance.
- Buttery / Skunky reports 0% without claiming that no shared compounds can exist beyond the
  current evidence graph.
- A shared-compound chip was opened on mobile; beta-Damascenone displayed its existing detail
  and literature-linked contributing-note evidence in the bottom sheet.

## Codex follow-up: bounded, biologically scoped Tree viewport (2026-08-05)

Kept the Branches tree as the detailed, gently curving fan rather than replacing it with
a vertical overview schematic. On a 360px portrait screen the natural tree is about 859px
wide, so left/right exploration remains intentional; `Fit tree` is an optional one-tap
whole-tree overview, while `Whole tree` returns to the readable natural scale.

- Added content-aware pan guards. The viewport may travel across the real tree, but if a
  drag reaches an outer margin or an internal clearing with no rendered node/label visible,
  it catches on the nearest real branch point instead of allowing a long blank-screen trip.
- `Whole tree` now opens centered on the first rendered canopy content, rather than inheriting
  a stale corner scroll position or automatically forcing the tiny fit scale.
- The organism tree now contains only Plantae (109 notes) and Fungi (2) as ancestry branches.
  Process descriptors and the two cross-family umbrella notes stay available in the Wheel but
  are omitted from Tree; Honey remains a clickable, free-flying bee beside the trunk base rather
  than becoming a connected Animalia limb.
- Fungi begins below the shared trunk flare and its complete Order → Family → note lineage grows
  downward as the diagram's literal root system. Earth-toned tapered links distinguish those
  fungal roots while the shared base still keeps Fungi taxonomically separate from Plantae.
- Added an optional `Pollinators & dispersal` Visibility layer. Conservative family-level bee,
  butterfly/moth, fly, beetle, bird, bat, wind, and human-propagation icons sit directly inside
  the flower head without receiving branches; their titles describe the ecological association.
- Family florets now expose two distinct hit areas: the opaque family-name plate opens family
  detail, while the gold flower center toggles a compact pollinator/dispersal nameplate between
  the head and its first note petals. Clicking a second center moves the nameplate; clicking the
  same center again closes it.
- Berry now displays as `Berry*`. Expanding its varietals or opening its detail explains the
  culinary umbrella versus botanical classification, including the four represented families
  and the distinction among berries, a balausta, aggregate accessory fruit, and drupelets.

### Verification

- Chrome localhost at 360x760: natural SVG 859x4901, horizontal overflow 534px; 150 rendered
  note/family labels with zero measured overlap pairs. No Process or `(multiple families)` node.
- Chrome localhost at 1280x820: natural SVG 1299x3901; the same 150 labels with zero overlap pairs.
- `Fit tree` leaves zero horizontal or vertical overflow at both tested viewports; `Whole tree`
  restores the detailed pan/zoom view. Mobile base visually checked with Plantae centered,
  Honey's unconnected bee beside the trunk, and Fungi branching into a downward-growing root
  system below the flare.
- Chrome DOM check: exactly two Kingdom nodes (Plantae and Fungi), zero Animalia links, one
  free Honey bee control, five downward fungal root links, and 23 mapped family ecology marks.
- Pollinator-center interaction checked in Chrome at 1280x820 and 360x760. Rosaceae opens the
  254px desktop / 222px phone pill `🐝 honey + native bees · 🦋 butterflies / moths`; neither
  pill overlaps a rendered family/note label. Re-click closes it, clicking Solanaceae replaces
  it with `🐝 bees`, and the separate Rosaceae name-plate hitbox still opens family detail.

## Codex follow-up: family flower heads and label florets (2026-08-05)

Replaced the Branches view's nearly straight per-family note columns with one reusable
family-level floret layout. Large families now open into two outward-facing, brace-like
label wings; one-, two-, and three-note families use dedicated bud/fork/crown silhouettes.
The note dots stay small and serve only as stem endpoints—the labels themselves make the
flower shape.

Each family now has a central green-and-gold flower head at that convergence point, with
the family name on an opaque plate directly beneath it. The Order-to-Family branch reads as
the main stalk, while the note stems leave the head's upper rim and become the individual
label petals. The head, name, and petal arrangement move as one unit when collision packing
lengthens a stalk.

- A complete family is now the collision unit. If two family envelopes would overlap, the
  later family's whole floret grows a longer stem; individual labels are no longer nudged
  away from their family silhouette.
- The focused-Order view and All-notes view now share this same floret builder instead of
  switching to a separate five-across canopy algorithm.
- Focus centering uses the full rendered label envelope, not only note-dot coordinates, and
  re-runs when the viewport or mobile detail-sheet height changes.
- Compact-phone geometry uses shorter wings and 10px labels so the densest current family,
  Rosaceae (10 labels), fits within the 360px viewport without horizontal clipping.
- When a desktop zoom carries into the phone breakpoint, it is clamped back to 1 so the
  central family head and name plate remain visible above the minimized detail sheet.

### Verification

- Chrome localhost visual pass at 1280×820 and 360×760.
- Rosaceae: all 10 labels visible as petals around one family head, with the family name plate
  visible and zero bounding-box overlaps at both viewports.
- Fagales: Betulaceae's one-note Hazelnut reads as a single sprout; Juglandaceae's Pecan/Walnut
  pair reads as a forked bud; each has its own family head and name plate.
- All-notes view: 167 rendered note and family labels, zero measured bounding-box overlap pairs
  at both 1280×820 and 360×760.
- Mobile detail sheet tested minimized after resize; the focused floret re-centers when the
  sheet snap changes. Browser console reported no warnings or errors.
- Not claimed: physical-device or social in-app-browser verification.

## Claude follow-up: Constellation, Go Deeper's subjective hemisphere (2026-08-01)

Landed the feature discussed in-session with Nolan across several turns: Go Deeper is repositioning
from "deeper science" into, in his words, **"go deeper into my mind"** — a second hemisphere of the
app, opposite the objective, citation-backed Wheel/Tree/Map. Its flagship surface is Constellation: the
same tasting-note graph re-aligned four ways instead of re-measured.

- Added a sixth `DEPTH_STORIES` card ("Sixth lens · the maker's mind" / "Go deeper into my mind"),
  `actionType: "constellation"`, wired into the existing `#depth-card-action` dispatch alongside
  `chemistry`/`tree`/`map`.
- Built `#constellation-overlay`: a dedicated full-screen view (not a `#workspace-tabs` entry — that
  row is explicitly the three objective instruments, per its own title attribute), opened/closed via
  `openConstellation()`/`closeConstellation()` following the existing `openInfo()`/`openShare()`
  pattern, with its own Escape-key listener (matching this file's convention of one listener per
  overlay rather than a shared one).
- Four lenses, all computed live from the app's real `NOTES`/`COMPOUNDS`/`EDGES`/`NOTE_ORIGINS`/
  `GUIDE_MOUTH` (127 notes, 94 compounds, 262 edges, 93 origins as of this pass) — no curated sample,
  no hardcoded counts:
  - **Chemistry** — angle = weighted mean of shared-compound angle, radius = total edge weight.
    Compound-class sectors (alphabetical, enumerated from live data) double as the legend.
  - **Taxonomy** — reuses the app's own `taxonPath(note)` (did not reimplement kingdom/lineage
    logic) for a Kingdom → Order → Family → Note radial partition, dashed spokes wherever a note's
    real data skips a rank.
  - **Geography** — plain equirectangular projection of real `NOTE_ORIGINS` coordinates. Notes with
    no recorded origin (34 of 127) never get a guessed position.
  - **Embodied** — X (orthonasal/retronasal) only exists once a note is tagged *this session*
    (matches `PHASES` being a per-entry tag, not an intrinsic note property); Y (cooling/warming)
    reads the app's real `GUIDE_MOUTH` tags. Untagged notes don't get crammed into the canvas —
    see below.
  - **Compound story**: every compound's detail panel carries a live-computed verdict — "signature"
    (all carriers share one lineage) vs. "convergent" (carriers span multiple unrelated orders) —
    plus a **Trace on Taxonomy** action that dims everything except that compound's real carriers.
    At full scale this surfaces real, previously-undisplayed findings, e.g. Linalool: 9 unrelated
    orders, 11 families — which agrees with the compound's own pre-existing `specificity: "shared"`
    field, shown alongside as a cross-check.
- **Scale fix mid-build, not in the original sketch**: at the full 127-note graph, Embodied's
  "untagged" pool starts at all 127 notes and Geography's "no origin" pool is 34 — both would have
  overflowed a fixed in-canvas grid designed against a 28-note prototype sample. Replaced the SVG
  dot-grid tray with an HTML, keyboard-accessible, scrollable chip strip below the stage instead;
  clicking a chip does the same thing clicking its star would (tag it in Embodied, select it in
  Geography). Verified this renders and scrolls correctly with all 127 untagged chips present.
- **Real bug found and fixed during verification, not left for later**: the Trace-on-Taxonomy button
  called `cxSwitchLens()` with an argument in the wrong position, silently clearing the trace state
  it had just set — caption showed the plain Taxonomy caption instead of "Tracing Linalool — 9
  orders · 11 families," even though the dimming happened to look right via a different code path.
  Fixed by removing the dead unused `force` parameter entirely rather than just reordering, so the
  same class of positional-argument bug can't recur.
- CSS reuses the app's real tokens throughout (`--accent`, `--accent-2`, `--grp-*`, `--panel`,
  `--line`) — no duplicate palette. Follows the file's dominant single 760px breakpoint (not a
  second threshold) and the `.depth-card`'s own documented "opaque plate, not frosted" choice for
  the overlay chrome. Detail panel is self-contained rather than reusing the shared `renderDetail()`/
  `aside.detail` singleton — that panel is shared DOM state, and mutating `state.selectedNote`/
  `selectedCompound` from inside a full-screen overlay would leak into the Wheel/Tree view sitting
  behind it once the overlay closes.

### Verification

- In-app browser at 1280×800 and the 360×760 reference viewport. Opened via the real Sixth-lens
  depth-card action end to end; confirmed 221 star groups (127 notes + 94 compounds), correct live
  badge counts per lens, Geography's 34-chip and Embodied's full 127-chip tray, tagging Mint as
  "ortho" moving it live into the plot at the exact formula-predicted coordinate, and the Linalool
  trace producing the correct dimmed count and caption after the argument-order fix.
- Confirmed no regression: closing Constellation returns cleanly; Wheel note activation, Tree
  workspace, and Map workspace all still function normally afterward.
- Browser console reported no errors at any point. `git diff --check` passes.
- Not yet done: a physical-device/social-in-app-browser check, and Chemistry's density at the full
  262-edge scale hasn't had a dedicated visual pass beyond the existing min-weight-edge toggle — the
  original design spec already flagged this as a real, deferred risk at full scale, not new to this
  pass.

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

## Follow-up: optional reading layers + localized Order sprouts (2026-07-31)

- Added a prominent `Visibility` disclosure at the Tree's upper-left. It is a
  native keyboard-operable details/checkbox control, and its four layers can be
  combined freely: lineage landmarks, scientific Order names, flavor pictures,
  and cultivation-origin pips.
- Scientific Order names are off by default. The uncluttered default retains the
  hex collectors and recognition pictures plus high-level lineage landmarks such
  as Early superrosids. Portrait Order rows retain familiar example names while
  the scientific Order name remains optional.
- Expanded cultivation-origin color keys into the disclosure so their meaning is
  available exactly where that layer is toggled. The compact summary always lists
  the layers currently visible.
- Replaced global-fan placement for descendants of a selected desktop Order with a
  local sprout. The selected hex stays anchored; Families open in a tight row 132px
  above it; each Family's notes use a small maximum-five-column canopy immediately
  above. Sibling Orders and their spokes recede to 34%/28% opacity, the viewport
  recenters, and the selected branch receives a modest 1.28x zoom.
- Mobile continues its focused progression: Plantae's clade-grouped directory opens
  an Order disc containing only its Family choices; individual notes are not shown
  until the next taxonomic choice.

### Verification

- 1280-class landscape browser: default Plantae view renders 29 Order collectors
  with scientific names hidden, landmark captions visible, pictures/origin pips
  visible, and the summary `landmarks · pictures · origins`. Toggling Order names
  updates the SVG and summary without closing the multi-layer menu.
- Fagales drill-in renders two Families and three notes locally: Families are 200px
  apart, all descendants remain within 124px horizontally of the selected Order,
  and the note canopy is 220px deep rather than spanning the full canvas.
- 360 × 760 browser: the visibility disclosure fits the viewport with 44px options;
  Plantae shows 28 cards with Order names hidden, 28 right-ended collectors, and
  seven lineage headings. Poales opens a two-Family focused disc with zero note
  buttons at that stage.
- Inline script parsing and `git diff --check` pass. No physical kiosk/device claim
  is made.

### Coordination boundary

- This follow-up changes `index.html` plus this tracked handoff. The unrelated
  untracked `.claude/session-handoff-thesis-systems.md` remains untouched.

## Follow-up: progressive Tree default + intentional Order placement (2026-07-31)

- Made Kingdom overview the standard Tree entry state. Go Deeper now owns the
  intentionally dense all-notes state, while `All notes` and `Kingdom overview`
  remain explicit reversible controls.
- Kingdom activation now stops at Orders on every viewport; Order activation is
  the first point that reveals Families and notes. This removes the reported
  Plantae → notes jump.
- Replaced alphabetical/aesthetic Plantae Order placement with represented APG IV
  high-level lineage groups. Desktop Branches uses labeled clade hubs and real
  branch spokes; placement is explicitly labeled as lineage, not age.
- Kept geography independent from descent. Order collectors display colored pips
  aggregated from the app's existing cultivation-origin records; UI copy explicitly
  says these are not evolutionary ranges.
- Rebuilt portrait Plantae as a clade-grouped reading directory. At 360 × 760 it is
  one spacious Order row per line; each hexagonal note collector sits at the right
  end of its label, and selecting it opens the Order/Family layer rather than a note.
  Wider portrait kiosks progressively gain two or three columns. Landscape retains
  the branching form with a wider fan and the same right-ended collector grammar.

### Verification

- In-app browser at 360 × 760: verified five-node Kingdom overview; Plantae opens
  28 biological Order cards in seven labeled lineage sections; 28 right-aligned
  hex collectors and 44 cultivation-origin pips render; Vitales opens a one-Family
  Order view with zero note buttons.
- In-app browser at 1280 × 820: verified Kingdom overview, Plantae's 29 visible
  Order joints, seven clade hubs, zero Families/notes before Order activation, and
  automatic centering of the wider landscape branch canvas.
- Inline script parses successfully with the bundled Node runtime and
  `git diff --check` passes. No physical kiosk/device claim is made.

### Coordination boundary

- This pass changes `index.html` plus this tracked handoff. The unrelated untracked
  `.claude/session-handoff-thesis-systems.md` remains untouched.

## Human artistic direction for Claude's next Tree pass (verbatim, 2026-07-30)

The human explicitly wants Claude to have room to interpret this rather than merely
polish the current implementation. The present Branches renderer is a functional
first pass, not a locked visual specification. Their words:

> "so it initially was vertical but feedback from my test users said they liked the
> symbology of vertical reading more"

They immediately clarified which visualization that direction applies to:

> "i meant that the trees diagram with kingdom at bottom and individual notes at top"

Their fuller art and interaction direction:

> "Ah on the tree branch diagram, it is odd that families are bolded and underlined
> whereas the orderes are greyed and yet the order layer has the ability to completely
> ciollapse its entire branch so easily. that doesn't feel right when the flavor notes
> are the stars and the orders provide context. users should not be able to collapse
> any kingdoms, just focus on specific ones. the order needs a stronger glyph and block
> motif to show the lineage of the order and what it broadly represents. these are
> nodes between where we precisely diffentiate to another order once therei s family so
> to speak. this needs to be more visually poignant with how we render these branches
> with perhaps more of a hexagonal render where it is still a tree but think olive tree
> where it is hexagonal spiral going up so try to make that render on this 2d space
> where the orders are the first nocdules in the kingfdoms and they represent great
> many nuances that we zoom to with the families that are more like those more quirky
> twig-like branches or stem-like structures that become more leaf-like or leaflets or
> pines or something in-between to where we get that tree's innate fruiting body in
> either a conifer or a seed or flower or a spore or something else. i want to see it
> thoughtfully artistically rendered in a geometrically pleasing and thoughtful design
> making intentional encouragement for users to explore up the branch/down the rabbit
> hole/ zooming in, so to speak."

They then clarified the ecological composition and relative visual weight:

> "people will be spending the most time in plantae which will be the main part of the
> tree. fungus will be concnetrated in the roots of tree and not an organism will be
> placed next to the tree separately or nearby a small stick-figure humanoid
> representing humanity"

### Feature logic Claude should preserve while exploring

- The spatial reading is bottom-up: Kingdom/root context at the bottom, individual
  flavor notes at the top. The ascent itself should communicate progressively finer
  differentiation.
- Flavor notes are the stars and terminal fruiting bodies. Orders provide broad
  lineage context; Families are the finer, stranger twig/stem/leaflet transition
  between an Order and its notes.
- Kingdoms are persistent roots, not disposable disclosure rows. A user may focus a
  Kingdom, but clicking it must not make that Kingdom disappear or collapse the
  entire conceptual world beneath them without an explicit overview/reset action.
- Orders need stronger glyphs and a structural block/nodule motif than Families.
  Selecting an Order should feel like growing into or zooming through a major joint,
  not toggling an ordinary accordion row.
- The visual metaphor is a geometrically composed living tree, especially an
  olive-like ascending/spiraling rhythm translated into 2D. It need not be a literal
  botanical illustration. Claude has latitude to invent a clearer hexagonal,
  branching, spatial, or zoom-based grammar if it better creates the desired pull
  "up the branch / down the rabbit hole."
- Plantae should own most of the visual and interaction space because it is where
  users will spend most of their time. Fungi belongs concentrated around the roots.
  Animalia/humanity can be represented by a small humanoid marker. Process /
  not-a-single-organism is contextual and should sit separately beside the tree,
  near the human marker, rather than masquerading as an equal biological limb.
- The current hex joints, rootlet glyph, human glyph, detached Process node, and
  staggered Order canopy are proposals, not requirements. Preserve the ontology and
  interaction logic above; feel free to replace their rendering with a more
  beautiful, coherent, surprising solution.

### Request to Claude

Take a real art-direction pass. The human specifically said they want to see what
Claude can "throw at this." Prefer a strong compositional idea over incremental CSS
polish, while keeping the feature logic and mobile legibility intact.

## Follow-up: Branches as a rooted, focusable living tree (2026-07-30)

- Reworked the mobile Branches grammar so Kingdom and Order nodes are focus/grow
  actions instead of collapse toggles. Repeating a Kingdom or Order action never
  removes that lineage; `Kingdom overview` is now the explicit reset control.
- Plantae is the dominant central trunk. Fungi sits low as a compact rootlet
  cluster. Animalia is represented by a small human figure, while
  `Process / not a single organism` is a detached contextual node beside it rather
  than a falsely equivalent biological branch.
- Orders now use hexagonal growth joints, paired representative-note glyphs,
  angular branch geometry, and a five-step vertical cadence on phones. When one
  Order is grown, sibling Orders remain as quieter context rather than disappearing.
- Families use finer bud/stem motifs without the former bold-underlined emphasis.
  Flavor notes are explicitly framed as the fruit, inherit their aroma-group color,
  and remain the terminal interactive stars of the lineage.
- Added mobile overview coordinates that keep the rooted composition in one
  viewport and shorten the non-organism label to `Process` while preserving the
  full accessible name.
- Browser-verified at 360 × 760: four-root overview, keyboard focus of Plantae,
  29 visible Plantae Order joints, Poales growth to 2 Families and 10 flavor notes,
  repeated Poales activation retaining the grown branch, and repeated Kingdom
  focus retaining its Orders. `git diff --check` passes.

### Coordination boundary

- This pass remains Tree-only. The concurrent user-owned `CLAUDE.md` modification
  and untracked `.claude/session-handoff-thesis-systems.md` file remain untouched.

## Follow-up: live flavor-note search dropdowns (2026-07-30)

- Tree search now shows every matching note in a dropdown directly beneath the
  field while the user types, instead of reporting only an unexplained count.
- Extended the same dropdown component to the Wheel/Notes search and Origins Map
  search so every flavor-note search surface shares one interaction language.
- Each result names the note, its aroma group, and its taxonomic family. Group-color
  dots preserve the wheel's existing visual language.
- Results are clickable and support Arrow Up/Down, Enter, and Escape. The search
  field exposes combobox/listbox state for assistive technology.
- Exact note-id matches rank first, so `grape` shows `Grape / concord` before
  `Grapefruit`; pressing Enter on that query opens Grape directly.
- Notes search includes collapsed varietal children and expands/opens the selected
  note. Map search lists only currently eligible notes with origin placements and
  opens the chosen map marker plus its origin detail.

### Verification

- In-app browser viewport simulation at **360 x 760 CSS px**, not a physical
  device or social in-app browser.
- Confirmed `grape` reports two matches and lists `Grape / concord` and
  `Grapefruit`, with correct Fruity-group and Family metadata.
- Confirmed pointer selection and Arrow Down + Enter selection update the lineage
  and note detail. Confirmed exact-match Enter opens `Grape / concord`.
- At 360 x 760 the field/dropdown are 340px wide, result targets are 46px high,
  and the document has no horizontal overflow.
- Follow-up drawing-order fix raises the search toolbar above the later lineage
  strip. Reproduced with `gra` at 360 x 760: all five result cards paint above
  the story and Tree canvas, including through the overlapping region.
- Reverified all three searches at 360 x 760: Notes `cranberry` opens the collapsed
  varietal's mobile intensity sheet; Map `gra` lists Grapefruit and Pomegranate,
  and keyboard selection opens Grapefruit's marker/detail; Tree `grape` retains
  its two correctly ordered matches.
- Browser console reported no warnings or errors; `git diff --check` passes.

### Coordination boundary

- This pass changes only flavor-note search presentation/activation and this handoff.
  The concurrent `CLAUDE.md` modification and untracked
  `.claude/session-handoff-thesis-systems.md` file remain untouched.

## Follow-up: Save lap menu + exact-view links (2026-07-30)

- Changed the direct `Save lap` button into an accessible pulldown labeled
  `Save or share tasting`. Its menu describes the local action as
  `Save a snapshot in this session` and adds a
  visible, read-only exact-view URL with a one-tap Copy action.
- The exact-view payload preserves committed entries including ortho/retro phase
  keys, uncommitted slider positions, delivery conditions, pane and organization
  modes, Go Deeper state, active workspace, current note/compound/family focus,
  Tree/Map focus, filters, and expanded varietal rows.
- Existing Share-card URLs remain backward-compatible and separate. Opening an
  exact-view URL uses the new payload; opening an older `?t=` URL continues through
  the original aggregate-tasting hydrator.
- The menu disables only `Save a snapshot in this session` when the tasting is empty; sharing the
  empty/current view remains available. It closes after saving, on outside click,
  and on Escape.
- Moved the entire save/share control out of the wheel overlay and into the global
  header utility group. On compact phones it is the final item in the hamburger
  tray, beneath Feedback; its expanded panel participates in the tray's scrollable
  flow instead of drawing over the wheel. On desktop it remains an inline header
  utility and is available from Wheel, Map, and Tree.
- The wheel's snapshot rail now contains history only and stays absent until the
  first snapshot exists.

### Verification

- In-app browser viewport simulation at **360 x 760 CSS px**, not a physical
  device or social in-app browser.
- Confirmed the pulldown stays within the viewport, has no horizontal overflow,
  and exposes correct menu, menuitem, expanded, status, and link-field semantics.
- Confirmed at 360 x 760 that `Save or share tasting` is the hamburger tray's final
  DOM and visual item, its expanded panel remains contained by the tray, and the
  empty snapshot rail consumes no wheel space.
- Confirmed the control remains available in Tree and generates an exact-view URL
  there without horizontal overflow.
- Confirmed an Ethiopian coffee tasting enables `Save a snapshot in this session`,
  creates `Lap 1`, closes both the pulldown and mobile HUD, and reveals the saved
  snapshot rail.
- Confirmed Copy reports `Link copied`. Opened the generated 683-character URL in
  a fresh tab and verified Coffee / roast restored to 7, Berry to 6, and the
  Wheel + Notes pane configuration restored with no browser warnings/errors.

### Coordination boundary

- This pass changes the lap control, exact-view URL hydration, and this handoff.
  The concurrent `CLAUDE.md` modification and untracked
  `.claude/session-handoff-thesis-systems.md` file remain untouched.

## Follow-up: progressive mobile Plantae hierarchy (2026-07-30)

- Replaced the overloaded compact-phone Plantae disc, which drew Orders, Families,
  and all 111 plant note marks simultaneously, with a two-column Order directory.
  Each card shows only two recognizable example notes; the directory contains 28
  Order-level branches and preserves the separate cross-family flavor-word section.
- Multi-family cards lead to an Order disc containing Family slivers only. Individual
  note marks no longer appear at the Order level; they appear after choosing a Family.
- Each mobile Family sliver now carries a representative emoji, its common Family
  name, and its Latin Family name on the same sector. Poales, for example, reads as
  `🔥 Grass family / Poaceae` versus `🍍 Bromeliad family / Bromeliaceae`.
- Single-family Orders lead with the Family common name and put the Order in
  parentheses, for example `Laurel family` with `(Laurales)`. Because there is no
  meaningful fork, these cards open the Family's notes directly rather than forcing
  a one-sliver intermediate screen.
- Long Family names wrap inside their cards instead of truncating away `family`.
  The desktop radial Kingdom and Order views are unchanged.

### Verification

- In-app browser viewport simulation at **360 x 760 CSS px**, not a physical
  device or social in-app browser.
- Confirmed Plantae renders 28 Order cards, zero individual note marks, and no
  horizontal scroll. Each card exposes its examples and lineage in its accessible
  name.
- Confirmed Poales opens two Family slivers with both common and Latin names and
  no note rim; Bromeliaceae then opens its one-note Family wreath.
- Confirmed the single-family `Laurel family (Laurales)` card opens Lauraceae's
  two-note wreath directly and returns to Kingdom.

### Coordination boundary

- This pass changes only the compact-phone circular taxonomy hierarchy and this
  handoff. The concurrent `CLAUDE.md` modification and untracked
  `.claude/session-handoff-thesis-systems.md` file remain untouched.

## Follow-up: label-aware mobile Family-circle sizing (2026-07-30)

- Replaced the compact Family wreath's fixed 21.5%-of-canvas radius with a
  label-aware radius that uses the widest safe circle for each Family's actual
  note names and emoji.
- Decoupled the portrait-phone canvas height from its width. Sparse Families can
  now use nearly the full horizontal diameter while the SVG grows vertically to
  hold top/bottom labels, rather than shrinking the circle to fit a square.
- Crowded Families deterministically place their longest labels nearest the
  vertical axis and shorter labels near the horizontal edges. This preserves
  every note while allowing a materially larger ring.
- Desktop and mobile-landscape Family sizing remain on the existing square,
  smaller-axis behavior.

### Verification

- In-app browser viewport simulation at **360 x 760 CSS px**, not a physical
  device or social in-app browser.
- Lauraceae's two-note living edge expanded from a 235px to a 297px diameter in
  a 313px-wide SVG (94.9% width), with 9px top/bottom label clearance and no
  horizontal scrolling.
- Rutaceae's 11-note ring expanded from 120px before label-order optimization to
  about 186px afterward; its closest label remains 10px from the SVG edge.
- Rosaceae's 10-note layout keeps 9.6px minimum label clearance with no horizontal
  scrolling. At 1280 x 720, the existing 461px square desktop wreath is unchanged.

### Coordination boundary

- This pass changes only Family-circle layout on compact portrait viewports and
  this handoff. The concurrent `CLAUDE.md` modification and untracked
  `.claude/session-handoff-thesis-systems.md` file remain untouched.

## Follow-up: compact-phone detail hierarchy + interaction accessibility (2026-07-30)

- Reduced the Tree detail sheet's real minimized snap from 112px to 56px. The
  minimized state hides the detail body and exposes one 44px, keyboard-operable
  handle labeled with the current Family, Note, or Compound, so the Tree regains
  the bottom of the viewport without losing selection.
- Reset the Tree detail panel to its heading whenever its content changes. Switching
  Family â†’ Note no longer inherits a mid-document scroll position.
- Fixed the family-page helix at its source: the app-wide
  `svg { width:100%; height:100% }` rule was overriding the generated glyph's width
  and height. The glyph now carries explicit inline pixel dimensions; Rosaceae
  renders it at 15 Ã— 20 instead of filling the sheet.
- Converted Family and taxonomy-sibling links into native buttons with visible
  focus treatment. Literature compound links are native buttons, and generated
  compound-library rows receive role, label, focus, and Enter/Space activation.
- Made Scent-wheel compound tokens and Origin-map markers named, focusable SVG
  buttons with Enter/Space activation. Optional branch-view Tree nodes now expose
  the same semantic contract already used by the circular Tree.
- Tree search now reports `1 match Â· Enter to open`. Enter opens an exact or sole
  match in the circular Note focus, preserving the lineage readout and minimized
  detail access. A sole match in optional branch view is also centered in its
  scroll viewport.
- Raised the compact HUD's Go Deeper and menu targets to 44px, plus the Tree search
  field and zoom/toolbar controls, without adding horizontal document overflow.

### Verification

- Chrome viewport simulation at **360 Ã— 740 CSS px** (Galaxy S8+ class), not a
  physical device or social in-app browser.
- Confirmed the Wheel produces 17 focusable/named compound buttons from the
  Ethiopian coffee sample; Enter on Limonene opens its compound detail.
- Confirmed Tree search is 44px high, zoom buttons are 44 Ã— 44, Raspberry reports
  one actionable match, and Enter opens
  `Plantae â†’ Rosales â†’ Rosaceae â†’ Raspberry Â· note focus`.
- Confirmed Rosaceae minimizes to exactly 56px, preserves the selected family,
  expands to the half-height snap, starts at scrollTop 0, and renders the helix at
  15 Ã— 20 with lineage and diagnostic copy immediately visible.
- Confirmed Raspberry opens from the Family page at scrollTop 0 and exposes its
  three literature compounds as native buttons.
- Confirmed Origin markers expose role/button, tabindex, and region-aware accessible
  names. Chrome's automation layer timed out trying to send a keyboard press to an
  SVG marker, so the new key handler is code-reviewed but that one input path is not
  claimed as browser-verified.
- Inline script compilation, `git diff --check`, and browser console checks pass;
  no warnings or errors were reported.

### Approval boundary

- The proposed cross-workspace Insights inbox was not started. It requires a new
  shared notification model (tip lifecycle, generated-inference provenance,
  persistence/read state, and Wheel/Map/Tree deep links) rather than a small overlay
  adjustment, so it is being held for explicit architecture approval.

### Coordination boundary

- The pre-existing `CLAUDE.md` modification and untracked
  `.claude/session-handoff-thesis-systems.md` file were left untouched.

## Follow-up: Tree search activation feedback + Cranberry treatment (2026-07-30)

- Reproduced the reported Cranberry search behavior at 360 × 740: Enter correctly
  opened the note disc, lineage, and minimized detail handle, but the result line
  incorrectly remained `1 match · Enter to open`.
- The search result line is now a polite live status. After activation it changes
  to `Opened Cranberry - lineage and details updated` and receives a visible accent
  treatment; editing the query restores ordinary match-count behavior.
- The focused Cranberry Tree graphic keeps the berry emoji geometry but applies a
  Cranberry-only dark-crimson treatment with lighter ruby highlights. Other berry
  icons are unchanged.
- Reverified the complete keyboard path in Chrome at 360 × 740. The final state
  exposes the Cranberry lineage, Cranberry sheet handle, activation status, and
  scoped crimson icon filter. Inline scripts compile and `git diff --check` passes.

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
