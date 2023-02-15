# Using custom parameters in nf-core pipelines

In order to add custom parameters to nf-core pipeline you can create a
new custom.config file. For instance you would like to add
`--alignEndsProtrude 100 ConcordantPair`

    nextflow run nf-core/rnaseq -profile uppmax -r 3.4 --clip_r1 10 --clip_r2 10 --save_trimmed --save_align_intermeds --skip_markduplicates \
    --input Samples_read_Bulk.csv \
    --outdir nf_core_3.4_20211103 \
    --multiqc_title Project_111 \
    --fasta genome.fa \
    --gtf annotation.gtf \
    --project snic2021-22-505 \
    --aligner star_salmon \
    -c star_align.config
# Errors 
## check_samplesheet.py
```
-[nf-core/rnaseq] Pipeline completed with errors-

Error executing process > 'NFCORE_RNASEQ:RNASEQ:INPUT_CHECK:SAMPLESHEET_CHECK (Samples_read_test.csv)'

Caused by:
  Process `NFCORE_RNASEQ:RNASEQ:INPUT_CHECK:SAMPLESHEET_CHECK (Samples_read_test.csv)` terminated with an error exit status (255)

Command executed:

  check_samplesheet.py \
      Samples_read_test.csv \
      samplesheet.valid.csv
  
  cat <<-END_VERSIONS > versions.yml
  SAMPLESHEET_CHECK:
      python: $(python --version | sed 's/Python //g')
  END_VERSIONS

Command exit status:
  255

Command output:
  (empty)

Command error:
  INFO:    Environment variable SINGULARITYENV_TMPDIR is set, but APPTAINERENV_TMPDIR is preferred
  INFO:    Environment variable SINGULARITYENV_NXF_DEBUG is set, but APPTAINERENV_NXF_DEBUG is preferred
  INFO:    Environment variable SINGULARITYENV_SNIC_TMP is set, but APPTAINERENV_SNIC_TMP is preferred
  FATAL:   container creation failed: mount hook function failure: mount /proc/self/fd/3->/var/apptainer/mnt/session/rootfs error: while mounting image /proc/self/fd/3: kernel reported a bad superblock for squashfs image partition, possible causes are that your kernel doesn't support the compression algorithm or the image is corrupted

Work dir:
  /crex/proj/snic2021-23-602/private/SMS_6425_23_scRNA_Inhibitory_Efferents_Lateral_Line/code/work/d8/5549925221bc756bc88650c45a04e8

Tip: view the complete command output by changing to the process work dir and entering the command `cat .command.out```

You can fix it by setting `NXF_HOME` env. variable to path that you are running the pipeline. By default `NXF_HOME` is set to home directory.  
