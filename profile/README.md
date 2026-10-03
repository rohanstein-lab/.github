# rohanstein-lab

Bioinformatics and computational genomics work by [@rohanstein](https://github.com/rohanstein),
focused on cyanobacterial genomes, protein function discovery and phage / mobile-genetic-element
analysis.

## KUAC 3056 Novel Protein Discovery Pipeline

*Private repository until publication; reviewer access on request.*

An end-to-end pipeline that goes from raw Illumina reads of a non-axenic cyanobacterial culture
to a ranked set of functionally uncharacterized ("hypothetical") proteins, combining
sequence-based homology search with independent, cross-validated protein structure prediction.

**Genome assembly and annotation**
- Read QC (fastp), de novo assembly (SPAdes), metagenomic binning to separate the target genome
  from co-cultured organisms (MaxBin2), completeness and contamination checks (CheckM2),
  taxonomic classification (Kraken2), annotation (DFAST), 16S identity check (Barrnap, BLASTn)
- AMR screening (AMRFinderPlus) and biosynthetic gene cluster prediction (antiSMASH)

**Hypothetical-protein discovery**
- Three independent sequence-based lines of evidence: protein language model embeddings (ESM2,
  calibrated against positive and shuffled negative controls), BLASTP against Swiss-Prot and
  TrEMBL, and profile HMM search against Pfam (HMMER)
- Consensus tiering that rewards cross-method agreement, compiled into a colour-coded workbook
- Structure prediction with two independent methods (ESMFold2, and ColabFold/AlphaFold2 run on an
  HPC cluster), structural homology search against PDB and AlphaFold databases (Foldseek), and
  direct TM-score cross-validation between the two methods (US-align)
- Identification of proteins with no sequence-level homology that are recovered by structure, and
  of candidates for genuinely novel folds

**Phage / mobile-genetic-element branch**
- Virus, provirus and plasmid detection (geNomad), viral genome quality (CheckV), phage gene
  annotation (Pharokka), AMR, stress and virulence screening (AMRFinderPlus, VFDB)
- Every hit labelled by organism of origin in the mixed culture, and resistance/virulence genes
  linked to any phage or plasmid contig they sit on or near

**Engineering practice**
- Modular, documented scripts (Bash and Python) with explicit inputs and outputs, written for
  conversion to Nextflow
- Pinned tool and database versions recorded in each module's output
- HPC batch execution (PBS) for GPU structure prediction

## Access

The repository is private while the associated manuscript is in preparation. Reviewers (for
example, prospective employers) can be given read-only access: please get in touch with your
GitHub username.
