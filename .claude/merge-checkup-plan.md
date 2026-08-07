# Pre-merge check-up: `codex/aroma-wheel-responsive-ux-pass` → `prototype`

Written 2026-08-06. This is a **work plan for a single ordinary agent session** (no subagents,
no workflows). It replaces a multi-agent audit whose verification pass died partway through, so
read the confidence key before acting on anything.

Nolan's ask, in his words, was four things:

1. Go over everything that changed on this branch before it merges.
2. **Cinch up the language** across the app and its instructions.
3. **Guide users in real time into insights about their chart** — when the notes they entered
   share crossover in any of the other areas.
4. **Some notes need updating to be compatible with those other tools** (Tree / Map / Constellation).

Audience to design for: the inquisitive person who taps **Go Deeper**. They want to learn how notes
relate, and how to detect compounds by inferring from what their senses report. Sense exploration.
The two headline taste-science features are **entering tasting notes** and **note comparison**.
Constellation is the on-ramp to relationships that are real but not directly causal.

---

## Confidence key

Every item below is tagged. **Do not skip this.**

- ✅ **VERIFIED** — reproduced directly in the running app this session, with the probe recorded.
  Act on these without re-checking.
- ⚠️ **CLAIMED** — reported by an audit agent that read the code, but its verifier died on a
  session limit before confirming. The line numbers are usually right and the reasoning is usually
  sound, but **open the file and confirm the quoted code exists before editing.**
- ❓ **NOT AUDITED** — a lens that never ran. Listed at the end so the gap is visible.

---

## Order of priority

The batches below are **thematic groupings, not a running order**. Work in this order instead.
The batch number in each row says where the detail lives.

### Tier 0 — two decisions that are Nolan's, not an agent's

Ask both up front so they stop blocking. Neither is a big conversation.

| # | Decision | Batch | Why it blocks |
|---|---|---|---|
| 0.1 | `mushroom` taxonomy: Agaricales / Agaricaceae / *Agaricus*, or a new Fungi-capable umbrella bucket? | 3 | It is the only broken note. Either answer is one small edit, but the second needs a `taxonPath` change |
| ~~0.2~~ | ~~Constellation: gate it, or reword its eyebrow?~~ **RESOLVED 2026-08-06, see below** | 5 | — |

#### 0.2 resolved — Constellation stays ungated, as the window into Go Deeper

Nolan's call: *"Constellation could be a window into go deeper on the surface. go deeper should be a
key button on the hud."*

So **do not gate `openConstellation()`**. Constellation is deliberately reachable before Go Deeper,
and its job on the surface is to show an inquisitive visitor what the deep end contains. That makes
the shape of the whole disclosure model explicit:

- **Wheel** — always available. The tasting.
- **Constellation** — always available. The window. Shows that relationships between notes exist.
- **Map / Tree** — revealed by Go Deeper. The rooms you walk into.

Consequences for the rest of the plan:

1. **Crossover route buttons (2.1) split by target.** Tree and Map routes go through `setWorkspace`,
   which force-enables Go Deeper (15476). The Constellation route does not need to, and should not.
   That asymmetry is now correct rather than an inconsistency.
2. **The eyebrow at 4200 stays Go-Deeper-flavored but stops asserting a mode the user is not in.**
   It currently reads "Go Deeper · creator mind space" to someone who never pressed Go Deeper.
   Reword toward a window, not a location. Something on the order of
   `A window into Go Deeper · the maker's mind`.
3. **Constellation needs a way *into* Go Deeper**, or it is a window with no door. Add one control
   in the overlay that turns Go Deeper on and lands the user in Tree or Map. This is what makes the
   window functional rather than decorative, and it is the natural home for the empty-state prompt
   already noted in Batch 5.

#### 0.2b — Constellation as the true Go Deeper function (direction set 2026-08-06)

Nolan, after the above: *"maybe constellation is the true go deeper function… and those different
aspects can link to the other tools. it should always be accessible in the hamburger menu."*

**This is the right read, and the code supports it.** ✅ VERIFIED: `body.go-deeper` currently gates
three unrelated jobs.

| What Go Deeper gates | Line | What kind of thing it is |
|---|---|---|
| Map and Tree workspace tabs | 188-189 | navigation |
| Per-row Add / Ortho / Retro commit buttons | 814, 9698 | an **input-technique** change |
| The vine and the six depth stories | 993, 1266-1314 | narrative |

The second one is the incoherence. "Go Deeper" promises conceptual depth and one third of what it
delivers is a different way to log a slider. That is a tasting technique, not a depth of
understanding, and it is why the button can feel loud and silent at once.

Constellation is the thing that actually is about depth. And its four lenses map cleanly onto the
four surfaces, which is what makes the hub idea work rather than just sound good:

| Constellation lens | Links to |
|---|---|
| Chemistry | the Wheel in **Chemistry** organize mode — same idea, compounds by chemical class |
| Taxonomy | the **Tree** |
| Geography | the **Map** |
| Embodied | **delivery conditions + ortho/retro phase tagging** |

That last row is not a stretch. ✅ VERIFIED in `cxLegendFor` (12005): Embodied's X axis already reads
*"real phase tags from your actual tasting"* — the exact data the Go Deeper commit buttons produce.
The loop already exists in the code and is simply not drawn. Pointing Embodied at the phase-tagging
input **also gives Go Deeper's orphaned third job a home that makes sense**, which is the piece that
was missing from the reframe.

**Target model.** Go Deeper stays the gold key button. Pressing it opens Constellation, so the press
lands somewhere that explains itself instead of silently changing three things. Constellation is the
hub: four ways your notes relate, each tapping through to the tool that does it properly.

Go Deeper **stops being the gate on navigation** — see 0.3.

**What this collapses.** Nine open findings in this plan stop being separate problems: Go Deeper
explaining nothing, the sixth depth story having no entry point, the eyebrow asserting a mode the
user is not in, Map and Tree offering no reason to visit, Constellation having no empty state,
Constellation's overlap rows dead-ending, the ortho/retro mode having no coherent home, the
gated/ungated inconsistency, and the mobile burial. That much collapsing is the signal the reframe
is correct.

**What it costs, honestly.**

1. **Overlay versus workspace mismatch.** Constellation is an overlay, Map and Tree are workspaces.
   A hub you tap back into repeatedly wants to be a peer workspace, not a modal you dismiss each
   time. Routes out must close it cleanly. The clean end state is Constellation as a fourth
   workspace, which is a bigger change than the routing work.
2. **The toggle keeps a persistent state.** `body.go-deeper` still has to gate the Map/Tree tabs and
   the phase buttons, so Go Deeper becomes one press with two effects. Decide explicitly that
   closing Constellation does **not** turn Go Deeper back off.
3. **Knock-on state.** `setNotes` auto-enables Go Deeper when entries carry phases (~11130), and
   exact-view links and snapshots encode the flag. Each needs rechecking if the flag's meaning
   changes.
4. **Choreography.** The warp and workspace-reveal morph currently contract onto the HUD workspace
   switch. Landing in Constellation changes the target.
5. **`CLAUDE.md` documents Go Deeper as the ortho/retro toggle** in several places and would drift.

**Sequencing recommendation: do not do this before the merge.** The branch is coherent as it stands
and this is an architectural change, not a fix. Merge what is there, then take the hub reframe as
its own branch with its own tracking PR.

Nothing in Tiers 1-3 gets thrown away by it. The crossover cards in 2.1 are the *inline* version of
exactly this idea — a relationship, then a route to the tool that shows it — so they are the
groundwork, not wasted work. Build them, watch which routes people take, then design the hub knowing
the answer.

#### 0.3 — Map and Tree stop being gated. They live in the ☰ tray permanently.

Nolan, clarifying: *"it should always be accessible in the hamburger menu… by it i mean the ability
to switch to the other tree and the map."*

**This partly reverses the branch's headline UI change.** The 2026-08-05 commit made Map and Tree
follow Go Deeper's progressive-disclosure hierarchy, gating both tabs on `body.go-deeper` at CSS
188-189. That gate comes out. **The ability to switch to Map and Tree must always be reachable from
the hamburger tray**, with no Go Deeper press required.

This is not a walk-back of the idea, it is a correction of what Go Deeper was gating. Progressive
disclosure belongs on **meaning**, not on **navigation**. Hiding two of three workspaces made the
tools undiscoverable. Go Deeper's job is to open the hub that explains how the tools relate, and
Constellation is that hub. The tools themselves stay available to anyone who goes looking.

Revised model:

- **Wheel** — the front door. The tasting.
- **Map / Tree** — always reachable, in the ☰ tray at minimum. Tools you can find on your own.
- **Go Deeper → Constellation** — the hub. Why these tools relate, and the route into each.

**Work this creates.**

1. Remove or narrow the CSS gate at **188-189**. Decide whether desktop still de-emphasizes Map and
   Tree before Go Deeper, or whether they are simply always present at both viewports. **Measure at
   360 × 760 before committing** — the header currently holds brand, Go Deeper, and ☰ with the
   workspace switch inside the tray, and the mobile-first contract forbids any critical control
   colliding or clipping at a reference viewport.
2. **`setWorkspace` (15476) should stop force-enabling Go Deeper** for non-wheel modes. That line
   exists only because the tabs were hidden. With the gate gone it becomes a surprising side effect,
   and it is what currently makes a shared exact-view link to the Map silently flip the user into a
   mode they did not choose.
3. **`setGoDeeper(false)` (12414-12417) should stop bouncing the user back to the Wheel.** Same
   reason. Standing in the Tree with Go Deeper off becomes a legal state.
4. **The workspace-reveal morph loses its purpose.** ~200 lines at 12441-12600 exist to animate the
   Wheel rim contracting onto the workspace switch as it appears. If the switch is always there,
   there is nothing to reveal. Either retarget the flourish at Constellation opening, or retire it.
   Retiring it is the honest option and removes the timer-lifetime risk in Tier 4.
5. Tier 4's audit shrinks accordingly. Much of what was unreviewed is code that may not survive.

**Merge implication.** The gate removal and the hub reframe are **separable**, and they have very
different costs.

- **Ungating is cheap and can land pre-merge.** Items 1-3 are one CSS rule and two behavior lines.
  Leave the morph alone for now, or fire it only on the first Go Deeper press. A reveal animation
  contracting onto a switch that is already visible reads as redundant, not broken.
- **The hub reframe (0.2b) should not land pre-merge.** Constellation becoming the Go Deeper
  destination touches state, choreography, snapshots, exact-view links, and `CLAUDE.md`.

Recommended: **ungate now, reframe next branch.** That gets the discoverability fix in while the
branch is fresh, and leaves the architectural change to a branch that can carry its own tracking PR.

The measurements below are kept as the record of the Constellation-placement question that prompted
this. The header-promotion option for `#constellation-toggle` is **closed** — it stays in the tray.

✅ **VERIFIED at 360 × 760.** Constellation cannot be a window into anything on a phone right now,
because it is **not on the surface at all**. It sits inside `#hud-extra`, so with the ☰ tray closed
its rect is `0 × 0`. Two taps deep and invisible.

| | 1280 × 720 | 360 × 760 |
|---|---|---|
| **Go Deeper** | 140 × 28, gold fill `rgb(216,166,87)`, weight 600, direct `<header>` child | **124 × 44, gold, always visible** |
| **Constellation** | 109 × 28, plain dark, inside `#hud-extra` | **0 × 0, collapsed in the closed tray** |
| ☰ tray toggle | `display: none` | 44 × 44 |

Two things follow.

**Go Deeper is already the key HUD button — nothing to build.** It is the only filled button in the
header at either viewport, it is a direct child of `<header>` rather than of the collapsible tray,
and it meets the 44 px touch minimum on the compact-phone reference. Header height 56 px, zero
horizontal overflow. The instruction is already satisfied by the shipped design.

What Go Deeper is missing is not prominence, it is **explanation**. Pressing it reveals three new UI
layers and says nothing (Batch 5, ⚠️ claimed: `openDepthCard` is never called from the toggle). That
is the real work behind "key button" — it is loud and silent at the same time.

**Constellation, by contrast, needs promoting.** If it is the surface-level window, it has to be on
the surface at the viewport most people arrive on. Options, cheapest first:

- Promote `#constellation-toggle` out of `#hud-extra` to a direct `<header>` child, beside Go Deeper,
  styled as the quiet sibling to Go Deeper's gold. Header currently holds brand + Go Deeper + ☰ at
  360 px with room to spare, but **measure before committing** — the mobile-first contract forbids
  any critical control colliding or clipping at a reference viewport.
- Or leave the header alone and put the window where the curiosity already is: a Constellation entry
  on the crossover cards built in 2.1, which is where a user has just been told two of their notes
  are related.

The second is cheaper, is testable, and fits the brief better. **Recommend doing 2.1 first and
deciding on the header promotion after seeing whether the crossover cards already carry the traffic.**

### Tier 1 — cheap, verified, and wrong right now

All six are small, all are ✅ verified, and every one is something a reviewer could catch on the PR.
Roughly an hour together. **Do these before the big build** — if the session ends early the branch is
still better off, and 1.1 warms up the exact functions Batch 1 builds on.

| # | Item | Batch | Size |
|---|---|---|---|
| 1.1 | Ungate the comparison crossover (15737, 15748) | 2 | 2 lines |
| 1.2 | Fix the stale data-model counts in Methodology (13077-13079): 44→**127** notes, 8→**9** scent families, 53→**94** compounds, 120→**262** edges | 4 | 3 list items |
| 1.3 | Make the instructions match what shipped: "Compass"→**Radar** (13185, 13036), "the header's Organize toggle" (13176) after Organize moved wheel-local, and the Go Deeper section (13191) that still never mentions revealing Map and Tree | 4 | one copy cluster |
| 1.4 | Scrub the three leaked internal identifiers (4265, 12004, 12005) | 4 | 3 strings |
| 1.5 | Restore focus when Escape closes the compound-definition popover (15957, 19349) | 2 | small, **the only adversarially verified finding** |
| 1.6 | De-lead the alcohol in the first-run empty state (4088, move the IPA chip off position 2) | 4 | 2 edits |

### Tier 2 — the actual brief

| # | Item | Batch | Size |
|---|---|---|---|
| 2.1 | **Build `crossoverInsights()` and render it** — bouquet cards plus the tasting-tray pointer, with routes into Tree / Map / Constellation | 1 | the main build |

This is the one item that answers what Nolan asked for. If there is appetite for exactly one thing
this session, it is this, not Tier 1.

### Tier 3 — completes the thesis

Each of these turns a dead end into a route. They only pay off once 2.1 exists.

| # | Item | Batch |
|---|---|---|
| 3.1 | Add route buttons to the six comparison layer cards, which name Tree, Map, and Constellation and link to none of them (16113-16138) | 2 |
| 3.2 | Tie comparison to the live tasting: seed the two strongest active notes, and say which of the pair is already logged (15684 / 19292 / 16163) | 2 |
| 3.3 | Make the zero-overlap case a finding rather than a disclaimer, by comparing compound classes (16178) | 2 |
| 3.4 | Give the sixth depth — the one that explains Constellation — an entry point on the vine (4063-4067) | 5 |
| 3.5 | Let a note be added to the tasting from its detail panel (10135), and make contributing notes clickable in compound detail (10623) | 5 |

### Tier 4 — the risk nobody has looked at

| # | Item | Batch |
|---|---|---|
| 4.1 | Review the Go Deeper reveal mechanics: timer lifetime across rapid toggles, overlay cleanup on Escape mid-animation, snapshot restore across modes, focus after the reveal, whether hidden tabs leave the tab order | ❓ |

This is the newest structural change on the branch and **no agent ever audited it**. It is last by
value and high by risk. Do not merge without at least a manual pass.

### Tier 5 — the long tail

| # | Item | Batch |
|---|---|---|
| 5.1 | Adopt the canonical vocabulary as a comment block, then sweep the app once | 4 |
| 5.2 | Semicolons and "X, not Y" framing across interface copy | 4 |
| 5.3 | Reframe the cocktail-named gestalts in `FLAVOR_COMBOS` (Mulled wine, Mojito, Piña colada) | 4 |
| 5.4 | Escaping, dead Climate card, optgroups, live-region scope, mobile leaf hit targets, and the rest | 2, 5 |

5.1 is the largest single item in the whole plan and the least urgent. It touches hundreds of
strings for no behavior change. **Do not start it in the same session as 2.1** — a huge copy diff on
top of a new feature makes the PR unreviewable.

---

## Running and verifying

```bash
git rev-parse --abbrev-ref HEAD
```

The app is one file: `index.html` (~20,900 lines, 1.37 MB). No build step.

Start the preview with the **preview tools**, never Bash:
`preview_start({name: "aroma-wheel"})` — config already exists in `.claude/launch.json`, port 9321.

Screenshots may fail if the Browser pane is not displayed. That is fine, everything below is
verifiable with `javascript_tool` and `read_page`. These probes are how the ✅ items were confirmed:

```js
// dataset shape
JSON.stringify({notes: NOTES.length, compounds: COMPOUNDS.length, edges: EDGES.length,
  visible: getVisibleNotes().length, groups: GROUPS.length})

// what a real tasting actually surfaces
(function(){ setNotes([{note:"lemon",intensity:7},{note:"orange",intensity:6},{note:"mint",intensity:5}]);
  setView('analysis'); const b=document.querySelector('.bouquet');
  return b ? b.innerText.replace(/\n+/g,' | ') : 'NONE'; })()

// crossover context, on the Wheel vs inside Tree/Map
(function(){ const a=NOTE_BY_ID.lemon,b=NOTE_BY_ID.orange;
  const onWheel=taxonomyComparisonContext(a,b);
  document.body.classList.add("taxonomy-mode","origins-mode");
  const inLenses=taxonomyComparisonContext(a,b);
  document.body.classList.remove("taxonomy-mode","origins-mode");
  return JSON.stringify({onWheel: onWheel||"(EMPTY)", inLenses}); })()
```

Wrap every probe in an IIFE. Bare `const` at top level throws `already been declared` on the
second run in the same tab.

---

## Batch 1 — The crossover engine (the biggest ask, build this first)

### The gap, ✅ VERIFIED

Enter Lemon 7, Orange 6, Mint 5. The entire live synthesis reads:

> Main aroma compound class · 🌲 Terpene · citrusy, piney, herbal.
> You might also smell · 🌿 Mojito · lime and fresh mint.

It never says that Lemon and Orange both point to **limonene**, that they are both **genus
*Citrus* (Rutaceae)**, or that their recorded origins sit ~2,470 km apart in the same region.
All three facts are already computable from loaded data.

Worse, ✅ VERIFIED: `taxonomyComparisonContext` (index.html:15729) gates the botanical block on
`document.body.classList.contains("taxonomy-mode")` (15737) and the map block on `origins-mode`
(15748). Comparing Lemon to Orange **from the Wheel returns an empty string**. The same call inside
Tree/Map returns:

> Botanical link: both are represented in genus Citrus (Rutaceae). Map context: Historical-origin
> markers: Lemon — Eastern Himalayan foothills…; Orange — South-central China…; approximately 2,473 km apart.

That is exactly backwards from what Nolan wants. The crossover fact should be **the reason you go
to the Tree and the Map**, not a reward for already being there.

Sharpest case, ✅ VERIFIED: **Rose vs Almond**. Zero shared compounds, and both are **Rosaceae**,
filed in different scent families (Floral and Nutty). Comparing them today produces literally
nothing. That single pair is the thesis of the whole feature.

### The material you have, ✅ VERIFIED

14 botanical families in the dataset span **more than one scent family**, and none of them surface
during a tasting:

| Family | Common | Members across scent families |
|---|---|---|
| Rubiaceae | Coffee family | Gardenia (floral) + Coffee (roasted) |
| Anacardiaceae | Cashew family | Mango (fruity) + Pistachio (nutty) |
| Sapindaceae | Soapberry family | Lychee (fruity) + Maple (sweet) |
| Fabaceae | Legume family | Licorice (spice) + Peanut (nutty) |
| Myrtaceae | Myrtle family | Clove (spice) + Eucalyptus (earthy) |
| Rosaceae | Rose family | Rose (floral) + Almond (nutty) + 8 fruits |
| Amaranthaceae | Goosefoot family | Quinoa (roasted) + Beet (vegetal) |
| Asteraceae | Daisy family | Chamomile (floral) + Lettuce (vegetal) |
| Ericaceae | Heath family | Cranberry, Blueberry (fruity) + Wintergreen (earthy) |
| Oleaceae | Olive family | Jasmine, Lilac (floral) + Olive (vegetal) |
| Apiaceae | Carrot family | Anise (spice) + Celery, Carrot (vegetal) |
| Solanaceae | Nightshade family | Bell pepper, Tobacco (earthy) + Tomato, Potato (vegetal) |
| Lamiaceae | Mint family | Lavender, Sage, Thyme (floral) + Mint (earthy) |
| Rutaceae | Citrus family | 10 citrus (fruity) + Orange blossom (floral) |

### Build it

Add `crossoverInsights(activeNotes)` immediately **above** `renderBouquetHtml` (insert at ~10341,
just after `detectFlavorCombos` closes). Return a ranked array of
`{axis, kicker, headline, why, plain, route}`, capped at 3, at most one per axis.

Use **the same three axes Constellation already uses** — chemistry, taxonomy, geography — plus a
process row. That alignment is itself part of "cinching up the language": one set of axes across
Wheel, Tree, Map, Compare, and Constellation.

**Chemistry row.** ⚠️ CLAIMED but strong: `computeFloatHomes()` already stores `node.supportNoteIds`
and `node.supportCount` on every compound node on every recompute (~8508-8510), and the only place
it is read is an SVG `<title>` tooltip at ~8830-8836 — which does not exist on touch, and mobile is
the canonical viewport. **Read those fields instead of recomputing.** Filter
`compoundNodes.filter(n => n.intensity_raw > 0 && (n.supportCount||0) >= 2)`, sort by score, take
the top. This keeps the card consistent with the shared-orbit gravity the user is watching on the
wheel, so the card explains the visual rather than duplicating it.

> Confirm first: ⚠️ CLAIMED that `compoundActiveSupportNoteIds` (~8463) has a dead branch — line
> ~8466 filters on `isNoteVisible`, which returns false for every `subOf` child, making the
> inherited-edge branch at ~8469-8471 unreachable. If true, a varietal scored alone (Peppermint
> without Mint) can never count as a crossover source. Proposed fix is `isNoteScoreable` at 8466.
> **Check whether `computeFloatHomes` line ~8512 still needs `isNoteVisible` for the position
> lookup before changing this** — a `subOf` child has no `_x`/`_y`.

**Taxonomy row.** Group active notes by `family`. Prefer a **cross-scent-family** match (different
`n.group` values) over a same-family one — that is the surprise. Prefer genus when every member
shares one. `taxonClusterLabel` (7570) already encodes the genus-vs-family rule, reuse it rather
than writing a second. `TAXON_COMMON` (7447) has the plain-English family names.

**Geography row.** `taxonomyOriginRegion(origin)` (16499) buckets a `NOTE_ORIGINS` record into one
of five regions (16491). `taxonomyOriginDistance(a,b)` (15751) gives great-circle km. Both are pure
functions, both reusable as-is. Fire the region row when a region holds ≥2 active notes.

**Process row.** ✅ VERIFIED that 13 notes carry `taxonBucket:"process"` and are excluded from the
Tree entirely (`buildTaxonomyTreeData`, 7627). When ≥2 are active, say so plainly rather than going
silent — they have no Tree branch and no Map origin, and their crossover lives in the chemistry.

**Do not** call `taxonomyComparisonData` from here. ⚠️ CLAIMED: `cxOverlapSpectrum` (12103) runs
8,001 pair evaluations. Restrict the live scan to pairs of *active* notes (2-8 notes, ≤28 pairs).

**Drop shared-delivery from the plan.** ⚠️ CLAIMED and it looks right: `DELIVERY_CONDITIONS` (6461)
is tasting-level state with no per-note or per-compound link — the comment at ~9351 says
"nothing here touches recompute()". There is no data behind "two of your notes share a delivery
condition." Substitute the real adjacent fact: compounds carry a `threshold` tier, so
"most of your evidence sits on very-low-threshold compounds" is honest and leads naturally to the
delivery strip.

### Where it renders

✅ VERIFIED problem: in the default fresh-load view the results pane is `display:none`.
`autoDetectViewMode` (10821) calls `setView("note-input")`, which sets `state.detailHidden = true`.
So the bouquet — and anything added to it — is **invisible on a fresh tasting**.

Do **both**:

- **Rich cards** in the bouquet, as a third cloud in `renderBouquetHtml` between `mainCloud` and
  `comboCloud`. Reuse `.bouquet-cloud` / `.bouquet-kicker` / `.bouquet-headline` / `.bouquet-sub`
  (CSS 263-286). Compound names get `data-cpd="…"` and they are wired automatically — the sweep at
  ~10543 catches every `[data-cpd]` inside `detailPanel`.
- **A pointer in the tasting tray**, which is the surface actually on screen at the moment of
  entry. In `renderTastingTray` (9782), after the chips loop, append one button when
  `crossoverInsights()` is non-empty. Click opens the results pane.

Do **not** overload the wheel hint (`WHEEL_HINTS`, 10776). Its job is the Scent/Chemistry mode
caption and it is the only place that explains the organize modes.

### Routes

Every row ends with a route into the workspace that shows it. ⚠️ CLAIMED that the app has exactly
one such control today — `cxTraceBtn` inside Constellation (~12226) — and nothing in the Wheel,
bouquet, hint, or tray routes anywhere.

- chemistry → Constellation, chemistry lens, select the compound
- taxonomy → `setWorkspace("tree")` then `setTaxonomyFocus("family", family)` (16665)
- geography → `setWorkspace("map")` then `selectOriginNote(id)` (15448)
- process → Constellation, taxonomy lens (it does include process notes as a
  "Process / not a single organism" ring, ✅ VERIFIED via `cxLayoutTaxonomy`, 11772)

`setWorkspace` already force-enables Go Deeper for any non-wheel mode (✅ VERIFIED at 15476), so
route buttons work from a cold start. That is the honest behavior: the route button *is* the
invitation Go Deeper is supposed to be.

### Copy rules for every string you write

From Nolan's standing style: **no semicolons. Minimal em dashes. No "not X, it's Y" contrastive
framing. No persuasive or defensive tone. Keep the real scientific terms** — using the actual word
is the honest representation. Never lead with wine, beer, or spirits.

Pattern:

> **Shared molecule** — Lemon and Orange both point to Limonene.
> Two notes landing on one compound is what raises its confidence in your results.
> [ See it in Constellation → ]

> **Shared family** — Rose and Almond are both Rosaceae, the rose family.
> The wheel files them apart by smell and the botany puts them together. Relatives often run the
> same enzyme pathways, so a shared family is a reason to expect shared chemistry even where no
> compound overlaps yet.
> [ See it on the Tree → ]

---

## Batch 2 — Ungate the comparison crossover

Small, high-value, ✅ VERIFIED.

- **15737** — drop the `taxonomy-mode` guard so the botanical block always runs.
- **15748** — drop the `origins-mode` guard so `taxonomyComparisonMapContext(a, b)` always runs.
- The header toggle's own title at **3877** already promises "in any workspace", so the guards
  contradict shipped copy.
- Keep the per-workspace emphasis via the `is-workspace-lens` marker (~16069), which is the right
  mechanism for "this lens is the one you're standing in."

Then verify with the third probe above: `onWheel` must stop returning `(EMPTY)`.

⚠️ CLAIMED follow-ons in the same subsystem, confirm each before editing:

- **16113-16138** `taxonomyComparisonExpandedLayersHtml` emits six layer cards naming Tree, Map,
  and Constellation, and **not one of them contains a button, link, or `data-` hook**. Add
  `data-compare-goto` routes and wire them in the existing listener block at ~16187.
- **16163** the comparison never reads `state.entries`, so it is a detached reference lookup. Add a
  first line tying it to the live tasting: which of the two notes are already logged, and at what.
- **~15684 / 19292** Compare never seeds from the tasting the user just built. Seed the two
  strongest active notes when both slots are empty.
- **16178** the zero-overlap case is a disclaimer, not a finding. For this audience a clean
  non-overlap *is* a finding — compare compound **classes** instead and say so.
- **16007** unescaped `"` inside a `title="…"` attribute. Four compounds contain literal escaped
  double quotes (`aitc`, `ipmp`, `isobutylthiazole`, `butylphthalide`), which breaks the attribute.
- **16134** a permanent dead "Climate — awaiting sourced data" card renders on every comparison of
  every pair. Remove it or demote it to a footnote.
- **19349** Escape closes the compound-definition popover without restoring focus, dropping keyboard
  users to `<body>`. This is **the one finding that survived adversarial verification** — the
  verifier checked all 21 keydown listeners and all three popover-hide paths. Fix: store
  `popover._opener = opener` at ~15957, then `definition._opener?.focus()` at 19349. Add
  `aria-haspopup="dialog"` statically, but **only sync `aria-expanded` dynamically** — baking a
  static value into the templates would regress accessibility.

---

## Batch 3 — Notes that are not compatible with the other tools

✅ VERIFIED counts: 127 notes, 111 placed in the Tree, 83 visible at top level.

**The one real hole: `mushroom`.** It is the only note in the Tree with a broken path. It carries
`kingdom: "Fungi"` and **no `order`, no `family`, no `genus`**, so `taxonPath()` returns a
one-segment `["Fungi"]` and it hangs off the kingdom disc as an orphan while every other in-tree
note runs Kingdom → Order → Family → Note. It also has no `NOTE_ORIGINS` record.

For contrast, ✅ VERIFIED that the other two non-plant notes are complete:
`yeasty` has Saccharomycetales / Saccharomycetaceae / *Saccharomyces*, and `honey` has
Hymenoptera / Apidae / *Apis* plus its own `.tx-honey-bee` rendering in the Tree.

Recommended fix, following the precedent the app already set for `cereal` → Poaceae: give mushroom
**Agaricales / Agaricaceae / *Agaricus***, with an honest note that it stands for the button-mushroom
register, since the app's own compound for it (1-octen-3-ol) is literally the mushroom alcohol.
**Flag this to Nolan rather than deciding silently** — "Mushroom" genuinely spans many families, and
the alternative (an umbrella bucket) is currently hardcoded to `Plantae` in `taxonPath` (7612) and
would need a small code change to work under Fungi.

**Everything else that falls out of a tool is deliberate and correct**, ✅ VERIFIED:

- 13 `taxonBucket:"process"` notes (smoky, caramel, cottoncandy, winey, buttery, sulfury,
  cardboard, cheesy, sweaty, musty, skunky, miso, soysauce) and 2 `umbrella` notes (berry, green)
  are excluded from the Tree by design.
- 34 notes have no Map origin, 17 of them visible. Most are process or umbrella notes with no
  single origin. `brusselssprouts` is arguably a gap worth filling.
- `bloodorange` is the only note with no compound edges, which is the deliberate `noStandoutNote`
  honesty case (its identity is anthocyanin pigment, not aroma).

**Data integrity is clean.** ✅ VERIFIED with id cross-reference: zero dangling note or compound ids
in `EDGES`, zero dangling keys in `NOTE_ORIGINS`, and **the recurring bug class has not recurred** —
no `WAIS_DESCRIPTORS` entry and no `GUIDE_INGREDIENTS` / `GUIDE_NARROW` entry points only at
invisible `subOf` notes. That bug was fixed twice before, and the last ~45 commits did not
reintroduce it.

---

## Batch 4 — Canonical vocabulary, then one enforcement pass

⚠️ CLAIMED throughout, but this is the answer to "cinch up the language." There is no vocabulary
definition anywhere in the file, which is why every new feature coins a new name. `JARGON` (~6940)
defines chemistry terms, not product terms.

**Adopt this mapping, add it as a comment block near the top of the script, then enforce it.**

| Concept | Use | Retire |
|---|---|---|
| The thing you slide | **note** (`aroma note` on first mention in a panel and in aria-labels) | flavor note, tasting note, culinary aroma note, descriptor, scent |
| The thing inferred | **compound** (`aroma compound` on first mention) | molecule, odorant, aromatic compound. Keep "molecule" only for structural statements about one substance |
| The 9 wheel sectors | **scent family** | note group, aroma family, flavor family, flavor category, scent group |
| The botanical rank | **botanical family**, or the Latin name | bare "family" where it could collide |
| The wheel radar widget | **Radar** | Compass (reserve Compass for the Map only) |
| The saved tasting state | **snapshot** | lap |
| Constellation's four views | **lens** | mode, view |
| Go Deeper's six stories | **depth** | lens (collides with Constellation) |
| Wheel / Map / Tree | **workspace** | explorer, view |
| Notes / Results side panes | **Notes panel**, **Results panel** | sliders pane, analysis pane, Compounds pane, dashboard |
| `edge.w` | **link strength** (`base link strength` pre-scoring) | weight, base weight, signal, evidence strength |
| `comparisonData.score` | **shared-compound overlap** | weighted aroma overlap, weighted Jaccard overlap, correlation view |
| Clearing entries | **Clear tasting** | Start Over, Clear |

Highest-value individual edits, all ⚠️ CLAIMED — **verify each string exists before editing**:

- **13077-13079** Methodology states "~44 descriptors across 8 groups", "53 aromatic compounds",
  "120 connections". Actual, ✅ VERIFIED: **127 notes across 9 scent families (83 with their own
  slider), 94 compounds, 262 edges.** Stale by 2-3x on the page that documents the data model.
- **13185** How to Use still documents the wheel widget as **"Compass"**. It was renamed **Radar**
  (button text at 4049, header at 4130), and the CSS comment at ~1341 explicitly reserves Compass
  for the Map. Same stale name at **13036** in About.
- **13181-13188** the Controls list omits **Constellation** and **Compare notes** — the two features
  Nolan names as headline — plus delivery conditions and snapshots. It also presents Map and Tree as
  ordinary controls when both tabs are hidden until Go Deeper.
- **13191** the Go Deeper section describes *only* the ortho/retro commit step. Revealing Map and
  Tree is now its headline behavior and goes unmentioned. This is the most stale paragraph on the
  branch given what shipped.
- **13176** "The header's Organize toggle" — Organize moved out of the header into a wheel-local
  toolbar on 2026-08-05.
- **4088** the first-run empty state reads "Works with coffee, tea, wine, beer, botanicals, and
  food", and **IPA is the second of eight demo chips**. Against the standing rule that the audience
  priority is non-drinkers and sober folks. Move IPA last, reword to
  "coffee, tea, cocoa, botanicals, food, and anything fermented."
- `FLAVOR_COMBOS` (10287) similarly leads with **Mulled wine 🍷**, **Mojito 🍹**, **Piña colada**.
  ✅ VERIFIED these fire and render. Consider reframing as the drink-free gestalt
  (mint and lime cooler, pineapple coconut cream) rather than the cocktail name.
- **Three leaked internal identifiers in user-facing copy**, ✅ VERIFIED at
  **4265** ("this app's own NOTES/COMPOUNDS/EDGES graph"), **12004** ("no NOTE_ORIGINS record in the
  app"), **12005** ("from the app's own GUIDE_MOUTH cooling/warming tags"). The branch already had a
  "scrub tool tells" commit and these three survived it.
- Eleven semicolons in interface copy (10222, 10779, 10783, 11993, 12005, 15765, 16083, 16116,
  16125, 16180 and more) and "X, not Y" framing at 10396, 13027, 13134, 3999, 12184, 16178.
  Split each at the break into two plain sentences.

---

## Batch 5 — Journey and Go Deeper consistency

- ✅ **VERIFIED, and now resolved by design — see 0.2 above.** CSS 188-189 hides the Map and Tree
  tabs until `body.go-deeper`, while Constellation and Compare notes have no such rule. That is
  **intentional**: Constellation is the ungated window into Go Deeper. Do not gate it. The work here
  is the eyebrow at 4200 (stop asserting a mode the user is not in), a door out of the window into
  Go Deeper, and the mobile burial recorded in 0.3.
- ⚠️ **CLAIMED, high value.** `DEPTH_STORIES` has six entries but `#deeper-vines` has only five
  `.vine-leaf[data-depth]` elements (4063-4067). **The sixth depth — the one that explains
  Constellation — has no entry point.** The `aria-label` at 4058 also says "Five depths".
- ⚠️ **CLAIMED.** Go Deeper reveals three new UI layers (Map/Tree tabs, per-row Add/Ortho/Retro
  buttons, the vine) and explains none of them. `openDepthCard` is never called from the toggle.
  Proposal: call `openDepthCard(1)` once from `finishWorkspaceReveal` (~12509), gated on
  `state.dismissedHelpers`.
- ⚠️ **CLAIMED.** On mobile the only entry to the depth narrative is a ~25px decorative leaf
  (`r=15` hit circles, scaled 0.82 at ~1295), well under the 44px minimum the file's own comment
  cites. Mobile is the canonical viewport.
- ⚠️ **CLAIMED.** `renderNoteDetail` (~10135) tells a user "if you confirmed it" and gives them no
  control to confirm it. This is the panel every Tree leaf click lands on. The Map already solves
  this by committing at intensity 5 on marker select.
- ⚠️ **CLAIMED.** `renderCompoundDetail` (~10623) renders contributing notes as inert `<span>`s
  while every peer list in the same pane uses a `.view-note` button. The most relational screen in
  the app cannot be traversed.
- ⚠️ **CLAIMED.** Constellation with zero notes entered has no empty state.

Two Go Deeper claims from the handoff **were checked and are true**, ✅ VERIFIED: `setWorkspace`
force-enables Go Deeper for non-wheel modes (15476), and `setGoDeeper(false)` returns to the Wheel
rather than stranding the user (12414-12417). No fix needed.

---

## Batch 6 — Before opening the PR

- Re-run every probe in the "Running and verifying" section.
- Check the console is clean. ✅ VERIFIED clean on load today.
- Test at **360 × 760** portrait, the required compact-phone reference viewport, per the mobile-first
  product-design contract in `CLAUDE.md`. Wheel, Tree, Map, and Constellation must all load and
  switch with zero console errors and zero horizontal page overflow.
- Record the viewports and interactions checked in `.claude/codex-handoff.md`. Do not claim a
  physical-device result unless it was run on that device.
- **Do not open the PR without an explicit go-ahead from Nolan naming this branch and the target.**
  Per `CLAUDE.md`, `codex/*` may PR directly into `prototype` or `feature/bloom`, but only when he
  says it is time.

---

## What was not audited

Two of six audit lenses died on session limits before returning anything:

- ❓ **Data compatibility** — the systematic note-by-note sweep across all five subsystems. Partly
  covered by the direct verification in Batch 3, but no agent ever produced the full per-note table,
  and `DELIVERY_CONDITIONS` and `GUIDE_MOUTH` coverage were never checked.
- ❓ **Go Deeper mechanics** — the correctness review of the newest structural change. The two
  claims I checked by hand hold, but timer lifetime across rapid toggles, overlay cleanup on
  Escape mid-animation, saved-snapshot restore across modes, focus management after the reveal, and
  whether hidden tabs leave the tab order were **never examined**.

The verification pass also died for 57 of 62 agents, so every ⚠️ item carries a finder's reasoning
and a verifier's silence. **The one finding that survived adversarial verification** is the Escape
focus-restoration bug in Batch 2.
