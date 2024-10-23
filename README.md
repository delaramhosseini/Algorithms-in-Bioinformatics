# Algorithms in Bioinformatics

### Overview

This project focuses on analyzing paired next-generation sequencing expression profiles of normal and tumor colorectal tissues from the study with accession number **GSE104836**. The aim is to extract a gene expression matrix from fastq files and perform advanced analyses on the resulting data.

### Sample Information

| SRR Accession Number | Tissue            | Gender | Pair ID |
|----------------------|-------------------|--------|---------|
| SRR6159233           | Colon cancer tissue| Female | 94      |
| SRR6159234           | Non-tumor tissue   | Female | 94      |
| SRR6191641           | Colon cancer tissue| Female | 29      |
| SRR6191642           | Non-tumor tissue   | Female | 29      |
| SRR6191643           | Colon cancer tissue| Male   | 34      |
| SRR6191644           | Non-tumor tissue   | Male   | 34      |
| SRR6191645           | Colon cancer tissue| Female | 48      |
| SRR6191646           | Non-tumor tissue   | Female | 48      |
| SRR6191647           | Colon cancer tissue| Male   | 55      |
| SRR6191648           | Non-tumor tissue   | Male   | 55      |



### Data Preparation

1. **Convert SRA Files:** Each student will preprocess paired data for only one patient. Use the following command to convert SRA files to two Fastq.gz files:
   ```bash
   fastq-dump [options] file.sra

   ```

### Part A - Quality Control and Trimming

1. Assess read qualities using **FastQC**.
2. Use **Trimmomatic** for read trimming:
   ```bash
   trimmomatic PE [options] input_forward.fastq.gz input_reverse.fastq.gz output_forward_paired.fastq.gz output_forward_unpaired.fastq.gz output_reverse_paired.fastq.gz output_reverse_unpaired.fastq.gz
   ```
3. Recheck read qualities with FastQC.

#### Questions to Answer:
1. What is the average number of reads across samples before and after trimming?
2. Compare the read length averages before and after trimming.
3. Compare read quality distributions before and after trimming.
4. What does the Adaptor Content warning indicate?
5. Why do we first remove adapter sequences before low-quality bases?
6. What does the quality of bases mean, and how is it obtained?

### Part B - Read Mapping

1. **Map Reads:** Use **HISAT2** to map reads to the reference genome:
   ```bash
   hisat2 [options]* -x <ht2-idx> {-1 <m1> -2 <m2>} [-S <sam>]
   ```
2. Convert SAM files to BAM files using **Samtools**:
   ```bash
   samtools view [options] <in.sam> > <out.bam>
   ```
3. Index the reference genome with HISAT2:
   ```bash
   hisat2-build [options]* <reference_in> <ht2_index_name>
   ```

#### Questions to Answer:
1. What is the difference between SAM and BAM files?
2. What is the purpose of indexing the genome?
3. Report mapping percentages of all samples in a table and explain low mapping percentages.

### Part C - Building Gene Expression Matrix

1. Use **htseq-count** on aligned reads for differential expression analysis.
2. Merge results into a single matrix for use in the **edgeR** package.

#### Questions to Answer:
1. How many genes are not expressed in control and tumor samples?
2. Compare the obtained matrix with the main study's gene expression submatrix.
3. Name two other software for this step and discuss their advantages and disadvantages.

### Part D - Differential Gene Expression Analysis

1. Use **edgeR** for differential gene expression analysis.
  
#### Questions to Answer:
1. How many genes are input to edgeR? How many are differentially expressed?
2. Determine the percentage of differentially expressed genes with |log2FoldChange| > 1.5.
3. Explain the difference between P-value and FDR.

### Part E - Gene Ontology Enrichment Analysis

1. Use **GOseq** in R for GO enrichment analysis based on differentially expressed genes.
  
#### Questions to Answer:
1. Display results related to Biological Process, Molecular Function, Cellular Component, and KEGG as separate plots.
2. Briefly study each significant term and discuss important terms.
3. Write a general biological conclusion about the project's final results.

### Installation and Requirements

Make sure to install the necessary software packages before starting the analysis:

- **FastQC**
- **Trimmomatic**
- **HISAT2**
- **Samtools**
- **HTSeq**
- **edgeR**
- **GOseq**

