# Orchestration Log

A record of the prompts I sent to my own subagents while building the Aroma Wheel —
the delegation layer sitting underneath [`../README.md`](../README.md)'s record of what
Nolan asked me for.

This tool is a public educational artifact. The point isn't just the finished
interface; it's the **thinking** that shaped it. `../README.md` already captures one
layer of that thinking — the human's questions, constraints, corrections, and dead
ends. But once a task got handed to me, I made my own decisions about how to break it
down: what to research before writing code, what context a subagent needed to do the
job right, what judgment calls got embedded in how I briefed it. Those decisions are
also part of the thinking, and until now they only existed as scrollback in a
transcript file, not as a record anyone could read.

## Why this is a separate directory, not part of `../raw/`

Different authorship. Every prompt in `../raw/` was typed by Nolan — a human asking
for something. Every prompt in this directory's `raw/` was written by me — an agent
deciding how to decompose a task and briefing another instance of myself to go do
part of it. Filing both under one archive would blur a distinction this project cares
about: who decided what. `../PROVENANCE.md` already draws a hard line around what
counts as a *human* prompt (`type: "user"`, `origin.kind: "human"`, plain-string
content — explicitly excluding "synthetic user-role injections") specifically so the
human record stays uncontaminated by anything else the transcript contains. This
directory is the deliberate home for that "anything else," for the one slice of it —
`Agent` tool calls — worth keeping on its own terms rather than discarding.

This is a **companion** to `../README.md` and `../raw/`, not a replacement for either.
Where a session appears in both archives, each entry here names its counterpart there
(and vice versa isn't retrofitted — the human log's numbering is its own and doesn't
change to match this one). Read them side by side: the human log shows what was
asked; this log shows how the asking agent chose to delegate it.

## What counts as an entry here

Specifically: every call to the `Agent` tool — spawning a fresh subagent instance,
sometimes run in the background — found in this project's local Claude Code session
transcripts. Not every tool call, not every subagent's internal tool use (a
subagent's own actions are its business, not logged here), just the dispatch itself:
the prompt handed off, and enough surrounding context to know when and why.

## Extraction method (reproducible)

Source: every `*.jsonl` file directly under
`C:\Users\njale\.claude\projects\D--Git-NAE\` (the `memory\` subdirectory is not a
session transcript and is excluded). Filter: records with `type: "assistant"` whose
`message.content` array contains a block with `type: "tool_use"` and
`name: "Agent"`. For each match, the archive captures `input.description`,
`input.prompt` (verbatim, in full — no truncation, no paraphrase, regardless of
length), `input.subagent_type`, `input.model`, and `input.run_in_background` when
present, plus the call's timestamp and whether other `Agent` calls landed in the same
assistant turn (a same-turn batch is a genuine parallel dispatch; calls in
back-to-back turns seconds apart are noted as sequential, not conflated with a batch).

Results are matched by following the call's `tool_use_id` forward to its
`tool_result` (for a foregrounded call) or to the `<task-notification>` block that
later reports a backgrounded agent's completion (matched via the `agentId` the launch
response returns). Every result note in this archive is condensed to one factual
line — what the subagent actually reported, not an inferred or embellished summary —
and drawn from the real result text, not invented. Where a result couldn't be
confidently matched, the entry says so rather than guessing.

The live session that produced this archive (`b67a4a72-c437-458c-8242-21b37beab033`)
is deliberately excluded — its transcript wasn't finished being written at extraction
time, so it isn't a settled record yet. It will be eligible for a future extraction
pass once it's complete.

This method mirrors `../PROVENANCE.md`'s own standard: state the filter so the count
can be re-derived, don't fabricate anything absent commentary can't cover, and say
plainly when something can't be verified rather than smoothing over the gap.

## Current count

| Sessions with `Agent`-tool activity | Total `Agent` calls captured | Date range |
|---:|---:|---|
| 4 | 27 (1 rejected before running; 3 terminated early by a session usage limit) | 2026-06-28 → 2026-08-14 |

Measured 2026-08-15, against 24 session transcript files on disk at that time (the
live session excluded per above). 20 of those 24 files contain zero `Agent`-tool
calls and are not represented here — most of this project's history was written
directly, without delegating to subagents at all; the practice shows up only in a
handful of sessions, clustered around heavier research/audit work.

## Entries

### 01 — Building the herb/floral slice and the Tree workspace

**Date:** 2026-06-28 → 2026-06-29 · **Session:** `5223ccad` · **Calls:** 6 (1 rejected)

Six research dispatches (one rejected by Nolan before it ran, re-sent minutes later
in nearly the same form) that scouted the existing note/compound schema before
extending it, then went on to survey the Wheel/Map toggle architecture and D3 usage
as the direct feasibility check behind building the Tree workspace, and finally
traced the entry/scoring pipeline to find the exact visibility-gate bug that later
made varietal children (peppermint, spearmint, etc.) unscoreable independent of
their parent note.

**Companion:** [`../raw/20-prepare-herbal-floral-slice-for-pr.md`](../raw/20-prepare-herbal-floral-slice-for-pr.md)
**Raw:** [`raw/01-taxonomy-tree-research-dispatches.md`](raw/01-taxonomy-tree-research-dispatches.md)

---

### 02 — Map-layers systems analysis, watched not touched

**Date:** 2026-07-26 → 2026-07-27 · **Session:** `b91c5e6b` · **Calls:** 10

A dense back-to-back research/design/audit sequence run while ChatGPT worked the
same map feature live on the shared `codex/*` branch — a technical feasibility audit
of the world-SVG map, a sourcing-honesty audit that flagged a proposed "cultural
value" layer as unbuildable within the project's citation standard, a full
thesis-chain grading pass across every app surface, an interactive design-spec
artifact for the surviving map layers, an enforceable opacity/stacking rule set, and
two adversarial follow-up audits that caught a design proposal leaning on numbers
that don't actually exist in the codebase. The last three calls (parallel
production-data research) all hit a session usage limit mid-task and returned only
partial, explicitly-flagged-incomplete output.

**Companion:** [`../raw/36-session-handoff-thesis-systems.md`](../raw/36-session-handoff-thesis-systems.md)
**Raw:** [`raw/02-map-layers-systems-analysis-watched-not-touched.md`](raw/02-map-layers-systems-analysis-watched-not-touched.md)

---

### 03 — Map-layers systems analysis, the wreath idea

**Date:** 2026-07-26 → 2026-07-27 · **Session:** `def702be` · **Calls:** 10

A near-duplicate of entry 02 — same starting handoff document, same ten `Agent`
dispatches (identical prompts and results), run in parallel as a separate session.
Diverges from entry 02 only in what happened afterward: this session continued for
several more hours of human-directed work (surfacing the Tree "wreath" idea and a
map compass concept relayed from a conversation with ChatGPT), but with no further
`Agent`-tool delegation in that continuation.

**Companion:** [`../raw/37-session-handoff-thesis-systems.md`](../raw/37-session-handoff-thesis-systems.md)
**Raw:** [`raw/03-map-layers-systems-analysis-wreath-idea.md`](raw/03-map-layers-systems-analysis-wreath-idea.md)

---

### 04 — Dead-code audit before the tasting-relationship-guidance merge

**Date:** 2026-08-14 · **Session:** `e7282965` · **Calls:** 1

A single, tightly-scoped read-only audit dispatched ahead of reviewing a 60-commit
branch for merge-readiness: find CSS/JS left behind by superseded implementations,
cross-referencing definition sites against usage sites across a ~21,500-line file
rather than reading it linearly. Returned 6 confirmed findings with file:line
citations, plus an explicit "checked and ruled clean" list so those aren't
re-flagged in a future pass.

**Companion:** [`../raw/44-venn-overlap-and-enter-tasting-button.md`](../raw/44-venn-overlap-and-enter-tasting-button.md)
**Raw:** [`raw/04-dead-code-audit-tasting-relationship-guidance.md`](raw/04-dead-code-audit-tasting-relationship-guidance.md)
