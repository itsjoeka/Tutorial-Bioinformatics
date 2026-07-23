# Bioinformatics Roadmap: Zero to Mastery

A comprehensive, self-contained learning path for bioinformatics — from your first Linux command to integrated multi-omics analysis. Each stage lists core concepts, hands-on skills, and recommended tools/resources. Check items off as you go.

> **How to use this roadmap:** Work top to bottom. Don't skip the Linux/scripting/stats foundations — they underpin everything later. Expect 12–24+ months of consistent part-time study to move from zero to an advanced practitioner, depending on your starting point (biology background vs. CS background).

---

## Table of Contents

1. [Stage 0: Prerequisites & Mindset](#stage-0-prerequisites--mindset)
2. [Stage 1: Linux & Command Line Foundations](#stage-1-linux--command-line-foundations)
3. [Stage 2: Programming Foundations (Python & R)](#stage-2-programming-foundations-python--r)
4. [Stage 3: Statistics & Math Foundations](#stage-3-statistics--math-foundations)
5. [Stage 4: Molecular Biology & Genomics Fundamentals](#stage-4-molecular-biology--genomics-fundamentals)
6. [Stage 5: Core Bioinformatics File Formats & Databases](#stage-5-core-bioinformatics-file-formats--databases)
7. [Stage 6: Sequence Analysis Fundamentals](#stage-6-sequence-analysis-fundamentals)
8. [Stage 7: Next-Generation Sequencing (NGS) Pipelines](#stage-7-next-generation-sequencing-ngs-pipelines)
9. [Stage 8: Genomics](#stage-8-genomics)
10. [Stage 9: Transcriptomics (RNA-seq & Beyond)](#stage-9-transcriptomics-rna-seq--beyond)
11. [Stage 10: Epigenomics](#stage-10-epigenomics)
12. [Stage 11: Proteomics & Metabolomics](#stage-11-proteomics--metabolomics)
13. [Stage 12: Structural Bioinformatics](#stage-12-structural-bioinformatics)
14. [Stage 13: Metagenomics & Microbiome Analysis](#stage-13-metagenomics--microbiome-analysis)
15. [Stage 14: Population Genetics & Evolutionary Biology](#stage-14-population-genetics--evolutionary-biology)
16. [Stage 15: Single-Cell & Spatial Omics](#stage-15-single-cell--spatial-omics)
17. [Stage 16: Machine Learning & Deep Learning for Bioinformatics](#stage-16-machine-learning--deep-learning-for-bioinformatics)
18. [Stage 17: Databases, Workflow Management & Reproducibility](#stage-17-databases-workflow-management--reproducibility)
19. [Stage 18: Cloud & High-Performance Computing (HPC)](#stage-18-cloud--high-performance-computing-hpc)
20. [Stage 19: Integrated Multi-Omics & Systems Biology (Mastery)](#stage-19-integrated-multi-omics--systems-biology-mastery)
21. [Stage 20: Clinical & Translational Bioinformatics](#stage-20-clinical--translational-bioinformatics)
22. [Stage 21: Software Engineering Best Practices](#stage-21-software-engineering-best-practices)
23. [Capstone Projects](#capstone-projects)
24. [Recommended Books](#recommended-books)
25. [Communities & Staying Current](#communities--staying-current)

---

## Stage 0: Prerequisites & Mindset

- [ ] Comfortable using a computer, installing software, managing files
- [ ] Basic high-school algebra and biology
- [ ] Growth mindset: bioinformatics is ~50% biology, ~50% computation — you will learn both
- [ ] Set up a dedicated learning environment (a Linux machine, VM, or WSL2 on Windows)

**Goal:** Prepare your machine and mindset before writing any code.

---

## Stage 1: Linux & Command Line Foundations

- [ ] Install Linux (Ubuntu/Debian) natively, in a VM, or via WSL2
- [ ] Filesystem navigation: `pwd`, `ls`, `cd`, `mkdir`, `rm`, `cp`, `mv`, `find`
- [ ] File permissions & ownership: `chmod`, `chown`, `sudo`
- [ ] Text processing: `grep`, `sed`, `awk`, `cut`, `sort`, `uniq`, `wc`, `tr`
- [ ] Piping & redirection: `|`, `>`, `>>`, `<`, `2>`
- [ ] Process management: `ps`, `top`/`htop`, `kill`, `jobs`, `&`, `nohup`
- [ ] Compression: `tar`, `gzip`/`gunzip`, `zip`
- [ ] Package managers: `apt`, `conda`/`mamba`, `homebrew` (macOS)
- [ ] Shell scripting: variables, loops, conditionals, functions in `bash`
- [ ] SSH & remote computing basics: `ssh`, `scp`, `rsync`, `tmux`/`screen`
- [ ] Environment variables & `PATH`
- [ ] Text editors: `vim` or `nano` basics; configure VS Code for remote work

**Goal:** Navigate, manipulate files, and automate tasks entirely from the terminal.

---

## Stage 2: Programming Foundations (Python & R)

### Python
- [ ] Syntax, data types, control flow, functions
- [ ] Data structures: lists, dicts, sets, tuples
- [ ] File I/O and parsing text/CSV/JSON
- [ ] Object-oriented programming basics
- [ ] Core scientific stack: `NumPy`, `pandas`, `matplotlib`/`seaborn`
- [ ] Biology-specific: `Biopython`
- [ ] Virtual environments: `venv`, `conda`, `mamba`
- [ ] Jupyter notebooks / JupyterLab

### R
- [ ] Syntax, vectors, data frames, factors
- [ ] `tidyverse`: `dplyr`, `tidyr`, `ggplot2`, `readr`
- [ ] Bioconductor ecosystem basics (installation, `BiocManager`)
- [ ] R Markdown / Quarto for reproducible reports
- [ ] RStudio IDE proficiency

### Version Control
- [ ] Git fundamentals: `init`, `add`, `commit`, `branch`, `merge`, `log`
- [ ] Remote workflows: GitHub/GitLab, `push`/`pull`, pull requests
- [ ] `.gitignore`, resolving merge conflicts

**Goal:** Write scripts to parse, transform, analyze, and visualize data in both Python and R.

---

## Stage 3: Statistics & Math Foundations

- [ ] Descriptive statistics: mean, median, variance, distributions
- [ ] Probability theory basics
- [ ] Hypothesis testing: t-test, chi-square, ANOVA
- [ ] Multiple testing correction (Bonferroni, Benjamini-Hochberg/FDR)
- [ ] Linear regression & generalized linear models (GLMs)
- [ ] Correlation vs. causation; confounders
- [ ] Bayesian statistics fundamentals
- [ ] Linear algebra basics: vectors, matrices, eigen decomposition (for PCA/ML)
- [ ] Dimensionality reduction concepts: PCA, t-SNE, UMAP
- [ ] Experimental design: replicates, controls, power analysis, batch effects

**Goal:** Understand the statistical machinery underlying every omics analysis method you'll use.

---

## Stage 4: Molecular Biology & Genomics Fundamentals

- [ ] Central dogma: DNA → RNA → protein
- [ ] DNA/RNA structure, chromatin, chromosomes
- [ ] Gene structure: exons, introns, promoters, UTRs, splicing
- [ ] Transcription & translation mechanisms
- [ ] Mutation types: SNPs, indels, CNVs, structural variants
- [ ] Genetic inheritance and Mendelian genetics basics
- [ ] Cell biology essentials (organelles, cell cycle)
- [ ] Genome organization: prokaryotic vs. eukaryotic
- [ ] Epigenetic regulation basics: methylation, histone modification
- [ ] Model organisms (human, mouse, yeast, *E. coli*, *Drosophila*)

**Goal:** Ground every downstream computational step in solid biological understanding.

---

## Stage 5: Core Bioinformatics File Formats & Databases

### File Formats
- [ ] FASTA / FASTQ (sequences & quality scores, Phred encoding)
- [ ] SAM/BAM/CRAM (alignments)
- [ ] VCF/BCF (variants)
- [ ] GFF/GTF/BED (genomic features/annotations)
- [ ] PDB/mmCIF (protein structures)
- [ ] Wig/BigWig/BedGraph (signal tracks)
- [ ] MAF (multiple alignment/mutation annotation)

### Key Databases & Tools
- [ ] NCBI (GenBank, RefSeq, SRA, dbSNP, PubMed)
- [ ] Ensembl / UCSC Genome Browser
- [ ] UniProt, PDB (RCSB)
- [ ] GEO & ArrayExpress (expression data)
- [ ] KEGG, Reactome (pathways)
- [ ] gnomAD, 1000 Genomes, ClinVar (variation)
- [ ] `samtools`, `bcftools`, `bedtools` for format manipulation

**Goal:** Fluently read, convert, and manipulate every standard bioinformatics data format.

---

## Stage 6: Sequence Analysis Fundamentals

- [ ] Pairwise alignment: Needleman-Wunsch (global), Smith-Waterman (local)
- [ ] Scoring matrices: PAM, BLOSUM
- [ ] Multiple sequence alignment: `MUSCLE`, `MAFFT`, `Clustal Omega`
- [ ] Database searching: `BLAST`, `DIAMOND`, `HMMER`
- [ ] Sequence motifs & regular expressions
- [ ] k-mer analysis fundamentals
- [ ] Phylogenetic tree basics (precursor to Stage 14)

**Goal:** Master the algorithmic core that underlies alignment-based bioinformatics.

---

## Stage 7: Next-Generation Sequencing (NGS) Pipelines

- [ ] Sequencing technologies: Illumina (short-read), PacBio/Oxford Nanopore (long-read)
- [ ] Library prep concepts (WGS, WES, targeted panels)
- [ ] Quality control: `FastQC`, `MultiQC`
- [ ] Read trimming/filtering: `Trimmomatic`, `fastp`, `Cutadapt`
- [ ] Read alignment: `BWA`, `Bowtie2`, `STAR`, `HISAT2`, `minimap2` (long reads)
- [ ] Alignment post-processing: sorting, marking duplicates (`Picard`, `samtools`)
- [ ] Variant calling basics: `GATK` best practices, `bcftools`, `DeepVariant`
- [ ] Genome assembly concepts: de novo vs. reference-guided; `SPAdes`, `Canu`, `Flye`
- [ ] Assembly QC: `QUAST`, N50/L50 metrics
- [ ] Building a full FASTQ → BAM → VCF pipeline manually

**Goal:** Independently process raw sequencing reads into analysis-ready, quality-controlled results.

---

## Stage 8: Genomics

- [ ] Variant annotation: `SnpEff`, `VEP` (Variant Effect Predictor), `ANNOVAR`
- [ ] Variant filtering & interpretation (hard filters, VQSR)
- [ ] Structural variant (SV) detection: `Manta`, `DELLY`, `LUMPY`
- [ ] Copy number variant (CNV) analysis: `CNVkit`
- [ ] Whole-genome vs. whole-exome sequencing analysis
- [ ] Comparative genomics & synteny analysis
- [ ] Genome annotation pipelines: `Prokka` (prokaryotes), `MAKER`/`BRAKER` (eukaryotes)
- [ ] Pangenome concepts (graph genomes)
- [ ] Clinical variant classification: ACMG guidelines basics

**Goal:** Take raw variant calls to biologically and clinically interpreted results.

---

## Stage 9: Transcriptomics (RNA-seq & Beyond)

- [ ] RNA-seq experimental design & library types (poly-A, total RNA, stranded)
- [ ] Alignment-based quantification: `STAR` + `featureCounts`/`HTSeq`
- [ ] Alignment-free quantification: `Salmon`, `Kallisto`
- [ ] Differential expression analysis: `DESeq2`, `edgeR`, `limma-voom`
- [ ] Normalization methods (TPM, FPKM, TMM, CPM) and when each applies
- [ ] Batch effect correction: `ComBat`, `sva`
- [ ] Gene set enrichment analysis (GSEA), over-representation analysis (`clusterProfiler`)
- [ ] Alternative splicing analysis: `rMATS`, `LeafCutter`
- [ ] Isoform-level quantification
- [ ] Non-coding RNA analysis (miRNA, lncRNA)
- [ ] Time-course / longitudinal RNA-seq analysis
- [ ] Visualization: volcano plots, heatmaps, PCA plots of expression data

**Goal:** Design, run, and statistically interpret a complete RNA-seq differential expression study.

---

## Stage 10: Epigenomics

- [ ] Bisulfite sequencing & DNA methylation analysis: `Bismark`, methylation calling
- [ ] ChIP-seq: peak calling (`MACS2`), motif discovery (`MEME` suite)
- [ ] ATAC-seq: chromatin accessibility analysis
- [ ] Hi-C / chromatin conformation capture basics (3D genome organization)
- [ ] Differential methylation/binding analysis
- [ ] Integrating epigenomic tracks with gene expression
- [ ] Genome browsers for visualization: IGV, UCSC Genome Browser, `pyGenomeTracks`

**Goal:** Analyze regulatory and chromatin-level data and connect it to gene expression outcomes.

---

## Stage 11: Proteomics & Metabolomics

### Proteomics
- [ ] Mass spectrometry basics (MS/MS, peptide fragmentation)
- [ ] Protein identification & quantification: `MaxQuant`, `Proteome Discoverer`
- [ ] Post-translational modification (PTM) analysis
- [ ] Protein-protein interaction networks: STRING database

### Metabolomics
- [ ] LC-MS/GC-MS data basics
- [ ] Metabolite identification & pathway mapping
- [ ] Tools: `XCMS`, `MetaboAnalyst`

**Goal:** Extend omics literacy beyond nucleic acids into protein and small-molecule data.

---

## Stage 12: Structural Bioinformatics

- [ ] Protein structure fundamentals (primary → quaternary structure)
- [ ] Structure visualization: `PyMOL`, `ChimeraX`
- [ ] Structure prediction: homology modeling, `AlphaFold2`/`ColabFold`, `ESMFold`
- [ ] Protein-ligand docking basics: `AutoDock Vina`
- [ ] Structural alignment & comparison
- [ ] Molecular dynamics simulation concepts (`GROMACS` overview)

**Goal:** Predict, visualize, and reason about 3D protein structure and function.

---

## Stage 13: Metagenomics & Microbiome Analysis

- [ ] 16S rRNA amplicon sequencing analysis: `QIIME2`, `DADA2`
- [ ] Shotgun metagenomics: taxonomic profiling (`Kraken2`, `MetaPhlAn`)
- [ ] Functional profiling: `HUMAnN`
- [ ] Metagenome assembly & binning: `MEGAHIT`, `MetaBAT2`
- [ ] Diversity metrics: alpha/beta diversity, `PERMANOVA`
- [ ] Microbiome-host interaction analysis

**Goal:** Characterize microbial communities from raw sequencing data to ecological insight.

---

## Stage 14: Population Genetics & Evolutionary Biology

- [ ] Allele frequency, Hardy-Weinberg equilibrium
- [ ] Population structure: PCA, `ADMIXTURE`, `STRUCTURE`
- [ ] Linkage disequilibrium & GWAS: `PLINK`, `GCTA`
- [ ] Polygenic risk scores
- [ ] Phylogenetics: tree building (`RAxML`, `IQ-TREE`), molecular clocks
- [ ] Selection signatures (dN/dS, Tajima's D, Fst)
- [ ] Coalescent theory basics
- [ ] Ancient DNA analysis concepts

**Goal:** Analyze genetic variation across populations and reconstruct evolutionary relationships.

---

## Stage 15: Single-Cell & Spatial Omics

- [ ] Single-cell RNA-seq (scRNA-seq) workflow: `Cell Ranger`, `Seurat`, `Scanpy`
- [ ] QC, normalization, clustering (Louvain/Leiden), dimensionality reduction (UMAP/t-SNE)
- [ ] Cell type annotation & marker gene identification
- [ ] Trajectory inference / pseudotime: `Monocle3`, `scVelo` (RNA velocity)
- [ ] Single-cell ATAC-seq (`ArchR`, `Signac`)
- [ ] Multi-omic single-cell integration (CITE-seq, 10x Multiome)
- [ ] Spatial transcriptomics: Visium, MERFISH, Slide-seq analysis
- [ ] Cell-cell communication analysis: `CellPhoneDB`, `CellChat`
- [ ] Batch integration across single-cell datasets: `Harmony`, `scVI`, `BBKNN`

**Goal:** Resolve biology at single-cell and spatial resolution — the current frontier of most omics research.

---

## Stage 16: Machine Learning & Deep Learning for Bioinformatics

- [ ] Classical ML: regression, random forests, SVMs, gradient boosting (`scikit-learn`, `XGBoost`)
- [ ] Feature engineering & selection for biological data
- [ ] Cross-validation & avoiding data leakage in genomic contexts
- [ ] Neural network fundamentals: `PyTorch`/`TensorFlow`
- [ ] CNNs for genomic sequence/motif learning
- [ ] RNNs/Transformers for sequence data
- [ ] Applications: variant effect prediction, splicing prediction, protein structure (AlphaFold internals), genomic language models (DNABERT, Enformer)
- [ ] Explainability in biological ML (SHAP, attention maps)
- [ ] Foundations of biological "foundation models" (ESM, scGPT, Geneformer)

**Goal:** Apply and critically evaluate ML/DL methods on genomic, transcriptomic, and structural data.

---

## Stage 17: Databases, Workflow Management & Reproducibility

- [ ] SQL fundamentals for biological databases
- [ ] Workflow managers: `Snakemake`, `Nextflow` (write full reproducible pipelines)
- [ ] Containerization: `Docker`, `Singularity/Apptainer`
- [ ] Package/environment management: `conda`, `mamba`, `renv` (R)
- [ ] Reproducible reporting: R Markdown/Quarto, Jupyter + `papermill`
- [ ] FAIR data principles
- [ ] Pipeline registries: `nf-core`, Snakemake workflow catalog

**Goal:** Build pipelines that are automated, portable, and reproducible by anyone, anywhere.

---

## Stage 18: Cloud & High-Performance Computing (HPC)

- [ ] HPC cluster basics: job schedulers (`SLURM`, `PBS`), submitting/monitoring jobs
- [ ] Parallelization strategies for large-scale genomic data
- [ ] Cloud platforms: AWS/GCP/Azure basics for bioinformatics (S3/buckets, compute instances)
- [ ] Cloud-native genomics platforms: DNAnexus, Terra, Seven Bridges
- [ ] Cost-aware large-scale data processing
- [ ] Data management for large omics datasets (storage tiers, indexing, streaming)

**Goal:** Scale analyses from a laptop to institutional or cloud-scale infrastructure.

---

## Stage 19: Integrated Multi-Omics & Systems Biology (Mastery)

- [ ] Multi-omics integration strategies: early/intermediate/late fusion
- [ ] Statistical integration methods: `MOFA+`, canonical correlation analysis, joint NMF
- [ ] Network biology: gene regulatory networks, co-expression networks (`WGCNA`)
- [ ] Pathway-level multi-omics integration (KEGG/Reactome mapping across layers)
- [ ] Multi-omics single-cell integration (see Stage 15) at cohort scale
- [ ] Systems biology modeling: Boolean networks, flux balance analysis
- [ ] Causal inference in omics data (Mendelian randomization)
- [ ] Building an end-to-end integrated pipeline: genome + transcriptome + epigenome + proteome → biological model
- [ ] Interpreting multi-omics results in a disease/phenotype context

**Goal:** Synthesize multiple omics layers into a coherent, biologically meaningful systems-level model — the mark of mastery.

---

## Stage 20: Clinical & Translational Bioinformatics

- [ ] Precision medicine pipelines (tumor-normal analysis, somatic vs. germline)
- [ ] Pharmacogenomics basics
- [ ] Biomarker discovery & validation frameworks
- [ ] Regulatory & ethical considerations: HIPAA/GDPR, informed consent, data privacy
- [ ] Clinical reporting standards (ACMG, CAP/CLIA awareness)
- [ ] Electronic health record (EHR) data integration basics

**Goal:** Apply bioinformatics rigor in contexts where results affect real clinical decisions.

---

## Stage 21: Software Engineering Best Practices

- [ ] Writing modular, tested code (`pytest`, `testthat`)
- [ ] Packaging: Python packages (`pip`/`PyPI`), R packages (Bioconductor submission standards)
- [ ] Code review & collaborative Git workflows (branching strategies, PRs)
- [ ] Documentation: docstrings, README standards, Sphinx/`pkgdown`
- [ ] CI/CD basics (GitHub Actions) for pipeline testing
- [ ] Command-line interface (CLI) tool design
- [ ] Contributing to open-source bioinformatics tools

**Goal:** Produce tools and pipelines that other scientists can trust, reuse, and build on.

---

## Capstone Projects

Apply everything by completing (or better, publishing/open-sourcing) projects like:

- [ ] End-to-end WGS variant calling & annotation pipeline (Nextflow/Snakemake, containerized)
- [ ] Full RNA-seq differential expression study with GSEA and publication-quality figures
- [ ] scRNA-seq atlas of a tissue/condition with cell type annotation and trajectory analysis
- [ ] Multi-omics integration project (e.g., RNA-seq + methylation + variant data on a public cohort like TCGA)
- [ ] A GWAS from raw genotypes to Manhattan plot and polygenic score
- [ ] A protein structure prediction + docking study for a target of interest
- [ ] A metagenomics comparative analysis across sample groups
- [ ] Contribute a bug fix or feature to an established open-source bioinformatics tool

---

## Recommended Books

- *Bioinformatics Data Skills* — Vince Buffalo
- *Biological Sequence Analysis* — Durbin, Eddy, Krogh, Mitchison
- *Molecular Biology of the Cell* — Alberts et al. (biology reference)
- *An Introduction to Statistical Learning* — James, Witten, Hastie, Tibshirani
- *Deep Learning for the Life Sciences* — Ramsundar et al.
- *Modern Statistics for Modern Biology* — Holmes & Huber (free online)
- *Computational Genomics with R* — Akalin (free online)

---

## Communities & Staying Current

- [ ] Follow Bioconductor and Bioconda release notes
- [ ] Read preprints: bioRxiv, medRxiv
- [ ] Engage on Biostars, r/bioinformatics, and relevant Discord/Slack communities
- [ ] Follow key journals: *Bioinformatics*, *Genome Biology*, *Nature Methods*, *Nucleic Acids Research*
- [ ] Attend/watch conference talks: ISMB, ASHG, RECOMB
- [ ] Reproduce analyses from recent high-impact papers as practice

---

*This roadmap is a living document — update it as tools and best practices evolve. Star or fork this repo to track your own progress through each stage.*
