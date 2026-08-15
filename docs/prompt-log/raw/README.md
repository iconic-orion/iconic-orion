# Raw transcripts

Verbatim chat transcripts — the unedited receipts behind the curated entries in
[`../README.md`](../README.md).

Nothing here is cleaned up. Typos, false starts, agent missteps, and the messy
middle of getting to a result all stay in. The curated log is the story; this is
the source.

## Naming

One file per entry, matching the curated entry's number and slug:

```
NNN-short-slug.md   e.g. 001-prompt-log-setup.md
```

## Format

No strict schema — paste the transcript. A light header helps:

```markdown
# 001 — Short title

Date: 2026-06-12
Curated entry: ../README.md (#001)

---

[paste the verbatim chat here]
```

## Two generations of file in here

**01–13** were assembled by hand. Each prompt is followed by a one-line summary of
how the agent responded, so the prompt → effect → next-prompt chain reads as a
chain. Twelve of the fourteen sessions behind these files no longer have a
transcript on disk — for those, this folder is not a receipt, it is the only
surviving record. See [`../PROVENANCE.md`](../PROVENANCE.md).

**14–37** were generated directly from surviving transcripts on 2026-07-26, to get
them archived before they age out the same way. They carry verbatim prompts and
**no** response summaries. That omission is deliberate: writing those summaries
means reading each agent reply and characterising it, which is authorship, and
inventing them to match the older format would be exactly the kind of plausible
backfill this project refuses elsewhere. Absent commentary is absent, not implied.

## Citing one prompt

`<8-char session id>#<1-based index>` — e.g. `db3bb295#2` is the second human
prompt of session `db3bb295`. Both parts are in every file's header and headings.
Stable across reformatting, unlike line numbers.
