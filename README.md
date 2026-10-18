# Predation on frogs and tadpoles: records from natural-history notes

Species-interaction data for [Global Biotic Interactions](http://globalbioticinteractions.org) (GloBI). Version 0.1.0.

Each row is one predation or feeding event on a frog or tadpole, reported by the authors of a recent open-access natural-history note (2022-2026) in Reptiles & Amphibians, Revista Latinoamericana de Herpetologia, Phyllomedusa, Herpetozoa or The Herpetological Bulletin. Each row records who ate whom, where, when, and cites the paper by DOI.

Licence: [CC BY 4.0](LICENSE). The dataset contains facts and citations only. No text from the papers is copied.

Citation: Ashley, C. 2026. Predation on frogs and tadpoles: interaction records extracted from open-access natural-history notes, 2022-2026. Version 0.1.0.

## What is in it
- 46 interactions from 36 notes: 22 `preysOn`, 24 `eats`. Source taxon = predator, target taxon = prey.
- 28 rows are species on both sides. 15 rows have a predator only to genus (mostly spiders) and 3 have a prey only to genus.
- 43 rows have coordinates as given in the paper. All have an observation date. Local times are in `row_provenance.tsv`, not in `interactions.tsv`.
- 31 rows are high confidence and 15 medium (see `row_provenance.tsv`).

"New" in this project's notes means **new to GloBI, not new to science**. When checked on 18 Oct 2026, 41 of the 46 pairs were not in GloBI under any name variant, 4 were already there and 1 was uncertain (other species of the same genus were recorded). The rows that GloBI already has are kept because they add a dated, cited source.

## Files
- `interactions.tsv`: the data, in the GloBI template columns.
- `globi.json`: dataset descriptor.
- `row_provenance.tsv`: per row (line number counts the header as line 1): page or figure, outcome, local time, observer interference, confidence, notes, GloBI duplicate check.
- `names_audit.tsv`: the name in the paper next to the name used here and the sources checked.
- `LICENSE`: CC BY 4.0. `.zenodo.json`: metadata for the Zenodo release.

## Rules
- `preysOn` only when the authors saw the capture or kill, or the prey was clearly alive when first seen. Otherwise `eats`: found already eating, prey state not stated, stomach or regurgitated contents, or scavenging not excluded.
- Wild animals only. Where observers moved, collected or disturbed animals during the event, `row_provenance.tsv` says so (5 rows).
- Left out: attacks the frog escaped, events cut short by observers with unknown outcome, attacks the authors themselves call attempts, observations a paper only cites from other papers, captive animals.
- Names: frogs follow Amphibian Species of the World (ASW). Seven names where GBIF and the Catalogue of Life disagreed were checked in ASW itself; the other frog names were checked against GBIF and the Catalogue of Life only. Predators follow GBIF and the Catalogue of Life (Reptile Database for reptiles). A predator or prey identified only to genus stays at genus, and "cf." identifications are lowered to genus.
- Every record cites a DOI. If later versions need a paper without a DOI (for example in Herpetology Notes), a URL reference will be used for that row only, and this README will say so.

## How records were checked
1. One reader extracted the rows from each paper.
2. A second, separate pass, which saw only the papers and the extracted rows, re-checked every field of every row and read each paper for missed events.
3. Each pair was searched in the GloBI API under every name variant (as written, accepted names, synonyms).
4. GloBI's checker (Elton 0.17.2) was run on this folder: 46 interactions, no warnings.

**Second-pass result:** 884 field checks, 20 disagreements (2.3%). None of the 520 hard-fact fields (names as written, life stage, locality, coordinates, date, page or figure) was wrong. 18 of 52 first-pass rows had at least one disagreement, nearly all about how an event was coded (observer interference, `preysOn` versus `eats`). All were fixed, and 6 rows were dropped, before this release. The first pass extracted 52 rows; 46 are published here.

## Things to know about the sources
Contradictions inside the papers, flagged rather than resolved:
- 10.17161/randa.v33i1.23621: figure panel letters for two of the six spider events disagree between text and caption (both rows kept, noted). A third event (a toad said both to be killed and to be alive) was dropped.
- 10.22201/fc.25942158e.2025.4.1472: elevation is 1865 m in the text and 865 m in a figure caption. Altitude is not in the data.
- 10.22201/fc.25942158e.2025.3.1255: one event is timed 01:17 but described as daytime. Time is left out of the row.
- 10.17161/randa.v30i1.18531: the snake is said to occur only in south-west Costa Rica, but the record is from the north of the country.
- 10.17161/randa.v30i1.20759 and 10.22201/fc.25942158e.2025.3.1369: the event was cut short by the observers, and in one the caption contradicts the text. No rows are included.

Name questions (the paper's name is kept):
- 10.17161/randa.v30i1.20275: the Reptile Database restricts *Dendrelaphis pictus* to Southeast Asia east of Myanmar; Bangladeshi snakes may be *D. proarchos*.
- 10.22201/fc.25942158e.2022.4.551: the prey of one row was identified from a partly digested frog in a decomposed snake, and one spider is "cf.".
- 10.17161/randa.v32i1.24117 and 10.22201/fc.25942158e.2025.4.1472: prey identified from partly digested or regurgitated material.
- 10.3897/herpetozoa.39.e176733: crab identification tentative; scavenging cannot be excluded.
- *Megophrys* sp. in one paper is entered as *Xenophrys* (ASW treats Himalayan horned frogs as *Xenophrys*). *Lysapsus limellum* is entered as *Pseudis limellum* (ASW).

Records are only as good as the original notes. Corrections are welcome via an issue on this repository.
