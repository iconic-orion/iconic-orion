# Inference: from perception to compound

Why does reporting what you smell or taste produce meaningful information about
which aromatic compounds are likely present? This document makes the explicit case
for the tool's central claim — the reasoning that SCOPE-AND-RATIONALE.md calls
"the load-bearing wall" but mostly treats as assumed.

---

## The core chain

```
Human olfactory perception
         ↓
Shared sensory vocabulary (trained by sensory science)
         ↓
Probabilistic signal about volatile compound families
         ↓
Structured, falsifiable compound hypothesis
```

Each link in this chain is doing real work. The tool is only as good as the
weakest one.

---

## Link 1: Olfaction is a molecular detection system

This is the mechanistic foundation. You don't smell "lemon" in the abstract —
you smell molecules. Limonene, linalool, citral, and a handful of other volatiles
are binding olfactory receptors in your nose, and the percept "lemon" is the
downstream readout of that binding pattern. The flavor-chemistry literature has,
for many descriptors, already characterized this inverse mapping: it has isolated
*which* molecules reliably produce *which* percepts by presenting purified
compounds to trained panels and asking what they smell.

This means a percept is evidence about a cause. "Clove" is the readout of
eugenol. "Cinnamon" is the readout of cinnamaldehyde. "Roasted coffee" is
substantially the readout of furfurylthiol at parts-per-trillion. When you report
these, you are reporting the downstream effect of molecular causes that are, at
least probabilistically, named.

**The limit:** olfaction is holistic, not one-to-one. A percept is produced by a
pattern of receptor activations, and different molecules can produce similar
patterns. "Fruity" is not one molecule. This is why the tool never outputs a
single answer — it outputs a ranked hypothesis space, weighted by how many of
your notes converge on each candidate.

---

## Link 2: Shared vocabulary is a trained encoding

The note vocabulary on the wheel (lemon, rose, toast, clove…) is not arbitrary.
It derives from sensory science practice — specifically, the standardized
descriptors developed and stabilized through trained-panel work in coffee, wine,
beer, and food science. The most influential formalization is probably the SCAA
Coffee Taster's Flavor Wheel (World Coffee Research lexicon, 2016), but the
vocabulary family extends through Meilgaard et al.'s *Beer Flavor Terminology*
(1979), the UC Davis wine aroma wheel (Noble et al. 1987), and the broader
flavor-chemistry literature.

Why does this matter? Because a trained sensory vocabulary is, functionally, a
*calibrated encoder* — a shared coordinate system that translates private
perceptual experience into communicable signal. When a trained taster says
"lemon," and a GC-MS shows elevated limonene, the two are speaking about the same
underlying reality through different observational channels. The vocabulary is the
bridge.

The tool does not require users to be trained panelists. But it inherits the
calibration work of those who built the vocabulary. When you pick "grapefruit"
because it's the best word for what you're experiencing, you're using an encoder
that was built to be chemically coherent — and the note→compound links in the
tool's data are the explicit articulation of that coherence.

---

## Link 3: Convergence produces probabilistic signal

A single note is weak evidence. "I notice something floral" could implicate
dozens of compounds and is easily confounded by expectation, context, and
individual variation. But the tool's signal comes from convergence across multiple
notes pointing at the same compound.

When you report lemon + grapefruit + passionfruit, you are reporting:
- Three independent perceptual observations
- Each grounded in its own receptor-binding event
- Each connecting, in the literature, to overlapping compound sets

Polyfunctional thiols (3-mercaptohexanol, 3-mercaptohexyl acetate) sit at the
intersection of tropical-citrus-grapefruit-passionfruit aroma. Three independent
perceptions triangulating to the same molecular target is a meaningfully different
epistemic situation than one perception alone. The convergence is the signal.

This is why the tool's confidence formula is `0.55 × breadth + 0.45 × strength`
— it deliberately weights *how many notes agree* alongside *how strong the
association is*. The breadth term is the direct operationalization of
triangulation: three notes agreeing hits max breadth score; one note alone does
not.

The probabilistic framing is important: the output is not "compound X is present"
but "given what's published about the aroma pattern you reported, compound X is
among the most likely things accounting for it." That's a legitimate, everyday
form of scientific reasoning — abduction, or inference to the best explanation —
and it remains defeasible. Run the sample through GC-MS and you can check it.

---

## Link 4: The output is a falsifiable shortlist

The chain closes empirically. The tool turns vague perceptual experience into a
**named, testable molecular hypothesis**. Every compound it surfaces is a real
molecule with a real CAS number, a real odor-threshold measurement, and a real
citation connecting it to the aromas you reported.

That's the entire value proposition: not the answer, but a well-reasoned shortlist
that tells you *where to look* — and that a GC-MS instrument could confirm or
overturn in an afternoon.

---

## Why shared vocabulary is the strongest part

The piece most specific to this tool — and most differentiating from, say, asking
an LLM to guess what compounds are in your cup — is the vocabulary encoding step.

An LLM trained on general text will produce plausible-sounding compound names
because compound names appear near flavor words in food science papers. But the
associations are untraceable: you cannot audit why GPT suggests limonene for
lemon. The tool's associations are *explicit graph edges with cited sources*. Every
note→compound link is attributed to a specific paper or dataset. That traceability
is what separates a grounded probabilistic inference from a confident guess.

The vocabulary also constrains the input usefully. Rather than free-form text
(which an LLM can handle but cannot ground), the descriptor vocabulary provides a
shared coordinate system where the tool's linkages are calibrated. Using the
vocabulary is like using a standardized measurement protocol: it reduces
idiosyncratic variation and improves the signal quality of the report.

---

## Relationship to SCOPE-AND-RATIONALE.md

This document focuses on *why the inference works* — the epistemics.
[SCOPE-AND-RATIONALE.md](./SCOPE-AND-RATIONALE.md) covers the broader questions
of what the tool is for, what it isn't, and the honest limits of the claim. Both
are companions to the in-app **Methodology** tab, which gives the operational
math.
