# 04 — Build terpene wheel scent mapper visualization

- **Date:** 2026-05-21 → 2026-05-31
- **Branch(es):** claude/determined-williams-8ac428
- **Source:** Claude Code session `4df3d0ad`
- **Prompts:** 19

> Curated summary: [../README.md](../README.md) (entry 04)

---

### 1 · May 21, 21:06
> Aight so the terpene wheel scent mapper just needs to be built from scratch we should just start buioldign it. just do it like i referenced here: Got it — the substrate is broad-palate aromatics (coffee + mocktails as primary, foodie/cannabis-adjacent as bonus) and the inference grounds in published GC-MS literature rather than vibes.
> 
> Here's the shape I'd recommend, then I'll build:
> 
> Single static index.html (vanilla JS + D3 via CDN) — same shipping path as your old prototype, easy to host, easy to fork.
> Viz: force-directed graph with a radial backbone. Flavor notes sit on an outer ring (groups: Fruity, Roasted, Floral, Spice, Nutty, Earthy, Sweet, Fermented…), compounds float in the center, and edges thicken as your 1–10 ratings push contributions. Reads like a wheel but reveals compound clusters, which a sunburst can't.
> Rule-based scoring table with literature citations baked into each note→compound edge (e.g. furfurylthiol → roasted coffee, Blank et al. 2002). Click an edge → see the source. That's the "new brain": transparent, auditable, foodie-friendly.
> Seed library: ~40 notes, ~30 compounds spanning terpenes (limonene, linalool, myrcene), pyrazines (2-methoxy-3-isobutylpyrazine), furans (furfural), thiols (furfurylthiol, 3-MH), esters (ethyl butanoate), lactones (γ-decalactone), aldehydes (vanillin, hexanal). Enough to feel real, small enough to ship in one file.

**→ Agent:** Got it. Building a single static `index.html` — force-directed graph with notes on an outer radial backbone, compounds in the middle, edges weighted by 1–10 sliders, citations bake…  _Actions:_ Bash: List repo contents · Read README.md · Read project_aroma_wheel.md · Write index.html

### 2 · May 21, 21:15
> that's cool that it's kinda reverse engineering perceived scents from the literature saying that these compounds smell like these things

**→ Agent:** 

### 3 · May 21, 21:28
> somehow i want there to be two buttons to go from sensory info to a compounds tab that shows the list of all compounds, with a grey-out applied if it is not suggested at all, and then a liklihood score or confidence score on that specific ingredient for how intense/present it is and how confident we are according to the research on the presence and how humans tend to report perceived smell experiences on the whole and also for very sensitive smellers

**→ Agent:** Good direction. I'll add: - **Tab switcher** in the header (Sensory ↔ Compounds) - **Threshold tier** for every compound (very-low / low / medium / high) — this is the bridge betwe…  _Actions:_ Edit index.html ×7

### 4 · May 21, 21:33
> can we commit this and push

**→ Agent:** Committed (`237f7b7`) and pushed.  _Actions:_ Bash: Check git state and branches · Bash: Stage and commit the new index.html · Bash: Push the feature branch to origin

### 5 · May 21, 21:40
> yeah go ahead and create the pr

**→ Agent:** `gh` isn't installed on this machine, so I can't create the PR programmatically.  _Actions:_ Bash: Create PR targeting prototype branch · PowerShell

### 6 · May 21, 21:41
> yes

**→ Agent:** `gh` is already installed but not on this shell's PATH.  _Actions:_ PowerShell ×8

### 7 · May 21, 21:52
> here's my feedback: most people dont know what blackcurrant tastes like here, so perhaps find other analogs that would be apparent to a wider audience. add lavender and chamomile to florals. remove orange blossom to not confuse with orange fruit. remove dried fruit and tropical unless you specify tropical better - mango and banana in that one, maybe just specify those directly if there corresponding compounds are very individual specific. actually maybe even have a common vs unique flavor note checkbox or slider. for notes that correspond to severla compounds or ones where that compound only really exists in that one thing like i imagine cinnamaldehyde appearing really only in cinnamon.

**→ Agent:** Solid feedback. Going to: 1.  _Actions:_ Edit index.html ×17

### 8 · May 21, 22:00
> it would also be nice to have a legend with what the colors mean and a checkbox next to each entry for visibility. especially if that includes a section with the different compound classes

**→ Agent:** Good call. Adding a Legend panel at the top of the left sidebar with two sections (Note groups + Compound classes), each with a color swatch, label, count, and a visibility checkbo…  _Actions:_ Edit index.html ×11

### 9 · May 21, 22:05
> hmmm i seem to be honing in on two differnt methods of identifying scent. by saying discriptive words vs by identifying taste-alike comparisons. should i make that a flippable option or allow both somehow? i think there should be a search function in there if possible unless its too beefy for a standalone html

**→ Agent:** 

### 10 · May 21, 22:06
> hold that htought. lets commit and push where we are at on prototype

**→ Agent:** Committed (`120568d`) and pushed.  _Actions:_ Bash: Check git state and diff summary · Bash: Commit the iteration and push to the PR branch

### 11 · May 21, 22:07
> let's creat that pr

**→ Agent:** Quick check — what's the state?  _Actions:_ AskUserQuestion · PowerShell ×3

### 12 · May 21, 22:10
> remove typical/sensitive. it's self reported anyway so not much help

**→ Agent:** Pulling it out. I'll collapse the two profiles into a single threshold-modulated intensity so low-threshold compounds still bloom from small evidence, but there's no user-facing to…  _Actions:_ Edit index.html ×8 · Grep profile|intensity_typ|intensity_sens|sensitive|… · Edit index.html

### 13 · May 21, 22:16
> yep and push to prototype

**→ Agent:** Pushed to the feature branch.  _Actions:_ Bash: Check working tree state · Bash: Commit profile-removal and push to feature bra… · PowerShell ×3 · ScheduleWakeup

### 14 · May 21, 22:20
> Confirm PR #2 auto-merged into prototype.

**→ Agent:** Merged. PR [#2](https://github.com/iconic-orion/iconic-orion/pull/2) is closed; CI passed in ~4s; merge commit `f066d15` is on `prototype`.  _Actions:_ PowerShell

### 15 · May 21, 22:23
> where is the index.html being kept rn

**→ Agent:** Stale local ref earlier — `index.html` is on `origin/prototype` (just re-fetched).  _Actions:_ Bash: Check which remote branches have index.html · Bash: Check index.html presence on each remote branc… · Bash: Refresh remote refs and re-check prototype con…

### 16 · May 21, 22:24
> does that cost

**→ Agent:** Free. The repo is public, so GitHub Pages is included at no cost.  _Actions:_ PowerShell

### 17 · May 21, 22:25
> yee

**→ Agent:** Enabled. URL: https://iconic-orion.github.io/iconic-orion/ First build is queued (typically 30 s – 2 min).  _Actions:_ PowerShell ×2 · Bash: Poll Pages build until it finishes

### 18 · May 21, 22:29
> check the build state

**→ Agent:** Built. Site is live at https://iconic-orion.github.io/iconic-orion/ — deploying commit `f066d15` (current `prototype` tip).  _Actions:_ PowerShell

### 19 · May 31, 15:19
> Hey, we got a major accessibility issue here. I think we need to remove the Common/All option and just default to All. On Mobile, that option gets eaten and is nonexistent on smaller screens. plus making a distinction directly says "you're too slow to get this". so let's default to All Notes and just remove that opiton on the header entirely so we have more space to prioritize the View Switcher, Info "i",  Reset (which should be renamed "Start Over", and Go Deeper which adds the ability to do ortho/retro-nasal olfaction and I think might add some percentages at the bottom... but eh those seem misleading because they look like they should add to 100 instead of each of themselves being I suppose percentage represented in the model??? I feel like Go Deeper is missing any real functionality difference that shouldn't already be public-facing.

**→ Agent:** 

