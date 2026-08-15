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
this project, cross-checked against the git history so each session is tied to the
commits, PRs, and tags it produced. Tool-result noise and interrupt markers were
filtered out; the prompts themselves are verbatim. See [`TEMPLATE.md`](TEMPLATE.md)
for the entry skeleton.

**Current count (re-measured 2026-08-15): 34 sessions, 397 prompts, 19,944 words,
2026-05-22 → 2026-08-15.**

This replaces an earlier claim of *"14 sessions, 192 real prompts, May 21 – Jun 12
2026,"* which had gone stale and was wrong in both directions: it overstated what
was still verifiable from that window (only 5 of those sessions still have
transcripts), and it understated the project, since 21 later sessions had no entry
at all. Entries 14–37 close that gap. Entries 38–45, added 2026-08-15, extend the
record through PR #20 ("Tree, Map, Constellation, Laps & Delivery") and PR #21
("Promote prototype to main") — the run-up to and including `prototype` catching
`main` up a second time.

**[`PROVENANCE.md`](PROVENANCE.md) is required reading before citing any number
here.** Not every entry is equally verifiable — the transcripts behind 12 of the
13 original entries have since been deleted, so for those the file in
[`raw/`](raw/) is no longer a receipt, it *is* the only record. That file defines
the tiers, states the exact filter behind the counts so they can be re-derived,
and names what is missing outright rather than estimating it.

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

---

### 14 — Standing up prototype branch protection

**Date:** 2026-05-21 · **Branch:** `claude/frosty-hoover-765d4c` · **Prompts:** 7

**What it did:** Same day as entry 02's git bootstrap, a second short session that set up the actual `main`/`prototype` split and the GitHub branch-protection ruleset now documented in CLAUDE.md — required status checks, and "restrict creations; restrict updates; restrict deletions; require a pull request before merging." No commits are traceable to this branch (it no longer exists and left no merge trail), consistent with this being GitHub UI configuration work rather than code.

**Raw:** [`raw/14-create-prototype-branch-for-development.md`](raw/14-create-prototype-branch-for-development.md)

---

### 15 — The UX-pass grade, then the fixes

**Date:** 2026-06-09 → 06-11 · **Branch:** `claude/thirsty-dijkstra-de159b` · **Prompts:** 9

**What it did:** Opened with a no-code usability grade — "really grade it for useability, discoverability, inferred targeted audience demographics" — before touching anything. Then worked the resulting punch list start to finish: the first-run nudge (`bf39985`), the ≤760px mobile breakpoint (`f149b6d`), float-label de-clutter and a trimmed header (`0aafd61`), a saturated data palette with coherent class colors plus two mobile-flag fixes (`be911ae`), clipped-label fixes for scent-mode anchors and curved category labels (`2a1045c`, `2124cf3`), dropped interpretive Note Suggester mappings (`85b204f`), a "note on the sources" methodology addition (`aef79a8`), and an em-dash/AI-isms copy strip (`f0a7a4f`). Shipped as PR #8 (merge commit `4c074d0`).

**Back-and-forth:** "nutty spicy roasted all clip" is the whole bug report for the label-clipping fix. The citation push-back — "are there not citations we can get from within the last decade?" — and the Note Suggester correction on elderflower ("it is its own thing," not chamomile + jasmine) both landed as direct edits.

**Raw:** [`raw/15-evaluate-html-usability-and-design-architect.md`](raw/15-evaluate-html-usability-and-design-architect.md)

---

### 16 — Citations, sourcing docs, and the berry problem

**Date:** 2026-06-10 → 06-14 · **Branch:** `claude/compound-library` (citation work shipped as `claude/citation-audit`) · **Prompts:** 20

**What it did:** Asked for a full citations list and supporting scope/sourcing docs, then interrogated every short-form citation for legitimacy. Landed as PR #11 (`93c16e7` — fix 8 unverifiable citations, add SOURCES + SCOPE docs; merged `bb6f1d6`), followed by a compound-library expansion (`3c5f5d2`) and — after noticing "a lot of berry note suggester just go to 'berry' flavor note... blueberry gives widely different flavor than strawberry" — dedicated strawberry/blueberry/blackberry notes and compounds (`6b8716d`). The session picked back up Jun 14 after a GPT-5.5 interference scare, landing a combined "Compound library expansion + onboarding pass" (`d835434`) straight to `prototype`.

**Back-and-forth:** "ah so we ran out of limits last night and then i had gpt5.5 try to help but that might have messed something up on local" — the session's next moves were entirely about verifying nothing got clobbered before continuing.

**Raw:** [`raw/16-create-citations-list-and-project-documentat.md`](raw/16-create-citations-list-and-project-documentat.md)

---

### 17 — Onboarding pass and the cotton-candy line

**Date:** 2026-06-14 · **Branch:** `claude/upbeat-mendel-6ef2f6` · **Prompts:** 11

**What it did:** A live Netlify-preview review that turned into the onboarding pass: tagline, explicit domain scope, 7 example demos, a translation ladder, and `INFERENCE.md` (`a55680e`). Also dropped misleading Note Suggester fruit redirects and added a confectionery category (`b035958`), surfaced blue raspberry/cotton candy context on the relevant compound notes (`c9cbb39`), then walked that back per the user's own rule (`fed9949`), split cheesy from sweaty into distinct notes (`d99ee60`), and fixed stray compound edges that survived after notes were cleared (`0694fc2`).

**Back-and-forth:** The cotton-candy call is a good example of the project's compound-forward stance in action — "input cotton candy is fine, just that if it is used as a descriptor enough anyway let's be compound forward and then parenthetical to describe that combo in common flavors" walked back an over-literal first pass.

**Raw:** [`raw/17-review-netlify-preview-for-legibility.md`](raw/17-review-netlify-preview-for-legibility.md)

---

### 18 — The Compass is born

**Date:** 2026-06-24 → 06-26 · **Branch:** `claude/upbeat-mendel-6ef2f6` · **Prompts:** 30

**What it did:** Recovered from a stray WIP commit that had dropped the compound-library expansion out of the working tree (`dfd04d4`), decoupled full citations from Go Deeper (`b847ebf`), then built device-motion Jiggle under a new settings gear (`e9e9cee`, `e707d57`), a five-ring "event horizon" warp transition into Go Deeper (`e4e4918`, `deb46f1`), typeable note intensity (`b90b755`), a Starburst display-shape experiment that was built then fully reverted, and — from the user sharing screenshots of an earlier personal prototype — the **Perception Compass**: a draggable radar (`da7e87a`) generalized from a fixed terpene axis into Notes/Compounds/Class modes with a 17-class dropdown and proportional resize (`447dcfe`, `a601e1f`), plus a full header wayfinding reorganization (`d12400f`). Merged to `prototype` via PR #14 (`15c1758`).

**Back-and-forth:** The Compass concept itself pivoted mid-session — first framed as a "terpene compass" nod to the user's original prototype, then corrected: "this one should not be just terpenes because i want it to actually be a representation of what the person is... inputting as their flavor notes." The resulting three-mode design is a direct answer to that correction.

**Raw:** [`raw/18-review-compound-library-and-go-deeper-sectio.md`](raw/18-review-compound-library-and-go-deeper-sectio.md)

---

### 19 — Varietal tables, starting with citrus

**Date:** 2026-06-27 → 06-28 · **Branch:** `claude/mobile-ui-pass-3` · **Prompts:** 17

**What it did:** Opened by modeling the app at Galaxy S10e portrait dimensions "because that's honestly how it will be demoed irl," fixing Compass mobile sizing and a slider/page-scroll conflict along the way (`7222ecc`). The core of the session is the first Go Deeper varietal-distinction table — bergamot vs. yuzu vs. Meyer lemon vs. navel orange vs. tangerine, generalized from an earlier cereal-only mechanism to citrus (`155bc39`), then extended to berry (`aa2b4cd`) and mint (`032e3f0`), each backed by a real distinguishing compound where the literature actually supports one.

**Back-and-forth:** "please rewrite this phrase so it just states what is listed. un ai-speak please" got a direct rewrite. The berry table's honest-gap framing — "this is what's layered on top of Berry's own shared compounds... not where it'd be tidy to invent a difference for every variety" — is the user's own words, quoted back into the resulting copy.

**Raw:** [`raw/19-create-pr-for-mobile-ui-fixes.md`](raw/19-create-pr-for-mobile-ui-fixes.md)

---

### 20 — The Tree workspace and independently-scoreable varietals

**Date:** 2026-06-28 → 06-29 · **Branch:** `claude/mobile-ui-pass-3` · **Prompts:** 20

**What it did:** Extended the varietal table to herb/floral (`df10b95`), fixed a WAIS word-bank bug it exposed (`402bd4b`), then added the Phase 1 plant-taxonomy layer (`9062b5a`) and, from "can we put all of the flavor notes on a taxonomy tree? this is the third viewer along with wheel and map" — the full Tree workspace (`fcdd956`), with zoom controls (`594428b`). Made varietal children independently scoreable rather than locked to their parent's slider (`58afe5c`), then built out Peach/Plum plus a ghost-row mirror for Cherry (`b43490a`), ghost rows for Cereal's Toast/Burnt sugar/Popcorn (`246c50d`), and a five-way Melon split (`ced6d3e`). The large protein/vegetable list in prompt 15 (chicken, turkey, duck, bacon, pork, beef, stocks) was **not** built this session — later explicitly closed as out of scope (see entry 31) — but its vegetable half became the Vegetal category slice (`35fd978`). Also made compound anchors active-only to de-crowd the wheel (`ee29bc5`), widened the dropdown-arrow hit target (`b5eca8e`), and fixed `subOf` children (e.g. Cranberry) not lighting up their parent's shared compounds when scored alone (`d628121`).

**Back-and-forth:** "if I just do 5 cranberry, without anything on berry parent, only circles show up with no lines leading to anything on the wheel" is a precise bug report that led directly to `d628121`'s edge-folding fix.

**Raw:** [`raw/20-prepare-herbal-floral-slice-for-pr.md`](raw/20-prepare-herbal-floral-slice-for-pr.md)

---

### 21 — "Opus you have such taste... own it"

**Date:** 2026-06-29 → 07-01 · **Branch:** `claude/mobile-ui-pass-3` · **Prompts:** 8

**Prompt:** *"Major ui overhaul needed for visibility, and usability... take an honest look from multiple perspectives — a probable expert, a novice, an enthusiast, someone with visual disability, or difficulties with short term memory... Opus you have such taste above chatgpt, own it, you deserve to shine here in ui and ux design."*

**What it did:** One long, open-ended brief turned into the saturation-as-evidence palette and iconographic wheel (`e2f1704`), a reading/dyslexia mode with fit-tested chemistry-ring labels (`99e2972`), the "dominant class" + "you might also smell" bouquet readout (`74aa96b`), calmer wheel edges with focus-to-reveal (`2222d3a`), and — after "argh, mobile ui didn't get the same attention" — matching mobile treatment: natural page scroll with a fixed Tasting Tray (`94cf4e0`) and a fix for a visual bug on the Roasted note's slider background (`00743dd`).

**Raw:** [`raw/21-major-ui-overhaul-for-accessibility-and-usab.md`](raw/21-major-ui-overhaul-for-accessibility-and-usab.md)

---

### 22 — Taming the float physics

**Date:** 2026-07-01 · **Branch:** `claude/mobile-ui-pass-3` · **Prompts:** 7

**What it did:** A focused physics-tuning pass on the wheel's floating bubbles — crowding ("the icons need to be aware of each other and have some sort of forcefield"), an abrupt freeze that needed a softer curve, desktop-vs-mobile scale awareness, and a "rave mode" overcorrection that needed slowing back down. Landed as perpetual gentle drift with a freeze toggle and pin-on-drag (`4639ff1`).

**Back-and-forth:** The physics metaphor came from the user, not the agent — "it's like blowing up a balloon with hot air and all of the gas molecules are colliding with each other in the confined space" — and "dude it's rave mode activated! argh and now desktop is dead by comparison!" is a genuine overcorrection caught and walked back within the same session.

**Raw:** [`raw/22-preview-mobile-portrait-view-of-index-html.md`](raw/22-preview-mobile-portrait-view-of-index-html.md)

---

### 23 — Ideas only, no code

**Date:** 2026-07-01 · **Branch:** `claude/mobile-ui-pass-3` · **Prompts:** 2

**Prompt:** *"perhaps write ideas to a doc, don't worry about updating agent.md or claude.md directly. I'll make sure those changes are applied later, I just want to see your idea."*

**What it did:** A short, deliberately code-free session — explicitly a workbench for HUD/mobile ideas, written to a doc rather than the app. No commit is traceable to this session specifically; a near-identical prompt opened session 24 (entry 24) minutes later, which is where the actual shipped work landed.

**Raw:** [`raw/23-improve-mobile-ui-smoothness-for-flavor-perc.md`](raw/23-improve-mobile-ui-smoothness-for-flavor-perc.md)

---

### 24 — Touch-reachable explanations and the honesty policy

**Date:** 2026-07-01 · **Branch:** `claude/mobile-ui-pass-3` · **Prompts:** 3

**What it did:** A parallel session to entry 23 (same opening prompt, same minute), but this one shipped: touch-reachable explanatory text for mobile users without hover (`d9f8dfc`), and — from "i think i also need an honesty policy in here where all citations have a 'under human review' until I personally review them" — the citation honesty policy that still governs `UNVERIFIED_REFS` today (`50996dd`).

**Raw:** [`raw/24-improve-mobile-ui-smoothness-for-flavor-perc.md`](raw/24-improve-mobile-ui-smoothness-for-flavor-perc.md)

---

### 25 — The Tree grows up, and PR #15 ships

**Date:** 2026-07-02 → 07-03 · **Branch:** `claude/mobile-ui-pass-3` · **Prompts:** 18

**What it did:** Compass on by default (`a0888b7`), the "Guide me" question-based Note Suggester mode (`b2d885c`), and a real physics rework — cached "home" positions plus a palm-tree restoring spring so only moved nodes get touched per tick (`1cb45b4`), then a polar redesign where angle encodes which note(s) feed a compound and radius encodes evidence strength (`67cdc4a`, `a31648c`). The Compass's close button and resize handle got fixed and repositioned to match OS convention (`00de4a3`). The Tree got rotated vertical (`dfb03f6`), a mobile scrunch bug fixed (`fc31c2e`), Anise split from Licorice as honest separate notes (`3f6126e`), expanded-by-default with zig-zag labels and wheel icons (`8b66d47`, `406c22c`), and family detail pages (`39e119a`). Closed with a whole-app PROTOTYPE watermark (`4fac036`) and PR #15 merging into `prototype` (`931a10d`).

**Raw:** [`raw/25-commit-and-push-local-changes-to-branch.md`](raw/25-commit-and-push-local-changes-to-branch.md)

---

### 26 — Nolan Æckhart, iconic-orion, and the credits question

**Date:** 2026-07-03 → 07-04 · **Branch:** `feature/favicon-polish` · **Prompts:** 34

**What it did:** A long identity/branding session. Started as maker credits and a footer (`33cca03`), then worked through a real privacy tension — whether to put a legal name on a public repo — landing on "Nolan [Æ]" / "© Æckhart" rather than a full legal name, with the brand itself named `iconic-orion` (distinct from the generic "aroma wheel" term, since "someone already has claim to 'wine aroma wheel'"). Shipped branding assets (`0e95905`), a feedback CTA in the HUD and About tab (`fad73d2`, `84f9ebc`), non-destructive map marker selection with a legend toggle-all (`d4ab53b`), a mobile nudge-dismiss fix (`501b451`), and two favicon passes — a 9-wedge ring adding Vegetal (`30a07d3`) then a thin glowing ring deliberately distinct from "a generic or even already copyrighted wine aroma wheel" (`47c38a7`).

**Back-and-forth:** The credits question is a genuine, visible deliberation — from offering a full bio and legal name, through a password-gate option, to "scratch all of this... just put it once in the credits. as Nolan [Æ]." Also a real mobile bug: the dismissible helper boxes were "impossible to close on mobile," fixed same session.

**Raw:** [`raw/26-work-on-local-prototype-before-github-push.md`](raw/26-work-on-local-prototype-before-github-push.md)

---

### 27 — feature/bloom: quick-use as powerful as Go Deeper

**Date:** 2026-07-04 → 07-07 · **Branch:** `feature/bloom` · **Prompts:** 16

**What it did:** Started from the app-checkup request that also opens entry 26/28, worked through a screen-reader punch list (`1fb8052`, `3578eff`), then a genuine design pivot: Go Deeper reframed as a naturalist "canopy to soil" descent — vines, an ecobrutalist plant-and-vine motif, "back to nature mannn" — instead of a generic sci-fi transition (`0102cb4`, `6d4689a`). The session's second half is the thesis statement for `feature/bloom` itself: quick-use should be "just as powerful as a go deeper experience," the wheel should be front-and-center and shareable, and Go Deeper should "bloom" into extended science. That thesis produced the P3 shareable tasting-card slice — client-side PNG/JPG/PDF export with a share/bookmark link, no backend (`263a382`, `def523c`, `052aeec`).

**Back-and-forth:** The long prompt 9 is the branch's founding document in the user's own words — merging two until-then-separate branches (UX-checkup and go-deeper-naturalist) because "these are basically looking at a natural expanded learning moment... that's kind of the point of go deeper." It explicitly asks for a project-management roadmap, not just a brainstorm — "this is not a plan that goes nowhere."

**Raw:** [`raw/27-conduct-ux-audit-for-different-user-personas.md`](raw/27-conduct-ux-audit-for-different-user-personas.md)

---

### 28 — Map inset for the trading card

**Date:** 2026-07-10 · **Branch:** `feature/bloom` · **Prompts:** 9

**What it did:** Built the map inset for the share card's front/back flip layout, reversed the Compass resize-drag axis to match OS convention ("drag left to expand left"), and made Reading Mode the default state — swallowing the separate "turn jiggle off" toggle and freezing the float sim on load rather than leaving it perpetually drifting. All landed in one commit (`44fda9e`).

**Back-and-forth:** "Too many options is my point. Let's remove these options entirely and make the state be the default experience of the app" is a deliberate simplification call — collapsing what had been a growing settings surface back down.

**Raw:** [`raw/28-share-trading-card-ux-ui.md`](raw/28-share-trading-card-ux-ui.md)

---

### 29 — Fencing ChatGPT to its own branch

**Date:** 2026-07-11 · **Branch:** `codex/aroma-wheel-responsive-ux-pass` · **Prompts:** 5

**What it did:** Set up the `codex/*` branch policy now in `CLAUDE.md` — one branch namespace ChatGPT may touch, with Claude free to work everywhere else and to also commit there. Landed as the initial protocol docs (`e38d171`, `169b98e`) and the check-in handoff templates (`fc96d51`, `07d91a0`).

**Back-and-forth:** "in case any new openai models hopefully will keep whatever bugs or snips inside its own area and we keep most of the repo supported solely by claudel" states the actual motivation plainly — this is a containment decision, not a trust statement about ChatGPT's work quality.

**Raw:** [`raw/29-codex-integration-branch-strategy.md`](raw/29-codex-integration-branch-strategy.md)

---

### 30 — Reviewing ChatGPT's first pass

**Date:** 2026-07-11 · **Branch:** `codex/aroma-wheel-responsive-ux-pass` · **Prompts:** 10

**What it did:** The first post-hoc review of ChatGPT's work on the codex branch — checking commits, verifying `index.html` still worked, testing mobile. Formalized the agent working agreement (`660c666`). On explicit one-off permission ("eh, this is special permission this time to go ahead and edit it"), repositioned the Go Deeper button to the header's center (`c9c62b4`) and fixed it overlapping the organize-viewer tab (`0e53953`).

**Back-and-forth:** The "special permission... (agian special permission from I, Nolan)" framing on prompts 8 and 10 is the user being explicit about a one-time exception to the codex-branch-is-ChatGPT's-domain rule, not a standing change.

**Raw:** [`raw/30-claude-vs-chatgpt-relationship.md`](raw/30-claude-vs-chatgpt-relationship.md)

---

### 31 — feature/bloom archived, scope closed to botanical

**Date:** 2026-07-11 · **Branch:** `feature/bloom` · **Prompts:** 9

**What it did:** Marked `feature/bloom` as a historical baseline predating the dual-agent era (`af65d65`) — "the codex branch is the active experimentation tab... I like claude as my preferred and openai as my workhorse." Also closed the meats/eggs/stocks Slice 2 that had been queued since entry 20: "i dont want to explore meats anymore. i think i want to keep this mostly botanical focused."

**Back-and-forth:** The meats-scope closure is a clean, explicit reversal of an idea that had been on the table since prompt 15 of entry 20 — worth noting because the raw prompt log otherwise makes it look like an open thread.

**Raw:** [`raw/31-historical-branch-marker.md`](raw/31-historical-branch-marker.md)

---

### 32 — Scoping the shareable-card review

**Date:** 2026-07-11 · **Branch:** `codex/aroma-wheel-responsive-ux-pass` · **Prompts:** 4

**What it did:** Set up a PR from the codex branch to `prototype` with Nolan retaining final merge say, then asked for a tightly scoped review procedure an agent could follow that looks *only* at the shareable-card UI. That procedure is what shows up verbatim as the single prompt in entry 33 and the opening prompt of entry 34 — this session produced the review brief, not app code.

**Raw:** [`raw/32-prototype-pr-setup.md`](raw/32-prototype-pr-setup.md)

---

### 33 — The scoped review, dispatched

**Date:** 2026-07-11 · **Branch:** `codex/aroma-wheel-responsive-ux-pass` · **Prompts:** 1

**Prompt:** The full "Shareable Card UI Review Scope" brief drafted in entry 32 — in/out-of-scope boundaries, a numbered procedure, and "when in doubt, ask: is this a control or UI element that belongs to the shareable card?"

**What it did:** A single, self-contained scoped-review prompt with no back-and-forth in this session — the review itself is what entry 34 continues from.

**Raw:** [`raw/33-shareable-card-ui-review.md`](raw/33-shareable-card-ui-review.md)

---

### 34 — Card review lands: "more stunning" means less, not more

**Date:** 2026-07-11 · **Branch:** `codex/aroma-wheel-responsive-ux-pass` · **Prompts:** 7

**What it did:** Ran the same scoped card review (a near-duplicate brief to entry 33, extended with compound/note visibility toggles in scope), then extended Claude's own commit access to the codex branch as a standing rule rather than one-off permission ("update the rule where you can also update this branch. this is just the only one i want chatgpt touching") (`aceddb1`). Redefined the card's "More stunning" style to be wheel-only with no compound bar or map readout, and "More informative" to keep everything (`9c71a97`, `aa159a0`).

**Back-and-forth:** A real correction on the card styles: "eh better. go for more stunning. like no extra details besides the flavor notes and dominant compounds... the compounds data bar graph is too much for stunning, that's more informative coded." The first pass had "stunning" include too much.

**Raw:** [`raw/34-shareable-tasting-card-ui-review.md`](raw/34-shareable-tasting-card-ui-review.md)

---

### 35 — The systems-thinking session: laps, strata, and the GIS turn

**Date:** 2026-07-25 → 07-26 · **Branch:** `codex/aroma-wheel-responsive-ux-pass` · **Prompts:** 33

**What it did:** Opened as an orientation check on a branch that had drifted, then a real design correction — Map demoted from a peer pane in a three-way Wheel/Tree/Map switcher to needing its own dedicated button, because "there needs to be a more reflexive link between the family tree... and the chemical analysis" than a flat tab switch implies. Documented the mobile-first product-design contract (`17c7fdd`) and closed out the citation audit with a compact-phone HUD and resizable Tree sheet (`305d0d0`). Landed a real "aha" moment as shipped features: **Laps** — timestamped tasting snapshots, "like a stopwatch... it stacks on the righthand side... oldest is on bottom (kinda like geology)" (`22b4527`, `1aff3ea`), and the Go Deeper visual changed from an expanding circle to descending strata (`3db48b2`). Added Delivery as a third sensory dimension (`38e37db`), fenced the unrelated `Ideas/` project out of the repo (`e688599`), and kicked off the prompt-log archival effort that produced entries 14–37 themselves (`2533afc`). The session ends by explicitly asking to branch off into a fresh context window for a GIS-driven map-layers pass (economic-cultivation and cultural-value layers, in addition to origins) — that continuation is entries 36 and 37.

**Back-and-forth:** "i admit i didnt read most of that cause I got stuck at 'a hard context switch, no continuity of what you were doing.' which I want to open up more into" is a genuine mid-session redirect — the user pushed past a long status report to interrogate one specific complaint. The prompt-log integrity request (prompt 12) — "we need to actually go back through the entire git history to locate the exact ideas and prompts... this is so that there is a defensible 'here is the human work'" — is the direct origin of `PROVENANCE.md` and this batch of entries.

**Raw:** [`raw/35-ui-design-and-feature-transitions.md`](raw/35-ui-design-and-feature-transitions.md)

---

### 36 — Map layers, watched not touched

**Date:** 2026-07-26 · **Branch:** `codex/aroma-wheel-responsive-ux-pass` · **Prompts:** 7

**What it did:** A continuation session working from a written handoff doc (`.claude/session-handoff-thesis-systems.md`), resuming the map-layers systems-analysis workflow from entry 35's close. Ended with an explicit instruction to observe rather than act — ChatGPT was live-editing the map's three data views at the same time, and the ask was to "follow along... but dont interfere with them... codex has a special way with geographic data that i want you to watch." No commit in this session's window is attributable specifically to it rather than to the parallel entry 37 session or to ChatGPT's own concurrent work; both threads feed the same map/lens work later described in `CLAUDE.md`'s 2026-08-04 status note (production and cultural-tradition lenses for coffee/cacao/vanilla).

**Raw:** [`raw/36-session-handoff-thesis-systems.md`](raw/36-session-handoff-thesis-systems.md)

---

### 37 — The wreath idea

**Date:** 2026-07-26 · **Branch:** `codex/aroma-wheel-responsive-ux-pass` · **Prompts:** 8

**What it did:** A near-duplicate of entry 36 (same handoff doc, same first six prompts, run in parallel), diverging at the end with a concrete design direction relayed from a conversation with ChatGPT: the Wheel/Map switcher's third option was unclickable and needed fixing, the Tree "might do better if when you zoom to family level it looks more like a wreath... to carry over the circle design of aroma wheel," and the Map "could also have a compass approach to show generally where in the world your notes are." The wreath idea specifically surfaces later in `CLAUDE.md`'s description of the Tree's "conical-helix layout... family wreaths."

**Raw:** [`raw/37-session-handoff-thesis-systems.md`](raw/37-session-handoff-thesis-systems.md)

---

### 38 — Desktop landscape and iPad polish, tree leaves

**Date:** 2026-07-26 · **Branch:** `codex/aroma-wheel-responsive-ux-pass` · **Prompts:** 3

**What it did:** A short tail end of the same session covered in entry 37 (`def702be`), picking back up later the same evening — "well while codex is c[on]tinuing to work on its aspects let's really make sure that what you have sanctioned off as your work is as prstine as we can make it... check desktop landscape especially and also ipad sizze." Landed as `060519e` ("Tree: bloom family leaves into wheels") and `b15380f` ("Header: wrap instead of squeeze, so no control is ever amputated"), with `1a557ee` ("Tree: read the family scale as growth rings, not branches") following shortly after.

**Back-and-forth:** None major — the three prompts are short green lights in sequence. Prompt 3 ("yeah maybe it should read as leaves at that point yes you go for it with your ui artistry") is a direct sign-off on the leaves framing that shipped in `060519e`.

**Raw:** [`raw/38-desktop-landscape-polish-tree-leaves.md`](raw/38-desktop-landscape-polish-tree-leaves.md)

---

### 39 — Extending codex the same trust as Claude

**Date:** 2026-07-27 · **Branch:** `codex/aroma-wheel-responsive-ux-pass` · **Prompts:** 2

**What it did:** Opened with "can you make sure that prototype is copied over to main so we can update main to whatever the most recent is" — fulfilled later the same day as PR [#19](https://github.com/iconic-orion/iconic-orion/pull/19), "Promote prototype to main: mobile UI overhaul, taxonomy tree, compass, shareable tasting card" (merged `e30994d`), though not within this two-prompt exchange itself; no commits are directly traceable to this session.

**Back-and-forth:** The real content of this short session is prompt 2, a direct correction of a boundary Claude had apparently cited back at the user — the pre-existing CLAUDE.md gate requiring codex work to be extracted/re-implemented rather than merged straight into `prototype`: *"that's against the branching rule in CLAUDE.md ('Do not merge codex/* directly to prototype... move work onward by extracting/re-implementing onto a proper branch'). I trust codex to do everything claude can do now that Ive had time to test their newest model. its trustworthy."* This is the origin of the "Policy update (2026-07-27)" now recorded in [`CLAUDE.md`](../../CLAUDE.md): the extraction/re-implementation gate dropped, `codex/*` allowed to merge directly into `prototype` or `feature/bloom`, with Claude's review moved from a pre-merge gate to periodic post-hoc review. Worth naming plainly, per this log's own purpose: this is the user overriding an agent's caution, not the other way around.

**Raw:** [`raw/39-prototype-to-main-branching-pushback.md`](raw/39-prototype-to-main-branching-pushback.md)

---

### 40 — The conical helix

**Date:** 2026-07-30 · **Branch:** `codex/aroma-wheel-responsive-ux-pass` · **Prompts:** 7

**What it did:** Opened by asking Claude to digest a codex handoff ("codex gave you some handoff info please make sure you digest it and report back") before treating codex's mobile-visualization work as a running start rather than a from-scratch build — "you have perhaps an equally meaningful task but it might prove beneficial to save some of your processing for the actual creative clean ui design." The resulting purely-visual pass on the Tree (asked twice: "let's see what you can do purely visually aesthetically") landed as `bd00f53` ("refine responsive aroma exploration") and, after a correction that desktop was still cramped ("desktop view is still pretty unviewable because its a super side but short interactive... is there another way to show hierarchy while spiraling?"), the conical-helix layout itself — `61d069f` ("conical-helix layout for the Branches tree") — committed on request ("commit and push").

**Back-and-forth:** Prompt 6 is a direct design correction mid-pass: the first visual answer to "purely aesthetic" wasn't using the desktop screen well, and the spiral/conical-helix framing is the specific fix that came out of naming that problem.

**Raw:** [`raw/40-conical-helix-tree-visual-pass.md`](raw/40-conical-helix-tree-visual-pass.md)

---

### 41 — The Constellation is born

**Date:** 2026-07-31 → 08-01 · **Branch:** `codex/aroma-wheel-responsive-ux-pass` · **Prompts:** 9

**What it did:** Opened reacting to a codex tree experiment, then built out — largely in the user's own words — the concept for Go Deeper's subjective hemisphere: *"i see / imagine a constellation section where we map it by chemistry, the notes align by shared aroma molecules... in another visual the constellation of flavor notes align in a way that points to taxonomy and tree of life. another still aligns flavor notes by world map locations... this is a separate visualization 'hemisphere' for the aroma wheel. one is what we already have, the completely practical citation-based, the other is the subjective creator mind space."* A sketch request ("i want that constellation visualization to be real. can you sketch something like that out?") and a callback to an earlier discovery ("limonene is owned by citrus wheras linalool appears everywhere") led to it shipping for real: `482729a` ("add Constellation, Go Deeper's subjective hemisphere"), `d8dc2a3` ("promote Constellation to a direct header toggle"), and `f980b88` ("wire Constellation to the actual tasting, fix tween NaN bug").

**Back-and-forth:** Two real corrections close the session — "wait where is it? i dont see. maybe would be better on the front hud not behind go deeper" (led directly to `d8dc2a3`'s header-toggle promotion) and "the constellation does not appear to be updating with the tasting notes or with anything no matter what notes are active" (a functional bug, fixed same session in `f980b88`).

**Raw:** [`raw/41-constellation-creator-mindspace-concept.md`](raw/41-constellation-creator-mindspace-concept.md)

---

### 42 — The pre-merge checkup, and a branch rename

**Date:** 2026-08-06 → 08-07 · **Branch:** `codex/aroma-wheel-responsive-ux-pass` → `codex/tasting-relationship-guidance` (branched off `7594936` partway through) · **Prompts:** 24

**What it did:** The long opening prompt sets the session's whole brief: codex's tree/HUD work was nearly ready to merge into `prototype`, and the ask was a usability/language checkup keyed toward the audience Go Deeper is actually for — "inquisitive and want to go deeper into how these notes relate and how to detect these different compounds by inferring from detecting flavors/aromas with our senses." Partway through, the working branch itself was renamed from `codex/aroma-wheel-responsive-ux-pass` to `codex/tasting-relationship-guidance`, branched off commit `7594936` ("center deeper exploration on tasting insights") — a real structural pivot mid-session, reflecting the session's own thesis shift toward surfacing relationships between notes rather than just responsive polish. From there: ungating Map and Tree from behind Go Deeper (`ee22b5b`), one shared relationship engine behind the Wheel and Constellation (`04c7057`), the top relationship surfaced live above the tasting tray (`205a488`), retiring the workspace-reveal morph (`a6bdf5e`, matching "retire reveal mirph and regen line nums"), moving the Go Deeper button to where "the sprout comes out of the bottom left corner of wheel" (`eb1eee8`), an animated tappable-leaves cue (`8825e45`), Compounds becoming a peer panel stacked below Notes on mobile with a Results→Compounds rename (`27bd1a8`), a way back to the wheel on mobile (`dd13062`), screen-reader announcement of the top relationship (`e499184`), and — from a question about whether banana's flavor compounds reflect modern cultivars versus older varieties — a new "widely-repeated claims" evidence tier that separates verified from speculative (`1511c2d`).

**Back-and-forth:** Prompt 9's telegraphic shorthand ("retire reveal mirph and regen line nums") landed correctly despite the typos. Prompt 22's question about banana cultivars — "are we sure there aren't multiple possible origins for some species... based on versions that no longer exist" — is the direct origin of the new evidence-tier distinction, not a passing aside; prompt 23 explicitly asks that the guesses be labeled as such rather than dropped.

**Raw:** [`raw/42-pre-merge-usability-checkup.md`](raw/42-pre-merge-usability-checkup.md)

---

### 43 — Honest About copy, in the user's own voice

**Date:** 2026-08-04 → 08-05 · **Branch:** `codex/aroma-wheel-responsive-ux-pass` · **Prompts:** 17

**What it did:** Opened with pre-merge cleanup — retiring a stale handoff doc (`dd4cccd`) and, on request to strip "agentic coding tells," dropping human-verified badges for under-construction tags and scrubbing mentions of codex/claude from the shipped HTML while adding an About section on the information-design decisions behind the wheel (`3137370`). The session's core correction is prompt 5: the existing "citation honesty policy" copy read as an admission of doubt rather than a description of process — *"it makes it sound dishonest and possibly completely false... just say what criteria was considered for choosing works cited to rely on"* — replaced with source-selection criteria (`850afa1`). A long voice pass followed: no idioms unless the user's own, minimal em dashes, no semicolons ("I speak as clearly as possible and really rely on colons for lists and commas and oxford comma style"), no contractions outside quoted literature, and a shorter, plainer gas-chromatography paragraph refocused on coffee and botanical aromatics generally rather than wine. Separately, the Tree's floret grouping was corrected to respect family boundaries strictly — "cant have multiple families in one floret... it needs to be one 'wingspan' of notes for each family," sized to family membership (`9665eb5`, `b60d890`).

**Back-and-forth:** The citation-honesty-policy reversal (prompt 5) is the clearest correction in this entry: a feature built earlier in the project (entry 24's honesty policy) is explicitly walked back here as counterproductive once it shipped in copy, not because the underlying practice changed.

**Raw:** [`raw/43-about-section-honesty-and-voice-pass.md`](raw/43-about-section-honesty-and-voice-pass.md)

---

### 44 — Venn overlaps and an always-accessible Enter tasting button

**Date:** 2026-08-14 · **Branch:** `codex/tasting-relationship-guidance` · **Prompts:** 21

**What it did:** Picked up a compounds-drawer conversion left mid-flight by a prior session that had hit a usage limit (`2a87914`), then swept stale CSS/state left behind by superseded features (`531eaba`). The session's centerpiece follows a moment of genuinely getting something out of the tool: scoring a tasting and seeing "Strongest: Lychee" under Rose, questioning whether that meant lychee was rose's "real" smell, and landing on "that's kind of neat if I start saying I smell 'lychee' when I'm smelling rose" — then asking for a better visual than a bare percentage: *"this reads like a venn diagram in my head, show the overlap of compounds that make up the aroma profile... if they actually differ in quantities and also have unique aromatic compounds to each their own, the diagram would be more closer to an infiniti symbol."* Shipped as a proportional Venn diagram (`03f20ac`), plus Constellation's lenses linked to their tools and a sixth "bloom" depth for Go Deeper — the asteraceae/aster/star/constellation pun, explicitly signed off on (`05d5604`). Closed with a run of mobile fixes found by testing live: a scrollable compounds drawer (`a255b02`), vertically-stacked Venn labels (`eaeda1d`), a half-sized Map compass with a minimized badge (`72df64b`), the always-accessible Enter tasting button (`a199994`), and a standardized "Sensory exploration only! Not medical advice." disclaimer given its own line (`9bb1c8c`, `5a0219c`). Ended with the PR to `prototype` opened from this branch — this becomes PR [#20](https://github.com/iconic-orion/iconic-orion/pull/20).

**Back-and-forth:** The Venn-diagram request (prompt 11) is a strong example of the user reframing an abstract percentage into a shape they could reason with, then getting exactly that shape shipped. Prompts 8 through 10 are a small back-and-forth of their own — checking, then re-checking, whether "Strongest: Lychee" was accurately worded before trusting it enough to build on.

**Raw:** [`raw/44-venn-overlap-and-enter-tasting-button.md`](raw/44-venn-overlap-and-enter-tasting-button.md)

---

### 45 — Prototype promoted to main, again

**Date:** 2026-08-15 · **Branch:** `codex/tasting-relationship-guidance` · **Prompts:** 1

**Prompt:** *"can we also copy prototype over to main so it's updated with the most recent version"*

**What it did:** A one-line request, fulfilled within minutes as PR [#21](https://github.com/iconic-orion/iconic-orion/pull/21) "Promote prototype to main" (merged `c96c40b`, roughly four minutes after this prompt) — following PR [#20](https://github.com/iconic-orion/iconic-orion/pull/20) "Tree, Map, Constellation, Laps & Delivery: 70 commits of new features + mobile polish" merging into `prototype` earlier the same morning (`abe0174`). The second time this exact request has been made: entry 39 asked for the same thing on 2026-07-27, becoming PR #19.

**Raw:** [`raw/45-second-prototype-to-main-request.md`](raw/45-second-prototype-to-main-request.md)
