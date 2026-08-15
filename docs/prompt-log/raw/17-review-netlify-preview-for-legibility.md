# 17 - Review Netlify preview for legibility

- **Date:** 2026-06-14
- **Branch(es):** claude/upbeat-mendel-6ef2f6
- **Source:** Claude Code session `f6fd4070`
- **Prompts:** 11
- **Provenance:** transcript-backed (verbatim, extracted 2026-07-26)

> Verbatim human prompts only. Unlike entries 01-13, this file carries **no**
> per-prompt response summaries - those were written by hand for the earlier
> entries and have not been written for this one yet. Nothing here is
> paraphrased; absent commentary is absent, not implied.

---

### 1 - Jun 14, 19:31
> Let's have you run through the online netlify preview and check to make sure things are legible to your likiing

### 2 - Jun 14, 19:33
> 1. i have it open on firefox rn

### 3 - Jun 14, 19:33
> 3

### 4 - Jun 14, 19:38
> Can you do the following: Up-front identity — The biggest real gap. Nothing tells a first-time visitor what this is before they start interacting. The nudge says "Slide a flavor note to begin" but not why or what they'll see. The GPT's suggested one-liner — "Describe what you smell. Explore the chemistry that might explain it." — is basically perfect and could sit right under the h1 as a tagline, visible at all times.
> Domain scope — The app works for coffee/tea/wine/beer/botanicals but nothing makes that explicit upfront. A first visitor might think it's coffee-only.
> "Try these examples" breadth — Two demos is thin. The GPT's list (Ethiopian coffee, orange soda, IPA, dark chocolate, lavender, marinara, black tea) is good precisely because it shows the breadth. This also directly addresses the missing citation coverage for those domains.
> Translation ladder — "What you perceive → Flavor notes → Shared patterns → Aromatic compounds" — this doesn't exist anywhere. It's the one genuinely new structural piece the GPT identified. It belongs in How to Use or as a visual panel in the About tab.
> The "inquiry-based exhibit" framing — The content is there, but the flow doesn't guide people into hypothesis-building. Right now: land → nudge → start sliding. A museum version might be: land → one-sentence frame → try an example → see what lit up → ask why → click a compound → read a citation. The scaffold between steps 2–5 is currently invisible.
> We need documentation about scope + source rationale + the theoretical basis for the sensory→compound inference.
> INFERENCE.md — The conceptual case: why human olfactory perception, when organized through a shared vocabulary trained by sensory science, produces probabilistically meaningful signal about volatile compound families. This is the intellectual backbone GPT identified as the strongest differentiator, and it's currently only implicit in the Methodology tab math.

### 5 - Jun 14, 19:48
> these will be added but are yet to be there due to being on the pr still

### 6 - Jun 14, 19:58
> there's a few chips in the note suggester that i think are not belonging. papaya or guava divert to completely differnt freuits. i think if we dont actualy have that fruit reflected, it doesn't need to be a chip in the note suggester. now fruity flavors that are not real like blue raspberry or bubble gum or  tutti fruitti, these are made up flavors that I think would be cool to suggest likely pairings that manufacturers use in confectionary uses for those natural/artificial flavors which is basically going to be aromatics anyway

### 7 - Jun 14, 20:01
> beautiful. i'd suggest not using cotton candy as its own descriptor in other things unless it is parenthetical when raspberry ketones and methyl anthranilate show up together (cotton candy)

### 8 - Jun 14, 20:02
> input cotton candy is fine, just that if it is nused as a descriptor enough anyway let's be compound forward and then parenthetical to describe that combo in common flavors

### 9 - Jun 14, 20:05
> can we separate cheesey from sweaty

### 10 - Jun 14, 20:15
> even when all flavor notes are off, stray lines stay behind. it isn't until i hit start over... and even sometimes they stay and i have to refresh the page. can we look into that?

### 11 - Jun 14, 20:34
> great go ahead and commit and push everything where it needs to be for prototype to gain all of these fantastic features

