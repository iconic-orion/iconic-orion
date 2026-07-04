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
| `../favicon.svg` | vector | The live site favicon (8-wedge ring) |

The ring mark currently has **8 wedges** (matching `favicon.svg`). The app has
since added a 9th family (Vegetal `#5a9c4f`); the mark has not been updated to
9 wedges yet.

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

Match `--window-size` to the SVG's width/height. For the favicon PNGs, point at
`favicon.svg` and set the window size to 512,512 or 32,32.
