# RNA_Seq_Alignment_Workflow_using_STAR_-SRR11548957-_chr22-
RNA_Seq_Alignment_Workflow_using_STAR_(SRR11548957,_chr22)
# 🧬 STAR RNA-Seq Alignment Workflow (SRR11548957 on Human Chromosome 22)

This repository contains a comprehensive **Jupyter Notebook** pipeline for performing **RNA-Seq read alignment** using the ultra-fast aligner, **STAR** (Spliced Transcripts Alignment to a Reference).

The workflow demonstrates best practices for handling public RNA-Seq data by fetching a specific accession (**SRR11548957**), preparing a subset of the reference genome (**Human Chromosome 22**), generating the STAR index, performing the alignment, and analyzing the resulting quality control (QC) log file.

## 🚀 Key Features

* **Complete End-to-End Pipeline:** Covers environment setup, data download, reference preparation, indexing, alignment, and QC visualization.
* **STAR Implementation:** Uses the robust STAR aligner (version 2.7.10a) to align spliced reads.
* **Targeted Reference:** Aligns reads to a specific, reduced reference (**Human GRCh38, Chromosome 22**) to minimize processing time for testing or specialized analyses.
* **Data Source:** Downloads paired-end reads directly from the **SRA database** using the `sra-toolkit`.
* **Integrated QC Visualization:** Parses the STAR log file and generates a **Plotly Pie Chart** to visualize read mapping statistics (unique, multi-mapping, and unmapped rates).
* **Output Formats:** Generates industry-standard output files: **Sorted BAM** (for visualization/variant calling) and **ReadsPerGene.out.tab** (for Differential Expression Analysis).

---

## 🔬 Analysis Steps

The notebook is structured into the following executable steps:

1.  **Environment Setup:** Installs `sra-toolkit`, `build-essential`, and compiles the `STAR` aligner.
2.  **Data Download:** Fetches and converts **SRR11548957** from SRA into paired-end FASTQ files (`SRR11548957_1.fastq`, `SRR11548957_2.fastq`).
3.  **Reference Preparation:** Downloads the FASTA and GTF files for Human Chromosome 22 (Ensembl GRCh38).
4.  **Genome Indexing:** Runs `STAR --runMode genomeGenerate` to create the alignment index.
5.  **Read Alignment:** Executes `STAR --runMode alignReads` to align the FASTQ files, producing a coordinate-sorted BAM file and gene counts (`--quantMode GeneCounts`).
6.  **QC & Plotting:** Parses the **`Log.final.out`** file and generates an interactive **Plotly Pie Chart** summarizing read mapping percentages.

## ⚠️ Key Findings from Alignment Log (QC)

The alignment results for **SRR11548957** against only Human Chromosome 22 showed:

* **Low Unique Mapping Rate:** Only **8.76%** of input reads mapped uniquely.
* **High Unmapped Rate:** **89.38%** of reads were unmapped because they were **too short**.
* **High Mismatch Rate:** The mismatch rate was **5.16%** per base.

This strongly suggests that the reads likely originate from the **full human genome** and/or require better quality trimming prior to alignment. The current setup serves as an effective demonstration of the pipeline steps but requires adjustment (e.g., aligning to the full genome) for a meaningful biological study.

---

## 🛠️ Prerequisites and Execution

### Requirements

To run this pipeline locally or on Google Colab, you need access to a Linux environment with **GCC/G++** for compiling STAR, and the following tools (which the script installs):

* **`sra-toolkit`** (for `prefetch` and `fasterq-dump`)
* **`STAR`** (version 2.7.10a)
* **Python** libraries: `pandas`, `plotly.express`

### How to Run

1.  Open the **`RNA_Seq_Alignment_Workflow_using_STAR_(SRR11548957,_chr22).ipynb`** file in Google Colab or a Jupyter environment with a Python kernel.
2.  Execute all cells sequentially. The first four steps download the necessary data and executables.
3.  The final cells will output the statistical metrics and display the interactive Plotly visualization.

---

## 📁 Output Files

The pipeline generates the following key files in the `star_output/` directory:

| Filename | Format | Description |
| :--- | :--- | :--- |
| `SRR11548957_Aligned.sortedByCoord.out.bam` | BAM | The primary alignment file, sorted by genomic coordinate. |
| `SRR11548957_ReadsPerGene.out.tab` | TSV | Gene count matrix quantified using the provided GTF annotation. |
| `SRR11548957_Log.final.out` | Text | Detailed log of alignment metrics, used for quality control. |
