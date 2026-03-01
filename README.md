# Variant-Calling-with-nf-core/sarek

This repository demonstrates the usage of the nf-core/sarek workflow developed and
maintained by the nf-core community.

Workflow source:
https://github.com/nf-core/sarek

This repository contains configuration files, sample metadata, and execution scripts
used to run the nf-core/sarek pipeline for variant discovery.
# Command to run in the terminal;
nextflow run nf-core/sarek     -r 3.5.1     -profile docker     -c local_resources.config     --input samplesheet.csv     --outdir ./sarek_results     --genome GATK.GRCh38     --tools haplotypecaller,manta,cnvkit     -resume

# cat .nextflow.log
# nextflow log
# echo "patient,sample,lane,fastq_1,fastq_2" > samplesheet.csv
# for f in /home/ricky/Nexflow/red/Sample_*/*_R1_*.fastq.gz; do     SNAME=$(basename $(dirname $f));     R2=${f/_R1_/_R2_};     echo "$SNAME,$SNAME,lane_1,$f,$R2" >> samplesheet.csv; done
# # 1. Start by writing the header
# echo "patient,sample,lane,fastq_1,fastq_2" > samplesheet.csv
# 2. Loop through every R1 file in your subdirectories
# This finds files like: /home/ricky/Nexflow/red/Sample_2A1/2A1_R1.fastq.gz
# for f1 in /home/ricky/Nexflow/red/Sample_*/*_R1_*.fastq.gz; do     
# SAMPLE_ID=$(basename $(dirname "$f1"))
#  f2=${f1/_R1_/_R2_}
# LANE_ID=$(basename "$f1" .fastq.gz)
# echo "$SAMPLE_ID,$SAMPLE_ID,$LANE_ID,$f1,$f2" >> samplesheet.csv; done
# for f1 in /home/ricky/Nexflow/red/Sample_*/*_R1_*.fastq.gz; do          SAMPLE_ID=$(basename $(dirname "$f1"))    ;     f2=${f1/_R1_/_R2_}    ;     LANE_ID=$(basename "$f1" .fastq.gz);     echo "$SAMPLE_ID,$SAMPLE_ID,$LANE_ID,$f1,$f2" >> samplesheet.csv; done
# echo "patient,sample,lane,fastq_1,fastq_2" > samplesheet.csv
# for f1 in /home/ricky/Nexflow/red/**/*_R1_001.fastq.gz; do     f2=${f1/_R1_001.fastq.gz/_R2_001.fastq.gz};     ID=$(basename $f1 | cut -d_ -f1);     echo "$ID,$ID,L001,$f1,$f2" >> samplesheet.csv; done
# shopt -s globstar
# echo "patient,sample,lane,fastq_1,fastq_2" > samplesheet.csv
# for f1 in /home/ricky/Nexflow/red/**/*_R1_001.fastq.gz; do
#   [ -e "$f1" ] || continue
# f2=${f1/_R1_001.fastq.gz/_R2_001.fastq.gz}    
# FILENAME=$(basename "$f1");     ID=${FILENAME%%_*}    
#  echo "$ID,$ID,L001,$f1,$f2" >> samplesheet.csv; done
# head -n 5 samplesheet_1.csv
# what is this command; samtools flagstat /results/align/XY006-AGRF.bam and this one: samtools flagstat XY007-AGRF.bam


-[nf-core/sarek] Pipeline completed with errors-
ERROR ~ Error executing process > 'NFCORE_SAREK:SAREK:FASTQ_ALIGN_BWAMEM_MEM2_DRAGMAP_SENTIEON:BWAMEM1_MEM (SampleName)'

Caused by:
  Process requirement exceeds available CPUs -- req: 24; avail: 12


Command executed:

  INDEX=`find -L ./ -name "*.amb" | sed 's/\.amb$//'`
  
  bwa mem \
      -K 100000000 -Y -R "@RG\tID:null.SampleName.L001\tPU:L001\tSM:SampleName_SampleName\tLB:SampleName\tDS:s3://ngi-igenomes/igenomes//Homo_sapiens/GATK/GRCh38/Sequence/WholeGenomeFasta/Homo_sapiens_assembly38.fasta\tPL:ILLUMINA" \
      -t 24 \
      $INDEX \
      0004.SampleName-L001_1.fastp.fastq.gz 0004.SampleName-L001_2.fastp.fastq.gz \
      | samtools sort   --threads 24 -o SampleName.0004.bam -
  
  cat <<-END_VERSIONS > versions.yml
  "NFCORE_SAREK:SAREK:FASTQ_ALIGN_BWAMEM_MEM2_DRAGMAP_SENTIEON:BWAMEM1_MEM":
      bwa: $(echo $(bwa 2>&1) | sed 's/^.*Version: //; s/Contact:.*$//')
      samtools: $(echo $(samtools --version 2>&1) | sed 's/^.*samtools //; s/Using.*$//')
  END_VERSIONS

Command exit status:
  -

Command output:
  (empty)

Work dir:
  /home/ricky/Desktop/work/ec/278956150d57d5068837a5815553df

Container:
  quay.io/biocontainers/mulled-v2-fe8faa35dbf6dc65a0f7f5d4ea12e31a79f73e40:1bd8542a8a0b42e0981337910954371d0230828e-0

Tip: view the complete command output by changing to the process work dir and entering the command `cat .command.out`

 -- Check '.nextflow.log' file for details
ERROR ~ Pipeline failed. Please refer to troubleshooting docs: https://nf-co.re/docs/usage/troubleshooting

 -- Check '.nextflow.log' file for details








Plus 21 more processes waiting for tasks…
Execution cancelled -- Finishing pending tasks before exit
-[nf-core/sarek] Pipeline completed with errors-
ERROR ~ Error executing process > 'NFCORE_SAREK:SAREK:VCF_ANNOTATE_ALL:VCF_ANNOTATE_ENSEMBLVEP:ENSEMBLVEP_VEP (SampleName)'

Caused by:
  Process requirement exceeds available memory -- req: 36 GB; avail: 31.3 GB


Command executed:

  vep \
      -i SampleName.haplotypecaller.vcf.gz \
      -o SampleName.haplotypecaller_VEP.ann.vcf.gz \
      --stats_file SampleName.haplotypecaller_VEP.ann.summary.html      --vcf --everything --filter_common --per_gene --total_length --offline --format vcf \
      --compress_output bgzip \
       \
      --assembly GRCh38 \
      --species homo_sapiens \
      --cache \
      --cache_version 113 \
      --dir_cache ${PWD}/113_GRCh38 \
      --fork 6
  
  
  cat <<-END_VERSIONS > versions.yml
  "NFCORE_SAREK:SAREK:VCF_ANNOTATE_ALL:VCF_ANNOTATE_ENSEMBLVEP:ENSEMBLVEP_VEP":
      ensemblvep: $( echo $(vep --help 2>&1) | sed 's/^.*Versions:.*ensembl-vep : //;s/ .*$//')
  END_VERSIONS

Command exit status:
  -

Command output:
  (empty)

Work dir:
  /home/ricky/Desktop/work/1e/a517f4e62e58fcb82dfff539ac8c3f

Container:
  quay.io/biocontainers/ensembl-vep:113.0--pl5321h2a3209d_0

Tip: you can replicate the issue by changing to the process work dir and entering the command `bash .command.run`

 -- Check '.nextflow.log' file for details
ERROR ~ Pipeline failed. Please refer to troubleshooting docs: https://nf-co.re/docs/usage/troubleshooting

 -- Check '.nextflow.log' file for details





# Final command
nextflow run nf-core/sarek   -r 3.5.1   -profile docker   -c local_resources.config   --input samplesheet.csv   --outdir results   --genome GATK.GRCh38   --tools haplotypecaller,vep   --skip_tools haplotypecaller_filter   --max_cpus 12   -resume


# Final 'local_resources.config' file
// local_resources.config
process {
    // Using '.*' ensures it hits the process even inside subworkflows
    withName: '.*:BWAMEM1_MEM' {
        cpus = 12
        memory = '16 GB'
    }
    withName: '.*:BWAMEM2_MEM' {
        cpus = 12
        memory = '16 GB'
    }
    withName: '.*:GATK4_HAPLOTYPECALLER' {
        cpus = 4
        memory = '12 GB' 
    }
    withName: '.*:CNVKIT_BATCH' {
        cpus = 2
        memory = '12 GB'
    }
    withName: '.*:ENSEMBLVEP_VEP' {
        cpus = 4
        memory = '12 GB'
        // We add this to stop VEP from trying to use too many internal threads
        ext.args = '--fork 4'
    }
}

