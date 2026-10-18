# Frog and tadpole predation records from natural-history notes (pilot, draft)

DRAFT. Not published, not registered. Data for [Global Biotic Interactions](http://globalbioticinteractions.org) (GloBI).

Each row is one predation or feeding event on a frog or tadpole, reported by the authors of a recent open-access natural-history note (2022-2026) in Reptiles & Amphibians, Revista Latinoamericana de Herpetologia, Phyllomedusa, Herpetozoa or The Herpetological Bulletin. Only the facts are recorded (who ate whom, where, when, which paper and page). No text from the papers is copied. Each row cites the paper by DOI.

## Files
- `interactions.tsv`: the data, in the GloBI template columns. Source = predator, target = prey.
- `globi.json`: dataset descriptor (citation, licence, version). Author name and licence are placeholders to confirm.
- `row_provenance.tsv`: for each line of `interactions.tsv` (line number counts the header as line 1): page or figure, outcome, local time, whether observers interfered, confidence, and what the GloBI duplicate check found.
- `names_audit.tsv`: the name in the paper next to the name used here, with the sources checked.

## Rules used
- `preysOn` only when the authors saw the capture or kill, or the prey was clearly alive when first seen. Otherwise `eats` (found already eating, prey state not stated, stomach or regurgitated contents, scavenging not excluded).
- Wild animals only. Where observers moved, collected or disturbed animals during the event this is noted in `row_provenance.tsv`.
- Left out: attacks the frog escaped, events cut short by observers with unknown outcome, observations the paper only cites from other papers, captive animals.
- Names follow Amphibian Species of the World for frogs and GBIF / Catalogue of Life (Reptile Database for reptiles) for predators. Identifications to genus only are kept at genus. Where the paper says "cf." the row is kept at genus.
- Times are local and not in `interactions.tsv`, only in `row_provenance.tsv`.

## How it was made
Rows were extracted by hand-reading each paper, then every row was re-checked against the paper by a second, independent pass. Disagreements and decisions are in the parent project's `data/disagreements.csv`.

Records are only as good as the original notes. Corrections welcome via an issue on this repository.
