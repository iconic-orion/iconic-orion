# 34 - Shareable tasting card UI review

- **Date:** 2026-07-11
- **Branch(es):** codex/aroma-wheel-responsive-ux-pass
- **Source:** Claude Code session `d5322d55`
- **Prompts:** 7
- **Provenance:** transcript-backed (verbatim, extracted 2026-07-26)

> Verbatim human prompts only. Unlike entries 01-13, this file carries **no**
> per-prompt response summaries - those were written by hand for the earlier
> entries and have not been written for this one yet. Nothing here is
> paraphrased; absent commentary is absent, not implied.

---

### 1 - Jul 11, 20:34
> # Shareable Tasting Card UI Review Scope
> 
> ## Objective
> Review ONLY the shareable tasting card UI and its interaction surface. Ignore all other features, workspaces, controls, and content in the page.
> 
> ## Strict Scope Boundaries
> 
> ### IN SCOPE — Review these and only these:
> - The shareable card's visual container/frame
> - Compound list with per-compound visibility toggles (checkboxes or equivalent)
> - Notes list with visibility toggles
> - Export button(s) or action(s) that trigger export (PNG/JPG/PDF)
> - Share/bookmark link generation UI
> - Any modals, popovers, or panels that open when these controls are clicked
> - Copy-to-clipboard affordance for the share link
> - Layout, spacing, typography, color, and accessibility of the card UI itself
> 
> ### OUT OF SCOPE — Explicitly ignore:
> - The main aroma wheel and its interactions
> - The compass widget (all three modes)
> - Map/origins workspace
> - Tree/taxonomy workspace  
> - Any note row sliders or intensity inputs
> - Go Deeper panel and its contents
> - Header navigation (Wheel/Map/Tree tabs, Settings, ••• menu)
> - Legend, group visibility toggles
> - Chemistry mode or compound-anchor interactions
> - Mobile HUD layout outside the shareable card context
> - Any help text, tooltips, or explanatory content not directly tied to the card UI
> 
> ## Procedure
> 
> 1. Start the app and let it fully load
> 2. Take a screenshot of the full page (for context only)
> 3. Locate the shareable card UI — it should be a discrete panel/modal showing compounds and notes with visibility toggles and export/share actions
> 4. Review only that card's:
>    - Visual hierarchy and alignment
>    - Toggle switch behavior and responsiveness
>    - Export button state/visibility/labeling
>    - Share link display and copy interaction
>    - Mobile vs. desktop layout of the card itself
>    - Color contrast and readability of the card content
>    - Keyboard accessibility (tab order, focus states) **within the card only**

### 2 - Jul 11, 20:47
> update the rule where you can also update this branch. this si just the only one i want chatgpt touching

### 3 - Jul 11, 20:51
> commit aND PUSH

### 4 - Jul 11, 20:52
> More stunning should mean "Bigger wheel and less text" more informative is pretty much what it lokos like by default

### 5 - Jul 11, 20:56
> eh better. go for more stunning. like no extra details besides the flavor notes and dominatnt compounds which users can choose if theyshow all or only a few. they can customize the caption ifthey wish and also if they want the perception compass to be visible or their flavor note hud visible. but the compounds data bar graph is too much for stunning, that's more informative coded, as is the map read out. so by default, more stunning should ONLY be the wheel. fusers can add more if they wish but these are optional.

### 6 - Jul 11, 21:09
> this is pretty cool.

### 7 - Jul 11, 21:09
> commit and push

