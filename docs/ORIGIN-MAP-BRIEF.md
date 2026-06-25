# Origin Map — Agent Implementation Brief

## What this is

Add a "Origins" view to the existing Aroma Wheel tool. The entire app lives in one file: `index.html` (~3930 lines), with all HTML, CSS, and JS inline. No build step, no framework, no external data files. Any additions must follow that pattern.

---

## Current data model to understand first

**`NOTES`** (line 880) — 43 aroma/flavor notes, each representing a real ingredient or sensory category. These are the things that get mapped to regions.

```js
{ id: "lemon", label: "Lemon", group: "fruity", common: true }
```

Note IDs (all 43): lemon, orange, grapefruit, berry, stonefruit, apple, banana, pineapple, cherry, mango, passionfruit, rose, jasmine, lavender, chamomile, violet, coffee, toast, smoky, burnt, clove, cinnamon, pepper, anise, almond, hazelnut, peanut, woody, pine, mushroom, green, bellpepper, mint, tobacco, vanilla, caramel, honey, chocolate, maple, winey, buttery, yeasty, sulfury, cardboard

**`COMPOUNDS`** (line 942) — chemical compounds, each with class, threshold, and specificity. Not the things being mapped — these are already handled by the existing wheel.

**`COMPOUND_ORIGINS`** (line 1154) — a plain object keyed by compound ID, values are prose strings. Reference this pattern; the new `NOTE_ORIGINS` will be similar but structured (not prose).

---

## New data constant to add

Define `NOTE_ORIGINS` as a JS object in the data section (after `COMPOUND_ORIGINS`), one entry per note ID:

```js
const NOTE_ORIGINS = {
  lemon: {
    region: "South/Southeast Asia",
    lat: 25, lon: 85,           // centroid of the region for map placement
    certainty: "approximate",   // "known" | "approximate"
  },
  coffee: {
    region: "Ethiopian Highlands",
    lat: 9, lon: 40,
    certainty: "known",
  },
  // ...
};
```

**Framing rules for assigning origins:**

1. **Pre-Columbian Exchange baseline.** Origins should reflect where the plant was cultivated or first used by humans *before* 1492 European contact reshaped global agriculture. Do not place the origin where a crop is now most commercially grown (e.g., coffee → Ethiopia/Yemen, not Brazil; vanilla → Mesoamerica, not Madagascar; pineapple → South America, not Hawaii).

2. **Region-level granularity, not country-level.** Use named geographic regions ("Ethiopian Highlands", "South/Southeast Asia", "Mesoamerica", "Eastern Mediterranean", "South American Andes") — vague enough to stay accurate when the exact origin is unknown or when the plant was independently domesticated in multiple areas.

3. **Modern/synthetic flavors** (e.g., caramel, burnt sugar, cardboard/stale, sulfury, buttery, yeasty) don't have a crop origin. For these, assign the region where the underlying chemical process or compound was first identified or most strongly culturally associated. `certainty` should be `"approximate"` and a brief `note` field may optionally explain the rationale.

4. **Multiple independent origins.** If a note genuinely arose from two well-separated cultivation centers (e.g., mint was cultivated in both the Mediterranean and South Asia), assign the primary cultural/historical center as `lat/lon` and set `certainty: "approximate"`. Do not add multiple coordinates per entry — keep the data model flat.

5. **American SoCal frame.** Optimize for what a modern US grocery/specialty-store audience would recognize. Don't split hairs on sub-regional debate when a broad region name communicates accurately.

---

## New view: Origins map

### Top-level view switching

The existing UI has a top-level layout with a central wheel pane and left/right side panes toggled by edge tabs. The header has view tabs (Notes / Dashboard / Compounds) that control the *right* pane's content.

The Origins view is a **full-canvas replacement** — it replaces the entire 3-pane layout (wheel + both side panes) with a single map canvas. It is not a tab inside the existing view — it is a peer *mode*.

Add a small pill/button toggle in the header (near the existing controls, consistent with `.tabs` styling) to switch between:
- **Wheel** (default, the existing 3-pane layout)
- **Origins** (new full-canvas map view)

When switched, hide the wheel layout (`display:none`) and show the map canvas, and vice versa. Switching back to Wheel should restore previous state (selected notes, etc.) — don't reset.

### Map rendering

Use an **inline SVG world map** — either:
- A Natural Earth–derived simplified SVG (can be fetched from a public CDN and pasted inline), or
- D3.js + TopoJSON loaded from unpkg (`https://unpkg.com/d3@7` + `https://unpkg.com/topojson@3`) — acceptable since the app already has no CDN dependencies *but* this is the first; prefer inline SVG to keep the file self-contained.

Whichever approach: the map should render as an SVG with a Robinson or Winkel Tripel-like projection (approx equal-area feel), sized to fill the available canvas area responsively.

Land masses should use a neutral fill (use existing CSS variables `--panel-2` or `--panel` for land, `--bg` for ocean, `--line` for borders between countries). No country-level coloring needed.

### Ingredient markers

For each entry in `NOTE_ORIGINS`, place a marker at the `[lat, lon]` coordinate:

- A small filled circle (6px radius, color = the group color from `COMPOUND_CLASS_COLOR` mapped to the note's group — or just use `var(--accent)` uniformly if per-group color is complex).
- A label line from the circle to the note's label text.
  - **Solid line** if `certainty === "known"`.
  - **Dashed line** (`stroke-dasharray: 4 3`) if `certainty === "approximate"`.
- The label text: the note's `label` value from the `NOTES` array.

When a note is selected (already in `state.notes` selection), highlight its marker (larger circle, brighter color). Clicking a marker in the Origins view should toggle that note's selection, exactly as clicking the note on the wheel does — reuse the same toggle function.

### Interaction

- Hovering a marker shows a small tooltip (reuse existing tooltip pattern) with the note label + region name.
- If no notes are selected, all markers are shown at normal weight.
- If notes are selected, dim unselected markers (0.3 opacity), highlight selected ones.
- No zoom/pan required for v1. Keep it simple.

### Empty-state / loading

If `NOTE_ORIGINS` is missing an entry for a given note, skip that note silently (no marker). This allows the data to be filled in incrementally.

---

## Aroma Wheel tab (existing view)

The existing wheel view should be reachable as the **Wheel** mode (default). Its header, controls, favicon, and behavior are unchanged. The aroma wheel favicon (`favicon.svg`) already exists and is already set in `<head>` — no change needed there.

---

## Implementation order

1. Add `NOTE_ORIGINS` data constant with all 43 entries. Research and populate origins carefully using the framing rules above before writing any UI code.
2. Add the mode toggle button to the header HTML and CSS (pill style, consistent with `.tabs`).
3. Add the map canvas HTML container (an `<svg id="origin-map">` inside a `<div id="origins-view">`).
4. Add JS: map initialization, projection, land-path rendering.
5. Add JS: marker + label-line rendering from `NOTE_ORIGINS`.
6. Wire mode toggle: show/hide `#origins-view` vs the existing wheel layout; update toggle button active state.
7. Wire marker click to the existing note-toggle function.
8. Wire selection state changes to update marker highlight on the map (so both views stay in sync).
9. Add hover tooltip.
10. Test all 43 notes render without overlap issues; adjust label offsets as needed.

---

## Constraints

- Single `index.html` — all additions go inline.
- No new files unless absolutely necessary (a separate JS data file is acceptable if `NOTE_ORIGINS` bloats the HTML significantly, but prefer inline for now).
- Maintain existing mobile behavior — the Origins view should be usable on mobile too; a single-column map that fills the screen is fine.
- Do not alter the existing wheel rendering, compound logic, or state model except to add the marker-sync hook in step 8.
