# Identification of Drug-resistance Based Mutations  in Mycobacterium tuberculosis using Whole Genome Sequencing Data

## Project Overview

This project involves the bioinformatics analysis of whole-genome sequencing (WGS) data from *Mycobacterium tuberculosis* to identify and investigate mutations associated with anti-tuberculosis drug resistance.

The analysis covers preprocessing of the paired-end WGS data i.e. raw read quality assessment, read trimming followed by reference-based genome alignment, alignment quality evaluation, variant calling, variant annotation, resistance-associated mutation interpretation and visualisation.

The project was carried out as part of a one-month BioTechTrek internship.

## Project Objectives

- Assess the quality of raw  paired-end sequencing reads.
- Perform quality-based trimming of the sequencing reads.
- Align sequencing reads against the *M. tuberculosis* reference genome (H37Rv).
- Evaluate alignment statistics and genome coverage.
- Identify genomic variants using variant-calling tools.
- Annotate variants to understand their genomic and functional effects.
- Investigate mutations associated with the three important drug resistance-associated genes i.e. rpoB, katG, gyrA using TB-profiler.
- Visualize selected variants using IGV.

## Dataset Information

- Organism: *Mycobacterium tuberculosis*
- Sample accession: ERR5987300 
- Study accession: PRJEB45389
- Sequencing strategy : Whole Genome Sequencing
- Sequencing type: Paired-end
- Reference genome: *M. tuberculosis* H37Rv
- Reference accession: NC_000962.3

The sequencing dataset was obtained from the European Nucleotide Archive (ENA).

## Reference Genome

The *Mycobacterium tuberculosis* H37Rv reference genome (NC_000962.3) was used for reference-based alignment and variant analysis.
The reference genome was obtained from the National Center for Biotechnology Information (NCBI).

Reference annotation files included:
- `NC_000962.3.gff`
- `NC_000962.3.gbff`

These files contain genomic features and annotation information of the reference genome used during downstream analysis.

## Bioinformatics Analysis Workflow

The analysis is followed by these steps:

1. **Raw Read Quality Assessment**
   - FastQC was used to assess the quality of raw sequencing reads.
   - MultiQC was used to compile quality-control reports.

2. **Read Trimming and Filtering**
   - fastp was used for adapter trimming and quality-based filtering.
   - FastQC and MultiQC were used again to evaluate the processed reads and compile the quality-control reports.

3. **Reference-based Alignment**
   - Processed reads were aligned against the H37Rv reference genome.
   - SAM to BAM processing and alignment statistics were evaluated using SAMtools.

4. **Alignment Quality Assessment**
   - Alignment statistics, mapped reads and genome coverage were examined.
   - Coverage information was generated using SAMtools.

5. **Variant Calling and Processing**
   - BCFtools was used for variant identification and processing.
   - Variant files were prepared for downstream annotation.

6. **Variant Annotation**
   - SnpEff was used to annotate variants and predict their potential functional effects.
   - Annotated variants were examined for their genomic locations, consequences and predicted impact.

7. **Drug Resistance Analysis**
   - TB-profiler was used to investigate mutations associated with anti-tuberculosis drug resistance.
   - Results were compared with the annotated variant data.

8. **Variant Visualization**
   - Integrative Genomics Viewer (IGV) was used to inspect the genomic variants in the selected regions and visualize supporting the evidence.

## Tools and Software

- FastQC: Raw and processed read quality assessment | Version: 0.13.0 
- fastp: Read trimming and filtering | Version: 1.4.0 
- SAMtools: Alignment processing and statistics | Version: 1.24 
- BCFtools: Variant calling and processing | Version: 1.24 
- SnpEff: Variant annotation | Version: 5.4c 


The software environment was managed using Conda.

##Target Genes Function

The downstream investigation focused on three important genes:

| Gene | Associated Drug | Biological Significance |

- rpoB | Rifampicin | Encodes the beta subunit of RNA polymerase. Mutations in this gene can contribute to rifampicin resistance.
- katG | Isoniazid | Encodes catalase-peroxidase, involved in activation of the isoniazid prodrug.
- gyrA | Fluoroquinolones | Encodes the A subunit of DNA gyrase, a target of fluoroquinolone antibiotics.



## Results

### 1. Alignment and Coverage Statistics

The alignment statistics obtained for sample ERR5987300 were:


| Reference genome length | 4,411,532 bp |
| Number of reads | 2,830,685 |
| Covered bases | 4,376,718 bp |
| Genome coverage | 99.21% |
| Mean sequencing depth | 96.14× |
| Mean base quality | 32.4 |
| Mean mapping quality | 59 |

The sequencing reads covered approximately 99.21% of the reference genome, with an average sequencing depth of approximately 96×.

### 2. Variant Annotation

Identified variants were annotated using SnpEff to determine their genomic locations and predicted functional consequences.

The annotation results included information such as:
- Gene and genomic position
- Variant type
- Predicted functional consequence
- Impact classification
- HGVS coding and protein-level annotations

### 3. Drug Resistance-Associated Mutation

One of the key findings was a mutation in  on of the targeted *rpoB* gene:

| Parameter | Result |
|---|---|
| Gene | rpoB |
| Genomic position | 761155 |
| Nucleotide change | C>T |
| Coding change | c.1349C>T |
| Protein change | p.Ser450Leu |
| Predicted impact | MODERATE |
| Functional consequence | Missense variant |

The rpoB p.Ser450Leu mutation is a well-known mutation associated with rifampicin resistance in *Mycobacterium tuberculosis*.

This finding was investigated using SnpEff annotation, TB-profiler results and IGV visualization.

Other selected variants, including variants in genes such as gyrA and katG, were also examined. However, not all identified missense variants could be independently confirmed as drug resistance-associated findings by TB-profiler.

*Interpretation:* The rpoB p.Ser450Leu mutation was the main resistance-associated finding supported by the combined analysis. These are computational findings and should not be considered a substitute for phenotypic drug susceptibility testing.

## Repository Structure

```text
Project_01/
│
├── alignment/
│   ├── ERR5987300.coverage.txt
│   ├── ERR5987300.flagstat.txt
│   └── ERR5987300.stats.txt
│
├── annotation/
│   ├── ERR5987300.annotated.vcf
│   ├── ERR5987300.snpeff_input.vcf.gz
│   ├── ERR5987300.snpeff_input.vcf.gz.tbi
│   ├── ERR5987300_snpEff_summary.genes.txt
│   ├── ERR5987300_snpEff_summary.html
│   └── chromosome_map.txt

│
├── igv/
│   ├── gyrA_variant_1.png
│   ├── gyrA_variant_2.png
│   ├── gyrA_variant_3.png
│   ├── katG_variant.png
│   ├── rpoB_variant_1.png
│   └── rpoB_variant_2.png
│
├── qc/
│   ├── multiqc_raw/
│   ├── multiqc_after_trimming/
│   └── FastQC and fastp reports
│
├── reference/
│   ├── NC_000962.3.gff
│   └── NC_000962.3.gbff
│
├── results/
│   ├── ENA_metadata.tsv
│   ├── ERR5987300.results.csv
│   ├── ERR5987300.results.json
│   ├── ERR5987300.results.txt
│   ├── ERR5987300_annotated_variants.tsv
│   ├── ERR5987300_variants.tsv
│   ├── Final_variant_table.xlsx
│   ├── QC_report.xlsx
│   ├── Resistance_summary.xlsx
│   ├── mandatory_genes.tsv
│   ├── sample_metadata.txt
│   ├── software_versions.txt
│   └── command_history.txt
│
├── .gitignore
├── snpEff_genes.txt
├── snpEff_summary.html
└── README.md
```

*Note: Large raw sequencing files and intermediate files are excluded from the Git repository. The repository contains selected reports, annotation files, summary results and visualization outputs.*

## Reproducibility

The analysis was performed in a Conda-managed Linux environment.

The `results/command_history.txt` file contains the recorded analysis commands, while `results/software_versions.txt` documents the software versions used.

The reference annotation files, quality-control reports, alignment statistics, variant annotation outputs and result tables are provided to support examination of the analysis.

##Skills Developed

- Whole Genome Sequencing (WGS) data analysis.
- NGS quality control and read preprocessing.
- Reference-based sequence alignment.
- Variant calling and functional annotation.
- Interpretation of drug-resistance-associated mutations.
- Linux command-line operations.
- Bioinformatics pipeline handling and result documentation.
- Genomic data visualisation using IGV

## Limitations

- The analysis focuses on a single sequencing sample.
- The analysis focuses mainly on three important drug-resistant genes.
- Variant interpretation is dependent on the reference genome, variant-calling approach and available annotation databases.
- Predicted resistance-associated mutations do not independently establish phenotypic drug resistance.
- Phenotypic drug susceptibility testing would be required for experimental confirmation.

## Conclusion

- This project provided practical experience in processing and analysing bacterial whole-genome sequencing data, from initial quality assessment to variant identification, functional annotation and resistance-associated mutation investigation.
- The integration of BCFtools, SnpEff, TB-Profiler and IGV helped develop an understanding of how genomic variations can be investigated in the context of antimicrobial drug resistance.
- The identification and investigation of the rpoB p.Ser450Leu mutation highlight the application of WGS-based approaches in studying mutations associated with anti-tuberculosis drug resistance.

## Acknowledgement

This work was undertaken as part of a one-month bioinformatics internship by BioTechTrek  focusing on the identification of drug-resistance-associated mutations in Mycobacterium tuberculosis using Whole Genome Sequencing.
