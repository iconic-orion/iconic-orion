# 13 — Archive and document prompts for transparency

- **Date:** 2026-06-12
- **Branch(es):** prototype / feature/prompt-log
- **Source:** Claude Code session `7362c7c8`
- **Prompts:** 3

> Curated summary: [../README.md](../README.md) (entry 13)

---

### 1 · Jun 12, 08:37
> i had prompts that i harchived in past chats. i realized I should be keeping a record of these so I can show what human work went into this tool. Can we start keeping a record of my prompts in a doc in the repo? that way I could show down the line: here are my prompts, here's what they did, here's where I had back and forth with the agent, and then here's the raw chat.

**→ Agent:** I'll take a look at the repo structure first to see where this would best fit and match existing conventions.  _Actions:_ Bash: List repo root and find markdown docs · AskUserQuestion · Bash: Create branch off prototype for the prompt log · Write README.md · Write TEMPLATE.md · Write README.md

### 2 · Jun 12, 08:44
> where are my archived chats stored on claude app

**→ Agent:** Good question — and the answer depends on *which* "chats" you mean, because there are two different things with two different storage locations.  _Actions:_ Bash: Check local Claude Code session transcripts fo…

### 3 · Jun 12, 08:46
> Brilliant then that's what we'll do:  parse these files and extract every human prompt automatically, then match each to what shipped (via git history) and format them into entries.

**→ Agent:** Let's do it. First I need to understand the transcript schema so I extract *real* human prompts (not tool results or system injections, which also carry the `user` role).  _Actions:_ Bash: Inspect JSONL transcript schema · Bash: Check for node/python3/jq · PowerShell ×2 · TaskCreate · PowerShell ×3 · AskUserQuestion · PowerShell

