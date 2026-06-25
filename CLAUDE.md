# Branching workflow

Source of truth for how branches, tags, and PRs flow in this repo. Update this file first when the workflow changes, then propagate to agent memory.

## Long-lived branches

- **`main`** — production. Reflects the last shipped baseline. As of 2026-05-31 (PR #5, merge commit `74bd1ef`), `main` is caught up to `prototype` — V2 and the Compound library have been promoted. Only merge here via PR once changes are tested and the user explicitly says it's ready to ship.
- **`prototype`** — the **deploy / staging branch** and the day-to-day source of truth for the live app. Netlify deploys from here to https://aromawheel.net. Treat as semi-stable: only land work here that's coherent on its own. Day-to-day exploration happens on branches *off* `prototype`, not directly on it. Expect `prototype` to drift ahead of `main` between promotions.

## Short-lived branches

- **`feature/*` or `claude/*`** — branched off `prototype` (or off a long-running dev branch, see below) for a specific scoped change. PR back to whichever branch you branched from. Delete after merge.

## Long-running dev branches (for multi-slice work)

When a body of work is big enough to need multiple coherent commits before it's ready to merge into `prototype`, give it a dedicated long-running branch off `prototype`. Rules:

- Each slice lands as a commit (or a small PR into the long-running branch from a short-lived sub-branch if review checkpoints are wanted).
- The long-running branch has **one tracking PR** open against `prototype`, kept in **draft** until the whole body of work is ready.
- The tracking PR's description lists slices so reviewers (and future-you) can see progress at a glance.
- Do NOT auto-merge the tracking PR. Wait for explicit approval before merging into `prototype`.

### Current feature branches (in flight)

- **`claude/ui-pass-2`** — draft PR **[#9](https://github.com/iconic-orion/iconic-orion/pull/9)** against `prototype`. Second UI pass: mobile + overall refinements following the PR #8 merge. **In progress** — slices accumulate here before merge.
- **`claude/upbeat-mendel-6ef2f6`** — PR **[#13](https://github.com/iconic-orion/iconic-orion/pull/13)** (origins map) merged into `prototype` 2026-06-25. The branch stayed alive past that merge: a stray local `WIP: epitaxy pre-switch` commit had reverted the compound-library expansion (17 compounds, 12 notes, ~50 edges, `docs/INFERENCE.md`) out of the working tree, since fixed. New draft PR **[#14](https://github.com/iconic-orion/iconic-orion/pull/14)** against `prototype` carries that restoration plus a Go Deeper scope cleanup (full citations and the note inverse-view click no longer require Go Deeper to be on — it's now just the ortho/retro commit-button toggle). **In progress** — awaiting merge approval.

Recently merged into `prototype`:
- **`claude/upbeat-mendel-6ef2f6`** — PR **#13** (merged 2026-06-25). Origins map: compass-icon toggle on the wheel opens a full-screen world map of ingredient cultivation regions (pre-Columbian Exchange framing), synced note selection, scroll-zoom/drag-pan, neighbor-aware label layout.
- **`claude/thirsty-dijkstra-de159b`** — PR **#8** (merged 2026-06-10, merge commit `4c074d0`). UX pass: first-run nudge, mobile single-column breakpoint (≤760px), compound callout labels (mobile toggle with leader lines), collapsible HUD header (view tabs always visible, ••• expands secondary controls), float-label de-clutter, data palette saturation pass, copy polish (em-dash strip, Note Suggester pruning, Methodology sources note). Branch safe to delete.
- **`feature/compound-lens`** — PR **#7** (merged 2026-06-06, merge commit `bdb8039`). Branch deleted.
- **`claude/header-cleanup`** — PR **#6** (merged 2026-06-06, merge commit `d96ebaa`). Branch safe to delete.

`prototype` is now ahead of `main` by PRs #6, #7, and #8. No additional long-running dev branch active beyond `claude/ui-pass-2`.

### Historical: V2 (shipped 2026-05-26)

- Branch: **`claude/vigilant-lovelace-2cb582`** — now stale; `prototype` is ahead of it. Safe to delete locally.
- Tracking PR: **[#4](https://github.com/iconic-orion/iconic-orion/pull/4)** — **merged** 2026-05-26.
- Merge commit on `prototype`: `20643d3` (tagged **`v2`**).
- Slices delivered: (1) ortho/retro foundation, (2) three view modes + responsive layout, (3) "i" info tab with About / How to Use / Types of Aroma, (4) Go Deeper additional contents, (5) mouthfeel dimension as its own tab, (6) nudge / search / visible word bank, (7) perceptual-tone copy pass.

## Flow at a glance

```
feature/X ──PR──▶ prototype ──PR──▶ main      (small self-contained changes)

(future long-running work) ──PR──▶ prototype ──PR──▶ main
   ▲
   │ slice commits accumulate here
```

## Tags

Tags mark historical snapshots. Recover any with `git checkout <tag>`. Both are pushed to origin and visible in GitHub's Tags / Releases UI.

- **`v1`** → commit `f066d15` — first workable HTML prototype, captured before V2 design changes. Historical snapshot.
- **`v2`** → commit `20643d3` — the moment V2 landed on `prototype` (merge of PR #4, 2026-05-26). Historical snapshot; `prototype` has continued forward since.

`prototype` is always newer than the highest-numbered `vN` tag.

## Branch protection (set in GitHub UI)

On `main`:
- Require pull request before merging
- Require status checks to pass
- Disallow direct pushes

## Worktrees

This repo uses **Claude Code worktrees** (under `.claude/worktrees/`) so multiple agent sessions can work on different branches in parallel without stepping on each other. Each worktree is a separate working directory checked out to one branch.

All current `.claude/worktrees/*` directories — including `vigilant-lovelace-2cb582/` — are **historical leftovers from the V2 era**. None are canonical anymore. They're safe to ignore, or to clean up with `git worktree remove <path>` if you want a tidier filesystem. The matching `claude/*` branches (sad-beaver, frosty-hoover, blissful-franklin, etc.) are all behind `prototype` with zero unique commits — they can be deleted without losing work.

When new long-running work starts, create a fresh worktree off `prototype` and document it here.
