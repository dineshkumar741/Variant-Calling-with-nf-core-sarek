# Variant-Calling-with-nf-core/sarek

This repository demonstrates the usage of the nf-core/sarek workflow developed and
maintained by the nf-core community.

Workflow source:
https://github.com/nf-core/sarek

This repository contains configuration files, sample metadata, and execution scripts used to run the nf-core/sarek pipeline for variant discovery.

# Command to run in the terminal for normal sarek pipeline.

nextflow run nf-core/sarek     -r 3.5.1     -profile docker     -c local_resources.config     --input samplesheet.csv     --outdir ./sarek_results     --genome GATK.GRCh38     --tools haplotypecaller,manta,cnvkit     -resume

cat .nextflow.log

nextflow log

echo "patient,sample,lane,fastq_1,fastq_2" > samplesheet.csv
 
for f in /home/ricky/Nexflow/red/Sample_*/*_R1_*.fastq.gz; do     SNAME=$(basename $(dirname $f));     R2=${f/_R1_/_R2_};     echo "$SNAME,$SNAME,lane_1,$f,$R2" >> samplesheet.csv; done

1. Start by writing the header
   
echo "patient,sample,lane,fastq_1,fastq_2" > samplesheet.csv

2. Loop through every R1 file in your subdirectories

This finds files like: /home/ricky/Nexflow/red/Sample_2A1/2A1_R1.fastq.gz

for f1 in /home/ricky/Nexflow/red/Sample_*/*_R1_*.fastq.gz; do     

SAMPLE_ID=$(basename $(dirname "$f1"))

f2=${f1/_R1_/_R2_}

LANE_ID=$(basename "$f1" .fastq.gz)

echo "$SAMPLE_ID,$SAMPLE_ID,$LANE_ID,$f1,$f2" >> samplesheet.csv; done

for f1 in /home/ricky/Nexflow/red/Sample_*/*_R1_*.fastq.gz; do          SAMPLE_ID=$(basename $(dirname "$f1"))    ;     f2=${f1/_R1_/_R2_}    ;     LANE_ID=$(basename "$f1" .fastq.gz);     echo "$SAMPLE_ID,$SAMPLE_ID,$LANE_ID,$f1,$f2" >> samplesheet.csv; done

echo "patient,sample,lane,fastq_1,fastq_2" > samplesheet.csv

for f1 in /home/ricky/Nexflow/red/**/*_R1_001.fastq.gz; do     f2=${f1/_R1_001.fastq.gz/_R2_001.fastq.gz};     ID=$(basename $f1 | cut -d_ -f1);     echo "$ID,$ID,L001,$f1,$f2" >> samplesheet.csv; done

shopt -s globstar

echo "patient,sample,lane,fastq_1,fastq_2" > samplesheet.csv

for f1 in /home/ricky/Nexflow/red/**/*_R1_001.fastq.gz; do

 [ -e "$f1" ] || continue

 f2=${f1/_R1_001.fastq.gz/_R2_001.fastq.gz}    

 FILENAME=$(basename "$f1");     ID=${FILENAME%%_*}    

 echo "$ID,$ID,L001,$f1,$f2" >> samplesheet.csv; done

head -n 5 samplesheet_1.csv

what is this command; samtools flagstat /results/align/XY006-AGRF.bam and this one: samtools flagstat XY007-AGRF.bam




# Final command
nextflow run nf-core/sarek   -r 3.5.1   -profile docker   -c local_resources.config   --input samplesheet.csv   --outdir results   --genome GATK.GRCh38   --tools haplotypecaller,vep   --skip_tools haplotypecaller_filter   --max_cpus 12   -resume



