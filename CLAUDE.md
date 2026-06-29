# Branching workflow

Source of truth for how branches, tags, and PRs flow in this repo. Update this file first when the workflow changes, then propagate to agent memory.

## Long-lived branches

- **`main`** — production. Reflects the last shipped baseline. As of 2026-05-31 (PR #5, merge commit `74bd1ef`), `main` is caught up to `prototype` — V2 and the Compound library have been promoted. Only merge here via PR once changes are tested and the user explicitly says it's ready to ship.
- **`prototype`** — the **deploy / staging branch** and the day-to-day source of truth for the live app. Netlify deploys from here to https://aromawheel.net. Treat as semi-stable: only land work here that's coherent on its own. Day-to-day exploration happens on branches *off* `prototype`, not directly on it. Expect `prototype` to drift ahead of `main` between promotions.

## Short-lived branches

- **`feature/*` or `claude/*`** — branched off `prototype` (or off a long-running dev branch, see below) for a specific scoped change. PR back to whichever branch you branched from. Delete after merge.

## Long-running dev branches (for multi-slice work)

When a body of work is big enough to need multiple coherent commits before it's ready to merge into `prototype`, give it a dedicated long-running branch off `prototype`. Rules:

- Each slice lands as a commit (or a small PR into the long-running branch from a short-lived sub-branch if review checkpoints are wanted).
- The long-running branch has **one tracking PR** open against `prototype`, kept in **draft** until the whole body of work is ready.
- The tracking PR's description lists slices so reviewers (and future-you) can see progress at a glance.
- Do NOT auto-merge the tracking PR. Wait for explicit approval before merging into `prototype`.

### Current feature branches (in flight)

- **`claude/mobile-ui-pass-3`** — branched off `prototype` on 2026-06-27 (right after PR #14 merged). Tracking PR **[#15](https://github.com/iconic-orion/iconic-orion/pull/15)** opened 2026-06-28, kept in **draft** against `prototype` — ready to merge in one click once herb/floral slice lands and Nolan signs off. Scope has grown beyond mobile UI to include a flavor-note nuance pass (see below); kept on this branch per explicit call rather than splitting it out.
  - **Committed** (`7222ecc`): Compass widget mobile sizing + label-clipping fix; note-row slider scroll-conflict fix (33% width, left-justified); first new-notes slice — Coconut, Pistachio, Pecan (Nutty), Ginger (Spice), and the six grains collapsed into one "Cereal / grain" quick-use slider (Rice/Wheat/Barley/Oats/Millet/Quinoa kept as data-only `subOf: "cereal"` children — own compound/citation/map pin, but no slider of their own, surfaced only via a live-computed Go Deeper comparison table). New `sulfide` compound class (barley's dimethyl sulfide).
  - **Committed** (`155bc39`): citrus sub-categorization, generalizing the same `subOf`/Go-Deeper-table mechanism (renamed `varietalRows(parentId)`, no longer cereal-specific) to lemon/orange/grapefruit. Added Lime, Yuzu, Meyer lemon (subOf lemon); Mandarin/tangerine, Bergamot, Blood orange (subOf orange); Pomelo/pummelo (subOf grapefruit) — each with a sourced distinguishing compound except Blood orange, which honestly has none (its identity is anthocyanin pigment, not aroma — surfaced via a new `noStandoutNote` override field rather than invented chemistry). Grapefruit's own edges gained nootkatone, its actual textbook signature compound.
  - **Committed** (`aa2b4cd`): berry sub-categorization — Cranberry, Red currant, Black currant/cassis, Pomegranate (all subOf berry). Cassis reuses 4MMP (already in the data, tied to passionfruit) as its textbook signature thiol. Pomegranate gets a new compound, acetoin. Red currant is the honest "no confirmed standout" case here (no dedicated study found, left without a `noStandoutNote` so the generic fallback renders rather than a fabricated explanation). Cranberry's first-choice compound (β-ionone) turned out to already be one of berry's own parent-level edges from an earlier differentiation pass, so it wouldn't have shown as "distinguishing" — swapped to (E)-2-nonenal, also confirmed in the same source study and not already on berry's edge list.
  - **Committed** (this commit): mint sub-categorization — Peppermint, Spearmint, Wintergreen (subOf mint). Menthone for peppermint, L-carvone for spearmint, methyl salicylate for wintergreen — all clean, well-documented, no honest-gap cases this time. Wintergreen's note text flags that Gaultheria procumbens isn't actually in the mint family at all, just grouped in by flavor convention.
  - **Committed** (this commit): herb/floral sub-categorization — Eucalyptus (subOf pine), Sage and Thyme (subOf lavender), Orange blossom and Honeysuckle (subOf jasmine). Aromadendrene for eucalyptus, α-thujone for sage, thymol for thyme, methyl anthranilate for orange blossom (reuses the existing `methanthr` compound, already in the data for grape), farnesol for honeysuckle — all clean, well-documented, no honest-gap cases. Fixed a latent `formatRefFull` bug while adding the first book-type entry to the EDGES-citation `REFERENCES` object (book refs only previously existed in the separate Origins-map `ORIGIN_REFERENCES` object, which has its own renderer). Also fixed a pre-existing bug in `.claude/launch.json`'s static-server script (`SendChunked` conflicting with an implicit content-length) that broke local preview entirely.
  - All five queued families now landed; this branch's flavor-note nuance pass is complete.
  - **Committed** (this commit): fixed a latent bug spanning the whole varietal-table feature (citrus through herb/floral) — 16 "What am I smelling?" word-bank (`WAIS_DESCRIPTORS`) entries pointed only at `subOf` notes (lime, yuzu, meyer lemon, mandarin, blood orange, pomelo, cranberry, red currant, peppermint, spearmint, wintergreen, orange blossom, honeysuckle, eucalyptus, sage, thyme). Since `subOf` notes are filtered out of the visible-notes list, clicking those descriptor chips silently produced zero suggestions. Repointed each at its visible parent note (e.g. "thyme" → lavender, "cranberry" → berry).
  - **Committed** (this commit): new Phase 1 plant-taxonomy layer, additive alongside the existing flavor-category `GROUPS` (kept primary and unchanged, per explicit call). New optional `family`/`genus` fields on `NOTES`, seeded only for a curated, verified set: Citrus genus (lemon/orange/grapefruit, Rutaceae), Rosaceae (apple/stonefruit/cherry/raspberry/strawberry/blackberry — Fruity group — plus Rose/Floral and Almond/Nutty, which cross group boundaries; stonefruit/cherry/almond share the tighter genus *Prunus*), Lamiaceae (mint/Earthy + lavender/Floral, cross-group), Solanaceae (bell pepper + tobacco, same group), Poaceae (cereal/toast/burnt, same group; quinoa, a hidden `subOf:"cereal"` child, is honestly Amaranthaceae — a pseudocereal, not Poaceae). Four new UI surfaces: (1) in-group taxon sub-headers in the note-selection panel that pull same-family notes together (`buildNotesPanel()`); (2) a small 🧬 cross-group badge on notes whose family tie crosses a flavor category with no in-group cluster to anchor to (rose, almond, mint, lavender), click-to-jump to the first cross-group sibling; (3) a "Plant taxonomy" section in the Go Deeper note-detail panel listing all family siblings as clickable `.view-note` links; (4) an auto-generated "taxonomic surprise" sentence in the existing varietal comparison table whenever a `subOf` child's family differs from its parent's (fires for quinoa vs. cereal, wintergreen vs. mint; silent for non-mismatches) — needs no new prose, just the `family` field. Explicitly out of scope this pass: the wheel's ring layout, the legend, and exhaustive family/genus coverage of all ~86 notes — queued as natural follow-ups.
  - **Committed** (this commit): **Phase 2 — a third full-screen workspace**, "Tree," peer to Wheel and Map (`#workspace-tabs` extended from 2 buttons to 3; `setOriginsMode()` generalized to `setWorkspace(mode)`). Shows **all 86 `NOTES`** (including every `subOf` varietal child the wheel/map/panel intentionally hide) as a horizontal collapsible `d3.tree()` dendrogram — Kingdom → Order → Family → Note, the same depth as a real phylogenetic tree, not just the Phase-1 family layer. Extended `family`/`genus` with new `order`, `kingdom` (default `"Plantae"`), and `taxonBucket` (`"process"` | `"umbrella"`) fields, seeded across every note this time. Two honest non-phylogenetic buckets sit alongside the biological kingdoms rather than inventing taxa: **"Process / not a single organism"** (skunky, buttery, smoky, musty, cardboard, sulfury, sweaty, cheesy, winey, caramel, cottoncandy) and **Plantae "(multiple families)"** (berry, green, anise — real plant-derived but spanning unrelated families; anise/licorice specifically conflates *Illicium*/Schisandraceae and *Glycyrrhiza*/Fabaceae, a convergent-flavor case like wintergreen). New honest taxonomic mismatches surfaced once `subOf` children got full data: eucalyptus is Myrtaceae (not pine's Pinaceae), honeysuckle is Caprifoliaceae (different order from jasmine's Oleaceae), orange blossom is literally orange's own flower (Rutaceae, nothing like jasmine). Clicking a tree leaf reuses the exact same `renderDetail()`/`aside.detail` panel the wheel uses — found and fixed a real crash in the process: the Phase-1 "Plant taxonomy" detail section computed siblings from `getVisibleNotes()`, which excludes the very `subOf` note being displayed, crashing `taxonClusterLabel()` on `undefined`. Fixed by pooling from `NOTES` instead — also fixed cassis/redcurrant's sibling list as a side effect (they're both genuinely Grossulariaceae and now show each other). New `taxonPath()`/`buildTaxonomyTreeData()` helpers; tree search (`applyTaxonomySearch`) auto-expands collapsed ancestors of any match. Taxonomy data verified via targeted web search this session (riskiest calls: maple→Sapindaceae, pineapple→Poales, baker's-yeast and honeybee taxonomy, passionfruit→Malpighiales). Out of scope: radial tree layout, retrofitting the Map's pan/zoom math onto the tree, and a rank beyond Order/below genus.

Recently merged into `prototype`:
- **`claude/ui-pass-2`** — PR **#9** (merged 2026-06-10, merge commit `d4f41cd`). Second UI pass following PR #8: nudge copy simplification, ••• toggle pinned top-right so the mobile header never wraps, nudge dark-pill background + width clamp to fit inside the wheel's ring interior on phones, wheel pane grown 44vh→46vh with ring radius 0.32→0.36, favicon (8-wedge color ring), mobile header collapsed to `[Aroma Wheel] [•••]` with Start Over always visible and Dashboard tab hidden (redundant with Notes in single-column), tray restructured to a 2-col grid with View label + divider. Branch safe to delete.
- **`claude/upbeat-mendel-6ef2f6`** — PR **#14** (merged 2026-06-27). Compound-library restoration (a stray local `WIP: epitaxy pre-switch` commit had reverted it out of the working tree, since fixed), a Go Deeper scope cleanup (full citations and the note inverse-view click no longer require Go Deeper — it's now just the ortho/retro commit-button toggle), device-motion Jiggle (now in a settings gear dropdown), typeable note intensity, a five-ring event-horizon warp transition, and the **Perception Compass** — a draggable, resizable corner radar widget with Notes / Compounds / Class axis modes (Class is a dropdown over all 17 chemical classes, terpene default) — plus a header reorganization (Wheel/Map workspace switch, Compass promoted to the header, Settings now Jiggle-only). An earlier full-wheel Starburst display-shape toggle was built then reverted; the radial chart lives only in the Compass. Branch safe to delete.
- **`claude/upbeat-mendel-6ef2f6`** — PR **#13** (merged 2026-06-25). Origins map: compass-icon toggle on the wheel opens a full-screen world map of ingredient cultivation regions (pre-Columbian Exchange framing), synced note selection, scroll-zoom/drag-pan, neighbor-aware label layout.
- **`claude/thirsty-dijkstra-de159b`** — PR **#8** (merged 2026-06-10, merge commit `4c074d0`). UX pass: first-run nudge, mobile single-column breakpoint (≤760px), compound callout labels (mobile toggle with leader lines), collapsible HUD header (view tabs always visible, ••• expands secondary controls), float-label de-clutter, data palette saturation pass, copy polish (em-dash strip, Note Suggester pruning, Methodology sources note). Branch safe to delete.
- **`feature/compound-lens`** — PR **#7** (merged 2026-06-06, merge commit `bdb8039`). Branch deleted.
- **`claude/header-cleanup`** — PR **#6** (merged 2026-06-06, merge commit `d96ebaa`). Branch safe to delete.

`prototype` is now ahead of `main` by PRs #6, #7, #8, #9, #13, and #14. `claude/mobile-ui-pass-3` is the only branch active off `prototype`.

### Historical: V2 (shipped 2026-05-26)

- Branch: **`claude/vigilant-lovelace-2cb582`** — now stale; `prototype` is ahead of it. Safe to delete locally.
- Tracking PR: **[#4](https://github.com/iconic-orion/iconic-orion/pull/4)** — **merged** 2026-05-26.
- Merge commit on `prototype`: `20643d3` (tagged **`v2`**).
- Slices delivered: (1) ortho/retro foundation, (2) three view modes + responsive layout, (3) "i" info tab with About / How to Use / Types of Aroma, (4) Go Deeper additional contents, (5) mouthfeel dimension as its own tab, (6) nudge / search / visible word bank, (7) perceptual-tone copy pass.

## Flow at a glance

```
feature/X ──PR──▶ prototype ──PR──▶ main      (small self-contained changes)

(future long-running work) ──PR──▶ prototype ──PR──▶ main
   ▲
   │ slice commits accumulate here
```

## Tags

Tags mark historical snapshots. Recover any with `git checkout <tag>`. Both are pushed to origin and visible in GitHub's Tags / Releases UI.

- **`v1`** → commit `f066d15` — first workable HTML prototype, captured before V2 design changes. Historical snapshot.
- **`v2`** → commit `20643d3` — the moment V2 landed on `prototype` (merge of PR #4, 2026-05-26). Historical snapshot; `prototype` has continued forward since.

`prototype` is always newer than the highest-numbered `vN` tag.

## Branch protection (set in GitHub UI)

On `main`:
- Require pull request before merging
- Require status checks to pass
- Disallow direct pushes

## Worktrees

This repo uses **Claude Code worktrees** (under `.claude/worktrees/`) so multiple agent sessions can work on different branches in parallel without stepping on each other. Each worktree is a separate working directory checked out to one branch.

All current `.claude/worktrees/*` directories — including `vigilant-lovelace-2cb582/` — are **historical leftovers from the V2 era**. None are canonical anymore. They're safe to ignore, or to clean up with `git worktree remove <path>` if you want a tidier filesystem. The matching `claude/*` branches (sad-beaver, frosty-hoover, blissful-franklin, etc.) are all behind `prototype` with zero unique commits — they can be deleted without losing work.

When new long-running work starts, create a fresh worktree off `prototype` and document it here.
