# Samtools

### What are .sam and .bam files?

Files that end in .sam are called SAM files. Sequence Alignment Map (SAM) is a text-based format for storing biological sequences aligned to a reference sequence for storing data like nucleotide sequences.

SAM files can be converted into BAM (Binary Alignment/Map) files. BAM files are typically compressed and more efficient for software to work with than SAM. 

#### To convert

`samtools view sample.bam > sample.sam`
Convert a bam file into a sam file.

`samtools view -bS sample.sam > sample.bam`
Convert a sam file into a bam file. The -b option compresses or leaves compressed input data.
