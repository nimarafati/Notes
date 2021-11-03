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
