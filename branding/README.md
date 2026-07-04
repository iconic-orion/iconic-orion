# Branding — iconic-orion / aromawheel.net

Brand assets for the aromawheel.net prototype (an aroma-wheel-styled tool for
recording taste & smell experiences). Brand: **iconic-orion**.

> Note: "aroma wheel" is a generic description of the tool type — this is *an
> aroma-wheel-styled* tool, not a proprietary "Aroma Wheel" mark. Use the
> lowercase domain `aromawheel.net` as the tool identifier.

## Assets

| File | Size | Use |
|---|---|---|
| `banner.png` | 1600×400 | Google Forms header / social banner |
| `banner.svg` | vector | Editable source for the banner |
| `mark.png` | 512×512 | Square app icon / avatar (rounded) |
| `mark.svg` | vector | Editable source for the square mark |
| `favicon-512.png` | 512×512 | Large raster of the site favicon |
| `favicon-32.png` | 32×32 | Small raster of the site favicon |
| `../favicon.svg` | vector | The live site favicon (thin glowing ring — see below) |

### Two different marks, on purpose (for now)

`banner.svg` / `mark.svg` still use the **solid 9-wedge pie** (40° each,
fruity → vegetal). `../favicon.svg` was changed to a **thin ring of 9 stroked
arcs** — dim/muted by default, two lit brighter with a soft glow — because a
solid, fully-saturated pie-wedge disc is the specific visual signature of the
generic wine/flavor "aroma wheel" genre (a design already claimed elsewhere as
"wine aroma wheel"). The real app never fills a solid wedge: `drawGroupArcs()`
draws a thin ring that sits dim at rest and blooms (brighter + CSS
`drop-shadow`) as evidence accumulates — the favicon is a static snapshot of
that actual visual language instead of the generic genre look.

This was verified to hold up at true rendered size, not just as a big preview:
at the real 32×32 and 16×16 favicon sizes the ring keeps a proportionate dark
hole (~65% of the radius) and each of the 9 segments stays a distinguishable
color, confirmed via direct pixel sampling (not just eyeballing a screenshot,
which can mislead due to recompression at preview size).

**Known inconsistency, not yet resolved:** the bigger surfaces (`banner.svg`,
`mark.svg`, and their PNGs) still use the solid-wedge look. Whether to bring
the ring/glow treatment to those too is an open decision — the favicon change
was scoped narrowly on purpose.

## Palette (matches the live app CSS variables)

| Token | Hex |
|---|---|
| Background | `#0e0d10` |
| Panel | `#17161b` |
| Ink (text) | `#e9e6df` |
| Ink dim | `#8a8579` |
| Gold accent | `#d8a657` |
| Teal accent | `#7daea3` |

Wheel families: fruity `#eb894a` · floral `#db7e97` · roasted `#b65b3d` ·
spice `#ee665e` · nutty `#d19456` · earthy `#7fc275` · sweet `#dfa850` ·
fermented `#6ebdab` · vegetal `#5a9c4f`

## Regenerating the PNGs from SVG

Rendered with headless Chrome (no ImageMagick/Inkscape needed):

```
chrome --headless=new --disable-gpu --hide-scrollbars --force-device-scale-factor=1 \
  --default-background-color=00000000 --window-size=1600,400 \
  --screenshot=banner.png "file:///<abs-path>/banner.svg"
```

Match `--window-size` to the SVG's width/height. `banner.svg`/`mark.svg` can be
rendered this way directly.

For `favicon.svg` specifically, render it as a **decoded image resource**
(matching how `<link rel="icon">` actually loads it) rather than navigating to
the raw file as a top-level document — wrap it in a tiny HTML page, draw it to
a same-size `<canvas>` via `new Image()`, then screenshot that page:

```html
<canvas id="c" width="32" height="32"></canvas>
<script>
  const img = new Image();
  img.onload = () => document.getElementById("c").getContext("2d").drawImage(img, 0, 0, 32, 32);
  img.src = "file:///<abs-path>/favicon.svg";
</script>
```

then `--screenshot` that wrapper page at the matching `--window-size`.
