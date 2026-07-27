# 12 — Understand terpene naming conventions on aromawheel

- **Date:** 2026-06-08
- **Branch(es):** prototype
- **Source:** Claude Code session `f7daba22`
- **Prompts:** 4

> Curated summary: [../README.md](../README.md) (entry 12)

---

### 1 · Jun 8, 10:01
> I loaded up the wheel on aromawheel.net One thing that stuck out: In terpenes, I see 1,8-Cineole and then right beneath in the description it says "eucalyptol". Why does it have two different names and not have eucalyptol as the main name?

**→ Agent:** Good catch — and it's a fair thing to be confused by.  _Actions:_ Grep [Cc]ineole|[Ee]ucalyptol

### 2 · Jun 8, 10:03
> Can we add the common name to all of the compounds when hovered over. best way is if is just shows up in parentheses when focused on with mouse over or long press on mobile

**→ Agent:** Let me dig into how compounds are rendered and what already happens on hover, so I can find the cleanest place to add this.  _Actions:_ Bash: Count lines in index.html · Read index.html

### 3 · Jun 8, 10:04
> Let me be specific, in the Results Pane specifically. Which honestly needs a rename too because it is more the chemistry pane.

**→ Agent:** Let me find the Results Pane in the code and see how it renders compound names.  _Actions:_ Grep [Rr]esult|results-pane|resultsPane|panel · Grep cpd-card|cpd-name|\.label|c\.label · Read index.html · AskUserQuestion · Read index.html · Grep view-cpd|detailPanel.addEventListener|addEventL… · Read index.html ×3 · Grep function renderCompoundDetail · Read index.html ×3 · Grep Results · Read index.html · mcp__ccd_session__mark_chapter · …

### 4 · Jun 8, 10:31
> nah it's fine on prototype cause these are "smaller" changes. My claude.md file was more for big changes to the system. go ahead and commit and push these to prototype

**→ Agent:** I'll commit and push to prototype.  _Actions:_ Bash: Check working tree status and current branch · Bash: Commit the changes · Bash: Push to prototype

