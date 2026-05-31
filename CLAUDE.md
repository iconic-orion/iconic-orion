# Branching workflow

Source of truth for how branches, tags, and PRs flow in this repo. Update this file first when the workflow changes, then propagate to agent memory.

## Long-lived branches

- **`main`** — production. Only merge here via PR once changes are tested and the user explicitly says it's ready to ship.
- **`prototype`** — the **deploy / staging branch**. GitHub Pages is configured to serve from here (or is the natural target). Treat as semi-stable: only land work here that's coherent on its own. Day-to-day exploration happens on branches *off* `prototype`, not directly on it.

## Short-lived branches

- **`feature/*` or `claude/*`** — branched off `prototype` (or off a long-running dev branch, see below) for a specific scoped change. PR back to whichever branch you branched from. Delete after merge.

## Long-running dev branches (for multi-slice work)

When a body of work is big enough to need multiple coherent commits before it's ready to merge into `prototype`, give it a dedicated long-running branch off `prototype`. Rules:

- Each slice lands as a commit (or a small PR into the long-running branch from a short-lived sub-branch if review checkpoints are wanted).
- The long-running branch has **one tracking PR** open against `prototype`, kept in **draft** until the whole body of work is ready.
- The tracking PR's description lists slices so reviewers (and future-you) can see progress at a glance.
- Do NOT auto-merge the tracking PR. Wait for explicit approval before merging into `prototype`.

### Current long-running dev branch: V2

- Branch: **`claude/vigilant-lovelace-2cb582`**
- Tracking PR: **[#4](https://github.com/iconic-orion/iconic-orion/pull/4)** — kept in draft until V2 is ready to merge into `prototype`.
- Slice plan: (1) ortho/retro foundation [done], (2) three view modes + responsive layout, (3) "i" info tab with About / How to Use / Types of Aroma, (4) Go Deeper additional contents (expanded citations, methodology, cross-dimension correlations), (5) mouthfeel dimension as its own tab, (6) nudge / search / visible word bank, (7) perceptual-tone copy pass.

## Flow at a glance

```
feature/X ──PR──▶ prototype ──PR──▶ main      (small self-contained changes)

claude/vigilant-lovelace ──PR──▶ prototype ──PR──▶ main   (long-running V2)
   ▲
   │ slice commits accumulate here
```

## Tags

- **`v1`** → commit `f066d15`. Checkpoint of the first workable HTML prototype, captured before V2 design changes. Recover any time with `git checkout v1`. Pushed to origin; visible in GitHub's Tags / Releases UI.

## Branch protection (set in GitHub UI)

On `main`:
- Require pull request before merging
- Require status checks to pass
- Disallow direct pushes

## Worktrees

This repo uses **Claude Code worktrees** (under `.claude/worktrees/`) so multiple agent sessions can work on different branches in parallel without stepping on each other. Each worktree is a separate working directory checked out to one branch.

The canonical worktree for V2 work is:

```
D:\Git_NAE\.claude\worktrees\vigilant-lovelace-2cb582\
```

Other directories under `.claude/worktrees/` are leftovers from earlier sessions. They're safe to ignore, or to clean up with `git worktree remove <path>` if you want a tidier filesystem.
