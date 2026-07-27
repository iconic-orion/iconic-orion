# 20 - Prepare herbal floral slice for PR

- **Date:** 2026-06-28
- **Branch(es):** claude/mobile-ui-pass-3
- **Source:** Claude Code session `5223ccad`
- **Prompts:** 20
- **Provenance:** transcript-backed (verbatim, extracted 2026-07-26)

> Verbatim human prompts only. Unlike entries 01-13, this file carries **no**
> per-prompt response summaries - those were written by hand for the earlier
> entries and have not been written for this one yet. Nothing here is
> paraphrased; absent commentary is absent, not implied.

---

### 1 - Jun 28, 08:38
> Let's continue the herbal/floral slice and prepare this branch to be pr'd into prototype asap

### 2 - Jun 28, 08:40
> let's prepare this branch to be pr'd into prototype in one click

### 3 - Jun 28, 14:54
> yes please. all clear to continue

### 4 - Jun 28, 15:34
> where does thyme surface in the ui?

### 5 - Jun 28, 15:38
> The note selection needs to be updated to surafce the categories first - Fruity, floral, etc. and then under that, divide by plant family, order, class, or genus if needed if enough notes in the wheel are related that closely that we need to label their grouping according to that taxonomy level that contains them all.

### 6 - Jun 28, 17:07
> can we put all of the flavor notes on a taxonomy tree? this is the third viewer along with wheel and map.

### 7 - Jun 28, 19:19
> please add zoom + - to tree.

### 8 - Jun 28, 20:40
> I want to see the varietals of notes as a dropdown choooseable on it's flavor note slider title. so mint would have a mint dropdown for peppermint spearming and wintergreen specification

### 9 - Jun 28, 20:41
> rather its expandable in all modes (both default and in go deeper,  which basically means it's just a daefault feature). So I want to be able to apply a flavor note score from 1-10 for peppermint and for spearmint independently which I cannot do in the current config

### 10 - Jun 29, 01:23
> some of these drop-downs need to be restructured with flavor notes that logically fit. for example, berry note can fit all notes that have berry in the name or are culinary berries (not botanic berries as that would be a far larger group)

### 11 - Jun 29, 01:41
> also stonefruit should involve peach, plum, and a copy of cherry (ghost opacity that copies automatically to cherry's own flavor note even though it is stone fruit it's iconic enough to need it's own flavor note row still in fruity)

### 12 - Jun 29, 02:24
> I want the same to happen with all notes under cereal

### 13 - Jun 29, 02:36
> melon / Cucumber implies plain melon flesh as opposed to sweet distinguished melon flavor right?

### 14 - Jun 29, 02:40
> go with Cucumber  and then separately, melon rind, different kinds of melon s individual notes watermelon, honeydew, cantaloupe,

### 15 - Jun 29, 02:51
> let's also add chicken egg, chicken (white meat), and chicken (dark meat), turkey, duck egg, duck meat, bacon, pork (plain), beef (plain), chicken flavor (celery, onion, carrot, tumeric), beef flavor (tomato, onion... (look this up for veg base, non animal ingredients that usually enhance beef worldwide)
> 
> also chicken stock, beef stock, pork stock
> 
> red, white, sweet, green onion, celery, carrots, tomato, arugula, romaine lettuce,  iceberg lettuce, white and green cabbage, potato, Brussel sprouts, sweet potato, ube, taro, garlic, Wasabi, horseradish, miso paste, soy sauce...

### 16 - Jun 29, 06:57
> when looking at the compounds as opposed to flavor notes on the wheel, let's make the only compounds that visibly take up space on the wheel, the active ones announced in the flavor notes  a user adds. attempting to show all possible at all times crowds the wheel, especially on mobile.

### 17 - Jun 29, 07:32
> the dropdown arrow is incredibly small, even with mouse pointer and on mobile. please make that arrow more prominent so it's obvious it's a dropdown and not just a speck on screen

### 18 - Jun 29, 07:35
> the dropdown arrow is incredibly small, even with mouse pointer and on mobile. please make that arrow more prominent so it's obvious it's a dropdown and not just a speck on screen. if anything make the entire label row up to the number that displays note score be a "button" but not changing the look, just expanding the clickable area that makes the dropdown trigger. Also let's include a "thumb width" of space between the end of the slider width and the end of the pane in case someone is using a touch screen widescreen monitor. similar issue with not being able to scroll witrhout clicking a slider accidentally.

### 19 - Jun 29, 07:52
> if I just do 5 cranberry, without anything on berry parent, only circles show up with no lines leading to anything on the wheel. furthermore it seems like you'd have to do both berry and cranberry for the full compound list to show up. can you figure out how to simplify this where I could just put cranberry instead of having to hit  "berry" first and rhen add cranberry on top of it

### 20 - Jun 29, 11:35
> beautiful these changes are exactly what I wanted. can you get this ready so I can merge into prototype

