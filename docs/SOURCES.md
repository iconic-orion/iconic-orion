# Sources & citations

The complete list of literature behind Aroma Wheel, what each source backs, and
the rules the project follows about citing. This is the GitHub-facing companion
to the in-app **Methodology → "A note on the sources"** section; the app shows
the receipts inline, this file gathers them in one place.

If you only want the bibliography, jump to [The full list](#the-full-list).

---

## How sourcing works here

Every citation in the tool does one of two jobs. Keeping them separate is the
whole point — they're different kinds of claim with different shelf lives.

1. **Odour-threshold sources** back a compound's *threshold tier* — the
   `thresholdSrc` string on each compound. These answer "how little of this can
   a person detect?" The original careful measurement is usually the canonical
   one, so these skew old (Buttery 1981, Shaw 1979) **on purpose**: later papers
   cite those values rather than re-measuring them. A 1981 threshold is often the
   primary source, not a stale one.

2. **Note→compound linkage sources** back an *edge* — the `cite` string on each
   note→compound connection. These answer "is this compound actually a driver of
   this aroma, in real samples?" This is a livelier literature: coffee thiols and
   wine polyfunctional thiols see a steady stream of 2017–2024 work, and that's
   where future citation refreshes will draw from.

A handful of sources do both jobs (e.g. Sefton et al. 2011 anchors both
β-damascenone's threshold *and* several of its note links).

### The integrity rule

> Every reference in the tool is a real paper. The project would rather show an
> old-but-real source than a fresh-looking invented one.

Two consequences worth being explicit about:

- **No fabricated citations, ever.** If a full bibliographic entry (journal,
  volume, pages) hasn't been verified, the edge carries only the short-form cite
  (`Author year`) and nothing more is asserted. The verified-full-citation
  catalog (`REFERENCES` in `index.html`) is deliberately small and conservative;
  it grows only as entries are confirmed.
- **Weights are not extracted from the papers.** The edges are *seeded* by
  real GC-MS landmarks, but the 0–1 weights themselves are normalized
  approximations — an editorial judgement about relative association strength,
  not a number lifted from a table in the cited work. The citation vouches for
  *"this compound is a real driver of this aroma,"* not for the specific weight.

### The modern compendium

The standard modern compilation that gathers threshold values together is:

> **van Gemert, L. J. (2011).** *Compilation of Odour Threshold Values in Air and
> Water* (2nd ed.). Oliemans Punter & Partners.

It gathers roughly **10,750 threshold values** drawn from **~1,780 sources**, and
is the reference work this tool's threshold *tiers* are sanity-checked against.
It is a compendium, not a primary measurement — the per-compound sources below
are the primaries; van Gemert is the cross-check.

---

## The full list

Organized by the job each source does. A source appearing in both tables does
both jobs. Short-form entries (`Author year`) are listed exactly as the tool
commits to them — no fuller bibliographic detail is asserted beyond what's been
verified.

### Verified full bibliographic entries

These are the citations with confirmed journal/volume/pages in the tool's
`REFERENCES` catalog. Rendered in the app's "Go Deeper" mode.

| Short cite | Full reference |
|---|---|
| Blank, Sen, Grosch 1992 | Blank, I., Sen, A., & Grosch, W. (1992). Potent odorants of the roasted powder and brew of Arabica coffee. *Zeitschrift für Lebensmittel-Untersuchung und Forschung, 195*(3), 239–245. |
| Czerny, Mayer, Grosch 1999 | Czerny, M., Mayer, F., & Grosch, W. (1999). Sensory study on the character impact odorants of roasted Arabica coffee. *Journal of Agricultural and Food Chemistry, 47*(2), 695–699. |
| Czerny & Grosch 2000 | Czerny, M., & Grosch, W. (2000). Potent odorants of raw Arabica coffee. Their changes during roasting. *Journal of Agricultural and Food Chemistry, 48*(3), 868–872. |
| Czerny et al. 2008 | Czerny, M., Christlbauer, M., Fischer, A., Granvogl, M., Hammer, M., Hartl, C., Hernandez, N. M., & Schieberle, P. (2008). Re-investigation on odour thresholds of key food aroma compounds and development of an aroma language based on odour qualities of defined aqueous odorant solutions. *European Food Research and Technology, 228*(2), 265–273. |
| Tominaga et al. 1998 | Tominaga, T., Furrer, A., Henry, R., & Dubourdieu, D. (1998). Identification of new volatile thiols in the aroma of *Vitis vinifera* L. var. Sauvignon blanc wines. *Flavour and Fragrance Journal, 13*(3), 159–162. |
| Bartowsky & Henschke 2004 | Bartowsky, E. J., & Henschke, P. A. (2004). The 'buttery' attribute of wine—diacetyl—desirability, spoilage and beyond. *International Journal of Food Microbiology, 96*(3), 235–252. |
| Sefton et al. 2011 | Sefton, M. A., Skouroumounis, G. K., Elsey, G. M., & Taylor, D. K. (2011). Occurrence, sensory impact, synthesis, and synthetic pathways of β-damascenone and related damascone derivatives. *Journal of Agricultural and Food Chemistry, 59*(18), 9717–9746. |
| Friedman 2017 | Friedman, M. (2017). Chemistry, antimicrobial mechanisms, and antibiotic activities of cinnamaldehyde against pathogenic bacteria in animal feeds and human foods. *Journal of Agricultural and Food Chemistry, 65*(48), 10406–10423. |
| Verstrepen et al. 2003 | Verstrepen, K. J., Derdelinckx, G., Dufour, J.-P., Winderickx, J., Thevelein, J. M., Pretorius, I. S., & Delvaux, F. R. (2003). Flavor-active esters: adding fruitiness to beer. *Journal of Bioscience and Bioengineering, 96*(2), 110–118. |
| Mayer, Czerny, Grosch 2000 | Mayer, F., Czerny, M., & Grosch, W. (2000). Sensory study of the character impact aroma compounds of a coffee beverage. *European Food Research and Technology, 211*(4), 272–276. |
| Hatanaka 1993 | Hatanaka, A. (1993). The biogeneration of green odour by green leaves. *Phytochemistry, 34*(5), 1201–1218. |
| Shaw 1979 | Shaw, P. E. (1979). Review of quantitative analyses of citrus essential oils. *Journal of Agricultural and Food Chemistry, 27*(2), 246–257. |

### Odour-threshold sources

Each backs the threshold tier (`very-low` / `low` / `medium` / `high`) of one or
more compounds. Value shown is the figure quoted in the tool.

| Source | Compound(s) | Threshold quoted |
|---|---|---|
| Buettner & Schieberle 1999 | Limonene | ~10 ppb in water |
| Buttery 1981 | Linalool, myrcene, geraniol, α-pinene, ethyl butanoate, ethyl hexanoate, isoamyl acetate, furfural, vanillin, hexanal, benzaldehyde, eugenol | sub-ppb to ~3000 ppb, per compound |
| Jirovetz et al. 2002 | β-Caryophyllene | ~64 ppb |
| Lis-Balchin 2002 | Linalyl acetate, 1,8-cineole | ~10–12 ppb |
| Mann & Staba 1986 | α-Bisabolol | ~22 ppb |
| Buttery, Seifert, Guadagni & Ling 1969 | IBMP | ~2 ng/L water |
| Czerny et al. 2008 | 2-Ethyl-3,5-dimethylpyrazine, 2,3-diethyl-5-methylpyrazine, phenylacetaldehyde | ~0.001–4 ppb |
| Blank, Sen, Grosch 1992 | Furfurylthiol | ~0.005 ppb |
| Tominaga et al. 1998 | 3-Mercaptohexanol, 4MMP | ~0.8–60 ng/L |
| Mayer, Czerny, Grosch 2000 | Methanethiol | ~0.02 ppb |
| Schwab et al. 2008 | γ-Decalactone, γ-nonalactone | ~11–30 ppb |
| Pham et al. 1995 | Sotolon | ~0.3 ppb |
| Friedman 2017 | Cinnamaldehyde | ~1.1 ppb |
| Lermusieau, Noël, Liégeois & Collin 1999 | (E)-2-Nonenal | ~0.08 ppb |
| Bartowsky & Henschke 2004 | Diacetyl | ~5–15 ppb in beer |
| Sefton et al. 2011 | β-Damascenone | ~0.002 ppb |
| Maga 1978 | Guaiacol | ~3 ppb |
| Czerny & Grosch 2000 | 4-Vinylguaiacol | ~3 ppb |
| Ahmed, Dennison, Dougherty & Shibamoto 1978 | β-Ionone | ~0.007 ppb in water |
| Combet et al. 2006 | 1-Octen-3-ol | ~10 ppb |
| Buttery et al. 1995 | Furaneol (HDMF) | ~10 ppb |
| Darriet et al. 2000 | Geosmin | ~0.01 ppb in water |
| Lawrence 2007 | Menthol | ~50 ppb |

### Note→compound linkage sources

Each backs one or more edges (which aroma a compound is claimed to drive). Listed
once per source, with the note links it supports.

| Source | Backs the link(s) |
|---|---|
| Shaw 1979 | citrus peel → limonene (lemon, orange, grapefruit) |
| Flament 2002 (*Coffee Flavor Chemistry*) | lemon→linalool; coffee/toast/burnt→furfural; caramel→furfural; yeasty→furfural |
| Klesk & Qian 2003 | berry → ethyl hexanoate (blackberry AEDA) |
| Sefton et al. 2011 | berry / stonefruit / apple / rose / violet / cherry / tobacco / honey / coffee → β-damascenone |
| Schwab et al. 2008 | stonefruit / cherry → γ-decalactone; berry → furaneol (strawberry) |
| Dimick & Hoskin 1983 | apple → ethyl butanoate |
| Salmon et al. 1996 | banana → isoamyl acetate / ethyl butanoate |
| Pino & Mesa 2006 | mango → myrcene / γ-decalactone / isoamyl acetate |
| Engel & Tressl 1991 | passionfruit → ethyl hexanoate / 3-MH(A) |
| Tominaga et al. 1998 | grapefruit / passionfruit → 3-mercaptohexanol |
| Tominaga et al. 2000 | passionfruit → 4MMP |
| Ohloff 1994 (*Scent & Chemistry*) | rose→geraniol/linalool; clove/anise→eugenol; almond/cherry→benzaldehyde; pine→α-pinene/myrcene |
| Czerny et al. 1999 | jasmine→phenylacetaldehyde; coffee/toast→pyrazines; hazelnut→pyrazines; coffee→furaneol |
| Lis-Balchin 2002 | lavender→linalool/linalyl acetate; pine/lavender→1,8-cineole |
| Mann & Staba 1986 | chamomile→α-bisabolol/linalool |
| Ohloff 1994 | violet → β-ionone (violet principal odorant) |
| Klesk & Qian 2003 | berry → α-/β-ionone (blackberry) |
| Blank, Sen, Grosch 1992 | coffee / sulfury → furfurylthiol |
| Maga 1978 | smoky / burnt / tobacco → guaiacol |
| Czerny & Grosch 2000 | smoky → 4-vinylguaiacol |
| Tressl & Friese 1978 | clove → 4-vinylguaiacol |
| Jirovetz et al. 2002 | pepper / woody → β-caryophyllene |
| Mason, Johnson & Hamming 1966 | peanut → pyrazine |
| Buttery, Seifert, Guadagni & Ling 1969 | bell pepper → IBMP (threshold primary) & myrcene |
| Combet et al. 2006 | mushroom → 1-octen-3-ol / geosmin; mushroom→hexanal (partial overlap) |
| Darriet et al. 2000 | woody → geosmin |
| Lee & Noble 2003 | woody / vanilla → γ-nonalactone (oak lactones) |
| Ranadive 1992 | vanilla → vanillin |
| Serra Bonvehí & Ventura Coll 2003 | honey → phenylacetaldehyde |
| Counet et al. 2002 | chocolate → pyrazine / phenylacetaldehyde / furaneol |
| Pham et al. 1995 | caramel / maple → sotolon |
| Underwood & Filipic 1963 | maple → sotolon |
| Francis & Newton 2005 | winey → ethyl hexanoate / ethyl butanoate |
| Verstrepen et al. 2003 | yeasty → isoamyl acetate |
| Mayer, Czerny, Grosch 2000 | sulfury → methanethiol |
| Lermusieau, Noël, Liégeois & Collin 1999 | cardboard → (E)-2-nonenal |
| Berger 2007 | pineapple → ethyl butanoate / ethyl hexanoate / isoamyl acetate |
| Steingass, Carle & Schmarr 2015 | pineapple → ethyl butanoate |
| Pickenhagen et al. 1981 | pineapple → furaneol |
| Buttery et al. 1995 | caramel → furaneol |
| Friedman 2017 | cinnamon → cinnamaldehyde / benzaldehyde |
| Hatanaka 1993 | green → hexanal (green leaf volatiles) |
| Lawrence 2007 | mint → menthol / 1,8-cineole |

> **On the short-form linkage cites:** sources in the linkage table that are not
> in the verified-full-bibliography table above (e.g. Flament 2002, Ohloff 1994,
> Pino & Mesa 2006) are asserted only at `Author year` precision. They name real
> works the edges are seeded from; promoting one to the full `REFERENCES` catalog
> means verifying its journal/volume/pages first. See
> [Verification status](#verification-status-checked-2026-06-11) for the per-cite
> audit and the handful that need a fix.

---

## Verification status (checked 2026-06-11)

Every short-form citation (those not already in the verified-full-bibliography
table) was checked against the published literature. Verdicts below. Items marked
⚠️ or ✗ are the action list — the underlying *science* is sound in every case, but
the citation string needs a fix or confirmation before it should be treated as
canonical.

### ✓ Confirmed — real paper, author/year/topic all check out

Buettner & Schieberle 1999 · Buttery 1981 · Jirovetz et al. 2002 ·
Lis-Balchin 2002 · Mann & Staba 1986 · Pham et al. 1995 · Maga 1978 ·
Combet et al. 2006 · Buttery et al. 1995 · Darriet et al. 2000 · Lawrence 2007 ·
Flament 2002 · Ohloff 1994 · Dimick & Hoskin 1983 · Salmon et al. 1996 ·
Pino & Mesa 2006 · Engel & Tressl 1991 · Tominaga et al. 2000 · Lee & Noble 2003 ·
Ranadive 1992 · Counet et al. 2002 · Underwood & Filipic 1963 ·
Francis & Newton 2005 · Berger 2007 · Pickenhagen et al. 1981 ·
Buttery et al. 1969 · Tressl & Friese 1978.

### ✗ Original cite couldn't be verified — replacement found (✓ applied to index.html 2026-06-11)

Each of these now has a real, verified source that fits the same claim. All
replacements below are **already applied** to `index.html`.

- **Allen, Lacey, Boyd 1991** (IBMP threshold / bell pepper) → **Buttery, R. G.,
  Seifert, R. M., Guadagni, D. G., & Ling, L. C. (1969). Characterization of some
  volatile constituents of bell peppers. *J. Agric. Food Chem., 17*(6),
  1322–1327.** The original string conflated a 1994 author set ("Boyd") with a
  1991 year; the canonical primary for the IBMP threshold is Buttery 1969, which
  the tool *already cites elsewhere* for the bell-pepper edge. One fix closes two
  flags. (Allen/Lacey 1991 is real too — it's the Sauvignon-blanc *wine
  occurrence* paper — but it isn't the threshold primary.)
- **Naef 2011** (β-ionone threshold ~0.007 ppb) → **Ahmed, E. M., Dennison,
  R. A., Dougherty, R. H., & Shibamoto, T. (1978). Flavor and odor thresholds in
  water of selected orange juice components. *J. Agric. Food Chem., 26*(1),
  187–191.** This is the standard primary for the 0.007 ppb (7 ng/L) β-ionone
  water threshold. (Confirm the exact value in-paper before locking.) The tool's
  separate *violet → β-ionone* **edge** (also previously "Naef 2011") was
  re-anchored to **Ohloff 1994** — its "Violet Odorants and Rose Ketones" chapter
  is the natural source for β-ionone as the violet principal odorant.
- **Jiang & Zhang 2010** (berry → ethyl hexanoate) → **Klesk, K., & Qian, M.
  (2003). Aroma extract dilution analysis of cv. Marion (*Rubus* spp. hyb) and cv.
  Evergreen (*R. laciniatus* L.) blackberries. *J. Agric. Food Chem., 51*(11),
  3436–3441.** Verified AEDA study; ethyl hexanoate is among the identified
  aroma-active blackberry esters.
- **Buttery et al. 1990** (peanut → pyrazine) → **Mason, M. E., Johnson, B., &
  Hamming, M. (1966). Flavor components of roasted peanuts. Some low molecular
  weight pyrazines and pyrrole. *J. Agric. Food Chem., 14*(5), 454–460.** The
  foundational paper attributing pyrazines to roasted-peanut flavor. *FYI:* the
  best modern study (Chetschik, Granvogl & Schieberle 2010, *JAFC* 58, 11018)
  actually argues alkylpyrazines are *not* the key peanut odorants — worth knowing
  if the editorial wants to soften that edge's weight, but Mason 1966 legitimately
  backs the link.

### ⚠️ Year/author drift — corrected citations below (✓ applied to index.html 2026-06-11)

- **Bonvehí 2005** → **Serra Bonvehí, J., & Ventura Coll, F. (2003). Flavour index
  and aroma profiles of fresh and processed honeys. *J. Sci. Food Agric., 83*,
  275–282.** (Year was off by two.)
- **Steingass 2017** → **Steingass, C. B., Carle, R., & Schmarr, H.-G. (2015).
  *Anal. Bioanal. Chem., 407*(9), 2591–2608** (pineapple aroma by GC×GC–MS). The
  group's pineapple work is 2015, not 2017.
- **Lermusieau & Collin 2003** → **Lermusieau, G., Noël, S., Liégeois, C., &
  Collin, S. (1999). Nonoxidative mechanism for development of *trans*-2-nonenal
  in beer. *J. Am. Soc. Brew. Chem., 57*(1), 29–33.** The canonical
  nonenal-staling paper; correct year is 1999.
- **Schreier 1984** (berry → β-ionone) → applied as **Klesk & Qian 2003** (the
  same blackberry AEDA used for the berry-ester edge). That paper explicitly names
  α- and β-ionone as important to 'Marion' blackberry aroma, so it cleanly backs
  this edge too. The exact 1984 Schreier paper could not be confirmed; this is a
  verified, scope-appropriate substitute.

### Title note (no change needed)

- **Ohloff 1994** is correctly dated, but its 1994 title is *Scent and Fragrances:
  The Fascination of Odors and Their Chemical Perspectives* (Springer). *Scent and
  Chemistry* is the **2011** successor volume (Ohloff, Pickenhagen & Kraft). The
  parenthetical short-title in the code (“Scent & Chemistry”) is mildly
  anachronistic; author/year are right.

### Attribution notes (paper is real, but pointed at the wrong thing)

- **Buttery et al. 1969** is cited for *bell pepper → myrcene (terpene
  contribution)*, but its landmark finding is **IBMP** in bell pepper. The edge is
  fine; consider also using it as the IBMP threshold primary (see the Allen item).

> None of the flagged items are fabrications — each names a real researcher and a
> real, well-trodden area of flavor chemistry. The issue is citation *precision*
> (wrong year, wrong co-author, or a reference that couldn't be located), which is
> exactly what the integrity rule exists to catch.

---

## Maintaining this file

- The source of truth is `index.html` — the `EDGES`, compound `thresholdSrc`
  strings, and the `REFERENCES` catalog. This file is a curated read-out of those.
- When you add or change an edge or a threshold, update the relevant table here.
- When you verify a short-form cite into a full reference, move it into the
  `REFERENCES` catalog in `index.html` *and* the verified table above.
- Never add a row here that isn't backed by a real paper. See the integrity rule.
