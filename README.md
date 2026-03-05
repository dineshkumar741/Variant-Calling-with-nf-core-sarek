# Variant-Calling-with-nf-core/sarek

This repository demonstrates the usage of the nf-core/sarek workflow developed and maintained by the nf-core community.

Workflow source:
https://github.com/nf-core/sarek

This repository contains configuration files, samplesheet and execution scripts used to run the nf-core/sarek pipeline for variant discovery.


Command-1 : full structural variant/CNV/deletions/duplications/HaplotypeCaller

1. nextflow run nf-core/sarek     -r 3.5.1     -profile docker     -c local_resources.config     --input samplesheet.csv     --outdir ./sarek_results     --genome GATK.GRCh38     --tools haplotypecaller,manta,cnvkit     -resume

Command-2: It bypasses the GATK filter especially for synthtic datasets.

2. nextflow run nf-core/sarek   -r 3.5.1   -profile docker   -c local_resources.config   --input samplesheet.csv   --outdir results   --genome GATK.GRCh38   --tools haplotypecaller,vep   --skip_tools haplotypecaller_filter   --max_cpus 12   -resume

SAREK Pipeline requires the preparation samplesheet.csv based on the fastq files in gz format i.e. 

XY001_S1_L001_R1_001.fastq.gz & XY001_S1_L001_R2_001.fastq.gz


