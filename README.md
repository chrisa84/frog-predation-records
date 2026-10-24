# Predation on frogs and tadpoles: records from natural-history notes

Species-interaction data for Global Biotic Interactions (GloBI, http://globalbioticinteractions.org). Version 0.2.0.

[![GloBI](https://api.globalbioticinteractions.org/interaction.svg?accordingTo=globi:chrisa84/frog-predation-records)](https://globalbioticinteractions.org/?accordingTo=globi:chrisa84/frog-predation-records)

Configured to be indexed by GloBI as `globi:chrisa84/frog-predation-records`.

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.23458279.svg)](https://doi.org/10.5281/zenodo.23458279)

Each row is one predation or feeding event on a frog, tadpole or frog eggs, reported by the authors of a recent open-access natural-history note (2022-2026) in Reptiles & Amphibians, Revista Latinoamericana de Herpetologia, Phyllomedusa, Herpetozoa or The Herpetological Bulletin. Each row records who ate whom, where, when, and cites the paper by DOI.

Licence: [CC BY 4.0](LICENSE). The dataset contains facts and citations only. No text from the papers is copied.

Citation: Ashley, C. 2026. Predation on frogs and tadpoles: interaction records extracted from open-access natural-history notes, 2022-2026. Version 0.2.0. https://doi.org/10.5281/zenodo.23458279

## What is in it
- 97 interactions from 72 notes: 36 `preysOn`, 61 `eats`. Source taxon = predator, target taxon = prey.
- 71 rows are species on both sides. 18 rows have a predator only to genus or family (mostly spiders) and 9 have a prey only to genus or order (1 have both).
- 92 rows have coordinates as given in the paper. 96 have an observation date. Local times are in `row_provenance.tsv`, not in `interactions.tsv`.
- 12 rows have frog eggs as the prey and 2 have tadpoles (see the life stage columns). Rows where a tadpole or frog is the predator are marked in the predator life stage column.
- 53 rows are high confidence and 44 medium (see `row_provenance.tsv`).

"New" in this project's notes means **new to GloBI, not new to science**. When checked (18 Oct 2026 for the first 46 rows, 24 Oct 2026 for the other 51), 80 of the 97 pairs were not in GloBI under any name variant, 16 were already there and 1 was uncertain (other species of the same genus were recorded). The rows that GloBI already has are kept because they add a dated, cited source.

## Files
- `interactions.tsv`: the data, in the GloBI template columns.
- `globi.json`: dataset descriptor.
- `row_provenance.tsv`: per row (line number counts the header as line 1): page or figure, outcome, local time, observer interference, confidence, notes, GloBI duplicate check.
- `names_audit.tsv`: the name in the paper next to the name used here, the sources checked and whether the frog name was checked in Amphibian Species of the World (ASW).
- `LICENSE`: CC BY 4.0. `.zenodo.json`: metadata for the Zenodo release.

## Rules
- `preysOn` only when the authors saw the capture or kill, or the prey was clearly alive when first seen. Otherwise `eats`: found already eating, prey state not stated, stomach or regurgitated contents, eating eggs, or scavenging a dead animal.
- Wild animals only. Where observers moved, collected or disturbed animals during the event, `row_provenance.tsv` says so (17 rows).
- Left out: attacks the frog escaped, events cut short by observers with unknown outcome, attacks the authors themselves call attempts, observations a paper only cites from other papers, captive or laboratory animals, parasitic blood feeding, and aggregate diet statements with no dated event.
- One row per predator taxon, prey taxon and event. When several individuals of the same predator taxon fed on the same prey taxon in one event (for example several capuchins eating one egg mass), they are one row and the number is in `row_provenance.tsv`.
- Names: names are kept as written in the paper unless the paper itself or the databases show a plain misspelling or the paper gives its own current name. Frogs follow Amphibian Species of the World (ASW) where it could be checked. Seven names (18 Oct 2026) were checked in ASW itself; on 24 Oct 2026 ASW could not be reached, so frog names where GBIF and the Catalogue of Life disagreed were left unchecked and are marked in `names_audit.tsv`. Predators follow GBIF and the Catalogue of Life (Reptile Database for reptiles). A predator or prey identified only to genus stays at genus, and "cf.", "aff." and "probably" identifications are lowered to genus.
- Every record cites a DOI. If later versions need a paper without a DOI (for example in Herpetology Notes), a URL reference will be used for that row only, and this README will say so.

## How records were checked
1. One reader extracted the rows from each paper.
2. A second, separate pass, which saw only the papers and the extracted rows, re-checked every field of every row and read each paper for missed events. This was done separately for each of the two sets of rows.
3. Each pair was searched in the GloBI API under every name variant (as written, accepted names, synonyms).
4. GloBI's checker (Elton 0.17.2) was run on this folder: 97 interactions, no warnings.

**Second-pass result, first 46 rows (v0.1.0):** 884 field checks over 52 extracted rows, 20 disagreements (2.3%). None of the 520 hard-fact fields (names as written, life stage, locality, coordinates, date, page or figure) was wrong. 18 of 52 extracted rows had at least one disagreement, nearly all about how an event was coded (observer interference, `preysOn` versus `eats`). All were fixed, and 6 rows were dropped, before release.

**Second-pass result, the other 51 rows (v0.2.0):** 936 field checks over 52 extracted rows, 15 disagreements (1.6%), including accepted-name checks. 6 of the 520 hard-fact fields differed: page pointers, life stages and one locality wording; none was a name as written, a coordinate or a date. 11 of 52 extracted rows had at least one disagreement. 1 row was dropped and 2 changed from `preysOn` to `eats`. The reviewer also asked for several group rows to be split into one row per animal; they were not split, because a row is one predator taxon eating one prey taxon in one event.

## Things to know about the sources
Contradictions inside the papers, flagged rather than resolved:
- 10.17161/randa.v33i1.23621: figure panel letters for two of the six spider events disagree between text and caption (both rows kept, noted). A third event (a toad said both to be killed and to be alive) was dropped.
- 10.22201/fc.25942158e.2025.4.1472: elevation is 1865 m in the text and 865 m in a figure caption. Altitude is not in the data.
- 10.22201/fc.25942158e.2025.3.1255: one event is timed 01:17 but described as daytime. Time is left out of the row.
- 10.17161/randa.v30i1.18531: the snake is said to occur only in south-west Costa Rica, but the record is from the north of the country.
- 10.17161/randa.v30i1.20759 and 10.22201/fc.25942158e.2025.3.1369: the event was cut short by the observers, and in one the caption contradicts the text. No rows are included.
- 10.22201/fc.25942158e.2025.2.1172: the figure caption describes a different animal and place (it looks copied from another note). The row rests on the text only.
- 10.22201/fc.25942158e.2023.4.810: the text names the frog *Craugastor rhodopis* but the figure caption says *C. loki*. The text name is used.
- 10.22201/fc.25942158e.2024.4.1023: two figure captions name *Leptodeira ornata* where the text says *L. ashmeadii*. The text is followed.
- 10.22201/fc.25942158e.2023.2.632: the time is printed as 24:13 h, so the date may be one day later.
- 10.22201/fc.25942158e.2023.4.629: figure numbers in the text and captions are swapped.
- 10.22201/fc.25942158e.2022.1.381: figure captions call the captures "attempts" but the text says the snake fed successfully (row kept).
- 10.22201/fc.25942158e.2023.3.665: one tadpole is said to be preserved and also to have grown up in captivity.
- 10.17161/randa.v31i1.20040 (a diving beetle on a gray treefrog) is not included: the figure caption says "predation attempt" and the frog's fate is not given.

Name questions (the paper's name is kept unless noted):
- 10.17161/randa.v30i1.20275: the Reptile Database restricts *Dendrelaphis pictus* to Southeast Asia east of Myanmar; Bangladeshi snakes may be *D. proarchos*.
- 10.22201/fc.25942158e.2022.4.551: the prey of one row was identified from a partly digested frog in a decomposed snake, and one spider is "cf.".
- 10.17161/randa.v32i1.24117, 10.22201/fc.25942158e.2025.4.1472, 10.22201/fc.25942158e.2023.4.810, 10.22201/fc.25942158e.2025.1.1139 and several others: prey identified from partly digested or regurgitated material.
- 10.3897/herpetozoa.39.e176733: crab identification tentative; scavenging cannot be excluded.
- *Megophrys* sp. in one paper is entered as *Xenophrys* (the genus used for Himalayan horned frogs in the current literature and in other notes cited here; not checked in ASW directly). *Lysapsus limellum* is entered as *Pseudis limellum* (ASW).
- The paper writes *Cophipora brevirostris*; entered as *Copiphora brevirostris* (its own table and the databases use this spelling). One paper writes *Rana sphenocephala* and *Bufo houstonensis* and states the current names itself; they are entered as *Lithobates sphenocephalus* and *Anaxyrus houstonensis*.
- Frog names not checked against ASW because the site was unreachable and GBIF and the Catalogue of Life disagree or GBIF lacks the species (7 names): *Amerana draytonii*, *Bufo houstonensis* (entered as *Anaxyrus houstonensis*), *Hyalinobatrachium viridissimum*, *Megophrys sp.* (entered as *Xenophrys*), *Pelophylax cerigensis*, *Rana sphenocephala* (entered as *Lithobates sphenocephalus*), *Trachycephalus vermiculatus*.
- One row has the prey only as "Anura" (an unidentified road-killed frog) and one has the predator only as "Lycosidae" (wolf spider).

Records are only as good as the original notes. Corrections are welcome via an issue on this repository.

## Version history
- 0.2.0: 51 rows from 36 further notes added (97 in total), including frog eggs and tadpoles as prey.
- 0.1.1: Zenodo DOI added to the citation and README.
- 0.1.0: first release, 46 rows from 36 notes.
