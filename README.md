# Extended GitHub repository description

## Suggested repository name

`oral-microbiome-16S-workflows`

Alternative names:

- `microbiome-16S-ont-emu-workflows`
- `oral-gut-microbiome-methods`
- `perio-microbiome-workflows`
- `16S-microbiome-analysis-workflows`

---

## Short description

Reproducible workflows for 16S rRNA microbiome analysis, including Oxford Nanopore long-read preprocessing, EMU taxonomic classification with prebuilt or custom databases, diversity estimation, differential abundance analysis, and microbial network analysis in R.

---

## Extended description

This repository contains practical, modular workflows for the analysis of 16S rRNA microbiome sequencing data, with emphasis on oral and gut microbiome applications. The materials are organized as Markdown-based methodological notes and example pipelines covering the main steps from long-read preprocessing to downstream ecological and statistical analyses in R.

The repository includes documentation for Oxford Nanopore 16S long-read data preprocessing, including adapter/barcode trimming, locus-specific primer trimming, quality and length filtering, chimera removal, and quality-control summaries. It also includes EMU-based taxonomic classification workflows for both long-read and short-read 16S datasets, including the use of prebuilt databases such as SILVA and the construction of custom EMU-compatible databases, for example using eHOMD.

Downstream analysis examples focus on how to use EMU outputs in R, generate `phyloseq`-ready objects, estimate alpha and beta diversity with packages such as `breakaway` and `DivNet`, perform differential abundance analysis with `radEmu`, and construct microbial association networks using compositionally aware approaches such as SPIEC-EASI and NetCoMi. The examples are intended to be adaptable to paired designs, such as pre/post periodontal treatment studies, and to unpaired designs, such as comparisons between clinical or exposure groups.

The repository is not intended to be a fully automated black-box pipeline. Instead, it provides transparent, editable templates that document analytical decisions and can be adapted to different projects, sequencing platforms, taxonomic databases, and study designs. Particular attention is given to common microbiome-specific issues, including compositionality, sparsity, zero inflation, rare taxa, paired sampling structures, and the distinction between taxonomic classification, ecological association, and statistical inference.

---

## Intended use

These workflows are intended for researchers working with 16S rRNA microbiome data who need reproducible notes and adaptable code templates for:

- Oxford Nanopore long-read 16S preprocessing.
- Short-read or long-read taxonomic classification with EMU.
- Use of prebuilt and custom EMU databases.
- Integration of EMU outputs into R.
- Creation of `phyloseq` objects.
- Alpha diversity and richness estimation.
- Beta diversity estimation and comparison.
- Differential abundance analysis.
- Microbial association network construction and comparison.

The examples are especially relevant for oral microbiome, gut microbiome, oral-gut axis, periodontitis, and antimicrobial resistance-oriented microbiome projects, but the general structure can be adapted to other microbiome studies.

---

## Repository contents

Suggested structure:

```text
.
├── README.md
├── 01_long_read_16S_preprocessing.md
├── 02_emu_installation_and_databases.md
├── 03_emu_outputs_to_phyloseq.md
├── 04_diversity_and_differential_abundance.md
├── 05_network_analysis.md

```

Each Markdown file is designed to be readable as a standalone protocol or methodological note.

---

## Main workflows

### 1. Long-read 16S preprocessing

The long-read workflow describes how to process Oxford Nanopore 16S reads after basecalling and demultiplexing. It distinguishes between ONT adapter/barcode trimming and locus-specific primer trimming. This distinction is important when the amplicon is generated using bacterial 16S primers such as 27F and 1492R and then sequenced using an ONT ligation kit such as SQK-LSK114.

### 2. EMU taxonomic classification

The EMU workflow describes how to install EMU, download prebuilt databases, build a custom database such as eHOMD, and run taxonomic classification on short-read or long-read 16S data. The examples include FASTA and FASTQ input formats and show how to keep intermediate output files, estimated counts, read assignments, and unclassified reads when needed.

### 3. EMU outputs to R and phyloseq

The R workflow describes how to combine multiple EMU `*_rel-abundance.tsv` files into a single taxon-by-sample table, retain taxonomic annotations, harmonize sample names with metadata, and generate a `phyloseq` object for downstream analysis.

### 4. Diversity and differential abundance

The diversity workflow summarizes examples using `breakaway`, `DivNet`, and `radEmu`. It covers richness estimation, Shannon and Simpson diversity estimation, beta diversity, and differential abundance models for paired and unpaired designs.

### 5. Network analysis

The network workflow summarizes how to construct and interpret microbial association networks using tools such as NetCoMi, SPIEC-EASI, and igraph. It includes examples for single-network construction, group-specific networks, pre/post paired designs, network comparison, centrality metrics, hub taxa identification, and export of edge/node tables.

---

## Methodological principles

The workflows follow five general principles:

1. Keep preprocessing, taxonomic classification, and statistical analysis conceptually separated.
2. Document the sequencing technology, primer set, database, parameters, and sample metadata used in each analysis.
3. Avoid interpreting correlation or network edges as direct biological interactions without additional evidence.
4. Account for paired or repeated-measures designs whenever the study structure requires it.
5. Preserve intermediate outputs when they are useful for quality control, reproducibility, or troubleshooting.

---

## Notes on paired and unpaired designs

Many examples are written to accommodate both paired and unpaired microbiome studies.

For paired designs, such as pre/post treatment sampling, the metadata should include a subject-level identifier, for example `SampleID`, and a within-subject variable, for example `Timepoint`. Differential abundance models should account for repeated measurements when possible. Network analyses can compare pre- and post-treatment association structures descriptively or with constrained/permutation-based approaches, but network-level inference should be interpreted carefully when the sample size is small.

For unpaired designs, such as comparisons between independent clinical groups, the metadata should include a group variable, for example `Group`, and optional covariates such as age, sex, sequencing batch, oral health status, or dietary variables.

---

## Important limitations

These workflows are examples and should be reviewed before being applied to a new dataset. Microbiome data are compositional, sparse, and highly dependent on sequencing depth, sample processing, primer choice, reference database, and filtering decisions. Network analysis is particularly sensitive to sample size, taxonomic filtering, zero handling, and the method used to infer associations.

The scripts and examples should not be interpreted as universal best practices. They are templates for transparent and reproducible analysis, and each project should justify its own parameter choices.

---

## Keywords

`microbiome`, `16S`, `Oxford Nanopore`, `EMU`, `eHOMD`, `SILVA`, `phyloseq`, `breakaway`, `DivNet`, `radEmu`, `NetCoMi`, `SPIEC-EASI`, `oral microbiome`, `gut microbiome`, `periodontitis`, `microbial networks`
