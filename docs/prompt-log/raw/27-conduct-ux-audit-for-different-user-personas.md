# 27 - Conduct UX audit for different user personas

- **Date:** 2026-07-04
- **Branch(es):** feature/bloom
- **Source:** Claude Code session `515cb5e5`
- **Prompts:** 16
- **Provenance:** transcript-backed (verbatim, extracted 2026-07-26)

> Verbatim human prompts only. Unlike entries 01-13, this file carries **no**
> per-prompt response summaries - those were written by hand for the earlier
> entries and have not been written for this one yet. Nothing here is
> paraphrased; absent commentary is absent, not implied.

---

### 1 - Jul 4, 16:16
> can you give my app a checkup from the viewpoints of a casual observer that wants to know what's the point quickly and visually orienting to the best of the best, and a more savvy observer that expects usability over handholding?

### 2 - Jul 4, 16:17
> can you give my app a checkup from the viewpoints of a casual observer that wants to know what's the point quickly and visually orienting to the best of the best, and a more savvy observer that expects usability over handholding?

### 3 - Jul 4, 18:47
> retry whatever you last were trying to do before usage hit

### 4 - Jul 4, 20:21
> Please start working through the punch list.

### 5 - Jul 4, 20:38
> I notice that as a tab through, it does not highlight the label of the note sliders. will a screen reader still see the text even though it's actually the drop down or the "dna" related aroma plant phylogenetic ... etc to the point that the average user isn't really going to get why the dna is there right? argh. is this a go deeper thing?  wait i think I've stumbled upon another go deeper feature - the tree in and of it self that then influences the notes input wit h the dna strands, and in fact the whole go deeper should be infused with vines - think ecobrutalism, go deeper should be sort of nature, flora, human as mammal mindset having that tree shrew back to the trees, back to the vines, "back to nature mannn..." kind of energy here, think otto from the simpsons mixed with alan watts.

### 6 - Jul 4, 20:54
> I like your taste in the design thus far. Go Deeper needs a true artist's lens. Can you help design the transition and artistic represenatation of this humanist perspective visually? This is just for fun and is intended as educational perspective to visualize aroma experience for entertainment purposes but we do cite our sources regardless

### 7 - Jul 4, 21:06
> Yep but both. Build it into the html and do it with this in mind: I like your taste in the design thus far. Go Deeper needs a true artist's lens. Can you help design the transition and artistic represenatation of this humanist perspective visually?  wait i think I've stumbled upon another go deeper feature - the tree in and of it self,, and in fact the whole go deeper should be infused with vines - think ecobrutalism, go deeper should be sort of nature, flora, human as mammal mindset having that tree shrew back to the trees, back to the vines, "back to nature mannn..." kind of energy here, think otto from the simpsons mixed with alan watts.

### 8 - Jul 5, 06:37
> Yeah can you do some artwork on this slice to keep growing the vines into the panels and the Tree next, tune this slice (vine size/opacity/placement, unfurl speed)

### 9 - Jul 6, 08:37
> OK so two things we need to merge together those two different feature branches These are actually connected with the UX checkup and also the greenhouse feature with the go deeper naturalist thing because these are basically looking at a natural expanded learning moment going into what you're already doing in the app and ultimately I want this to be part of a bigger user experience thought process where again people should have access to all the expanded tools when they want to actually sit down and play with this as an extended activity that's what kind of the point of go deeper I think is at this point it's it's when you really know you have time you hit go deeper it blooms and you can go much deeper into like the phylogenetic reasons why certain aromas tend to hang out in certain kinds of plants or they are from certain areas whereas the non go deeper mode is the quick use which is not just like surface level but rather I want the quick use to be able to be just as powerful as go deeper but you don't have to then be figuring out how deep is my question basically that's kind of a user selection to go deeper but what if they actually are still wanting to do something that's equally as important as a go deeper feature should sound like it is but it needs to be able to be like first and foremost on the screen because ultimately this experience is not just an individual journal I wanted to be able to be screenshotable and actually shareable for people to be able to compare and contrast each other's taste experiences together so that's why the display for the wheel needs to be front and center so that way it's an easy visual to share between two different people that is like the same native standard that's that's why it needs to be front and center in these checkups go along with the go deeper features as well so this needs to all be part of the same idea so I see that these are 2 S Pepperid branches at the moment and I think it makes more sense for these to be on the same branch so that way when we're done fixing all of these things it gets pushed altogether as part of a new experience that we're getting into this on top of that we also need to make sure that there is an easy way for someone to share what they have gathered from this and I don't really want to go through the work of making usernames and passwords and that kind of stuff like an actual back end but if there was a way to just generate a output in form of APDF or PNGJPG that kind of stuff Umm that would be really cool because then people can be able to share that to their social media really easily So I imagine you're going to want to make a plan What I want you to actually do is do the organization on Github that that makes these go together and then also I want to see the order of operations that would likely get us from this collection of ideas to a project management order So this is not a plan that goes nowhere this is not a brainstorm that just is into the ether this is an actual step by step process of what you expect it to look like to actually make that happen to make it so that way the default experience is just as powerful as a go deeper experience could be as in the most important features should be easily accessible and then the go deeper features basically round out the experience and make it so a user that is an enthusiast is able to explore a lot more intensely into like the specific aromatic science that is behind the compounds and maybe we can later add molecular structures and talk about even the chemistry and the actual shape of these different things and maybe how even just the shape determines how you're going to smell it and maybe some things are easier to smell and warm air versus cold air or more humid air or more dry air or even in like different circumstances like you're more likely to smell something through a mask versus just an open air that probably has to do with the threshold and maybe even the size of the molecule These are all the things that could be going into the go deeper thing I want you to put those into a list of a rolling list of go deeper features that could make it so again this is this is a project plan in terms of what we're actually going to do to make this all happen this is not a plan B plan C plan D this is road map of exactly where we're going please help me put that all together in your best visual guide So I wanna see checkpoints based on I guess there's kind of two different ways we could look at this BA basically like I want every change that happens to this tool to have a visible artifacts evidence of a visual change happening to show that our commits are actually doing something and also just for my own visually oriented brain I want to know that there is a process that is actually coming to fruition by building it out.

### 10 - Jul 6, 16:34
> Yep let's go with p3. tasting card should be as informative as possible in a mobile friendly portrait or 1:1 formatted image. The wheel ring speaks for itself. the edges that are visible should be in a preview options menu before user clicks to generate url for sharing. options include style changer - more informative, more visually stunning, perhaps option to add map for chosen flavor note selection. Also this could be good for someone to be able to bookmark what flavor notes they chose and what that output looks like. options should also include ability to customize all of your shareables again in the preview section of this feature's ux process. when user is happy, they can click generate share link/download button becomes available/active

### 11 - Jul 6, 17:14
> tune the card. i'd like there to be checkboxes for "show/hide" on the tasting notes, the compounds, and then dropdown that checkox includes individual checks for specific compounds to show - ordered by prominence in the wheel so pepole could check top 3 if they wanted to or leave them all even though it'll be an aroma soup

### 12 - Jul 6, 18:34
> right, so the inset map  should be resizeable and able to be cleanly reformed around the wheel but "liking" the diagonal relationship... not perfectly linear, actually a bit on a curvature from diagnonal as if it was curving to expose the sun behind it (metaphorical to ilustrate curvature eclipsing not perfectly diagonal relationship across from one antoehr on a 4 o'clock and 8 o'clock position. 
> 
> *PS* a visual/ spawning?? bug of th flavor notes where they appear in at around a 9-to-eleven o'clock positioning and then slowly migrate over... which sometimes gets missed by the visual agent's screenshots. If it could capture perhaps what is equivalent to a low res video in frames if necessary to get that visual access to the motion over time especially within the first 10-30 seconds of load-in (depending on user's device perforamance??)

### 13 - Jul 6, 18:46
> Ah... also, the "likely compounds by confidence could benefit from an optional (checkbox function) that would show a little icon of what that aroma is most known for. If there truly isn't a standard emoji that fits, we need to possibly just leave those for now but have a to-do of representing those 'chemically-sounding' aromatic compounds that don't yet have an accepted 'standardized' name that makes it sound closer to an ingredient in an apothecary and less like a lab formulation... even if that is the stone-cold reality of how we actually are able to accumulate enough of that compound for it to be smellable threshold for users to even pick up on and assess in the aromawheel site tools. I want your expert level call on usability from an expert level baked in , but let that be part of the backend curriculum, now something the average user feels they have to swim through to understand. perhaps optional tutorial (save that for later too, not this slice.) Any way there might benefit from some visual icon next to beta-demascenone - rose is the obvious choice, furaneol is coffee, linalool is sage/lavender, geraniol - geranium... limonene: lemon, and so on.

### 14 - Jul 6, 18:47
> Here would also be a fantastic spot for a help cloud to appaer to tell users to drag and place any notes that stand out for them. (introduces functionality of user pinning the notes, and double tapping to free)

### 15 - Jul 7, 20:31
> continue where left off. i put a few prompts in there so make sure to take the last 4-5 prompts into consideration

### 16 - Jul 8, 05:48
> I think the lens of coffee vs wine vs any other tasting experience needs to be a future update where you can "bias it" (need a better word that doesn't already come with a ... negative connotation)

