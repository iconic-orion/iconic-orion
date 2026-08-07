# Pre-merge check-up: `codex/aroma-wheel-responsive-ux-pass` → `prototype`

Work plan for a single ordinary agent session. No subagents, no workflows.
Line numbers regenerated **2026-08-07** against commit `a6bdf5e`.

> **Line numbers go stale fast.** Two agents work this branch. Before acting on any
> anchor below, regenerate it. Do not trust a number you did not just check:
>
> ```bash
> grep -n "^function taxonomyComparisonContext" index.html
> ```

---

## Status

Four commits have landed against this plan.

| Commit | What |
|---|---|
| `ee22b5b` | Ungated Map and Tree, placed Mushroom, unhid comparison crossover, fixed stale reference copy |
| `04c7057` | One relationship engine behind the Wheel and Constellation |
| `205a488` | Surfaced the top relationship live, above the tasting tray |
| `a6bdf5e` | Retired the workspace-reveal morph |

Codex is working the same branch in parallel. `7594936` landed a tasting-first Constellation,
Map and Tree coverage readouts, a How to Use rewrite, and a medical-use boundary. Its
`cxActiveTastingNotes` and `cxTastingOverlapPairs` are now thin delegates to the shared engine, so
**do not reimplement relationship logic in either surface.** Add to `tastingRelationships()`.

---

## Settled design decisions

Do not relitigate these. They came from Nolan directly.

1. **Wheel, Map, and Tree are peers.** All three reachable from first load, which on a phone means
   all three in the ☰ tray. Progressive disclosure belongs on meaning, not navigation. **Done.**
2. **Constellation is the window into Go Deeper**, and stays ungated. It visualizes relationships
   both across the whole tool and in the context of a selected note.
3. **Go Deeper is already the key HUD button.** Gold fill, direct `<header>` child, 124×44 at
   360 px. Nothing to build. What it lacks is explanation, not prominence.
4. **Constellation's four lenses should link out to the tools** — Chemistry to the Wheel's Chemistry
   organize mode, Taxonomy to the Tree, Geography to the Map, Embodied to delivery conditions and
   ortho/retro phase tagging. Not built yet. See item 3 below.
5. **`mushroom` is placed** on Agaricales / Agaricaceae / *Agaricus*, with a comment recording it as
   a representative placement rather than a claim about all fungi. **Done.**

---

## Confidence key

- ✅ **VERIFIED** — reproduced in the running app. Act without re-checking the claim, but still
  re-check the line number.
- ⚠️ **CLAIMED** — an audit agent read the code and reported it, but its verifier died on a session
  limit. Reasoning is usually sound. **Confirm the code exists before editing.**
- ❓ **NOT AUDITED** — nobody looked.

---

## Running and verifying

`index.html` is the whole app. No build step. Start the preview with the **preview tools**, never
Bash: `preview_start({name: "aroma-wheel"})`, config in `.claude/launch.json`.

Wrap every probe in an IIFE. A bare `const` at top level throws `already been declared` on the
second run in the same tab. The console buffer **persists across reloads**, so a stale error from a
failed probe will look like a live one. Open a fresh tab to be sure.

```js
// dataset shape: expect 127 / 94 / 262 / 83 / 9
(function(){ return JSON.stringify({notes:NOTES.length, compounds:COMPOUNDS.length,
  edges:EDGES.length, visible:getVisibleNotes().length, groups:GROUPS.length}); })()

// the relationship engine, across four shapes
(function(){ const t=(l,e)=>{ setNotes(e.map(([note,intensity])=>({note,intensity})));
  return {t:l, rows:tastingRelationships().map(r=>r.headline)}; };
  return JSON.stringify([ t("citrus",[["lemon",7],["orange",6],["mint",5]]),
    t("cross-scent",[["rose",6],["almond",5]]), t("bridge",[["gardenia",5],["coffee",7]]),
    t("process",[["smoky",5],["caramel",5],["buttery",4]]) ],null,1); })()

// no note left with a broken Tree path: expect []
(function(){ const inTree=new Set();
  (function w(n){ if(n.noteId) inTree.add(n.noteId); (n.children||[]).forEach(w); })(buildTaxonomyTreeData());
  return JSON.stringify(NOTES.filter(n=>inTree.has(n.id)&&taxonPath(n).length<3).map(n=>n.id)); })()
```

---

## Remaining work, in priority order

### 1. Constellation's lenses link out to the tools — ⚠️ not built

Decision 4 above. Each lens should hand off to the tool that does it properly. The routing helpers
already exist and are used by the relationship rows: `runRelationshipRoute` (near
`tastingRelationships`, **10459**) and `openConstellationAt`. Lens switching is `cxSwitchLens`
(**12615**).

Embodied is the interesting one. `cxLegendFor` already states that its X axis reads *"real phase
tags from your actual tasting"* — the exact data the Go Deeper commit buttons produce. Pointing it
at the phase-tagging input closes a loop that already exists in the code and is simply not drawn.

### 2. Go Deeper still explains nothing — ⚠️ CLAIMED

`openDepthCard` is never called from the toggle. Pressing Go Deeper now plays the warp and sets the
mode, and that is all. Proposal: call `openDepthCard(1)` once on the first off→on flip, gated on
`state.dismissedHelpers`. Handler is at the foot of the warp block, `setGoDeeper` **12728**.

### 3. The sixth depth has no entry point — ⚠️ CLAIMED

`DEPTH_STORIES` (**11824**) has six entries. `#deeper-vines` (**4056**) has five
`.vine-leaf[data-depth]` elements, and its `aria-label` says "Five depths". The sixth is the one
that explains Constellation.

### 4. Compare panel follow-ons — ⚠️ CLAIMED

Its crossover is unhidden now, but the panel still has gaps.

| Item | Anchor |
|---|---|
| Six layer cards name Tree, Map, and Constellation and route to none of them | `taxonomyComparisonExpandedLayersHtml` **16297** |
| Never reads the live tasting, so it is a detached lookup | `renderTaxonomyCompareResult` **16371** |
| Never seeds from the tasting just built | `renderTaxonomyComparePanel` **16432** |
| Zero-overlap is a disclaimer, not a finding. Compare compound classes instead | **16410** |
| Dead "Climate — awaiting sourced data" card on every comparison | **16366** |
| Unescaped `"` inside a `title=` attribute. Four compounds contain literal quotes | `taxonomyComparisonChartHtml` **16223** |
| Escape closes the definition popover without restoring focus. **The one finding that survived adversarial verification** | `renderTaxonomyCompoundDefinition` **16150** |

### 5. Canonical vocabulary, then one sweep — ⚠️ CLAIMED

Largest item here, least urgent, touches hundreds of strings for no behavior change. **Do not start
it in the same session as a feature** — the combined diff becomes unreviewable.

| Concept | Use | Retire |
|---|---|---|
| The thing you slide | **note** (`aroma note` on first mention, aria-labels) | flavor note, tasting note, culinary aroma note, descriptor |
| The thing inferred | **compound** | molecule, odorant. Keep "molecule" for structural statements only |
| The 9 wheel sectors | **scent family** | note group, aroma family, flavor family |
| The wheel widget | **Radar** | Compass (Map only) |
| Saved tasting state | **snapshot** | lap |
| Constellation's four views | **lens** | mode, view |
| Go Deeper's six stories | **depth** | lens |
| Side panes | **Notes panel**, **Results panel** | sliders pane, analysis pane, Compounds pane |
| `edge.w` | **link strength** | weight, base weight, signal, evidence strength |
| `comparisonData.score` | **shared-compound overlap** | weighted aroma overlap, Jaccard, correlation view |
| Clearing entries | **Clear tasting** | Start Over, Clear |

Known offenders: eleven semicolons in interface copy, "X, not Y" framing across every explanatory
surface, and the alcohol-led empty state (**4088** area, IPA sits second of eight demo chips against
the standing rule that the audience priority is non-drinkers).

`FLAVOR_COMBOS` (**10324**) also leads with Mulled wine, Mojito, and Piña colada. ✅ VERIFIED these
fire and render. Consider drink-free framings.

### 6. Style rules for anything you write

No semicolons. Minimal em dashes. No "not X, it's Y" contrastive framing. No persuasive or defensive
tone. Keep real scientific terms, using the actual word is the honest representation. Never lead
with wine, beer, or spirits. Never fabricate a citation, surface honest gaps explicitly.

---

## Closed, with the reason

- **Tier 4, the Go Deeper reveal mechanics audit.** Mostly moot. `a6bdf5e` deleted the morph, and
  timer lifetime, overlay cleanup, and mid-animation Escape were all questions about that code.
  What remains is the warp itself, which is a self-contained two-timer fade.
- **Promoting `#constellation-toggle` to a header child.** Nolan wants the tools in the hamburger.
  It stays in `#hud-extra`.
- **Data integrity sweep.** ✅ VERIFIED clean: no dangling ids in `EDGES` or `NOTE_ORIGINS`, and the
  WAIS-points-at-an-invisible-note bug that bit twice before has not recurred.

## Never audited

❓ The **data compatibility** lens died before returning anything. Batch 3's direct verification
covered the Tree and the Map, but `DELIVERY_CONDITIONS` (**6477**) and `GUIDE_MOUTH` coverage were
never checked note by note.

## Before opening the PR

Re-run the probes above. Check the console on a **fresh tab**. Test at **360 × 760** portrait per the
mobile-first contract in `CLAUDE.md`, with all four of Wheel, Map, Tree, and Constellation loading
and switching cleanly. Record viewports and interactions in `.claude/codex-handoff.md`, and do not
claim a physical-device result unless it ran on that device.

**Do not open the PR without an explicit go-ahead from Nolan naming this branch and the target.**
