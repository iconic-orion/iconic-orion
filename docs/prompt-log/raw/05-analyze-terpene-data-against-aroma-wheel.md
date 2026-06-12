# 05 — Analyze terpene data against aroma wheel

- **Date:** 2026-05-22
- **Branch(es):** claude/confident-wilbur-bec633
- **Source:** Claude Code session `208d07b1`
- **Prompts:** 5

> Curated summary: [../README.md](../README.md) (entry 05)

---

### 1 · May 22, 19:57
> Without changing our code, just investigate if this table could meaningfully add to our current understanding of aromas in the current aroma wheel.  this is what I had approximated when I made the terpene wheel earlier using chatgpt.  approximated for scoring between 1-10 how strongly each of these terpenes would have to show up in order to mimic the chosen aroma: 
> Aroma 	Linalool 	Limonene 	Geraniol 	Terpineol 	Myrcene 	Caryophyllene 	Pinene 	Humulene
> Orange	2	9	1	1	1	1	1	0
> Lemon	1	9	1	1	1	1	1	0
> Grapefruit	2	8	2	1	1	1	1	0
> Strawberry	4	3	3	2	3	2	1	0
> Cherry	3	3	3	2	2	4	1	1
> Raspberry	4	2	3	2	3	3	1	1
> Apple	2	4	2	1	1	1	1	0
> Pear	3	3	2	1	1	1	1	0
> Peach	4	3	3	2	3	1	1	0
> Pineapple	2	7	2	2	2	1	1	0
> Mango	2	3	2	2	7	2	1	1
> Jasmine	7	2	5	4	1	1	1	0
> Rose	6	2	8	3	1	1	1	0
> Lavender	7	2	4	5	2	1	1	0
> Elderflower	5	2	4	3	1	1	1	0
> Caramel	3	2	2	1	4	5	1	2
> Honey	5	2	3	3	2	2	1	1
> Vanilla	3	3	2	4	2	2	1	1
> Chocolate	2	2	2	2	4	5	2	3
> Almond	2	2	1	1	4	3	2	1
> Hazelnut	2	2	1	1	3	4	3	2
> Walnut	2	2	1	1	3	4	2	3
> Cocoa	2	2	1	1	4	5	2	3
> Cinnamon	2	3	1	1	2	5	1	1
> Clove	3	2	2	1	4	7	2	1
> Pepper	2	2	1	1	3	8	3	6
> Anise	3	4	2	2	1	2	1	0
> Toasted Nuts	2	2	1	1	4	4	2	2
> Caramelised Sugar	3	2	2	1	3	4	1	2
> Smoke	1	1	1	1	2	4	4	6
> Tobacco	1	1	1	1	3	6	2	7
> Fresh Grass	4	3	2	2	2	1	3	1
> Black Tea	5	2	4	2	3	3	1	1
> Mushroom	1	1	1	1	5	2	1	4
> Eucalyptus	3	5	1	1	2	1	7	1
> Winey	5	2	3	2	3	2	1	1
> Balsamic	2	3	1	1	3	5	1	4
> Yeast/Bready	1	1	1	1	3	4	1	3
> Leather	1	1	1	1	4	5	1	5

**→ Agent:** I've read through the current wheel ([index.html](index.html)) and compared it against your old terpene table.  _Actions:_ Read project_aroma_wheel.md · Bash: List repo root · Glob **/*.{html,js,json} · Read index.html

### 2 · May 22, 20:09
> So let's look for literature to check on the following: α-Terpineol — pine/lilac, present in citrus juice (heat-degraded limonene), tea, some coffees.
> α-Humulene — woody-hoppy, co-occurs with caryophyllene in pepper, hops, cannabis; relevant if you ever add a "hoppy" note.
> 2. Notes we don't yet have, but the table reminds us exist — these are real and well-studied:
> 
> Tobacco (megastigmatrienones, β-damascenone — we already have damascenone)
> Leather (4-ethylphenol, 4-ethylguaiacol — Brett markers in wine)
> Eucalyptus (1,8-cineole — a real monoterpene ether we don't carry)
> Black tea (linalool oxides, β-damascenone, hexanal)
> Elderflower (cis-rose oxide, linalool — niche but iconic for mocktails, your stated primary domain)
> Balsamic (acetic acid, ethyl acetate, sotolon — fermented-aged). 
> Blueberry; Soy sauce.

**→ Agent:** I'll research each in parallel — looking for GC-MS / odor-activity literature anchors comparable to what's already in the wheel.  _Actions:_ ToolSearch · WebSearch ×10

### 3 · May 22, 20:11
> Black tea (linalool oxides, β-damascenone, hexanal)
> Elderflower (cis-rose oxide, linalool — niche but iconic for mocktails, your stated primary domain)
> Balsamic (acetic acid, ethyl acetate, sotolon — fermented-aged). 
> Blueberry; Soy sauce.

**→ Agent:** Picking up from where I cut off — the literature anchors for those five: ## Black tea ✓ strong **Zhu, Xiao et al.

### 4 · May 22, 20:12
> yep add them in

**→ Agent:** API Error: Claude Code is unable to respond to this request, which appears to violate our Usage Policy (https://www.anthropic.com/legal/aup).

### 5 · May 22, 20:13
> can you  tell what would be a safe first step to kick us off

**→ Agent:** Smallest reversible slice that exercises the whole data-flow without touching any structure: **add just eucalyptus + 1,8-cineole as a single note/compound/edge triple, then visuall…

