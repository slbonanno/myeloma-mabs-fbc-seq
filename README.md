# myeloma-mabs-fbc-seq

Reanalysis of the FBC-seq whole-cell phage display data from Cyr, Wilson et al., "Concerted antibody and antigen discovery by differential whole-cell phage display selections and multi-omic target deconvolution" (J Mol Biol 2023; [PMC10148915](https://pmc.ncbi.nlm.nih.gov/articles/PMC10148915/)).

## Method in brief

- **Library:** naive chimeric rabbit/human Fab-phage library in the phagemid pC3Csort. Both variable domains (VH and VL) are rabbit; the constant domains (CH1, CL) are human.
- **FBC (Fab-phage biotinylation and capture):** Fab-phage are biotinylated with Sortase A so that phage not displaying a Fab ("bald phage") can be removed after panning, which cuts background in whole-cell selections.
- **Pilot target (ROR1):** ROR1 is a receptor tyrosine kinase overexpressed in several blood and solid cancers. It is not a myeloma marker here. It is a proof-of-concept antigen on HEK293 cells with doxycycline-inducible ROR1 (HEK293-ROR1-TetOn): ROR1-negative (no doxycycline) vs ROR1-positive (doxycycline). Three known anti-ROR1 clones were spiked into the pool at 1 in 1,000,000.
- **Main study (multiple myeloma):** target cell lines H929 and U266 vs healthy donor PBMCs as the non-target control.

## Panning strategy

- Two rounds.
- Round 1 is conventional (non-FBC) panning. Myeloma study: H929 and U266 panned separately, outputs combined and reamplified to make the round 2 phage pool. Pilot: ROR1-negative HEK293 cells.
- Round 2 is FBC panning in triplicate. Myeloma study: H929, U266 and PBMC, 9 replicates. Pilot: ROR1-negative vs ROR1-positive cells, FBC vs conventional, 12 replicates.
- Only round 2 outputs are sequenced. No input library or round 1 sequencing is described.

## Sequencing and analysis in the paper

- Rabbit VH amplified from each replicate output, MiSeq single-end reads.
- HCDR3 amino acid sequences counted per replicate, giving a count matrix.
- DESeq2 differential abundance, target vs non-target, to pick HCDR3s enriched on myeloma cells.

## Data

- GEO: [GSE222897](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE222897) (raw FASTQ and processed files)
- Paper's analysis code: [hedawils/FBCseq](https://github.com/hedawils/FBCseq) (raw reads via SRA PRJNA923794)

## Setup

    python -m pip install -r requirements.txt

Data go in `data/raw/` (not tracked by git). Notebooks are in `notebooks/`.
