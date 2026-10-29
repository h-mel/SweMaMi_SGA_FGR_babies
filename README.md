# Maternal gut microbiome diversity and SGA/FGR births
Analysis code for the manuscript:

> **Associations between maternal gut microbiome diversity in early and late pregnancy and small-for-gestational-age or growth restricted births: a nested case-control study**

> Anusha T. Antony*, Emma Hertting*, Lotta Herling, Lars Engstrand, Ina Schuppe-Koistinen, Pelle G. Lindqvist, Nele Brusselaers, Eva Wiberg-Itzel, Luisa W. Hugerth
*These authors share first authorship 

## Overview

This repository contains the code used to compare the maternal gut microbiome in early (TP1) and late (TP2) pregnancy between mothers who gave birth to:

- **SGA** – small-for-gestational-age infants
- **FGR** – fetal growth restricted infants
- **AGA** – appropriate-for-gestational-age infants (controls)

Births were classified using the Swedish population-based fetal growth reference chart. A common pool of AGA controls is shared between the two comparisons (**SGA vs AGA** and **FGR vs AGA**).

Taxonomic profiles were generated with MetaPhlAn 4 and functional profiles with HUMAnN 3, with Gut Metabolic Modules (GMMs) derived using Omixer-RPM.

## Repository structure

| Notebook | Description | Output in manuscript |
|---|---|---|
| `01_case_classification_matching.ipynb` | Classifies births as SGA, FGR or AGA, applies exclusion criteria, and performs case-control matching. Produces analysis-ready metadata with case/control status and matched-set IDs. | Input for notebooks 02–04 |
| `02_alpha_diversity.ipynb` | Observed species richness, Shannon diversity and Pielou's evenness. Unadjusted t-tests and confounder-adjusted logistic regression at TP1 and TP2. | Figure 2, Table 2, Figure 3, Table 3 |
| `03_beta_diversity.ipynb` | Community composition using Bray–Curtis, Jaccard and Aitchison (robust CLR) distances. Dispersion tests (betadisper), crude and adjusted PERMANOVA (adonis2), and PCoA plots. | Figure S2, Table S2 |
| `04_differential_abundance.ipynb` | MaAsLin 3 analysis of species and GMMs (abundance and prevalence models), crude and confounder-adjusted, at TP1 and TP2. | Figure S3, Supplementary Data S3 and S4 |

The notebooks should be run in order, as notebook 01 creates the metadata used by all later analyses.

## Analysis details

### Comparisons and time points
Each analysis is run for both comparisons (SGA vs AGA, FGR vs AGA) at both time points (TP1, TP2).

### Confounder adjustment
Adjusted models include advanced maternal age, pre-pregnancy BMI, alcohol use in the 3 months before pregnancy, parity, PMOS, insufficient gestational weight gain, antihypertensive use during pregnancy and sequencing read depth. Preeclampsia is additionally included at TP2.

### Differential abundance
Taxa and GMMs are analysed in separate MaAsLin 3 runs with a shared model specification, so FDR correction is applied within each feature set. Associations with `qval_individual < 0.1` are considered significant. Both abundance (linear, log2) and prevalence (logistic) models are reported.

## Data availability

The raw metagenomic sequences, along with selected metadata variables, are deposited in the European Nucleotide Archive (ENA) under project number **PRJEB81814**.

Individual-level participant data are restricted for privacy reasons and are not included in this repository. 
## Software


Analyses were performed in **R (v4.5.2)** within Jupyter notebooks (R kernel). Key packages:

- `tidyverse` (v2.0.0), `dplyr` (v1.2.0)
- `ggplot2` (v4.0.2), `ggrain` (v0.0.4)
- `vegan` (v2.7.3)
- `maaslin3` (v0.99.16)
- `lme4` (v1.1.33)
- `MatchIt`

Upstream bioinformatic processing used the StaG-mwc (v0.5.1) workflow (FastP, Kraken2, MetaPhlAn4, HUMAnN3, Omixer-RPM). See the manuscript Methods for full details.

## Contact

Anusha Antony – anushata94@gmail.com
