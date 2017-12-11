# BASH Commands

Here are some BASH commands

The following are bits of code that primarily serve as teaching tools and reminders.

## Helpful bash commands  

`man bash_command`  
Although I give examples of commands below with a short description, this only scratches the surface of what they can do.  If you have questions regarding a command, you should always check the man pages about the command.  These pages provide the full documentation for all bash commands.  If there are still questions after viewing the man pages, there is always <a href="http://www.google.com">Google</a> and <a href="http://stackoverflow.com/">stackoverflow</a>.  

`cd`  
Executed by itself will bring you to your home directory, while adding a path after cd will bring you to that directory.  

`cd ..`  
Changes directory to one-up the directory hierarchy  

`cp file_name path_to_new_directory`  
Copies a file from you current directory and places in a different directory.  

`mv file_name path_to_new_directory`  
Does the same thing as cp, but does not make a copy and just moves the file.  

`head file_name`  
Prints the first few lines of a file. Add -n # after the file name and it will return the specified number of lines starting from the top of the file.  

`tail file_name`  
Same as head command, but prints the last few lines of the file. You can also include the -n # to specify the number of lines to return.  

`pwd`  
Returns the path to the current directory.  

`cat file_name | grep -c "string"`  
Opens a file and then searches to file to count the occurrences of a string.  

`cat file_name | grep 'string'`  
Instead of counting, this searches a file for a particular string.  

`ls`  
Lists the files and directories in the current directory.  

`ls -s`  
Adding `-s` lists the files and directories, but also includes sizes.  

`ls -d */`  
Lists only the directories in the current directory.  

`ls | grep -c 'string'`  
Lists all files in a directory and then returns only those with a particular string.  

`ls *string | sort`  
Lists all the files in a directory containing the specified string and then sorts them alphabetically.  I typically use this to generate slurm array file lists to process fastqs (need to add `> file_name` to save the list to a file.  I also use the command with `| cat *string > file_name` to concatenate fastq files for genome/transcriptome assemblies.  

`history`  
Returns the last hundred or so commands issued.  

`history | grep 'string'`  
I usually combine history with grep to look for specific commands that I previously executed.  

`rm file_name`  
Delete a file  

`cat file_name | grep -Anumber 'string'`  
Searches a file for a string and returns the line with the string AND number lines after the string.  

```
    for FILE in *file_ending; do
        mv -v "$FILE"  
        "${FILE//string_to_replace/new_string}";
    done
```
Loops through the current directory files with file_ending, changes string_to_replace to new_string.  

`cat list_of_commands.txt | xargs -I cmd --max-procs=2 bash -c cmd &`  
This one-liner runs a list of commands in parallel.  The list of commands can be generated using the for loop above and writing them to a file, one per line. Also note that you can use <a href="http://www.gnu.org/software/parallel/">GNU Parallel</a>  

```
ls *.fa | xargs -I file -n 1 -P 2 /Applications/muscle3.8.31_i86darwin64 -in file -out file.aln  
```

Similar to the one-liner above, this one takes all of the fasta files in a directory and estimates an alignment for two at a time (i.e., '-P 2').  Note you don't have to add '$' to the variable 'file' coming through the pipe.  In addition, xargs can handle adding strings with no additional command (e.g., '-out file.aln' just adds '.aln' to the end of the file name)

### Download .sra file from <a href="http://www.ncbi.nlm.nih.gov/sra">NCBI SRA database</a> using the bash and extract the .fastq files from it using <a href="https://github.com/ncbi/sra-tools">SRA-tools</a>  

1) Get the web address to the .sra file  
2) Download the file to a local directory on your personal computer or HPC:  
`curl /web/address/to/sra/file/name_of_sra_file --output /path/where/you/want/.sra/file/to/live/name_of_sra_file`  
3) Extract .fastq files from .sra file:  
`/path/to/binary/fastq-dump.2.3.3-3 --split-files name_of_sra_file`

### Example Slurm shell script
Before running any jobs on the cluster, have a look at the <a href="https://colonialone.gwu.edu/">Colonial One wiki page</a>.

The text below is saved in a text file ending in .sh (i.e., a shell script).  The shell script contains the commands for the cluster to execute.

```
#!/bin/bash
#SBATCH -J insert-name-for-job
#SBATCH -o insert-name-for-std-output
#SBATCH -e insert-name-for-std-error
#SBATCH -p defq
#SBATCH -n 16
#SBATCH -t 2-00:00:00
#SBATCH --mail-type=ALL
#SBATCH --mail-user=insert-email-address

module load module_name
module load module_name

commands to perform on the cluster  
```

#### Explanation of the Slurm shell commands above:  

1. `-J` is the name of the Slurm job.  You can call it anything you want.
2. `-o` is the name of the std output file.
3. `-e` is the name of the std error file.
4. `-p` is the partition.  `defq` means the first available, but you can request specific memory nodes.  For example, you have the option of selecting the following memory nodes: `128gb` and `256gb`.  Simply replace `defq` with either one of those.  Jobs can run for up to 14 days, but if you know your job will be less than 2 days, you can request the partition `short`, which is 64gb node.
5. `-n` is the number of cores.  Each one of the nodes on the cluster contains 16 cores.  Therefore, if you want one node, request `-n 16`; two nodes, request `-n 32`, etc.
6. `-t` is the requested wall time for the job.  If your job takes longer than the requested time, it will FAIL and you will have to re-run it.  The format to request wall time is Days-Hours:Minutes:Seconds.  You do not need to use the days and you can simply request time using Hours:Minutes:Seconds.
7. `--mail-type` determines which emails you receive.  `ALL` means you receive an email when your job begins, ends, and/or fails.  You have the following options: `BEGIN`, `END`, or `FAIL`.  If I submit a large array job, I usually choose `FAIL` so I don't clog my inbox with Slurm emails.
8. `--mail-user` is the email address where job notifications are sent.
9. `module load` loads any modules you need to perform tasks on the cluster.  In order to see what modules are on the cluster, you can log into the cluster and execute `module avail` in the terminal.  A list will appear and just copy and past the name of the module after `module load`.  You can load as many modules as needed.  
**NOTE:** You can request cores instead of nodes, although I don't think it works on Colonial One. To select cores and not an entire node, remove `-n 16` from the shell script and add `-c 6` and `--mem-per-cpu=5333`. Here `-c` requests the number of cores, while `--mem-per-cpu` allocates an amount of memory (Mb) per cpu.   

### Slurm commands when logged in on the cluster  

`sbatch shell_file`  
When executed in your home directory, this submits a job to the cluster.  
`squeue`  
Shows your jobs that are either running or in the queue.  It returns the following information: Job ID, Partition, Name, User, Time, and Nodes.  
`scancel job_id`  
This cancels a job that is in the queue or running on the cluster.  You can get the job id by executing `squeue` when logged in on the cluster.  
`sinfo`  
Shows available and unavailable nodes on the cluster according to partition (i.e., 64gb, 128gb, etc.)

### Example Slurm array shell script

```
#!/bin/bash
#SBATCH -J garli_cicadidae_noambig
#SBATCH -o garli_cicadidae_noambig_out_%A_%a.out
#SBATCH -e garli_cicadidae_noambig_err_%A_%a.err
#The next line tells slurm this is an array that will submit 149 garli jobs across the cluster
#SBATCH --array=1-149
#SBATCH --nodes=1
#SBATCH -t 3-00:00:00
#SBATCH --mail-type=FAIL
#SBATCH --mail-user=add email address here

# move to the directory where the data files locate
cd /home/garli/garli_cicadidae_noambig

# the next line processes a text file with garli configs 1 per line and uses them as input
name1=$(sed -n "$SLURM_ARRAY_TASK_ID"p transcripts_hemip_files1.txt)

/groups/cbi/garli-2.01/bin/Garli-2.01 $name1
```

### Example SGE array shell file

```
#!/bin/bash
# ---------------------------
#$ -S /bin/bash
# job name
#$ -N FF1b_beast2
# The next line says to run an array of 100 jobs
#$ -t 1-100
# email
#$ -M add email address here
# -m be
#
# output file
#$ -o /home/beast/out-$JOB_ID-$TASK_ID
# error file
#$ -e /home/beast/err-$JOB_ID-$TASK_ID
#

cd /home/beast/
#$ -cwd

module load beast/2.1.2

# The next line processes a text file of beast xml files 1 per line to use as input
INFILE=$(sed -n "$SGE_TASK_ID"p my_file_list.txt)

# Generate the output file name by using search and replace in the input file name
OUTFILE=${INFILE/.xml/.result}

#Run Beast
beast $INFILE > $OUTFILE
```

## Make a REVEAL.js presentation from a jupyter notebook  
I am starting to get in the habit of using jupyter notebooks to work on code, but also to render html presentations. Doing it this way saves a TON of time and limits having to use PowerPoint (ugh!). Also, if you keep your presentations in a git repo, they are always available. The main driver behind this is [Reveal.js](http://lab.hakim.se/reveal-js/#/), which is the open source software behind rendering html presentations. I only know little bits of html, but jupyter notebooks have a function to convert the notebook to a html reveal presentation. Here are the main steps:  
1. Make sure each slide is marked in the notebook. Start by clicking to View->Cell Toolbar->Slideshow. This will show a *Slide Type* dropdown menu in every cell. If the cell contains a slide you want in the presentation, click *Slide* from the dropdown menu.  
2. To conver your presentation to html execute the following line in the terminal: `jupyter-nbconvert --to slides <jupyter_notebook_name> --reveal-prefix=<path/to/reveal.js/dir>`

## Download large files from a server 
Sometimes I have to download large HiSeq runs (GBs to TBs) from a remote server. Below are the commands I give via the terminal using [GNU Screen](https://www.gnu.org/software/screen/) and [Linux scp](https://linux.die.net/man/1/scp). In the past I have also used [Globus](https://www.globus.org). Globus is a pay service that has a GUI interface (and command line) and many universities pay to have access.  
1. SSH into your remote server  
2. Begin a screen session by typing `screen -S <session name>`  
3. Execute scp command `scp -P<port#> <wanted_file> <usr_name>@<local_ip_address>:/local/directory/path`  
4. Once the file(s) starts downloading, detach the screen by pressing `Ctrl` + `a` then `d`  
5. Log off of the SSH session  

To re-attach the screen, log back into the server (step 1) and type `screen -r <session name>`  

## Delete large (GBs to TBs) directories fast  
Occasionally I need to delete VERY large direcoties in my file system (local or HPC). I usually use `rm` to remove files (e.g., `rm <file_name>`) and directories (e.g., `rm -rf <directory>`), but it is exceptionally slow for large directories. I recently found a workaround on [Stack Exchange](http://unix.stackexchange.com/questions/37329/efficiently-delete-large-directory-containing-thousands-of-files) that significantly speeds up the process.  
1. Make an empty directory in the terminal `mkdir <directory_name>`  
2. rsync -a --delete <empty_directory> <directory_to_delete>  

## Git commands
These command assume you have created a git repo on <a href="https://bitbucket.org/">Bitbucket</a> and initiated it locally on your personal computer (`git init`).  
1. The first thing I do when I begin working on a repo at the start of the day, I pull the most recent version and sync it with my current version by executing `git pull` from the local repo directory.  You can also see if you local repo is up-to-date by executing `git status`.  
2. To add a file to the repository, put it in the local repo directory and execute `git add file_name`.  
3. Next, you need to commit the file by executing `git commit -m "info_about_the_commit"` The information should convey the status of the committed script.  
4. Lastly, the file should be pushed to the remote repo on Bitbucket by executing `git push`.

## Helpful python snippets  

Read file by line  

```
with open('file_name.txt') as f:
    for line in f:
        do something with line  
```

Read file by line and look for lines that start with '>'  

```
with open('file_name.txt') as f:
    for line in f:
        if line.startswith('>'):
            do something with line
```

Read tab-delimited file by line; split each line by tabs; add column 2 element to a list  

```
column2_list = []#empty list to store column 2 elements
with open('file_name.txt') as f:
    for line in f:
        elements = line.split('\t')
        wanted_element = elements[1]#python uses zero-based counting so element 2 is actually 1
        column2_list.append(wanted_element)
```

Loop through fasta files in a directory with a file ending of ".fa"  

```
import glob  
for fasta_file in glob.glob("*.fa"):
    do something with fasta file
```

An example of spawning multiple processes across computer cores using the python <a href="https://docs.python.org/2/library/multiprocessing.html">Multiprocessing Module</a>. The example below aligns multiple fastas in a directory spawning a number of processes equal to the number of cores in the computer.  

```  
import multiprocessing  
import os  
import time  

def get_files(dir_path, file_ending):
    '''get the files in a directory with a particular ending and put them in a list'''
    file_list = [f for f in os.listdir(dir_path) if f.endswith(file_ending)]
    return file_list

def run_muscle(x):
    '''runs an alignment throught muscle'''
    outfile = x[:-3] + '_aligned.fa'
    command = '/Applications/muscle3.8.31_i86darwin64 -in %s -out %s' % (x, outfile)
    os.system(command)

def start_process():
    print 'Starting', multiprocessing.current_process().name

start = time.time()
#Get the fasta files in the directory
fastas = get_files('/Users/owen/Documents/python/tmp', '.fa')
#Make the Pool of workers based on my number of cores
pool_size = multiprocessing.cpu_count()
pool = multiprocessing.Pool(processes=pool_size, initializer=start_process)
pool.map(run_muscle, fastas)
pool.close()
pool.join()
print 'It took', time.time() - start, 'seconds'
```  

Retrieves taxonomic ranks for a given NCBI taxon id and writes it to a single line. The taxon ids need to be in a separate file, one per line. The script can be executed by typing:  

`python script_name file_with_taxon_ids.txt outfile_name`  

```
import sys
import csv
import time
from Bio import Entrez

infile = sys.argv[1]
output_csv = sys.argv[2]

def get_tax_data(taxid):
    """once we have the taxid, we can fetch the record"""
    search = Entrez.efetch(id = taxid, db = "taxonomy", retmode = "xml")
    return Entrez.read(search)

start = time.time()
bacteria_taxonomy = open(output_csv, 'w')
header = ['superkingdom', 'kingdom', 'phylum', 'class', 'order', 'suborder', 'family', 'subfamily', 'genus', 'subgenus', 'species', 'no rank']#change these based on line 22
w = csv.writer(bacteria_taxonomy)
w.writerow(header)
Entrez.email = "you@email.com"#enter your email address here
if not Entrez.email:
    print "you must add your email address"
    sys.exit(2)
lines = open(infile).read().splitlines()
counter = 0
for line in lines:
     print counter, line
     search = Entrez.efetch(id = str(line), db = "taxonomy", retmode = "xml")
     data = Entrez.read(search)
     lineage = {d['Rank']:d['ScientificName'] for d in data[0]['LineageEx'] if d['Rank'] in ['superkingdom','kingdom','phylum','class','order','suborder','family','subfamily','genus','subgenus','species', 'no rank']}
     line = []
     ranks = ['superkingdom', 'kingdom', 'phylum', 'class', 'order', 'suborder', 'family', 'subfamily', 'genus', 'subgenus', 'species', 'no rank']
     for r in ranks:
         if r in lineage:
             line.append(lineage[r])
         else:
             line.append('NA')
    w.writerow(line)
    time.sleep(2)
    counter+=1
bacteria_taxonomy.close()
print 'It took', time.time()-start, 'seconds'
```

For an introduction to string slicing and lists go <a href="https://docs.python.org/2/tutorial/introduction.html">here</a>
