# Agent Working Agreement — Branch Boundaries

> **Mirror notice:** This file (`AGENTS.md`) and `CLAUDE.md` are mirrors and
> must stay identical below this notice block. `AGENTS.md` is canonical; if
> the two ever differ, `AGENTS.md` wins and the discrepancy should be flagged
> to Nolan. Any edit to one must be applied to both in the same commit.

This file defines enforceable rules for AI agents working in this repository.
The rationale and collaborative philosophy live in `docs/collaboration-model.md`.
When rules and philosophy appear to conflict, the rules win. When a rule is
ambiguous, stop and ask Nolan — do not resolve ambiguity with judgment.

## Branch roles

| Branch | Role | Codex (ChatGPT) | Claude |
|---|---|---|---|
| `codex/aroma-wheel-responsive-ux-pass` | Experimental sandbox | Read + write | Read only |
| `prototype` | Stable development line | Read only | Write via PR only |
| `main` | Canonical | Read only | Write via PR only |
| All other branches | — | Read only | Read only unless Nolan names the branch |

## Rules for Codex

1. **Write only to `codex/aroma-wheel-responsive-ux-pass`.** No commits, pushes,
   merges, tags, or force-pushes to any other branch, ever.
2. **"Explicitly instructed otherwise" means:** a written directive from Nolan,
   in the current session, that names both the target branch and the specific
   change. Anything less — implication, inference, a passing remark — is not
   authorization. If uncertain, it wasn't authorization.
3. **Alignment is one-directional.** To stay current, merge `prototype` *into*
   the codex branch: `git merge prototype`. Never the reverse. Never rebase the
   codex branch onto anything without Nolan's directive (per rule 2). Alignment
   is performed only when Nolan requests it, not on Codex's own judgment.
4. **Force-push is permitted only to the codex branch**, and only to clean up
   your own unshared work.
5. **On any boundary error or failed alignment:** stop immediately, do not
   attempt repair, write current state into the handoff file, and flag for
   Nolan. A documented mess is recoverable; a repaired one may not be.

## Rules for Claude

1. **Do not push to the codex branch.** Review it, test it, comment on it —
   but the experiment stays authored by Codex. Fixes or suggestions go in the
   review notes, not into the branch.
2. **Promotion mechanism:** carry work forward by creating a fresh branch off
   `prototype` (naming: `promote/<short-description>`), implementing or
   cherry-picking there, and opening a PR into `prototype`. The PR description
   must reference the codex commits or handoff entries it derives from, and
   must state what was changed in translation and what was deliberately
   dropped.
3. **All promotions require Nolan's approval before merge.** No self-merging.
4. **`main` is reached only from `prototype`**, via PR, with Nolan's approval.

## Handoff protocol (Codex → Claude)

At the end of each meaningful batch of work, append an entry to
`handoffs/YYYY-MM-DD-<short-slug>.md` on the codex branch, using this template:

```markdown
# Handoff: <title>
Date: YYYY-MM-DD
Commits: <first>..<last>

## What changed
<files/areas touched, and the shape of the change>

## Why
<the idea being explored; what question this batch answers>

## Verification
<exact commands run and their observed output — not "seems to work."
If untested, say "untested" explicitly.>

## Open questions / known gaps
<what a reviewer should poke at first>

## Promotion candidates
<which parts, if any, you believe are ready to carry forward, and why>
```

Claude treats the Verification section as claims to check, not conclusions to
trust.

## Enforcement note (for Nolan)

These rules are a soft fence. Back them with GitHub branch protection on
`main` and `prototype`: require pull requests, restrict direct pushes,
require review before merge. The agents should never be the only thing
standing between an experiment and the canonical branches.
