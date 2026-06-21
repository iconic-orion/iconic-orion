# Temporal — a 24-hour atmospheric clock

A single-file, dependency-free clock that renders a day as a perceptual
experience across three temporal scales. Open `index.html` in any modern
browser — no build step.

## The three scales

- **Macroscale (24h day).** A fixed color gradient runs midnight → noon →
  midnight (24 hourly stops, deep indigo through bright noon sky to golden
  dusk). A glowing "now" line sweeps the gradient once per 24 hours.
  Portrait runs the gradient vertically; landscape runs it diagonally and
  draws the now-line perpendicular to that axis.
- **Mesoscale (60 min).** Sixty columns form a decay strip — newest =
  current minute, oldest fading out. The strip sits on the right edge in
  portrait and the bottom edge in landscape. Columns inherit the current
  hour's color, desaturate with age, and slide continuously so the oldest
  expires smoothly each minute.
- **Microscale (60 sec).** Three optional layers (toggleable):
  1. **Pulse** — the current-minute column glows once per second.
  2. **Ticker** — a hairline sweeps across the minute strip once per minute.
  3. **Dial** — a 60-segment radial seconds ring in the corner.

## Behavior

- **Timezone dropdown.** The gradient is a *universal* day and stays fixed;
  changing the timezone moves the now-line and the numeric readout.
  Optional UTC-offset display.
- **Responsive.** Layout, gradient direction, strip placement, and dial
  position all reflow on portrait ↔ landscape. The minute strip collapses
  on screens under 320px.
- **Accessible.** An always-on `HH:MM:SS` readout with high-contrast text
  backs up the visualization; the canvas carries a descriptive label.

## Design notes

The spec's "vertical position proportional to age" and "oldest (bottom)
column disappears" are internally contradictory, so this build commits to a
single coherent reading: newest column at the leading edge, age increasing
toward the trailing edge, with a continuous per-minute slide standing in for
the discrete "drop + cascade" (it reads smoother and avoids layout pops).
Gaussian-style blending between hour stops comes from gradient interpolation
plus a blurred glow around the now-line rather than a post-process blur pass.
