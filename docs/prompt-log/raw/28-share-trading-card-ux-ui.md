# 28 - Share trading card UX/UI

- **Date:** 2026-07-10
- **Branch(es):** feature/bloom
- **Source:** Claude Code session `021f6dc9`
- **Prompts:** 9
- **Provenance:** transcript-backed (verbatim, extracted 2026-07-26)

> Verbatim human prompts only. Unlike entries 01-13, this file carries **no**
> per-prompt response summaries - those were written by hand for the earlier
> entries and have not been written for this one yet. Nothing here is
> paraphrased; absent commentary is absent, not implied.

---

### 1 - Jul 10, 07:13
> the next step for this branch is creating a map inset that can fit onto a "share trading card" (calling it that just to illustrate approximate size and display of information for people to compare readings) This is a feature that is optional for the user to check if they want it to display with their chosen ingredietns. to be fair, this might be something that needs to be a separate "card" like a front/back situation even though most people are going to only use this on their device - might be nice to actually make that a "flip over" animation where it does look like both sides rendered on a mockup of a card that gets flipped over when you select the "flip card" button - this should also be optional where a user can choose to instad dispaly it all on one card. Basically, i need you to help me with the user experience and ui side of this feature so that the sharing is sense-making in that what you see on the card is actually something that is easily caomparable with others and easy to add or subtract as much info as user wants to fit on their personalized card.

### 2 - Jul 10, 07:59
> please continue your thought process

### 3 - Jul 10, 18:07
> can we reverse the control axis on the compass englarger button-drag interface? I'd like it to expand to the left as I draqg the button to the left. Right now I need to drag my mouse button to the right in order for it to expand on the left side outward which feels opposite of what i would normally expect from a click-and-drag to expand the compass window to work.

### 4 - Jul 10, 18:25
> works beautifully. Let's have "Reading Mode" Swallow the "Turn Jiggle Off" aspect of the jiggle button. Right now, the flavor notes are all vibrating no matter waht. i need them to rest at equilibrium reasonably timely.

### 5 - Jul 10, 18:35
> Let's Make reading mode default. i like the ux of this

### 6 - Jul 10, 18:38
> Too many options is my point. Let's remove these options entirely and make the state be the default experience of the app

### 7 - Jul 10, 19:24
> Yeah either of those sound promising. go for it

### 8 - Jul 10, 19:48
> commit anything that needs it

### 9 - Jul 10, 19:49
> This session is being continued from a previous conversation that ran out of context. The summary below covers the earlier portion of the conversation.
> 
> Summary:
> 1. Primary Request and Intent:
>    - Create a map inset feature for a shareable "trading card" with optional front/back flip layout and customizable downloads
>    - Reverse the compass resize grip control axis to match OS conventions (drag left to expand left, right edge anchored)
>    - Make Reading Mode control both visual legibility AND motion (freezing the float sim's perpetual drift and device-motion jiggle)
>    - Make Reading Mode the default state (on by default on page load)
> 
> 2. Key Technical Concepts:
>    - 3D CSS flip-card transforms with perspective and preserve-3d
>    - Equirectangular map projection (lat/lon to SVG coordinates)
>    - D3 force-directed simulation control (alpha targets, idle state management)
>    - Device motion event handling and gesture-based UI
>    - Canvas stacking for multi-page image exports
>    - State predicate pattern (bubblesFrozen() as single source of truth for motion freeze)
>    - URL parameter persistence for shareable links
>    - Pointer events for drag-based resize with geometry anchoring
> 
> 3. Files and Code Sections:
>    - D:\Git_NAE\index.html (single file, comprehensive changes)
>      - CSS additions for share card flip stage (.share-flip-stage, .share-flip-inner, .share-face-front, .share-face-back with prefers-reduced-motion guard)
>      - CSS for map inset styling
>      - HTML controls: Layout segmented buttons (One card / Front & back), Origin map checkbox, Flip card button
>      - mapLatLonToXY() helper: converts lat/lon to SVG pixel coordinates using same projection as live Origins map
>      - originItemsFor() helper: filters active notes to those with NOTE_ORIGINS entries
>      - mapInsetGroup() helper: renders minimal dot-plot with numbered pins (colored by group, dashed for approximate origins), numbered legend, and graticule; includes fallback "No origin data" message
>      - buildShareCard(face) refactored: now accepts "single", "front", or "back" parameter; single card includes optional map section; front/back faces have independent layouts
>      - stackedCanvas() helper: stacks front+back canvases vertically for PNG/JPG downloads
>      - downloadPdf() updated: creates 2-page PDF (front on page 1, back on page 2) for flip layout
>      - bubblesFrozen() predicate: returns true when state.freezeBubbles OR state.readingMode is true (single source of truth)
>      - applyFreezeMode() updated: uses bubblesFrozen() instead of just state.freezeBubbles
>      - driftForce() updated: early-returns on bubblesFrozen() instead of state.freezeBubbles
>      - setReadingMode() updated: calls applyFreezeMode() when toggled, snaps jiggle offsets to zero if jiggleRAF is running
>      - jiggleTick() updated: holds notes layer at identity (no transform) while state.readingMode is true
>      - Compass resize handlers (setupCompassDragAndResize): inverted width calculation from (resizeStartWidth + delta) to (resizeStartWidth - delta), now anchors right edge and tracks left position
>      - State initialization: readingMode changed from false to true
>      - End-of-script sync added: setReadingMode(state.readingMode) called after all dependencies (jiggleRAF, gNotes, gComps) declared
> 
> 4. Errors and fixes:
>    - Initial compass resize test showed geometry squashing due to headless browser reporting degenerate viewport; fixed by overriding wheel.clientWidth/clientHeight in test to realistic desktop values (1200x800). Logic verified correct; behavior confirmed in real browser.
>    - Tools preview_click silently no-op'd; worked around by dispatching .click() via javascript_exec
>    - setReadingMode() initially placed inline at definition, causing temporal dead zone error for jiggleRAF; moved to end-of-script initialization block alongside setCompassVisible()
> 
> 5. Problem Solving:
>    - Share card map inset: designed as minimal dot-plot (no country borders) to maintain crispness at small inset size and ensure pins stay at consistent positions across different users' cards
>    - Flip card downloads: chose stacked PNG/JPG (practical for social sharing, single image) vs true 2-page PDF (for physical card printing)
>    - Reading Mode as freeze master switch: unified bubblesFrozen() predicate eliminates state disagreement between sim alpha target and drift force; ensures consistent settle behavior
>    - Compass resize UX: anchoring right edge (not left) while dragging left matches top-left-corner-grip OS convention
> 
> 6. All user messages:
>    - "the next step for this branch is creating a map inset that can fit onto a "share trading card" (calling it that just to illustrate approximate size and display of information for people to compare readings) This is a feature that is optional for the user to check if they want it to display with their chosen ingredietns. to be fair, this might be something that needs to be a separate "card" like a front/back situation even though most people are going to only use this on their device - might be nice to actually make that a "flip over" animation where it does look like both sides rendered on a mockup of a card that gets flipped over when you select the "flip card" button - this should also be optional where a user can choose to instad dispaly it all on one card. Basically, i need you to help me with the user experience and ui side of this feature so that the sharing is sense-making in that what you see on the card is actually something that is easily caomparable with others and easy to add or subtract as much info as user wants to fit on their personalized card."
>    - "can we reverse the control axis on the compass englarger button-drag interface? I'd like it to expand to the left as I draqg the button to the left. Right now I need to drag my mouse button to the right in order for it to expand on the left side outward which feels opposite of what i would normally expect from a click-and-drag to expand the compass window to work."
>    - "works beautifully. Let's have "Reading Mode" Swallow the "Turn Jiggle Off" aspect of the jiggle button. Right now, the flavor notes are all vibrating no matter waht. i need them to rest at equilibrium reasonably timely."
>    - "Let's Make reading mode default. i like the ux of this"
> 
> 7. Pending Tasks:
>    - Verify fresh page load with Reading Mode default (check body class applied, aria-pressed set, float sim frozen, no console errors)
> 
> 8. Current Work:
>    Completed implementation of Reading Mode as default by:
>    - Changed state.readingMode from false to true in initial state object (line ~4547)
>    - Added setReadingMode(state.readingMode) call at end of script initialization (after line 8590, after setCompassVisible and freezeToggleCheck.checked sync)
>    - This ensures on page load: body gets reading-mode class, Atkinson Hyperlegible font lazy-loads, aria-pressed set on toggle button, float sim receives initial freeze decision from applyFreezeMode()
>    Verification was about to begin in browser when summary request arrived.
> 
> 9. Optional Next Step:
>    Verify fresh page load displays Reading Mode active by checking: (1) body.classList contains "reading-mode", (2) #reading-toggle has aria-pressed="true", (3) sim.alphaTarget() === 0 (frozen), (4) console.readyState === "complete" with no errors. This confirms the state initialization and end-of-script sync worked correctly.
> 
> If you need specific details from before compaction (like exact code snippets, error messages, or content you generated), read the full transcript at: C:\Users\njale\.claude\projects\D--Git-NAE\021f6dc9-5284-465a-b3d9-3a5d2c8e8ca2.jsonl
> Continue the conversation from where it left off without asking the user any further questions. Resume directly — do not acknowledge the summary, do not recap what was happening, do not preface with "I'll continue" or similar. Pick up the last task as if the break never happened.

