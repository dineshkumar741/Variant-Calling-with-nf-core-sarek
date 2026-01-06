# Variant-Calling-with-nf-core/sarek

This repository demonstrates the usage of the nf-core/sarek workflow developed and
maintained by the nf-core community.

Workflow source:
https://github.com/nf-core/sarek

This repository contains configuration files, sample metadata, and execution scripts
used to run the nf-core/sarek pipeline for variant discovery.
# Command to run in the terminal;
nextflow run nf-core/sarek     -r 3.5.1     -profile docker     -c local_resources.config     --input samplesheet.csv     --outdir ./sarek_results     --genome GATK.GRCh38     --tools haplotypecaller,manta,cnvkit     -resume

