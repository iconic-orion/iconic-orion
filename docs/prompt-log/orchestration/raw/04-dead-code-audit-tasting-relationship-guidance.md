# 04 - Dead-code audit before the tasting-relationship-guidance merge

- **Date:** 2026-08-14
- **Source:** Claude Code session `e7282965`, branch `codex/tasting-relationship-guidance`
- **Agent calls:** 1
- **Provenance:** transcript-backed (verbatim, extracted 2026-08-15)
- **Companion:** also indexed in the human prompt log as [entry 44](../../raw/44-venn-overlap-and-enter-tasting-button.md).

---

### 1 - Aug 14, 14:26
**Description:** Audit branch for stale/dead code
**Subagent type:** general-purpose
**Prompt sent:**
> You're auditing a single large file, D:\Git_NAE\index.html (~21,500 lines — a single-page app: HTML+CSS+JS all in one file, the "Aroma Wheel" sensory-to-compound inference tool), on git branch `codex/tasting-relationship-guidance`, for STALE/DEAD CODE. This branch is 60 commits ahead of `prototype` and has had heavy iteration from two different agents (Claude and a ChatGPT/Codex agent) over recent weeks, so leftover cruft from superseded approaches is likely.
> 
> Goal: find dead code, not style issues or bugs. Specifically look for:
> 1. CSS rules that target classes/ids that are never added to any element in the JS (a rule keyed on a class name that used to exist but was renamed away from, similar to a known instance already found: `.compounds-collapsed` at line ~246 targets a class that was renamed to `compounds-peek`/`compounds-half`/`compounds-full` and is now permanently dead).
> 2. JS functions defined but never called anywhere else in the file.
> 3. JS variables/state fields declared (e.g. in the `state` object) but never read, only written (or vice versa).
> 4. Event listeners attached to elements that no longer exist (getElementById returning something for an id that's been removed from the HTML) — these would throw or silently no-op.
> 5. Duplicate/superseded implementations of the same concept (e.g. two different drawer/sheet dragging implementations, two different "collapsed" state mechanisms) where one is clearly the old one left behind after a rewrite.
> 6. HTML elements (ids, data attributes) referenced by getElementById/querySelector in JS that no longer exist in the markup.
> 7. Commented-out code blocks left in.
> 
> How to work efficiently on a 21k-line file: use grep/search for class/id/function names and cross-reference definition sites against usage sites, rather than reading the whole file linearly. Pay special attention to code that looks like it was touched across multiple recent commits (you can check `git log -p --follow -- index.html` on suspicious regions, or just `git log --oneline` for commit messages, to understand what got renamed/replaced — e.g. commit "compounds become a peer panel, stacked below notes on mobile" and "feat: convert compounds bar into a draggable snap drawer" both touched compounds-bar/detail-panel machinery, so that area is a good place to check first for other leftovers beyond the one already known).
> 
> Do NOT edit any files. This is read-only investigation. Report back a list of concrete findings, each with: file:line, what's stale, why (what superseded it or why it's unreachable), and confidence (confirmed via grep cross-reference vs suspected). Skip anything you're not reasonably confident about — false positives waste the user's time chasing ghosts. Keep the report tight: a findings list, not prose explanation of your process.

**Result (as captured):** confirmed 6 dead-code findings with file:line citations - a CSS class (`.compounds-collapsed`) never added by JS; a whole "sort compounds by intensity/confidence/class" header (`.compounds-header` and 5 descendant CSS rules) with no matching markup anywhere; its JS-side twin, `state.sortBy`, declared but never read or written elsewhere; a stale `header .spacer` CSS rule superseded by a renamed `.hud-spacer` (still correctly used at three other locations); a `.tx-rank-segment.noninteractive` CSS rule that JS never assigns; and an unused `.cx-caveat` (Constellation) class superseded by `.delivery-caveat`/`.taxonomy-compare-layer-caveat`. Also explicitly listed what it checked and ruled clean (all named functions are called, all `getElementById` targets exist, no orphaned commented-out code, the compounds-drawer and taxonomy-sheet drag systems are two genuinely separate live features rather than a duplicate pair) so those are not re-flagged later.
