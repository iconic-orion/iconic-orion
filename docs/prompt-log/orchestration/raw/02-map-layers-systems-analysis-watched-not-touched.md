# 02 - Map-layers systems analysis, watched not touched

- **Date:** 2026-07-26 to 2026-07-27
- **Source:** Claude Code session `b91c5e6b`, branch `codex/aroma-wheel-responsive-ux-pass`
- **Agent calls:** 10
- **Provenance:** transcript-backed (verbatim, extracted 2026-08-15)
- **Companion:** also indexed in the human prompt log as [entry 36](../../raw/36-session-handoff-thesis-systems.md). Entry 36 describes this session as resuming a map-layers systems-analysis workflow from a written handoff doc, run in parallel with a near-duplicate session (see 03 in this archive, `def702be` / prompt-log entry 37) - the two sessions share the identical first 10 Agent-tool dispatches below (same prompts, same tool-use ids, same results), then diverge: this session (`b91c5e6b`) ends here, while `def702be` continues on with further human-directed work but no additional Agent-tool calls.

The prompt-log entry frames the human instruction behind this whole batch plainly: watch the parallel ChatGPT/Codex work on the map without interfering, "codex has a special way with geographic data that i want you to watch." The ten dispatches below are Claude's own research/design/audit work running alongside that, not a response to ChatGPT's edits directly.

---

### 1 - Jul 27, 01:07
**Description:** Survey Origins Map data model
**Subagent type:** Explore
**Prompt sent:**
> You're auditing the Aroma Wheel app's Origins Map feature. This is a single-page app; all the code is in `D:\Git_NAE\index.html` (it's a large file — search rather than reading linearly). The Origins Map is a full-screen workspace mode showing an embedded world SVG with markers for where each aromatic-note ingredient originated/was cultivated pre-Columbian-Exchange.
> 
> Context: the app's thesis is perception → notes → compounds → families → lineage → geography, and the Map is the geography terminus. The team wants to add TWO new map layers on top of the existing "origins" layer: (b) economic cultivation (where a plant is grown most today, by production volume) and (c) cultural/culinary value (where it's most prized). Before anyone designs those layers, we need hard facts about what the current map can technically support.
> 
> Answer these specifically, quoting exact code (file:line) wherever possible:
> 
> 1. **The make-or-break question**: does the embedded world SVG template have region/country `<path>` elements with usable `id` attributes (e.g. ISO country codes, region names) that could be targeted for a choropleth/region-fill layer? Or is it purely a coastline/landmass silhouette with point markers layered on top, with no addressable per-region geometry? Search for the SVG definition (likely a large inline `<svg>` block or template string) and describe exactly what's there — element types, how many distinct addressable regions if any, whether it's a real projection (which one, if identifiable) or a stylized/simplified map.
> 
> 2. **`NOTE_ORIGINS` (or equivalently-named) data structure**: find the object/array that maps notes to origin locations. What's the exact record shape (fields, types)? What coordinate system do origin points use (lat/lng, or SVG-local x/y, or something else)? How many notes currently have origin data vs. how many notes exist total in the app?
> 
> 3. **`ORIGIN_REFERENCES`**: find the citation-backing object for origin claims. What's its shape, and roughly how is it rendered/displayed to the user (badge, footnote, etc.)?
> 
> 4. **The pre-Columbian-Exchange framing paragraph**: find the actual prose in the UI that frames the map's historical/geographic scope (likely an intro blurb or tooltip near the map). Quote it VERBATIM, with file:line.
> 
> 5. Briefly describe the map's current interaction model: pan/zoom implementation, how markers render, whether there's already any concept of a "layer" or "mode" toggle on the map (vs. just one fixed marker set), and any existing legend/filter system specific to the map (distinct from the wheel's legend).
> 
> Report factually and precisely — this is a technical feasibility audit, not a design proposal. Do not propose solutions, just report what exists. Keep your final report well-organized under these 5 numbered headers, with file:line citations for every claim.

**Result (as captured):** technical feasibility audit of the embedded world SVG - found 470 `<path>` elements, ~219 distinct addressable country/territory identifiers (169 unique `id`s plus 50 grouped `class` names), confirmed a choropleth is technically possible but not wired up (every path currently shares one uniform CSS fill), found the map is a stylized/hand-simplified decorative map rather than a rigorously projected one (Australia's path bbox disagrees with the app's own `latLonToXY()` formula by 20-30 degrees of latitude), reported `NOTE_ORIGINS` covers 85 of 119 notes, and confirmed no layer/mode toggle concept exists on the map today.

---

### 2 - Jul 27, 01:07 (dispatched right after call 1)
**Description:** Survey map-layer data sourcing honesty
**Subagent type:** general-purpose
**Prompt sent:**
> You're doing a rigorous, skeptical data-availability audit for a proposed feature on the Aroma Wheel app (a sensory-to-chemistry-to-geography educational tool, code at `D:\Git_NAE\index.html`). The team wants to add two NEW map layers on top of an existing "historical origin" layer that shows where ~90+ aromatic plant/food ingredients (coffee, citrus fruits, spices, herbs, vegetables, etc.) originated pre-Columbian-Exchange:
> 
> (b) **Economic cultivation layer** — where each ingredient is grown MOST today, by production volume (i.e. current top-producing countries/regions).
> (c) **Cultural/culinary value layer** — where each ingredient is "most prized" culturally/culinously.
> 
> This project has a hard, previously-tested standing rule: **never fabricate citations or data**. Every claim in the app must trace to a real source a human has actually opened and confirmed — no plausible-sounding but invented figures, no "AI-typical" citation hallucination. A near-miss already happened once this project (an agent nearly fabricated a patent inventor name) and was caught.
> 
> Your job — pure research/assessment, do NOT write any code or design anything:
> 
> 1. **For layer (b), economic cultivation**: name REAL, currently-existing authoritative data sources for global crop/ingredient production statistics — the kind of organizations that actually publish this (e.g. FAO/FAOSTAT, USDA, and any others you're confident genuinely exist and publish this class of data). For 4-5 example ingredients from a typical flavor/aroma dataset (e.g. coffee, vanilla, black pepper, citrus, cacao), describe in GENERAL TERMS what kind of production-ranking data would likely be available (e.g. "FAOSTAT publishes annual production-volume-by-country tables") WITHOUT inventing specific numbers, specific years, or specific rankings you haven't verified — if you're not certain of a real figure, say so explicitly rather than guessing. Flag clearly: is this the kind of data that's freely/publicly accessible, or does it require licensing/paid access?
> 
> 2. **For layer (c), cultural/culinary value — this is the dangerous one.** "Cultural value" or "most prized" is not a measured quantity like production tonnage. Assess honestly:
>    - Does ANY defensible, citable methodology exist for this at all (e.g. import/export price premiums as a proxy, protected-designation-of-origin registries like PDO/PGI/AOC, culinary-heritage UNESCO listings, price-per-kg as a market-value proxy)? Distinguish real measurable proxies from pure vibes/opinion.
>    - What's the risk that this layer, if built naively, ends up presenting one culture's or one author's opinion as objective data, or essentializes/flattens a culture's relationship to an ingredient into a single glib label?
>    - Give a genuinely honest verdict: is there a version of this layer that would survive this project's "a human personally verified a real source" bar, or does the underlying concept not actually support that bar no matter how it's implemented? Don't hedge to be agreeable — if your honest assessment is "this shouldn't be built as stated," say that plainly.
> 
> 3. Flag any other real risk you notice (e.g. production data changes year to year and could go stale/misleading if hardcoded without a date; conflating a country's TOTAL production with an ingredient's percent of that country's economy; treating colonial-era or currently-disputed-territory production data neutrally).
> 
> Report your findings under these 3 numbered headers. Be precise about what you know vs. don't know — explicitly say "I don't have a verified figure for X" rather than filling gaps with plausible-sounding numbers.

**Result (as captured):** data-sourcing honesty audit against the project's "a human personally verified the source" citation bar. Verdict on layer (b), economic cultivation: buildable, real free sources exist (FAOSTAT, USDA FAS PSD Online, UN Comtrade; ICO/IPC partially paywalled), no specific figures verified yet. Verdict on layer (c), "cultural/culinary value": explicitly **should not be built as stated** - no institution measures "most prized" as a comparable cross-culture metric; recommended a narrower "documented designations" (PDO/PGI/UNESCO) feature instead, with honest empty-case coverage. Also flagged staleness, production-vs-economic-significance conflation, and disputed-territory neutrality risks.

---

### 3 - Jul 27, 01:17
**Description:** Design thesis-chain mapping
**Subagent type:** general-purpose
**Prompt sent:**
> You're doing design/analysis work (no code changes) for the Aroma Wheel app (`D:\Git_NAE\index.html`), a sensory-to-chemistry-to-geography educational tool. The user's own stated thesis for the whole tool:
> 
> > "All these views and tools are to enhance the ability to organize human perception and analyze connections in the database from those perceived notes they inputted. Really the whole tool is expanding off of perception to try to deduce geographic lineage of plant families."
> 
> Chain: **perception → notes → compounds → families → lineage → geography**
> 
> A prior research pass (feature-inventory audit) already surveyed the whole codebase against this chain and found the following facts — treat these as verified ground truth, don't re-derive them:
> 
> **State-sharing architecture:** Wheel/Notes/Detail state lives in a shared `state` object (`state.selectedNote`, `hiddenGroups`, `entries`, etc.) readable across surfaces. But Map, Tree, Compass, and Share each keep their REAL working state in module-local JS variables (`mapView`, `taxTreeRoot`, compass position vars, the share module's private `opts`) that nothing outside those surfaces can read or restore. This is why a share URL can encode a tasting but not a view.
> 
> **The chain is literally coded as a comment**: the Tree's own path readout (`#taxonomy-path-readout`) says "Family is the chemistry clue" — the single most direct in-UI statement of the thesis. The Map's own internal `chainStep` comment says verbatim: "lineage → geography. The endpoint of the thesis chain."
> 
> **One reverse edge already exists**: clicking an origin marker on the Map for a not-yet-entered note commits it at intensity 5 — a small but real geography → perception edge, contradicting a purely-forward reading of the chain.
> 
> **Nine "islands" already named, each with a specific coded reason:**
> - **Tree** — zero reference to `state.entries` or any score; what you tasted is invisible to it.
> - **Delivery** (temperature/effervescence/agitation/breath dimension) — code comment literally says "nothing here touches recompute()."
> - **Laps** (the tasting-stopwatch/history feature) — comment says "nothing downstream knows laps exist"; laps can only be previewed one at a time, no compare-two-laps view; the temporal dimension never reaches the inference chain.
> - **Share card** — reads no `state.*` field at all, has its own private snapshot; silently ignores legend filters and drops the families/lineage step entirely from the one artifact that leaves the app.
> - **Compass "Class" mode** — never calls `isCompoundVisible()`, silently ignores the legend's hidden-classes filter that Notes/Compounds modes respect.
> - **Map legend filters** — `originsHiddenGroups`/`originsOnlyTasting` are a second, never-synced visibility system parallel to the Wheel's own `state.hiddenGroups`; this is a documented-as-deliberate design choice in the code, not an oversight, but user-facing it still means hiding a group in one place does nothing in the other.
> - **Go Deeper depth cards** — hardcoded prose that names the thesis chain more explicitly than any computed surface, but has zero inbound data; never reflects what the user actually tasted.
> - **Bouquet readout / FLAVOR_COMBOS** — "the one surface that does cross-note synthesis bypasses the taxonomy layer entirely"; matches hardcoded note-id slot lists, ignores family/genus/order.
> - **Three independent search boxes** (Notes/Map/Tree) — three different implementations, zero shared query state.
> 
> **Also found:** `state.sortBy` is dead code (declared, never read). The family detail page (richest single payload explaining "why relatives share aromatic pathways") is reachable ONLY from a Tree family-node click — no path to it from the Wheel, notes panel, or Map.
> 
> **Your job:** produce the core intellectual deliverable — map every one of these surfaces (Wheel, Notes panel, Detail panel, Map, Tree, Compass, Share, Go Deeper/depth cards, Bouquet, Laps, Delivery, search) onto the six-link chain (perception → notes → compounds → families → lineage → geography). For each surface:
> 1. Which link(s) of the chain does it actually serve?
> 2. Grade that service **strong / partial / weak / missing**, and say why in one sentence grounded in the facts above (not vibes).
> 3. Name the specific "seams" — points where a user's attention has to cross from one feature to another to keep following the chain — and say plainly whether that crossing currently WORKS (state carries over, framing is consistent) or BREAKS (state resets, no visual/narrative bridge, an island).
> 
> Then answer directly: of the disparities you find, which are **defects** (should be fixed — the chain genuinely breaks) vs. which are **correctly separate concerns** (e.g. maybe Delivery SHOULD stay outside the compound-scoring chain, because it's about physical presentation not chemistry — argue it, don't just assert it)? You are explicitly told to reach uncomfortable conclusions if warranted — this is a real critique, not a design pitch. Don't flatter the existing architecture.
> 
> End with a short ranked list: which 3 seam-breaks would most strengthen the "this is one coherent chain, not a pile of features" reading if fixed, and roughly why each ranks where it does.

**Result (as captured):** graded every major surface (Notes panel, Wheel, Detail panel, Map, Tree, Compass, Share, Go Deeper cards, Bouquet, Laps, Delivery, search) against the app's own perception-to-geography thesis chain as strong/partial/weak/missing, with reasons grounded in traced code rather than feature names. Ranked the three seam-breaks most worth fixing: (1) Tree never reading `state.entries`, (2) the Map's marker detail never showing family/genus/lineage, (3) the Share card dropping family/lineage and running a third, unsynced compound-visibility filter. Also argued that Delivery staying outside `recompute()` is a correct, deliberate honesty boundary, not a defect.

---

### 4 - Jul 27, 01:17 (dispatched right after call 3)
**Description:** Design multi-layer map
**Subagent type:** general-purpose
**Prompt sent:**
> You're doing GIS/UX design work (no code changes yet — this is a design proposal to review, not an implementation) for the Aroma Wheel app's Origins Map (`D:\Git_NAE\index.html`), a sensory-to-chemistry-to-geography educational tool. The map is the "geography" terminus of the app's thesis chain: perception → notes → compounds → families → lineage → geography.
> 
> **A technical feasibility audit of the current map ran this session. Treat these as verified facts, don't re-derive them:**
> 
> - The embedded world SVG (`<template id="world-svg-tpl">`, index.html:11961-12910, viewBox 2000×857) has **470 `<path>` elements**: 169 carry unique `id` attributes (ISO-2-style country codes, e.g. `id="AF" name="Afghanistan"`) and 301 more are grouped under 50 unique `class="<Country Name>"` values for multi-part countries (islands/exclaves). Combined: **~219 distinct addressable country/territory identifiers** — real per-region geometry, not a silhouette blob. 3 micro-states exist as hidden `<circle>`s. Antarctica is absent.
> - **BUT it's not a rigorously projected map.** Cross-checking known-location country bboxes against the app's own `latLonToXY()` linear (Plate-Carrée-style) formula shows real disagreement (Australia's mainland bbox is off by ~20-30° of latitude from where the formula would place it). ViewBox aspect ratio (2.33:1) isn't a standard equirectangular 2:1 either. **Conclusion: it's a stylized/hand-simplified decorative map, not a survey-accurate projection** — good enough for approximate region-level choropleth, not for anything requiring geometric precision.
> - **Choropleth is technically possible but not wired up today.** Currently ALL 470 paths get one uniform CSS fill (`#map-svg-container path { fill: var(--panel-2); ...}`, index.html:1742-1748) and are re-parented into a single `<g class="land">` specifically so a drop-shadow filter treats the whole landmass as ONE silhouette (index.html:10401-10408) — nothing today differentiates fill per-region. Building a choropleth means adding new per-region fill logic keyed off the existing `id`/`class` attributes; the geometry supports it, the current styling actively works against it.
> - **`NOTE_ORIGINS`** (index.html:3664-3933): 85 of 119 notes have an origin entry — `{region, lat, lon, certainty: "known"|"approximate", country?, cultivationDate?, modernNote?, citeKeys?}`. 34 notes deliberately have none (generic/process notes like "green" or "cardboard" — no forced/fabricated placement). Framing is explicitly **pre-Columbian Exchange**: "where a plant was cultivated or first used by humans before 1492 European contact, not necessarily where it is grown commercially today" (verbatim, index.html:2597) — this is the SINGLE existing layer's framing, shown once as a fixed footer.
> - **No layer/mode concept exists today** — one marker set (origins), one land layer, no toggle. Map-local legend filters (per-aroma-group + "only my tasting") are already a second visibility system parallel to the Wheel's own legend, deliberately unsynced.
> - Markers are colored by **aroma group** (not geography), clustered with leader lines (solid=known/dashed=approximate placement confidence), built fresh on every state change from `NOTE_ORIGINS`.
> 
> **A parallel data-availability audit ran this session on the two NEW layers being proposed. Treat this verdict as final for this design pass — do not re-litigate it:**
> 
> - **Layer (b), economic cultivation** (where each ingredient is grown MOST today by production volume): **buildable.** Real free sources exist — FAOSTAT (245+ countries, 173 products, free), USDA FAS PSD Online (free, US-trade-skewed), UN Comtrade (free tier). No specific figures have been verified yet — that's future human-sourcing work, not a blocker to designing the layer's shape.
> - **Layer (c), cultural/culinary "most prized" value**: **audited and rejected as originally scoped.** No institution measures this as a comparable cross-culture metric; the audit's explicit verdict was "this should not be built" as a synthesized "most prized" score, because it can't clear this project's human-verified-real-source citation bar (verifying a source exists doesn't verify its OPINION is objective truth about a culture). **A narrower alternative survived the audit**: a "documented designations" feature — individually-sourced PDO/PGI/GI registry entries (EU eAmbrosia, free, but Eurocentric in coverage) and/or UNESCO Intangible Cultural Heritage listings (real, ~50 entries, covers practices not ingredients) — most ingredients would simply have NO entry, and that gap should render as a visible gap, not be filled in. This is a smaller, differently-scoped feature than "cultural value," not a design constraint you need to solve around — **design for this narrower version, not the original "most prized" framing.**
> - Risk flagged for layer (b): production data goes stale year to year (needs a visible "as of [year]" vintage marker), raw tonnage can misleadingly imply "this country owns this ingredient" without per-capita/export-share context, and colonial-era production geography (e.g. why coffee/cacao are grown far from their origin today) needs acknowledgment in copy, not silent neutral presentation next to the origin layer.
> 
> **A separate opacity/stacking audit ran earlier this session and found this app already has a serious problem with alpha-layer stacking on mobile** (9 translucent layers compositing during one transition elsewhere in the app, 11 different `backdrop-filter` surfaces, etc.) — the team's explicit ask is "more layers, less opacity clutter," meaning **do not solve this by adding more translucent overlays that stack.**
> 
> **Your job:** design the actual GIS treatment for up to 3 layers (origins / economic cultivation / documented-designations-narrower-version-of-cultural) on this map:
> 
> 1. Choose real cartographic technique per layer — point marker vs. choropleth (region fill) vs. proportional symbol vs. something else — justified by what each layer's data actually IS (origins = point-in-time-and-place event → point marker fits; production volume = a per-region quantity → choropleth or proportional symbol fits; sparse designations = point-in-place-with-big-gaps → point marker or icon fits, NOT choropleth, since most regions would render as "no data" which reads badly as a fill).
> 2. Solve "3 layers, no opacity stacking" via technique, not alpha: e.g. one active layer at a time with a clear switcher (not simultaneous stacked layers), or distinct mark types that don't need transparency to coexist (e.g. opaque choropleth fill UNDER opaque point markers, since fill and point don't visually compete the way two translucent point layers would).
> 3. Design for the canonical mobile viewport, 360×760 (Galaxy S10e portrait) — where does a layer switcher live, how does someone read a choropleth legend at that width, do NOT assume desktop screen real estate.
> 4. Address the requested narrative payoff explicitly: for a given plant, origin ≠ economic-cultivation-today ≠ documented-designation-location can be a genuinely interesting story (e.g. coffee: origin Ethiopia, top production elsewhere, etc.) — the DISPLACEMENT between geographies is the interesting part. Design so that displacement is visually legible (e.g. a note's origin pin and its production choropleth region visibly disagreeing IS the point), not buried as a footnote three clicks deep.
> 5. Be concrete: name what UI element goes where, what happens on tap/click, what the legend looks like, what happens when a note has data for one layer but not another (the designations layer especially — most notes will have nothing, design the empty case as a first-class state, not an afterthought).
> 
> Do not design anything for "most prized" as a synthesized score — that door is closed per the audit above. If you think even the narrower designations layer has problems, say so, but your primary job is the cartographic/UX design, not re-auditing data honesty (a separate adversarial pass will do that next).

**Result (as captured):** published an interactive design-spec artifact (a claude.ai code artifact URL) for a three-layer map (origin points / classed choropleth for "grown today," scoped to one selected note at a time / point-marker "named and protected" designations), with a working 360x760 mobile mockup demonstrating a 4-state demo. Solved the "more layers, no more opacity stacking" constraint structurally (one overlay active at a time, everything stays fully opaque) rather than with alpha blending, and proposed surfacing the origin-vs-production displacement itself (e.g. vanilla: Veracruz origin vs. "Bourbon Vanilla" pointing to Madagascar) as the narrative payoff.

---

### 5 - Jul 27, 01:18
**Description:** Design layer-discipline rules
**Subagent type:** general-purpose
**Prompt sent:**
> You're doing design/analysis work (no code changes) for the Aroma Wheel app (`D:\Git_NAE\index.html`), a sensory-to-chemistry-to-geography educational tool with a naturalist/organic visual language (vines, strata, canopy-to-soil descent metaphors for its "Go Deeper" transition). The user has said they want to "limit how many layers use opacity" across the app. Your job is to turn that into an enforceable, codebase-specific rule set.
> 
> **An opacity/stacking audit already ran this session across the whole app. Treat these as verified facts — you're building rules FROM these findings, not re-auditing:**
> 
> - **Single highest-leverage fix**: `--line: rgba(210,226,218,.12)` on mobile (index.html ~1958 and ~2026 — this rule is duplicated across two separate mobile media-query blocks, more below) is the border color for nearly every element in the app below 760px viewport width. The desktop equivalent is opaque `#2a2730`. Making the mobile value opaque removes an alpha layer from hundreds of elements in one edit.
> - **Worst stacking chain — the Go Deeper warp transition**: for ~820ms, 9 translucent layers composite simultaneously (the live wheel, its evidence-strength alphas, 2 atmosphere gradients, a vine decoration, the tasting tray, the mobile header, all 5 warp strata — with `.warp-layer-1` itself at only 62% opacity, i.e. you see straight through the "descent" to everything underneath it — plus a `.prototype-watermark` at z-index 100000 compositing over literally everything including the warp).
> - **Other real stacking chains** (7-8 layers deep each): the mobile wheel band once any note is entered (`.lap-rail` physically overlaps `#callout-toggle` and `.wheel-hint` at the same coordinates); the Tree workspace on mobile with the detail sheet open + Go Deeper on (vines paint over the dendrogram, baked-in SVG opacity compounds inside an already-translucent sheet); the `.depth-card` Go Deeper story card (4 nested alphas in one 370px card before counting what's behind it); **11 distinct `backdrop-filter` surfaces exist across the mobile CSS**, several stacking directly (a comment at index.html:1380-1384 already documents blur roots fighting each other — a prior fix there was removing blur from ONE layer rather than reducing the layer count, i.e. the problem was patched locally once already without a systemic rule).
> - **The entire mobile media-query block is authored TWICE** (index.html:1945-2018 and 2019-2067 — same selectors, so nothing double-renders today, but every mobile alpha value currently must be edited in two places, and any future opacity-reduction pass will silently miss half the edits if this isn't deduplicated FIRST).
> - **Encoding vs. decorative split — this is the most important distinction, don't blur it:**
>   - **22 places where alpha does real informational work** (PRESERVE, do not flatten): evidence-strength ramps on the wheel (`.group-arc`, `.note-halo`, `.cpd-token`, and `.edge` stroke-opacity literally encodes edge weight × note signal — a real data encoding, not decoration), legend/search dimming (shows what's filtered out), ghost-row read-only state (visually distinguishes a mirrored/non-independent value from a real one), map marker active/dimmed state.
>   - **45 places are pure atmosphere/decoration** — fair game to cut or flatten to opaque tints (backgrounds, card treatments, decorative vine/strata overlays, etc. that carry no information, just mood).
>   - The audit's explicit design intent: cutting decorative alpha should make the 22 encoding cases read **HARDER**, not softer — right now a 0.16 evidence halo is competing for visual attention against things like a 0.82-opacity decorative vine and a 0.55-opacity decorative toggle box for no informational reason. Removing decorative alpha is partly IN SERVICE of making the real encoding more legible by contrast, not just a cleanup for its own sake.
> 
> **Your job — produce an enforceable rule set specific to this codebase:**
> 
> 1. **A strict layer budget**: how many translucent (non-opaque, alpha < 1) surfaces may visually stack at any single point on screen, with named exceptions (e.g. the wheel's own evidence-encoding layers might need their own higher local budget since they're intentionally multiple stacked alpha-encoded elements BY DESIGN — argue where the line is).
> 2. **A crisp rule distinguishing alpha-as-encoding from alpha-as-atmosphere**, phrased so a future contributor (human or agent) can apply it without re-deriving the whole audit — e.g. "if the opacity value changes based on user input/data, it's encoding; if it's a fixed value on a decorative element, it's atmosphere."
> 3. **A prioritized top-5-by-impact change list** with exact selectors from the audit above (the mobile `--line` var, the warp transition's `.warp-layer-1`/`-2`, the duplicated media-query block, the `.lap-rail` overlap, the `.depth-card` nesting) — ranked by (impact of the fix) × (how many other things depend on getting this one right first, e.g. dedup the media query block before anything else since it silently doubles future editing work).
> 4. **Specific treatment for the naturalist/vine/strata decorative language** — the user likes this visual identity and it should NOT be gutted. Propose HOW to keep the vine/strata/canopy-descent character while cutting the see-through cost — e.g. solid silhouettes instead of translucent overlays, opaque backing plates behind a decorative element instead of the element itself being translucent, baking a fixed light/dark tint instead of alpha-compositing live. Be concrete about at least 2-3 of the specific decorative elements named in the audit (the vine decoration, the warp strata, the atmosphere gradients).
> 5. **An explicit check for false positives**: go through the "45 decorative" bucket conceptually and flag anywhere you think removing alpha might actually break a real affordance that wasn't obviously "encoding" on first pass (e.g. does any backdrop-filter blur exist for actual legibility-over-busy-background reasons rather than pure atmosphere — check before recommending its removal). Don't recommend a change you can't justify hasn't been informationally load-bearing.
> 
> Output should be an actual rule document someone could hand to a contributor, not just prose observations — use clear headers/numbered rules.

**Result (as captured):** produced an enforceable "Opacity and Stacking Rule Set" grounded in a whole-app opacity audit (verified against the then-12,913-line `index.html`), built around a "layer budget" concept - any element whose own opacity/fill-opacity/stroke-opacity is under 1, or whose background/border/box-shadow has alpha under 1, or that carries a `backdrop-filter`, counts as one layer for the budget. Framed as a rule set to check future diffs against, not a one-time summary.

---

### 6 - Jul 27, 01:27
**Description:** Verify data honesty of map design
**Subagent type:** general-purpose
**Prompt sent:**
> You are an adversarial reviewer. Your job is to attack a design proposal for fabrication risk and cultural essentialism, defaulting to REFUTED under any uncertainty. Do not soften your verdict to be agreeable.
> 
> BACKGROUND: The Aroma Wheel app (`D:\Git_NAE\index.html`) has a hard, previously-tested rule: never fabricate data or citations; every claim must trace to a real source a human has personally opened and confirmed (a near-fabrication already happened once this project — an agent nearly invented a patent inventor name — and was caught).
> 
> A data-availability audit ran earlier and reached this verdict on a proposed "cultural/culinary value — most prized" map layer: **REJECTED as originally scoped.** No institution measures "most prized" as a comparable cross-culture metric; verifying a source exists doesn't verify its OPINION is objective truth about a culture. The audit approved a narrower substitute instead: a "documented designations" layer — individually-sourced PDO/PGI/GI geographic-indication registry entries (EU eAmbrosia, free but Eurocentric in coverage) and/or UNESCO Intangible Cultural Heritage listings (real, ~50 entries, covers practices not ingredients) — most ingredients would simply have NO entry, and that gap should render as a visible gap, not be filled in.
> 
> A GIS/UX designer then took that narrower, approved scope and produced this map design (your job is to check whether it actually honored the narrower scope or let the rejected "most prized" framing sneak back in through the design language):
> 
> ---
> DESIGN PROPOSAL TO AUDIT:
> 
> "Origins Map — three-layer design. Three layers: Origin (point marker, unchanged), 'Grown today' (classed choropleth — 3 buckets: leading/also produced/minimal-or-none — scoped to one selected note at a time, not the whole visible set), and 'Named & protected' (point/seal marker, NOT a choropleth — two sub-glyphs: a seal for PDO/PGI-style geographic indications, a laurel for UNESCO Intangible Cultural Heritage listings).
> 
> No opacity stacking: origin points always-on; exactly one overlay (production OR designations, never both) added via a 3-way segmented control; every mark stays fully opaque.
> 
> Mobile placement at 360x760: layer switcher is a full-width in-flow bar under the header.
> 
> Displacement is surfaced immediately: tapping a note with cross-layer data auto-draws a connector line from the origin pin to the production region or designation seal, and the bottom sheet LEADS WITH THE GAP ITSELF — example copy given: 'Grown today, mostly 6,600 mi from where it started.' Real example cited from the codebase's own data: Vanilla's origin is Totonac-cultivated Veracruz, Mexico, but 'Bourbon Vanilla' points to Madagascar.
> 
> Interaction spec: origin dots stay the only note-level tap target; choropleth regions are informational/non-interactive; the empty case for designations (will be the COMMON case, most notes will have nothing) gets an explicit non-apologetic line in the sheet — example copy given: 'No documented PDO/PGI... that's a real absence, not a research gap' — and simply no seal is drawn, no placeholder.
> 
> Flagged by the designer as NOT solved, left open: (1) designation coverage likely skews toward processed goods (cheese styles, wine appellations) rather than raw notes, so it may land more naturally on 'subOf' varietal children (e.g. a specific cheese or wine varietal) than umbrella notes; (2) production data needs a recurring 'as of [year]' refresh, not a one-time pull; (3) the colonial-geography context for WHY production moved (e.g. coffee, cacao grown far from origin today due to historical plantation systems) still has to be written carefully per-note in copy — the map's connector-line/contrast design does some of that work visually but can't fully carry it alone."
> 
> ---
> 
> YOUR AUDIT — answer each with a clear verdict, not a hedge:
> 
> 1. **Scope creep check**: does "Named & protected" as designed actually stay within the approved narrower scope (individually-sourced registry/heritage entries, gaps shown as gaps), or does anything about the design — the icon choice, the copy tone, the pairing with the "Grown today" layer, the segmented-control framing that puts it alongside a real measured-quantity layer — implicitly re-import the rejected "most prized" framing? Pay specific attention to whether presenting "Named & protected" as a sibling option to "Grown today" (same UI chrome, same segmented control, same visual weight) itself communicates "these are the same kind of fact" even if the underlying data differs — that exact risk was flagged by the original data-availability audit as a real risk of shipping the two layers as siblings.
> 
> 2. **The "displacement" narrative copy**: the designer's suggested copy — "Grown today, mostly 6,600 mi from where it started" — is a specific NUMBER (6,600 miles). Was this number sourced, or does it look fabricated/illustrative? (Assume it wasn't independently verified unless proven otherwise — check whether the design proposal cites where it came from.) More broadly: does leading the bottom sheet with "the gap" as the headline risk implying a causal or evaluative story (e.g. "this ingredient was taken from its origin culture") that the underlying data (which is just two independently-sourced facts: a historical origin point and a modern production statistic) doesn't actually support on its own — i.e., is the DESIGN asserting a narrative interpretation dressed as a data display?
> 
> 3. **Colonial framing**: the designer explicitly flagged colonial-geography context as unsolved and left to future copy work. Is that an acceptable thing to defer, or does shipping the displacement-highlighting UI (the connector line, the "mostly X mi from where it started" framing) BEFORE that copy work is done risk presenting a decontextualized, potentially misleading "gotcha" visual (e.g. implying voluntary migration or simple market forces when the actual history involves forced labor, colonial plantation systems, or trade coercion) with no editorial guardrail in the design to prevent that? Would you block shipping the visual mechanic until the copy work is done, or is it fine to ship the mechanic and backfill the copy?
> 
> 4. **Vanilla example fact-check risk**: the designer describes Vanilla's origin as "Totonac-cultivated Veracruz" and says "Bourbon Vanilla" points to Madagascar as the modern production location. Is this presented as verified fact or as an illustrative example? Does the design proposal cite a real source for either claim, or does it read as asserted-from-training-knowledge? Flag explicitly if this looks like exactly the kind of claim this project's own citation rule requires a human to verify before it ships.
> 
> 5. **PDO/PGI/UNESCO Eurocentric-coverage risk**: the original audit flagged that GI registries are Eurocentric (EU built the biggest searchable one). Does the map design do anything to prevent this from visually reading as "Europe has protected heritage foods, everywhere else does not" — a factually-true-about-the-registries but potentially misleading-about-the-world pattern? Does the empty-case copy ("that's a real absence, not a research gap") actually defuse this risk, or does it need to say more (e.g. explicitly noting registry coverage itself is geographically uneven, not just ingredient-by-ingredient)?
> 
> For each of the 5 points: give a verdict (CONFIRMED RISK / PARTIALLY MITIGATED / NOT A REAL RISK) and a one-sentence justification. End with an overall recommendation: should this design proceed to implementation as-is, proceed with specific required changes (list them), or does it need to go back to the design stage?

**Result (as captured):** an adversarial audit of the "Named and Protected" layer design (call 4/10's proposal). Verified vanilla's real origin data exists at `index.html:3871-3874`, sourced to `lubinsky2008vanilla` - but confirmed the specific numbers and terms the design example leaned on ("6,600," "6600," "Madagascar" as text, and "Bourbon Vanilla") do not appear anywhere in the file, meaning the design's illustrative example was not actually grounded in the app's own data as presented.

---

### 7 - Jul 27, 01:27 (dispatched right after call 6)
**Description:** Verify completeness across three designs
**Subagent type:** general-purpose
**Prompt sent:**
> You are a completeness/contradiction auditor reviewing three independent design outputs produced this session for the Aroma Wheel app (`D:\Git_NAE\index.html`). Your job: find gaps, unmapped features, and DIRECT CONTRADICTIONS between the three proposals. Do not resynthesize or praise them — hunt for what's missing or conflicting.
> 
> Chain the app is built around: perception → notes → compounds → families → lineage → geography.
> 
> ---
> DESIGN 1 — "thesis-chain" (maps every app surface onto the chain, grades each link, ranks fixes):
> 
> Grades: Notes panel (perception→notes, STRONG). Wheel (notes→compounds, STRONG). Detail panel (compounds→families PARTIAL — family section only renders if note has a `family` field, never reads geography at all despite having the note object in scope). Map (geography STRONG on its own, WEAK as connector — `openOriginDetail()` never reads family/genus/lineage despite that data being on the same note object; one reverse edge exists: clicking an origin marker for an unentered note commits it at intensity 5). Tree (families→lineage STRONG, but structurally blind to `state.entries` — zero reference to what the user tasted, contradicting its own in-UI caption "Family is the chemistry clue"). Compass (STRONG for Notes/Compounds modes, Class mode has a legend-filter bug, correctly never touches families/geography — argued as appropriate since family membership isn't a plottable intensity). Share (reads notes/compounds live and DOES include a geography inset via NOTE_ORIGINS, but skips family/lineage entirely, and uses a THIRD independent visibility filter unsynced from the Wheel's legend). Go Deeper depth cards (names all 6 links in prose, zero inbound data — same copy regardless of what user tasted). Bouquet/FLAVOR_COMBOS (notes→compounds strong, but hand-duplicates family/genus grouping in separate hardcoded arrays instead of reading the same `family`/`genus` fields Tree uses — data-integrity risk, will silently drift). Laps (perception→notes only; explicitly argued as CORRECTLY scoped this way, not a defect, since N-way lap comparison would be a large new feature not a promised one). Delivery (explicitly argued as CORRECTLY outside the chain entirely — code self-discloses "recorded, not calculated," folding it into compound scoring without real partition-coefficient data would be fabrication). Search (3 independent implementations across Notes/Map/Tree, no shared query state, argued as low-priority).
> 
> Top-3 ranked fixes: (1) Tree reading `state.entries` — highest priority, "stitches two separate half-chains together." (2) Map's `openOriginDetail()` surfacing family/genus/lineage — cheap, ~5-line fix. (3) Share reflecting full chain + honoring shared legend filters — highest external stakes (public-facing artifact) but technically riskier to implement (delicate existing layout math).
> 
> ---
> DESIGN 2 — "multi-layer-map" (GIS design for 3 map layers: origin / economic cultivation / documented designations):
> 
> Origin = point marker (unchanged). "Grown today" = classed choropleth (3 buckets), SCOPED TO ONE SELECTED NOTE AT A TIME (not drawn for all visible notes simultaneously — avoids overlap since many ingredients share producer countries). "Named & protected" = point/seal marker (NOT choropleth — most regions would be "no data" and read as a broken map), two sub-glyphs: seal for PDO/PGI, laurel for UNESCO ICH.
> 
> No opacity stacking: origin points always-on; exactly ONE overlay (production OR designations, never both) via 3-way segmented control; every mark fully opaque; choropleth fill sits UNDER points in z-order.
> 
> Mobile 360x760: layer switcher is a new full-width in-flow bar under the header (not an overlay).
> 
> Displacement narrative: tapping a note with cross-layer data draws a connector line from origin pin to production region/designation seal; bottom sheet leads with the gap ("Grown today, mostly 6,600 mi from where it started" — Vanilla example: origin Veracruz Mexico, modern production Madagascar/"Bourbon Vanilla").
> 
> Empty case for designations (will be the COMMON case) gets explicit non-apologetic copy ("No documented PDO/PGI... that's a real absence, not a research gap"), no placeholder drawn.
> 
> Flagged as unsolved by the designer: designation coverage skews toward processed goods/varietal children not umbrella notes; production data needs a recurring "as of [year]" refresh; colonial-geography context for WHY production moved still needs careful per-note copy, not fully carried by the visual design alone.
> 
> ---
> DESIGN 3 — "layer-discipline" (enforceable opacity/stacking rule set for the whole app, derived from an earlier opacity audit):
> 
> Layer budget table: General chrome = max 2 simultaneous translucent layers. Full-screen transitions (e.g. Go Deeper warp) = max 4, for the animation's duration only. Wheel/Tree/Compass EVIDENCE-ENCODING cluster = 5, a NAMED EXCEPTION (arc=category, halo/token=evidence strength, edge=connection weight, dimming=filtered state — 4 legitimate simultaneous data dimensions). Modal scrim = doesn't count against budget (functional occlusion). Sticky chrome-over-content (header/tray/nav) = max 1 per screen region, never 2 overlapping.
> 
> Core test: "Does the alpha value change because of user/data state? If yes = encoding, leave alone. If baked unconditionally into a decorative element's CSS = atmosphere, flatten freely." Named a third bucket: "functional chrome translucency" (sticky header, tray, nav — fixed alpha but doing real legibility signaling, e.g. "the wheel visibly slides UNDER the header" per an existing code comment) — keep the alpha, but these still count against the 1-per-region budget and must never stack with another translucent chrome layer.
> 
> Top-5 ranked fixes: (1) dedupe the duplicated mobile media-query block FIRST (infrastructure risk-reduction, everything else lives inside it). (2) flatten mobile `--line` border var to opaque (highest raw impact/line). (3) cut the Go Deeper warp transition from 9 layers to ≤4 (worst single UX moment). (4) fix `.lap-rail` overlapping `#callout-toggle`/`.wheel-hint` (layout bug, incidentally an opacity-adjacent fix). (5) simplify `.depth-card`'s 4+ nested alpha layers to 1 opaque plate.
> 
> Naturalist-language preservation techniques given: solid silhouette (land the vine's resting-state opacity at 1 instead of 0.82, keep only the one-time fade-IN transition), opaque gradient story (warp strata should be authored between opaque colors, not translucent), baked composite image (pre-rendered SVG data-URI backgrounds, already done correctly for one existing decoration), animate position/mask not alpha (for shimmer effects).
> 
> ---
> 
> YOUR AUDIT — be specific, cite which design(s) each finding involves:
> 
> 1. **The obvious contradiction to check**: does Design 2 (multi-layer-map) violate Design 3's (layer-discipline) rules anywhere? Specifically: does the connector line + choropleth fill + point marker + bottom sheet, all appearing together when a note has cross-layer data, exceed the "General chrome = max 2 simultaneous translucent layers" budget, or does Design 2's "every mark stays fully opaque" commitment mean it's actually compliant by construction? Check the layer switcher bar too — does its placement/treatment conflict with Design 3's "sticky chrome = max 1 per region, never stacks with another translucent chrome layer" rule (is there already a sticky header AND now a new sticky-ish layer-switcher bar in the same screen region)?
> 
> 2. **Unmapped chain links**: Design 1 identifies Map's `openOriginDetail()` as weak on lineage (fix #2 in its ranked list — surface family/genus there). Does Design 2's map redesign actually address this, make it harder, or leave it completely untouched? (Design 2 adds NEW data to the map — production, designations — but does it do anything about the EXISTING family/genus gap Design 1 flagged, or does adding two new layers on top of an unfixed gap compound the problem?)
> 
> 3. **Unmapped tool features**: go through Design 1's full surface list (Notes, Wheel, Detail, Map, Tree, Compass, Share, Go Deeper cards, Bouquet, Laps, Delivery, Search) — which of these are touched by NEITHER Design 2 nor Design 3? Are any of Design 1's top-3 ranked fixes (Tree reading state.entries; Map surfacing family/genus; Share reflecting full chain + honoring legend filters) actually acted on by Design 2 or 3, or do all three designs talk past each other — Design 1 prioritizes Tree/Map/Share, Design 2 only touches Map (and adds complexity rather than fixing the flagged gap), Design 3 touches app-wide CSS but doesn't mention Tree, Share, or the family/genus gap at all?
> 
> 4. **Was "disparate things tied through one narrative" actually articulated, or just asserted?** Design 1 explicitly argues (not just asserts) several "correctly separate" cases with reasoning (Delivery, Laps, Compass-vs-geography). Does Design 2's "displacement" framing (origin ≠ production ≠ designation IS the interesting story) actually connect back to Design 1's thesis-chain grading in any explicit way, or is Design 2's narrative payoff a free-standing design idea that doesn't reference or build on Design 1's specific findings (e.g. does Design 2 ever mention the lineage/family layer Design 1 says Map is missing)?
> 
> 5. **Any other direct contradiction or gap** you find between the three that isn't covered above — state it plainly with which two (or three) designs are in tension and why.
> 
> For each of the 5 points, give a clear finding — not hedged — and say whether it's a **blocking contradiction** (the designs can't both ship as written) or a **coexistence gap** (they just don't talk to each other, but nothing technically conflicts). End with a short list of what a synthesis pass MUST resolve rather than silently drop.

**Result (as captured):** completeness/contradiction audit across the three design outputs (calls 3, 4, and the layer-rules pass). Verified directly against code that `openOriginDetail()` (line 10605) never reads `note.family`/`note.genus`, that `buildTaxonomyTreeData()` (line 5474) builds only from `NOTES`/`taxonPath()` with zero reference to `state.entries`, and that `buildShareCard()`'s `opts.hiddenCompounds` (line 11398) is a separate `Set` from the wheel legend's own `state.hiddenGroups`/`state.hiddenClasses` filters - independently confirming the same seam-breaks call 3 had already named, from the design side rather than the audit side.

---

### 8 - Jul 27, 02:23
**Description:** Research tropical crop production
**Subagent type:** general-purpose
**Prompt sent:**
> You are sourcing real crop-production statistics for an educational aroma/flavor app. The app's absolute, non-negotiable rule is: NEVER write a number you have not personally read off a real, fetched source page. This project has already caught two near-fabrications (an invented patent inventor name; a made-up "6,600 miles" distance that was wrong by 4,000 miles). Do not become the third.
> 
> HARD RULES — read these twice:
> 1. You MUST actually fetch a real web page (use WebSearch to find, then WebFetch to READ) for every figure you report. Recall from training data is NOT acceptable, no matter how confident you feel.
> 2. For every note you report, record the EXACT source URL you fetched, the publishing organization, and the YEAR the data refers to (not the year you're reading it).
> 3. If you cannot verify a figure from a fetched page, report that note as a GAP. An honest gap is a correct answer here. Filling it with a plausible-sounding guess is a project-ending failure.
> 4. Do NOT round, adjust, or "clean up" numbers. Report what the source says.
> 5. If a source aggregates several things into one commodity line (FAOSTAT for example reports "Lemons and limes" as ONE line, and "Cantaloupes and other melons" as one line), report the EXACT commodity-line name the source uses. Do not silently split an aggregate into individual crops — that would be inventing precision the data doesn't have.
> 
> GOOD SOURCES (all real, all free — verify by fetching):
> - FAOSTAT (fao.org/faostat) — the primary global reference for crop production by country
> - FAO's annual statistical yearbook / "World Food and Agriculture" PDFs
> - USDA FAS PSD Online (apps.fas.usda.gov/psdonline) and USDA NASS
> - International Coffee Organization (ico.org), International Cocoa Organization, International Pepper Community
> - Any national statistics agency, if it's the authoritative one for that crop
> Wikipedia is acceptable ONLY as a pointer to a primary source — if you use it, follow through to the underlying FAOSTAT/USDA citation and fetch THAT, and say clearly that's what you did.
> 
> YOUR ASSIGNED NOTES (these are note IDs from the app — keep the IDs exactly as given):
> coffee (Coffee / roast), chocolate (Chocolate / cocoa), vanilla (Vanilla), pepper (Black pepper), cinnamon (Cinnamon), clove (Clove), ginger (Ginger), banana (Banana), mango (Mango), pineapple (Pineapple), coconut (Coconut), passionfruit (Passionfruit), taro (Taro), ube (Ube — note: this is purple yam, Dioscorea alata, NOT sweet potato; if the source only has generic "Yams", say so explicitly).
> 
> FOR EACH NOTE, REPORT:
> - noteId
> - The exact commodity-line name your source uses
> - Top 3 producing countries in rank order, with production figures and units if the source gives them
> - The data year
> - Source organization + exact fetched URL
> - A confidence note: did you read this off a primary statistical table, or off a secondary summary of one?
> 
> Then, SEPARATELY, list every assigned note you could NOT verify, and say what specifically blocked you (paywall, no such commodity line, aggregated into something else, couldn't find a fetchable table, etc).
> 
> Finish with an explicit self-audit: state plainly whether every single number in your report came from a page you actually fetched in this session. If any did not, name it. I would much rather receive 6 verified notes and 8 honest gaps than 14 confident-sounding guesses.

**Result (as captured):** terminated early - the transcript records "Agent terminated early due to an API error: You have hit your session limit." Only partial output survived (the agent had gotten as far as testing whether an old FAOSTAT API host worked, after FAOSTAT's own API returned a 521 and UNdata's FAO mirror was being tried as a fallback). Explicitly flagged in the result as incomplete - not usable production-data findings.

---

### 9 - Jul 27, 02:23 (dispatched right after call 8)
**Description:** Research fruit/citrus production
**Subagent type:** general-purpose
**Prompt sent:**
> You are sourcing real crop-production statistics for an educational aroma/flavor app. The app's absolute, non-negotiable rule is: NEVER write a number you have not personally read off a real, fetched source page. This project has already caught two near-fabrications (an invented patent inventor name; a made-up "6,600 miles" distance that was wrong by 4,000 miles). Do not become the third.
> 
> HARD RULES — read these twice:
> 1. You MUST actually fetch a real web page (use WebSearch to find, then WebFetch to READ) for every figure you report. Recall from training data is NOT acceptable, no matter how confident you feel.
> 2. For every note you report, record the EXACT source URL you fetched, the publishing organization, and the YEAR the data refers to (not the year you're reading it).
> 3. If you cannot verify a figure from a fetched page, report that note as a GAP. An honest gap is a correct answer here. Filling it with a plausible-sounding guess is a project-ending failure.
> 4. Do NOT round, adjust, or "clean up" numbers. Report what the source says.
> 5. CRITICAL FOR YOUR BATCH — aggregation: FAOSTAT reports "Lemons and limes" as ONE commodity line, and "Cantaloupes and other melons" as one line, and often "Currants" or "Berries nes" as grouped lines. Report the EXACT commodity-line name the source uses. Do NOT silently split an aggregate into individual crops — that invents precision the data doesn't have. If lemon and lime share one line, say so; I will handle that honestly in the app rather than pretending they're separate.
> 
> GOOD SOURCES (all real, all free — verify by fetching):
> - FAOSTAT (fao.org/faostat) — the primary global reference for crop production by country
> - FAO's annual statistical yearbook / "World Food and Agriculture" PDFs
> - USDA FAS PSD Online (apps.fas.usda.gov/psdonline) and USDA NASS
> - Any national statistics agency, if it's the authoritative one for that crop
> Wikipedia is acceptable ONLY as a pointer to a primary source — if you use it, follow through to the underlying FAOSTAT/USDA citation and fetch THAT, and say clearly that's what you did.
> 
> YOUR ASSIGNED NOTES (these are note IDs from the app — keep the IDs exactly as given):
> lemon (Lemon), lime (Lime), orange (Orange), mandarin (Mandarin / tangerine), grapefruit (Grapefruit), pomelo (Pomelo / pummelo), apple (Apple / pear — note the app pairs these; report whichever the source has and say which), grape (Grape / concord), cherry (Cherry), peach (Peach), plum (Plum), strawberry (Strawberry), raspberry (Raspberry), blueberry (Blueberry), cranberry (Cranberry), cassis (Black currant / cassis), pomegranate (Pomegranate), watermelon (Watermelon), cantaloupe (Cantaloupe), cucumber (Cucumber).
> 
> FOR EACH NOTE, REPORT:
> - noteId
> - The exact commodity-line name your source uses
> - Top 3 producing countries in rank order, with production figures and units if the source gives them
> - The data year
> - Source organization + exact fetched URL
> - A confidence note: did you read this off a primary statistical table, or off a secondary summary of one?
> 
> Then, SEPARATELY, list every assigned note you could NOT verify, and say what specifically blocked you (paywall, no such commodity line, aggregated into something else, couldn't find a fetchable table, etc).
> 
> Finish with an explicit self-audit: state plainly whether every single number in your report came from a page you actually fetched in this session. If any did not, name it. I would much rather receive 8 verified notes and 12 honest gaps than 20 confident-sounding guesses.

**Result (as captured):** also terminated early on the same session usage limit. Partial output shows the agent had confirmed no Python/Node was available locally and was testing an older FAOSTAT API host as a fallback before being cut off. Flagged incomplete.

---

### 10 - Jul 27, 02:23 (dispatched right after call 9)
**Description:** Research grain/veg/nut production
**Subagent type:** general-purpose
**Prompt sent:**
> You are sourcing real crop-production statistics for an educational aroma/flavor app. The app's absolute, non-negotiable rule is: NEVER write a number you have not personally read off a real, fetched source page. This project has already caught two near-fabrications (an invented patent inventor name; a made-up "6,600 miles" distance that was wrong by 4,000 miles). Do not become the third.
> 
> HARD RULES — read these twice:
> 1. You MUST actually fetch a real web page (use WebSearch to find, then WebFetch to READ) for every figure you report. Recall from training data is NOT acceptable, no matter how confident you feel.
> 2. For every note you report, record the EXACT source URL you fetched, the publishing organization, and the YEAR the data refers to (not the year you're reading it).
> 3. If you cannot verify a figure from a fetched page, report that note as a GAP. An honest gap is a correct answer here. Filling it with a plausible-sounding guess is a project-ending failure.
> 4. Do NOT round, adjust, or "clean up" numbers. Report what the source says.
> 5. Aggregation matters: FAOSTAT reports many of your items as grouped lines (e.g. "Lettuce and chicory", "Carrots and turnips", "Onions, dry", "Cabbages and other brassicas"). Report the EXACT commodity-line name the source uses, and do NOT silently split an aggregate into individual crops — that invents precision the data doesn't have.
> 
> GOOD SOURCES (all real, all free — verify by fetching):
> - FAOSTAT (fao.org/faostat) — the primary global reference for crop production by country
> - FAO's annual statistical yearbook / "World Food and Agriculture" PDFs
> - USDA FAS PSD Online (apps.fas.usda.gov/psdonline) and USDA NASS
> - Any national statistics agency, if it's the authoritative one for that crop
> Wikipedia is acceptable ONLY as a pointer to a primary source — if you use it, follow through to the underlying FAOSTAT/USDA citation and fetch THAT, and say clearly that's what you did.
> 
> YOUR ASSIGNED NOTES (these are note IDs from the app — keep the IDs exactly as given):
> rice (Rice), wheat (Wheat), barley (Barley / malt), oats (Oats), millet (Millet), quinoa (Quinoa), almond (Almond), hazelnut (Hazelnut), peanut (Peanut), pistachio (Pistachio), pecan (Pecan), coconut is NOT yours — skip it. Also: tomato (Tomato), potato (Potato), sweetpotato (Sweet potato), onion (Onion), garlic (Garlic), celery (Celery), carrot (Carrot), lettuce (Lettuce), cabbage (Cabbage), tobacco (Tobacco), honey (Honey — natural honey, from bees), maple (Maple / brown sugar — this is maple syrup; if the only authoritative source is Canadian/US national statistics rather than FAO, that's fine, say so).
> 
> FOR EACH NOTE, REPORT:
> - noteId
> - The exact commodity-line name your source uses
> - Top 3 producing countries in rank order, with production figures and units if the source gives them
> - The data year
> - Source organization + exact fetched URL
> - A confidence note: did you read this off a primary statistical table, or off a secondary summary of one?
> 
> Then, SEPARATELY, list every assigned note you could NOT verify, and say what specifically blocked you (paywall, no such commodity line, aggregated into something else, couldn't find a fetchable table, etc).
> 
> Finish with an explicit self-audit: state plainly whether every single number in your report came from a page you actually fetched in this session. If any did not, name it. I would much rather receive 10 verified notes and 14 honest gaps than 24 confident-sounding guesses.

**Result (as captured):** also terminated early on the same session usage limit. Partial output shows the agent had found the FAO yearbook HTML was fetchable and was reading it while probing USDA sources when cut off. Flagged incomplete.
