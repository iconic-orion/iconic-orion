# Temporal — a 24-hour atmospheric clock

A single-file, dependency-free clock that renders a day as a perceptual
experience across three temporal scales. Open `index.html` in any modern
browser — no build step.

## The three scales

- **Macroscale (24h day).** A fixed horizon view. The sky is a horizontal
  color band spanning midnight → noon → midnight (24 hourly stops, deep
  indigo through bright noon sky to golden dusk). The sun traces a curved
  path across that sky — height above the horizon represents solar
  elevation — rising at sunrise, peaking at noon, setting at sunset, and
  hidden below the horizon at night. A faint dashed guide previews the rest
  of today's arc; the elapsed portion is solid and brighter. A warm glow
  hugs the horizon near sunrise/sunset, fading near noon and midnight. An
  always-visible `HH:MM:SS` label tracks the sun's time-of-day position
  along the horizon, day or night. With location enabled (see below),
  "Sunrise HH:MM" / "Sunset HH:MM" labels mark the real edges of the
  visible arc.
- **Mesoscale (60 min).** Sixty columns form a decay strip along the ground,
  below the horizon — newest = current minute, oldest fading out. Columns
  inherit the current hour's sky color, desaturate with age, and slide
  continuously so the oldest expires smoothly each minute.
- **Microscale (60 sec).** Three optional layers (toggleable):
  1. **Pulse** — the current-minute column glows once per second.
  2. **Ticker** — a hairline sweeps across the minute strip once per minute.
  3. **Dial** — a 60-segment radial seconds ring in the corner.

## Behavior

- **Timezone dropdown.** The sky is a *universal* day and stays fixed;
  changing the timezone moves the sun and the numeric readout. Optional
  UTC-offset display.
- **Location (optional).** An explicit "Use my location" button in the
  settings panel — never requested automatically — feeds the browser's
  Geolocation coordinates into a low-precision solar-position calculation
  (Julian-date based, same formula family as the SunCalc.js library) to
  compute today's real sunrise and sunset for that latitude/longitude. Once
  known, the sun's arc reshapes to match real day length (still a smooth
  cosine curve, just anchored to the true sunrise/sunset fractions instead
  of the 6am/6pm default) and the two edge labels appear. Without location
  access, the clock falls back to the stylized 6am/6pm day silently — no
  errors, no missing functionality.
- **Responsive.** The horizon height, sun amplitude, and ground strip size
  scale with viewport; the layout is the same horizon-and-sun-path metaphor
  in both portrait and landscape, just proportioned differently. The minute
  strip collapses on screens under 320px.
- **Accessible.** An always-on `HH:MM:SS` readout with high-contrast text
  backs up the visualization; the canvas carries a descriptive label.

## Design notes

The spec's "vertical position proportional to age" and "oldest (bottom)
column disappears" are internally contradictory, so this build commits to a
single coherent reading: newest column at the leading edge, age increasing
toward the trailing edge, with a continuous per-minute slide standing in for
the discrete "drop + cascade" (it reads smoother and avoids layout pops).

The sun's elevation curve is a piecewise cosine parameterized by the
sunrise/sunset day-fractions: symmetric cosine lobes above and below the
horizon, sized to the actual day and night lengths. With no location granted
it defaults to `SUNRISE_F = 0.25, SUNSET_F = 0.75` (6am/6pm), which reduces
the formula exactly to the original fixed sinusoid (`-cos(2π·dayFraction)`).
The sun fades in/out over the ~29 minutes around each horizon crossing
(eased, not a hard pop). At night the sun simply isn't drawn — no moon arc —
to keep the visualization to exactly what was asked for.
