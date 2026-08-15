# 19 - Create PR for mobile UI fixes

- **Date:** 2026-06-27
- **Branch(es):** claude/mobile-ui-pass-3
- **Source:** Claude Code session `2ba1ce5d`
- **Prompts:** 17
- **Provenance:** transcript-backed (verbatim, extracted 2026-07-26)

> Verbatim human prompts only. Unlike entries 01-13, this file carries **no**
> per-prompt response summaries - those were written by hand for the earlier
> entries and have not been written for this one yet. Nothing here is
> paraphrased; absent commentary is absent, not implied.

---

### 1 - Jun 27, 08:33
> can we make a new pr from this branch to prototype? I want to work on more mobile ui fixes.

### 2 - Jun 27, 15:24
> so let's look at pr 9 then actually and see what got scoped out on there?

### 3 - Jun 27, 15:28
> let's model what this looks like on s10e phone screen size because that's honestly how it will be demoed irl

### 4 - Jun 27, 15:31
> yep go ahead and start fixing that. we'll deal with things as they come up together in real time.

### 5 - Jun 27, 15:36
> Another real issue I saw happen live with multiple users is that they have no obvious way to scroll the flavor notes without selecting a slider to change. Everytime they scroll, that thumbslide reads as input. Easiest fix for my taste is to shorten the horizontal axis on those sliders so they are left justified and only take up a   third of the horizontal axis of the portrait screen width.

### 6 - Jun 27, 15:45
> Also "I find the lack of [nuance between orange and lemon] disturbing." And for that matter it would  be very important to me to address what notes in the note suggester are simply approximated to flavor notes and which ones actually line up. Those that are truely represented in the official flavor note sliders can be left alone from the following task:
> Those notes in note suggester that are: a) naturally occuring, or retrieved through distillation/concentration of natural substances (not synthetic flavors like cotton candy), and are approximated in the flavor notes like bergamot ending up as an approximation of lemon and orange or just generic citrus. there are definitely some key compounds that identify bergamot from a yuzu from a meyer lemon from a  navel orange from a tangerine... this is a real use of go deeper. Having a streamlined quick-use mode as "default" and then go deeper turns each quick-use flavor note into a collection of categories based on the wheel itself - how meta! fruity > citrus > orange vs fruity > citrus > grapefruit.

### 7 - Jun 27, 15:50
> raise priority to high on olive, beetroot, artichoke.

### 8 - Jun 27, 15:54
> citrus and berry, oh and certainly the following flavors plus a personal necessity: coconut, ginger, pistachio, pecan, rice, maple, quinoa, barley, wheat, millet, oats, thyme, sage, eucalyptus, honeysuckle.

### 9 - Jun 27, 16:17
> +I definitely feel like for each of those we could routee to just default (cereal) and then there is a tiny table form of organizing tastefully displaying what special compounds each cereal grain distinguishes it from the others.

### 10 - Jun 27, 16:27
> commit and then continue with citrus

### 11 - Jun 27, 16:40
> also let's distinguish later with herbs spearmint from peppermint from wintergreen

### 12 - Jun 27, 17:07
> commit doc update and then move to berry

### 13 - Jun 27, 17:16
> please rewrite this phrase so it just states what is listed. un ai-speak please.

### 14 - Jun 27, 17:17
> This is what's layered on top of Berry's own shared compounds (above), where the evidence actually shows something distinct — not where it'd be tidy to invent a difference for every variet

### 15 - Jun 27, 17:18
> fold it in

### 16 - Jun 27, 17:25
> push to github branch

### 17 - Jun 28, 07:32
> let's try that again now that we have usage

