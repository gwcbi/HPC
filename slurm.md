## SLURM

Before running any jobs on the cluster, have a look at the <a href="https://colonialone.gwu.edu/">Colonial One wiki page</a>. Slurm (Simple Linux Utility for Resource Management) is Colonial One's cluster management and job scheduling system. This is the simplest way to run jobs.

### Slurm commands when logged in on Colonial One

`sbatch shell_file.sh`  
When executed in your home directory, sbatch submits a job to the cluster (see example below). The script will typically contain one or more srun commands to launch parallel tasks.

`squeue`  
Shows your jobs that are either running or in the queue.  It returns the following information: Job ID, Partition, Name, User, Time, and Nodes.  

`sinfo`  
Shows available and unavailable nodes on the cluster according to partition (i.e., 64gb, 128gb, etc.) It has a wide variety of filtering, sorting, and formatting options.  
The nodes that you can use are:
+ defq: This is the default queue. It has 64, 128 or 256GB nodes and a 14 day time limit
+ short: 128GB nodes, 2 day time limit
+ debug: 128GB, 2 hour time limit, for interactive jobs or quick tests
+ 2tb: for special requests

`salloc -N 1 -p short -t 300`  
Typically this is used to allocate resources for a job and spawn a shell. The shell is then used to execute srun commands to launch parallel tasks. Use this when you are [running interactive jobs](interactive_jobs.md) on Colonial One.

Before you can use the node that has been allocated to you, you must first ssh into it. First use `squeue` to find out which node has been allocated to you. Then, if node121 has been allocated, run the command `ssh node121` to get into the node. When you are finished running things on a node, type the command `exit` to return to the login node.

`srun`  
This is used to submit a job for execution or initiate job steps in real time. srun has a wide variety of options to specify resource requirements, including: minimum and maximum node count, processor count, specific nodes to use or not use, and specific node characteristics (so much memory, disk space, certain required features, etc.). A job can contain multiple job steps executing sequentially or in parallel on independent or shared resources within the job's node allocation.

`scancel job_id`  
This cancels a job that is in the queue or running on the cluster.  You can get the job id by executing `squeue` when logged in on the cluster.  

### Example Slurm shell script
The text below is saved in a text file ending in .sh (i.e., a shell script).  The shell script contains the commands for the cluster to execute.

```
#!/bin/bash
#SBATCH -J insert-name-for-job
#SBATCH -o insert-name-for-std-output.out
#SBATCH -e insert-name-for-std-error.err
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
9. `module load` loads any [modules](modules.md) you need to perform tasks on the cluster.  In order to see what modules are on the cluster, you can log into the cluster and execute `module avail` in the terminal.  A list will appear and just copy and paste the name of the module after `module load`.  You can load as many modules as needed.  
**NOTE:** You can request cores instead of nodes, although I don't think it works on Colonial One. To select cores and not an entire node, remove `-n 16` from the shell script and add `-c 6` and `--mem-per-cpu=5333`. Here `-c` requests the number of cores, while `--mem-per-cpu` allocates an amount of memory (Mb) per cpu.   


If you need to run multiple small similar jobs at the same time, you can use a [Slurm array](https://slurm.schedmd.com/job_array.html).

`ls *string | sort`  
Lists all the files in a directory containing the specified string and then sorts them alphabetically.  I typically use this to generate slurm array file lists to process fastqs (need to add `> file_name` to save the list to a file.  I also use the command with `| cat *string > file_name` to concatenate fastq files for genome/transcriptome assemblies.  


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
