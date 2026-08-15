# Provenance

How much of this log can still be checked against a source, and how much is now
the source. Written 2026-07-26, when a re-count found the numbers in
[`README.md`](README.md) no longer matched what actually exists on disk.

This file exists because a log about honest sourcing has to be honest about
itself. Everything below is measured, not estimated — the counts come from
parsing the local Claude Code transcripts directly, and the method is stated so
the numbers can be re-derived rather than trusted.

## What the corrected count is

| | Sessions | Prompts | Words |
|---|---:|---:|---:|
| Surviving local transcripts (2026-05-22 → 2026-07-27) | 26 | 313 | 17,220 |
| Surviving local transcripts (2026-05-22 → 2026-08-15) | 34 | 397 | 19,944 |

Filter, stated so the number is reproducible: records with `type: "user"` and
`origin.kind: "human"`, where the message content is a plain string. Content
arrays are tool results, not typed input. Sidechains (subagent turns) are
excluded, as are synthetic user-role injections — `<system-reminder>`,
`<local-command-stdout>`, slash-command echoes, and interrupt markers. A
different filter yields a different total; an earlier pass using a looser rule
counted 349. Neither is wrong, but a count without its filter is not a fact.

**Addendum, 2026-08-15:** a second extraction pass covering 2026-07-26 through
2026-08-15 (the run-up to PR #20, "Tree, Map, Constellation, Laps & Delivery,"
merging into `prototype`, and PR #21, "Promote prototype to main") added 8
sessions / 84 prompts / 2,724 words under the same filter above, entries 38–45.
The word count for this addendum was derived directly from the `raw/` files
rather than re-parsed from the source transcripts (each prompt block's own text,
summed per file) — consistent with the same filter in spirit, but a different
mechanical path than the original 26-session count, named here rather than
left implicit.

Excluded on purpose: two sessions under a separate `-Ideas` project directory.
That is the Glacier Line prototype, fenced out of this repo, not Aroma Wheel work.

## The three tiers

**Tier A — transcript-backed.** The original session transcript still exists
locally, so every prompt here can be re-extracted verbatim and re-verified today.
Entries 14–37 are all Tier A, generated directly from those transcripts. Entries
38–45 (session ids `def702be`, `ddb8c662`, `5c9bc8de`, `86663bc9`, `583a1a7e`,
`fc6150a0`, `e7282965`, `bc2d11f1`; extracted 2026-08-15) are Tier A as well.

**Tier B — archive-only.** The transcript is **gone**. The file in
[`raw/`](raw/) is now the only surviving record of that session, and nothing can
re-verify it. **12 of the 14 sessions cited by entries 01–13 are in this tier:**

```
05ed99e7  173b7958  208d07b1  4df3d0ad  54aef01c  586767f5
5f2fe804  67baba40  714d67b5  7f7fc7dd  c4aa3d83  f7daba22
```

Only `09166aa8` and `7362c7c8` from that original batch still have transcripts.

**Tier C — declared gap.** Work that never produced a Claude Code transcript at
all. The ChatGPT/Codex sessions on `codex/*` are the main case: that history
lives entirely outside this tool and is not recoverable from here. It is named
as a gap rather than estimated. Anything reconstructed from commit messages
alone would be a summary of the output, not a record of the ask.

## What was wrong before

The previous `README.md` stated the log was built from *"14 sessions, 192 real
prompts, May 21 – Jun 12 2026."* Re-checked against disk:

- Only **5 sessions / 54 prompts** from that window still have transcripts.
- Entries 01–13 self-report **184** prompts in their own headers, not 192. The
  8-prompt difference cannot now be resolved in either direction — the sessions
  that would settle it are Tier B.
- **21 sessions after Jun 12 had no entry at all.** The log covered roughly the
  first sixth of the project's prompts and then stopped, while still asserting a
  total. That is the error worth naming plainly: not that the count drifted, but
  that a stale count kept being presented as current.

Entries 14–37 close that gap. They carry verbatim prompts and **no** per-prompt
response summaries — those were hand-written for 01–13 and have not been written
for the new entries. Absent commentary is absent, not implied.

## Why this is urgent rather than tidy

Twelve sessions' transcripts were deleted between the original log being written
and this recount, without anyone noticing. That is the actual finding. Every
transcript still on disk is on the same clock, so archiving is time-sensitive
work: once a session ages out, `raw/` is not a convenience copy, it is the
artifact. Entries 14–37 were generated for that reason.

## Addressing a single prompt

Planned use: surfacing the prompt behind a feature inside the app (see below),
which needs prompts to be individually citable. The scheme is
`<8-char session id>#<1-based prompt index>` — for example `db3bb295#2` is the
second human prompt of session `db3bb295`. Both halves are already recorded in
every `raw/` file header and heading, the session id never changes, and the index
is positional within a file that is append-only once written. Deliberately not
line numbers, which shift whenever a file is reformatted.

## Prompt attribution in Go Deeper (planned, not built)

The intent is for Go Deeper to reveal the prompt that caused a feature to exist —
in the words it was actually asked for. Provenance rules, mirroring the citation
system this project already runs:

- An agent may **propose** a prompt → feature attribution, never publish one.
  Proposed attributions render as pending, the same way an agent-found source
  sits in `UNVERIFIED_REFS` as "under human review."
- A human **approves** each attribution before it is shown as established. The
  approval is the claim; the agent's tagging is only a suggestion.
- Attributions quote the prompt **verbatim** from `raw/`. No paraphrase, no
  cleanup, no reconstructing an ask from a commit message — a tidied prompt is a
  different prompt.
- A feature with no approved attribution shows nothing. It does not get a guessed
  one, and the blank is not backfilled from a plausible-looking nearby prompt.

The same reasoning as the citation badges: an agent finding something is evidence,
and a person confirming it is what makes it a claim.
