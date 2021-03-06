## General format for command-line trimmomatic

### trim paired-end reads by resulting read length

`forward_read.fastq.gz reverse_read.fastq.gz cropped_forward_read_paired.fastq cropped_forward_read_unpaired.fastq cropped_reverse_read_paired.fastq cropped_reverse_read_unpaired.fastq CROP:275 MINLEN:175`

shows "paired end". read 1 file, read 2 file (inputs), then 4 output files: Read1 paired, read1 unpaired, read2 paired, read2 unpaired. CROP is length of resulting read. MINLEN is the minimum length of reads to keep

### trim by paired-end reads by quality using sliding window

`trimmomatic PE forward_read.fastq.gz reverse_read.fastq.gz trimmed_forward_read_paired.fastq trimmed_forward_read_unpaired.fastq trimmed_reverse_read_paired.fastq trimmed_reverse_read_unpaired.fastq  MINLEN:175 SLIDINGWINDOW:15:25`

same format, but rather than cropping, evaluating the phred quality score of 15 bases at a time with a quality cut-off of 25. 
