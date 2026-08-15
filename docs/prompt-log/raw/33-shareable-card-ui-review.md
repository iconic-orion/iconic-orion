# 33 - Shareable card UI review

- **Date:** 2026-07-11
- **Branch(es):** codex/aroma-wheel-responsive-ux-pass
- **Source:** Claude Code session `f8cc6db1`
- **Prompts:** 1
- **Provenance:** transcript-backed (verbatim, extracted 2026-07-26)

> Verbatim human prompts only. Unlike entries 01-13, this file carries **no**
> per-prompt response summaries - those were written by hand for the earlier
> entries and have not been written for this one yet. Nothing here is
> paraphrased; absent commentary is absent, not implied.

---

### 1 - Jul 11, 20:31
> # Shareable Card UI Review Scope
> 
> ## Objective
> Review ONLY the shareable card UI and its interaction surface. Ignore all other features, workspaces, controls, and content in the page.
> 
> ## Strict Scope Boundaries
> 
> ### IN SCOPE — Review these and only these:
> - The shareable card's visual container/frame
> - Item list(s) with per-item visibility toggles (checkboxes or equivalent)
> - Export button(s) or action(s) that trigger export (PNG/JPG/PDF)
> - Share/bookmark link generation UI
> - Copy-to-clipboard affordance for the share link
> - Any modals, popovers, or panels that open when these controls are clicked
> - Layout, spacing, typography, color, and accessibility of the card UI itself
> - Button states, hover effects, disabled states
> 
> ### OUT OF SCOPE — Explicitly ignore:
> - Any wheel, compass, or visualization widgets
> - Main content areas or workspaces
> - Workspace navigation tabs
> - Header controls and menus
> - Settings, sliders, or input controls outside the card
> - Legend or category toggles
> - Panels or sidebars unrelated to the card
> - Help text or explanatory content not directly tied to the card UI
> - Any feature functionality outside the card itself
> 
> ## Procedure
> 
> 1. Start the app and let it fully load
> 2. Take a screenshot of the full page (for context only)
> 3. Locate the shareable card UI — it should be a discrete panel/modal showing lists with visibility toggles and export/share actions
> 4. Review only that card's:
>    - Visual hierarchy and alignment
>    - Toggle switch behavior and responsiveness
>    - Export button state/visibility/labeling
>    - Share link display and copy interaction
>    - Mobile vs. desktop layout of the card itself
>    - Color contrast and readability within the card
>    - Keyboard accessibility (tab order, focus states) **within the card only**
>    - Button styling and spacing consistency
> 5. Do not click, interact with, or review anything else on the page
> 6. Report findings ONLY about the shareable card UI — do not mention other features, even tangentially
> 
> ## When In Doubt
> Ask: "Is this a control or UI element that belongs to the shareable card?" If no, skip it entirely.

