# sbx_WGS (Whole Genome Sequencing)

## Introduction

sbx_WGS is an extension for the sunbeam pipeline for de novo microbial genome assembly and quality assessment. This pipeline uses SPAdes for single genome assembly and CheckM, QUAST, and Read map coverage of the assembled genome for quality assessment (sbx_SPARCQ.rules). In addition, it uses anvi'o for contamination assessment and taxonomic assignment with single copy genes, amongst other things (sbx_SCG.rules). An R markdown template has been provided that will nicely display the results generated from this pipeline. Illumina reads are provided for testing.

### Installation
1. Add packages in sbx_SPARCQ_env.yml to sunbeam environment.yml and install with your sunbeam's ./install.sh --update env
2. If you cannot install it in step #1, use a combination of conda and pip:
```
conda activate sunbeam
conda install -c conda-forge bedtools spades checkm-genome ncbi-genome-download
pip install quast
(If installed this way, may need to change quast to quast.py in sbx_SPARCQ.rules)
```
3. Add config.yml to sunbeam_config.yml
```
cat config.yml >> /path/to/sunbeam_config.yml
```
4. Recommended for cluster: add the memory specifications in cluster.json, especially for checkm_tree rule

## Options for config.yml
threads (SPAdes, BWA, samtools, anvio): # of threads to use for running programs

checkm_yml (optional): YAML file containing a sample:rank and sample:taxon dictionary for CheckM parameters (see example);
rank is one of {life,domain,phylum,class,order,family,genus,species};
taxon is the taxonomic classification for the specified 'rank'

taxid_yml (optional): YAML file containing a sample:TaxonID dictionary for reference genomes to be downloaded by ncbi-genome-download for comparison in QUAST

window_size (Read mapping): define the window size to do sliding window coverage

sampling (read mapping): define minimum length of the contig to slide over

## Contributors
This extension was adapted from pipelines written by Scott Daniel, Jung-Jin Lee, Ceylan Tanes, and Louis Taylor. Spades rules were adapted from sbx_spades (https://github.com/sunbeam-labs/sbx_spades). Read mapping rules were adapted from the sunbeam pipeline (https://github.com/sunbeam-labs/sunbeam/tree/stable/rules/mapping) and sbx_mapping_withFilter (https://github.com/ctanes/sbx_mapping_withFilter). Anvio rules were adapted from anvio_pan (https://github.com/junglee0713/anvio_pan)
