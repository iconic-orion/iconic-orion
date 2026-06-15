# Scope & rationale

What Aroma Wheel is for, where its boundaries are, and the conceptual case for
why a perceptual report can warrant *some* confidence about which aroma compounds
are probably present — the kind that could be confirmed chemically. This is the
"why" companion to [SOURCES.md](./SOURCES.md) (the "what") and the in-app
**About** and **Methodology** sections.

---

## 1. Scope

### What it is

A tool that takes what a person reports smelling or tasting and maps those words
onto the aromatic compounds most plausibly behind them, drawn from published
GC-MS work. **You report perceptions; the wheel shows compounds.** It is a
suggestion engine over a small, curated knowledge graph — not a chromatograph,
not a grader, not a verdict machine.

### What's in scope

- **Things you ingest.** Coffee, beer, wine, mocktails, and edible aromatics
  generally. The tool is *gustatory-agnostic* across these: it shouldn't matter
  whether you're tasting coffee, hops, wine, or spaghetti — the same loop applies.
- **The retronasal end of smell.** The post-swallow exhale that is most of what
  people mean by "flavor." This is the center of gravity on purpose.

### What's adjacent but out of scope (for now)

- **Perfumery / orthonasal "sniff" smell.** A close neighbour the project may
  explore later, but not supported today. The compound set and the linkage
  weights are tuned for the retronasal, edible context.
- **Concentration, matrix effects, co-occurrence physics, and individual
  perceptual variation** beyond the threshold-tier multiplier. These are
  deliberately not modeled; see [§4 Honest limits](#4-honest-limits).

### Who it's for

Curious tasters across the whole range of interest and tolerance — and
**explicitly inclusive of non-drinkers and sober folks.** Copy never leads with
wine, spirits, or beer; alcohol is one context among many, not the framing. The
default altitude is enthusiast-level: the tool owns its chemistry depth rather
than watering it down, and lets depth be opt-in through affordances (legends,
definition toggles, "Go Deeper" mode) rather than gating who gets the data.

### The stance

Your perceptions are real, and they change with the moment. The same cup can read
differently by time of day, what you ate, how alert you are — and that variation
is **signal, not noise.** The tool never grades you against a "correct answer."
What you smell *is* the data; the compounds it surfaces are plausible
contributors, not corrections.

---

## 2. The core claim

> A perceptual report, mapped through robust flavor-chemistry associations,
> licenses a *bounded, defeasible* hypothesis about which compounds are probably
> present — a hypothesis that is in principle confirmable by GC-MS.

This is the intellectual load-bearing wall of the whole project, so it's worth
stating carefully. The claim is **not** that perception reveals molecular truth.
It's that perception plus literature gets you to a *good guess with reasons* —
and that a good guess with reasons is genuinely worth something.

### Why perception carries information about molecules

Olfaction is, mechanistically, a molecular recognition system. A percept like
"clove" is not free-floating: it is the readout of specific volatiles binding
specific receptors. The flavor-chemistry literature has, for many aromas, already
done the inverse mapping — isolating *which* molecules reliably produce *which*
percepts (eugenol ↔ clove, cinnamaldehyde ↔ cinnamon, sotolon ↔ maple, geosmin ↔
wet earth). When a person reliably reports "clove," they are reporting the
downstream effect of a cause the literature has characterized. The percept is
evidence about the cause.

This is why the strongest single-compound cases are the **signature compounds**:
a trace of cinnamaldehyde *is* the smell of cinnamon; vanillin *is* the principal
smell of vanilla. For these, "I smell cinnamon" is close to "cinnamaldehyde is
present" — not certainty, but a high-prior inference.

### What kind of inference this is

It is **abduction** — inference to the best explanation — not deduction.

- Deduction would be: "perception X, therefore compound C, necessarily." The tool
  never claims this and it would be false (different molecules can evoke similar
  notes; the same drink carries dozens to hundreds of volatiles).
- Abduction is: "perception X is well explained by compound C being present;
  given the literature, C is among the best available explanations." That is a
  legitimate, everyday form of scientific reasoning, and it is *defeasible* — new
  evidence (a GC-MS run) can confirm or overturn it.

So the right reading of a lit-up compound is: *"given what's published about this
aroma, this compound is one plausible thing you're picking up"* — a hypothesis to
test, not a result.

### Why confidence is *graded*, not binary

The tool refuses to output a single yes/no because the inference genuinely has
degrees. Three things push confidence up, and the model encodes each:

1. **Convergence (breadth).** Several independent notes pointing at the same
   compound is much stronger than one. Lemon *and* orange *and* grapefruit all
   reinforcing limonene is a different epistemic situation than a lone match.
   (In the model: `breadth` = contributing notes ÷ 3, capped at 1.)
2. **Association strength.** Some note→compound links are near-defining; others
   are minor or speculative. The strongest contributing edge sets a floor on how
   seriously to take the compound. (In the model: `strength` = max edge weight.)
3. **Specificity / signature-ness.** A signature compound (distinctive enough
   that a trace reads as the source aroma) earns more from a single matching note
   than a "shared" compound that shows up across many aromas.

Confidence in the tool is `0.55 × breadth + 0.45 × strength` — a deliberate blend
that rewards *both* "many notes agree" and "the agreement is on a strong link."
That formula is the operational form of the core claim: the more your perception
converges, and the stronger and more specific the links it converges on, the more
confident the molecular hypothesis becomes.

### Why potency matters too (the threshold multiplier)

Detectability is not uniform. A trace of furfurylthiol reads loud; a much larger
amount of furfural barely registers. So a low-threshold compound deserves to be
taken seriously even on a faint percept, because faint-but-present is exactly how
those compounds behave. The threshold-tier multiplier (`very-low ×1.20` down to
`high ×0.55`) encodes this: it adjusts perceived *intensity* by how easily the
compound is smelled at all. This is why the inference "I caught just a whiff of
something roasty/sulfury → furfurylthiol" is defensible despite the whiff being
faint — the compound is detectable at parts-per-trillion.

### Where the chain is confirmable

The payoff of framing this as abduction is that the loop closes empirically. Each
lit-up compound is a *named, testable molecule*. Run the actual sample through
GC-MS and you can check it. The tool's job is to turn a vague perceptual
experience into a **structured, falsifiable shortlist** — to get from "this coffee
weirdly tastes like cotton-candy grapes" to a small set of named compounds you
could go confirm. That is the entire value proposition: not the answer, but a
well-reasoned, checkable hypothesis.

---

## 3. How the claim is operationalized

The rationale above is not just narrative — it's wired into the data model and
the scoring. Quick map from idea to mechanism (full math in the in-app
Methodology):

| Conceptual claim | Where it lives in the tool |
|---|---|
| Percepts are evidence about molecules | The `EDGES` graph: every note→compound link is seeded by real GC-MS work |
| Inference is graded, not binary | `Confidence = 0.55 × breadth + 0.45 × strength` |
| Convergence strengthens a hypothesis | `breadth` term (contributing notes ÷ 3, capped) |
| Some links are near-defining | `strength` term (max edge weight); signature vs. shared specificity |
| Detectability isn't uniform | Threshold-tier perception multiplier (`×1.20 … ×0.55`) |
| Every hypothesis is checkable | Each compound is a named molecule with a citation, confirmable by GC-MS |

The weights themselves are normalized editorial approximations seeded by the
literature, **not** values extracted from the cited papers — see the integrity
note in [SOURCES.md](./SOURCES.md#the-integrity-rule).

---

## 4. Honest limits

The claim is bounded, and naming the bounds is part of making it credible:

- **No concentration math.** The tool doesn't know how much of anything is in your
  cup. The threshold tier is a proxy for perceived loudness, not a quantity.
- **No matrix effects.** The same compound can read differently across different
  drinks; the model treats a given edge as contributing equally regardless of
  context.
- **No co-occurrence physics.** Real compounds amplify and mask each other; the
  model treats edges as independent contributions.
- **No correction of the perceiver.** Two people with the same experience can
  report differently; the tool honors the report rather than "fixing" it.
- **A curated set, not a full volatile profile.** Real samples carry dozens to
  hundreds of volatiles; the tool models 53 compounds chosen for usefulness in
  tasting.

These limits are exactly *why* it's a suggestion engine and not a lab — and why
the output is a hypothesis worth testing rather than a measurement to trust.

---

## 5. Why this is a public, educational artifact

One static HTML file, source on GitHub, commented so the design choices are
legible as they come up. The showcased value is the **thinking** — the systems
modeling of how sensory inference actually works — at least as much as the tool
itself. This doc exists so that reasoning is written down plainly, not just
implied by the code.
