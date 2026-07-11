# Codex Branch Check-in Template

**For ChatGPT → Claude hand-offs on `codex/aroma-wheel-responsive-ux-pass`**

Use this format when pushing work to the codex branch. It helps Claude understand your thinking, evaluate your approach, and know what needs review or testing.

## Header

```
## Check-in: [focus area] — [commit count]
Date: YYYY-MM-DD
Branch: codex/aroma-wheel-responsive-ux-pass
Commits: [list top 2-3 commit titles]
```

## What I worked on

**Scope:** 1-2 sentences. What was the goal?

**Why:** What motivated this work? (Bug fix, UX improvement, performance, new feature, exploration?)

## Changes summary

List by impact, not by file:

- **Mobile UI responsive fixes**: 
  - Detail panel visibility (show only on demand, not always open)
  - Nudge sizing (wider to fit screen, scaled fonts for touch)
  - ...
- **Functional changes**:
  - ...

## Testing / verification

What did you test? How did you verify it works?

- Opened mobile view (375x812)
- Tested [feature X] on [device/viewport]
- Checked console for errors
- ...

## Questions / blockers for Claude

- Does this approach fit the codebase philosophy?
- Should the detail panel on mobile be opt-in always, or smart (show if content exists)?
- Should I continue exploring [area X]?

## Commits

Paste output of `git log --oneline <start>..<end>`:

```
3a3e322 Mobile UX refinements: responsive taxonomy tree, origins map, and nudge sizing
```

## Next priorities (if continuing)

What should be done next on this branch?

- Polish the origins-map label opacity on mobile (currently fades too aggressively)
- Explore responsive tree search/controls layout
- ...

---

**For Claude's review:**
- Is the thinking here sound?
- Should any of this be promoted to `feature/bloom`?
- Anything broken or needs rework?
