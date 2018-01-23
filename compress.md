## Compressing files

In Bioinformatics, you often work with very big files. Because of this, programs will often compress them (also called zipping) so they are easier to work with. You can tell that a file is compressed because it will have a `.gz` at the end of a filename.


`zcat myreads.fastq.gz | head` will allow you to inspect the first few lines of a zipped .fastq file.

`zcat myreads.fastq.gz | wc -l` will tell you the number of lines in a zipped .fastq.gz file.

`zless myreads.fastq.gz` will let you browse through a document one line at a time using the spacebar to go forward and `b` to go back a page.

`zcat myreads.fastq.gz | head -400000 | gzip > Test100k.fastq.gz` will make a new file Test100k with just the firsth 400000 lines of myreads.
