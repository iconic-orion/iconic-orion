# 09 — Audit scent library for missing common sources

- **Date:** 2026-05-26
- **Branch(es):** prototype
- **Source:** Claude Code session `5f2fe804`
- **Prompts:** 8

> Curated summary: [../README.md](../README.md) (entry 09)

---

### 1 · May 26, 18:43
> Without changing code can you help me identify all examples where we miss key data that a quick google search would suggest otherwise? Example: β-Damascenone doesn't mention rose when that is a pretty significant one right? Can we do a pass on the scent library we have and make sure we don't miss any more of these "common natural sources".

**→ Agent:** I read through the whole compound library and the `COMPOUND_ORIGINS` block in [index.html:770-1011](index.html:770).  _Actions:_ Glob **/*.{json,js,ts,html} · Grep Damascenone · Bash: Count lines · Read index.html

### 2 · May 26, 18:46
> add all but cannabis unless you name it "hemp".

**→ Agent:** I'll add the origin updates plus the three edge additions.  _Actions:_ Edit index.html ×10

### 3 · May 26, 18:49
> It's hard to see compounds right now on their own. We need to probably just include the regular results panel minus the usuer inputs since there are none at  the start. put this under "Slide notes on the left to see what compounds they map to, ranked by literature confidence.
> Suggestions, not analysis. Based on common aroma knowledge and GC-MS citations. What this isn't →"

**→ Agent:** I'll update the empty-state block to also render a browseable list of all compounds (grouped by class, no intensity bars since there's no signal yet), clickable to drill into each…  _Actions:_ Grep Slide notes on the left · Read index.html · Edit index.html · Grep \.compound-compact|\.compact-row · Read index.html · Edit index.html

### 4 · May 26, 18:51
> please add rose first to the list that starts with "Cooked-apple/honey/tobacco;..." i'm just, c'mon let's be explicit about these associations

**→ Agent:** Done — rose now leads the β-Damascenone short descriptor.  _Actions:_ Edit index.html

### 5 · May 26, 18:53
> keep in mind though wine will inspire this, i feel the tone of this is getting too wine specific. remember this needs to be accessible to a non-drinking or sober crowd most of all.

**→ Agent:** Good catch. Let me revise the recent edits to de-emphasize wine/spirits and lead with sources a non-drinker would recognize.  _Actions:_ Edit index.html ×4 · Grep wine|Sauvignon|Riesling|Chardonnay|whisky|whisk… · Write feedback_non_wine_accessibility.md · Read MEMORY.md · Edit MEMORY.md

### 6 · May 26, 18:54
> i do think the oaky barrel taste is quite interesting so if there are some compounds that can ONLY exist in these processes but show up in other places in trace amounts, it's okay to talk about that.

**→ Agent:** Got it — the rule isn't a blanket scrub of alcohol; it's about default framing.  _Actions:_ Edit feedback_non_wine_accessibility.md · Edit index.html

### 7 · May 26, 18:56
> beautiful. absolutely. Do your best and make sure each compound gets some love. To the point but significant.

**→ Agent:** Let me reread all the current origin entries so I rewrite from the actual state.  _Actions:_ Read index.html ×2 · Edit index.html

### 8 · May 26, 19:39
> looks great. commit and push

**→ Agent:** We're on `prototype` (Netlify auto-deploys this to aromawheel.net).  _Actions:_ Bash: Show working tree status · Bash: Show diff stats · Bash: Show recent commits · Bash: Show current branch · Bash: Stage and commit the compound library updates · Bash: Push to origin/prototype

