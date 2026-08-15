# 16 - Create citations list and project documentation

- **Date:** 2026-06-10
- **Branch(es):** claude/compound-library
- **Source:** Claude Code session `8df00cf3`
- **Prompts:** 20
- **Provenance:** transcript-backed (verbatim, extracted 2026-07-26)

> Verbatim human prompts only. Unlike entries 01-13, this file carries **no**
> per-prompt response summaries - those were written by hand for the earlier
> entries and have not been written for this one yet. Nothing here is
> paraphrased; absent commentary is absent, not implied.

---

### 1 - Jun 10, 18:00
> Can I get a full list of the citations? In fact we should probably just make some supporting docs  about like the project scope and what sources were chosen and for what pieces of information, or broad conceptual or theorhetical claims about how aroma perception should inheriantly lead to at least some about of confidence of identifying the probably aroma compounds that would be confirmed chemically.

### 2 - Jun 10, 19:05
> soooo would it be wise to publish this in the current form to the live website?

### 3 - Jun 10, 19:42
> yep please check every short-form citation.

### 4 - Jun 10, 20:18
> Try again to find either the real citations for those last few that were unclear or another citation source that does fit.

### 5 - Jun 10, 20:25
> yes apply all to index.html except schreier for some reason? if you pick one that is good enough go with that

### 6 - Jun 11, 17:22
> let's double check and see if we are behind on commits here I think there's multiple things happening here. Can you see how you can merge to prototype these new additions without conflicting?

### 7 - Jun 11, 17:27
> standalone pr. yep get it up to mergeable without merging on your own

### 8 - Jun 11, 17:32
> "Compilation of Odour Threshold Values in Air and Water (2nd ed., Oliemans Punter & Partners, 2011), which gathers roughly 10,750 threshold values drawn from ~1,780 sources and is the reference work this tool's threshold tiers are sanity-checked against."  That's in the citations.... are we using all of those 10,000 threshold values? Is there anything in that compilation that we should add into the wheel?

### 9 - Jun 11, 17:36
> I like your instinct but I do want this to serve a wide audience so it should have compounds that will capture the experiences of more people. I'm cool taking the time to do it for the sake of the library we are building in this format.

### 10 - Jun 11, 17:55
> I also notice that a lot of berry note suggester just go to "berry" flavor note. That seems boring. I feel like blueberry gives widely different flavor than strawberry and it should be represented with the compounds that appear for that.

### 11 - Jun 12, 08:35
> ah so we ran out of limits last night and then i had gpt5.5 try to help but that might have messed something up on local. can you go through your context and seee where you left off and check and see where our newest info lives so we don't clobber any legit work 5.5 did?

### 12 - Jun 12, 08:43
> so a few things, let's fold berry expansion into the local library branch so we can pr it all at once

### 13 - Jun 12, 08:55
> what happened that limited python from your use?

### 14 - Jun 12, 08:58
> I think let's rely on netlify deploy preview which you can navigate to in the in-app browser

### 15 - Jun 12, 08:58
> also can we commit anything from this chat specifically that needs to be sent up to the pr?

### 16 - Jun 12, 09:07
> can you send me a link to that pr

### 17 - Jun 12, 09:42
> do most of these changes surface on the wheel in some way?

### 18 - Jun 12, 09:53
> anything else here that needs merging?

### 19 - Jun 14, 19:23
> can you check the curretn status of the local vs online repo and make sure we are updated local to whatever is newest?

### 20 - Jun 14, 19:26
> yeah let's make sure this pr is going for the latest prototype

