# Prompt Log

A record of the human prompts behind the Aroma Wheel — what I asked for, what it
produced, and where the work actually happened in the back-and-forth with the agent.

This tool is a public educational artifact. The point isn't just the finished
interface; it's the **thinking** that shaped it — the questions, the constraints,
the corrections, the dead ends. This log is where that thinking lives in the open.

## How this log is organized

There are two layers, on purpose:

- **This file — the curated log.** A readable, chronological narrative. Each entry
  distills one session into: what I was after, what shipped, and the notable
  back-and-forth. Written to be *shown*.
- **[`raw/`](raw/) — the archive.** Every verbatim prompt I typed, in order, each
  followed by a one-line summary of how the agent responded — so the
  prompt → effect → next-prompt chain is visible. Written to be *referenced*: the
  receipt behind the curated summary.

Each curated entry links to its raw transcript, so the claim ("here's what I asked")
is always one click from the proof ("here's the actual exchange").

## Provenance

These entries are reconstructed from the local Claude Code session transcripts for
this project (14 sessions, **192 real prompts**, May 21 – Jun 12 2026), cross-checked
against the git history so each session is tied to the commits, PRs, and tags it
produced. Tool-result noise and interrupt markers were filtered out; the prompts
themselves are verbatim. See [`TEMPLATE.md`](TEMPLATE.md) for the entry skeleton.

---

## Entries

### 01 — Setting the guardrails

**Date:** 2026-05-21 · **Branch:** `dev` · **Prompts:** 1

**Prompt:** *"I want you to only have access to Git_NAE under the D drive only.
Without changing anything, just [investigate]…"*

**What it did:** Before a single line of code, established the working-directory
sandbox and the security posture for a repo that would become public. No artifact —
this is the safety conversation that set the ground rules everything else ran under.

**Raw:** [`raw/01-brainstorm-local-file-access-restrictions.md`](raw/01-brainstorm-local-file-access-restrictions.md)

---

### 02 — Standing up the git workflow

**Date:** 2026-05-21 · **Branch:** `dev` · **Prompts:** 11

**What it did:** Bootstrapped the whole git setup — commits `4c52d9e` (CI workflow +
branching docs) and `158d285` (`.gitignore` for Windows, editors, Claude Code, and
secrets). This is where the `main` / `prototype` / `feature/*` flow now documented in
[`CLAUDE.md`](../../CLAUDE.md) was first laid down.

**Back-and-forth:** I told the agent up front, *"I am not a dev, I am a creative who
is versed in descriptive language"* — and the session reflects it: walking through
git-bash vs cmd, GitHub CLI auth, and (a recurring theme) where to keep credentials
on the D drive for security, before handing off "the rest — remote, gitignore, first
commit, push."

**Raw:** [`raw/02-set-up-git-tree-commit-updates-in-project.md`](raw/02-set-up-git-tree-commit-updates-in-project.md)

---

### 03 — First HTML prototype

**Date:** 2026-05-21 · **Branch:** `claude/frosty-driscoll-15130d` · **Prompts:** 1

**Prompt:** *"here's the deal — we don't need to expand claude.md, just start making
the html file first prototype…"*

**What it did:** Kicked off `237f7b7` "Add aroma wheel scent mapper prototype" — the
seed that grew into the `v1` tag. A deliberate "stop planning, start building" moment.

**Raw:** [`raw/03-create-html-file-first-prototype.md`](raw/03-create-html-file-first-prototype.md)

---

### 04 — Building the scent-mapper from scratch

**Date:** 2026-05-21 → 05-31 · **Branch:** `claude/determined-williams-8ac428` · **Prompts:** 19

**What it did:** The core build. Commits `237f7b7`, `120568d` (broader note set,
signature compounds, legend with visibility toggles), `f11ad86` (drop the
typical/sensitive smeller toggle); shipped via PRs
[#1](https://github.com/iconic-orion/iconic-orion/pull/1) and
[#2](https://github.com/iconic-orion/iconic-orion/pull/2), captured as tag `v1`.

**Back-and-forth:** A lot of the product's DNA is set here. I pushed back on
blackcurrant as a reference flavor (*"most people don't know what blackcurrant tastes
like, find other analogues"*), asked for the legend-with-checkboxes, killed the
self-reported smeller profile as unhelpful, and flagged the Common/All filter as an
accessibility problem. The central tension — describing with *words* vs. naming
*compounds* — first surfaces here.

**Raw:** [`raw/04-build-terpene-wheel-scent-mapper-visualiza.md`](raw/04-build-terpene-wheel-scent-mapper-visualiza.md)

---

### 05 — Vetting new data against the literature

**Date:** 2026-05-22 · **Branch:** `claude/confident-wilbur-bec633` · **Prompts:** 5

**What it did:** A deliberately *no-code* research session — checking α-terpineol,
black-tea and elderflower compounds against the literature before deciding whether
they earned a place in the data. Ended with "yep, add them in" and a request for the
safest first step. The discipline of vetting sources before adding them is a thread
that runs through the whole project.

**Raw:** [`raw/05-analyze-terpene-data-against-aroma-wheel.md`](raw/05-analyze-terpene-data-against-aroma-wheel.md)

---

### 06 — The V2 epic: security fix → full redesign

**Date:** 2026-05-23 → 05-26 · **Branch:** `claude/blissful-franklin-a7b245` → `claude/vigilant-lovelace-2cb582` · **Prompts:** 86

The biggest session by far, and two stories braided together.

**What it did — part 1 (security):** I'd spotted API/SSH keys in a repo about to go
public. We pulled them all out and set the rule that still governs the project:
secrets live in a separate file *outside* the repo, on the D drive.

**What it did — part 2 (the V2 redesign), delivered as slices:** ortho/retro phase as
a core input contract (`a1053bf`); three view modes replacing the sensory/compounds
dichotomy (`1a3a173`); the "i" info tab — About / How to Use / Types of Aroma
(`aa88323`); a Methodology tab with citations and a "show formulas" gate (Slice 4
series); the "What am I smelling?" → **Note Suggester** modal with multi-select chips
(`e4b03b1`, `38abf30`, `11ff598`); a perceptual-tone copy pass (`fc4b3cd`); and a
compound-library expansion (`e315ce2`). Merged at `20643d3`, tagged **`v2`**, shipped
as PR [#4](https://github.com/iconic-orion/iconic-orion/pull/4).

**Back-and-forth:** This is where the project's *voice* was decided. The core stance —
*"your perceptions are real, and they change depending on the moment"* — is stated
here. So is the scope call (*"don't put perfumery there yet, I'm still thinking
edible"*), the information-access principle (*"don't baby the audience — EVERYONE
should have access to EVERY bit of information"*), the decision to defer mouthfeel as
out-of-scope, and the small joy of *"why is buttery in fermented?"* becoming a
documented tooltip. Note the several *"the last chat cut off at usage limit, pick up
where you left off"* — V2 was built across multiple sittings against the model's
context limits.

**Raw:** [`raw/06-remove-sensitive-credentials-from-public-r.md`](raw/06-remove-sensitive-credentials-from-public-r.md)

---

### 07 — Orientation check

**Date:** 2026-05-23 · **Branch:** `claude/lucid-visvesvaraya-3bd04c` · **Prompts:** 1

**Prompt:** *"so index.html in prototype is the working project yes"* — a one-line
confirmation that `prototype/index.html` is canonical. No artifact; kept for a
complete record.

**Raw:** [`raw/07-confirm-prototype-index-html-is-working-pr.md`](raw/07-confirm-prototype-index-html-is-working-pr.md)

---

### 08 — Should the wheel split: notes vs. taste-alikes?

**Date:** 2026-05-23 · **Branch:** `main` · **Prompts:** 6

**What it did:** A design-thinking session, no code shipped — and a good example of
the log capturing *reasoning*, not just output. We explored splitting the wheel
between flavor notes and "taste-alikes," whether that belonged in a separate
"ingredient guesser" mode, and re-litigated the core stance ("here's the chemistry
your perception implies"). It landed on a durable principle: the real compound names
should always be present somewhere, even if at lower confidence.

**Raw:** [`raw/08-split-flavor-wheel-into-notes-and-taste-al.md`](raw/08-split-flavor-wheel-into-notes-and-taste-al.md)

---

### 09 — Auditing the scent library for gaps

**Date:** 2026-05-26 · **Branch:** `prototype` · **Prompts:** 8

**What it did:** Started *"without changing code, identify all examples where we miss
key data a quick google search could surface,"* then made targeted additions (rose;
oak-barrel-only compounds). Feeds the vocabulary expansion (`38abf30`) and richer
origins (`e315ce2`).

**Back-and-forth:** A guardrail I keep repeating shows up clearly here — *"the tone of
this is getting too wine specific… remember"* — plus a naming call (*"add all but
cannabis, unless you name it 'hemp'"*).

**Raw:** [`raw/09-audit-scent-library-for-missing-common-sou.md`](raw/09-audit-scent-library-for-missing-common-sou.md)

---

### 10 — Promote to `main` + the ortho/retro 101 popup

**Date:** 2026-05-31 · **Branch:** `prototype` → `claude/header-cleanup` · **Prompts:** 25

**What it did:** Caught `main` up to `prototype` via PR
[#5](https://github.com/iconic-orion/iconic-orion/pull/5) (`74bd1ef`), reality-checked
the docs (`dcc837c`), and cleaned up the header — dropping the Common/All filter and a
misleading wheel overlay (`29bbbee`) toward PR
[#6](https://github.com/iconic-orion/iconic-orion/pull/6). Also stale-worktree and
leftover-branch cleanup.

**Back-and-forth:** A long thread building a "Go Deeper" 101 explainer for orthonasal
vs. retronasal olfaction, with a Creative-Commons diagram — I supplied a ResearchGate
figure and asked it to *verify the licensing first*. Then heavy copy editing: *"anterior
nares → just say front of nose," "you cannot use peach for this conversation, gen z is
watching,"* settling on coffee / cinnamon / hazelnut and the idea that coffee smells
better than it tastes.

**Raw:** [`raw/10-compare-implementation-with-prototype.md`](raw/10-compare-implementation-with-prototype.md)

---

### 11 — About refresh + wheel-label legibility

**Date:** 2026-06-06 · **Branch:** `claude/header-cleanup` → `feature/compound-lens` · **Prompts:** 14

**What it did:** Refreshed the About popup with a table of contents and corrected copy
(`a364789`), added the "Organize by: Scent | Chemistry" lens (`c16d617`), and fixed a
stubborn label-collision problem — curving category labels along an outer circle
(`79ebf6b`), coloring them by category (`c1758c0`), shrinking the ring (`e07e6ab`), and
nudging "Linalyl acetate" off "Ethyl butanoate" (`c99e00d`). Shipped via PRs
[#6](https://github.com/iconic-orion/iconic-orion/pull/6) and
[#7](https://github.com/iconic-orion/iconic-orion/pull/7).

**Back-and-forth:** Pixel-level label tuning — *"I need all those labels at least 200
pixels away from the colored section on the inside edge."* The kind of iteration that's
invisible in the final product but is most of the actual work.

**Raw:** [`raw/11-update-about-section-ui-and-documentation.md`](raw/11-update-about-section-ui-and-documentation.md)

---

### 12 — Common names on hover + a pane rename

**Date:** 2026-06-08 · **Branch:** `prototype` · **Prompts:** 4

**What it did:** Shipped `aa326b7` — reveal compound common names on hover/long-press,
and rename the "Results" pane to "Compounds." Committed straight to `prototype` as a
"smaller change," per my own rule in [`CLAUDE.md`](../../CLAUDE.md).

**Back-and-forth:** Began as genuine confusion on the live site (*"why does 1,8-Cineole
also say eucalyptol?"*). The pivot — *"let me be specific, in the Results Pane… which
honestly needs a rename, it's more the chemistry pane"* — is what turned a question
into both a feature and a rename.

**Raw:** [`raw/12-understand-terpene-naming-conventions-on-a.md`](raw/12-understand-terpene-naming-conventions-on-a.md)

---

### 13 — This log

**Date:** 2026-06-12 · **Branch:** `prototype` → `feature/prompt-log` · **Prompts:** 3

**What it did:** The session that created this prompt log — realizing the prompts
themselves are part of the artifact worth showing, locating the archived chats (the
local Claude Code transcripts), and auto-extracting all 192 prompts into the record
you're reading. Entry 13 documents its own creation.

**Raw:** [`raw/13-archive-and-document-prompts-for-transpare.md`](raw/13-archive-and-document-prompts-for-transpare.md)
