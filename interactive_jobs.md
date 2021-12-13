# Running interactive jobs on ColonialOne

Make sure you are reading and writing to lustre for your interactive jobs!

### 1. Check what nodes are available

```bash
[bendall@login3 ~]$ sinfo
PARTITION    AVAIL  TIMELIMIT  NODES  STATE NODELIST
defq*           up 14-00:00:0    109  alloc node[033-049,051,053-062,064-070,074-078,080-098,101-109,111-116,118-119,121-127,129-137,139-142,146-153,155-157,159-160]
defq*           up 14-00:00:0     19   idle node[050,052,063,071-073,079,099-100,110,117,120,128,138,143-145,154,158]
short           up 2-00:00:00     75  alloc node[097-098,101-109,111-116,118-119,121-127,129-137,139-142,146-153,155-157,159-161,163-173,176-177,179-183,185,187-188,190]
short           up 2-00:00:00     20   idle node[099-100,110,117,120,128,138,143-145,154,158,162,174-175,178,184,186,189,191]
128gb           up 14-00:00:0     21  alloc node[041-049,051,053-062,064]
128gb           up 14-00:00:0      3   idle node[050,052,063]
256gb           up 14-00:00:0      8  alloc node[033-040]
2tb             up 14-00:00:0      1  alloc node901
gpu             up 7-00:00:00     11  alloc node[008-009,015-016,021-025,030,032]
gpu             up 7-00:00:00     21   idle node[001-007,010-014,017-020,026-029,031]
gpu-noecc       up 7-00:00:00     11  alloc node[008-009,015-016,021-025,030,032]
gpu-noecc       up 7-00:00:00     21   idle node[001-007,010-014,017-020,026-029,031]
ivygpu          up 7-00:00:00     19  alloc node[333-341,343,345-353]
ivygpu          up 7-00:00:00      2   idle node[342,344]
ivygpu-noecc    up 7-00:00:00     19  alloc node[333-341,343,345-353]
ivygpu-noecc    up 7-00:00:00      2   idle node[342,344]
allgpu-noecc    up 7-00:00:00     30  alloc node[008-009,015-016,021-025,030,032,333-341,343,345-353]
allgpu-noecc    up 7-00:00:00     23   idle node[001-007,010-014,017-020,026-029,031,342,344]
debug           up    4:00:00      2   idle node[991-992]
debug-cpu       up    4:00:00      1   idle node992
debug-gpu       up    4:00:00      1   idle node991
```

There appear to be some nodes available on the "short" queue.

### 2. Request an allocation on an available queue using `salloc`.

Request one node for 5 hours (300 minutes):

```bash
[bendall@login3 ~]$ salloc -N 1 -p short -t 300
```

If you see this:

```bash
salloc: Granted job allocation 2390150
```

it means your allocation is granted. But if you see this:

```bash
salloc: Pending job allocation 2390150
salloc: job 2390150 queued and waiting for resources
```

You may wait here for a little bit as SLURM finds you the resources you need.
Hopefully, within few minutes, you will see your allocation was granted. If there is not a node available, type control "C" to get out of the queue.


### 3. Log in to the allocated node

Unlike some other workload managers, SLURM does not automatically log you into the allocated node. 
To access the resources, first we need to use `squeue` to figure out what node we were assigned (in the `NODELIST` column).

```bash
[bendall@login3 ~]$ squeue
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON) 
           2390150     short     bash  bendall  R       0:17      1 node004
```

We can see that we were given access to `node004`. To login, simply SSH into this node:

```bash
[bendall@login3 ~]$ ssh node004
```

Now you have a compute node all to yourself!! Look how empty it is:

```bash
[bendall@node004 ~]$ top
```

Make sure to reload any modules you may have loaded as this is a completely new login shell.

You can also open multiple SSH sessions into this node from C1. This is useful if you are running single-threaded processes.

# TMUX
When you are running a job on an interactive node, if you log off the network or your computer goes to sleep, you will lose your interactive node and drop your job. To keep this from happening, you can use [tmux](https://github.com/tmux/tmux/wiki/Getting-Started), which runs a terminal inside the terminal that you can detach from, so your program will keep running. For all commands available with tmux, use the `man 1 tmux` command, but here are some basics:

* After logging on to Colonial One or pegasus, to start tmux, type `tmux`. You should see a blank screen with a green bar at the bottom.
* Allocate an interactive node and log in to it.
* Load all modules and begin running your job.
* When you finish, type Control-b and then d to disconnect. You may now exit from the server or close your computer.
* To reconnect, get back onto your interactive node, and type `tmux a -t 0`. This will allow you to attach to th 0th tmux window. Tmux allows you to have several windows running at once, and by changing the number in this command you can access different tmx windows.
* 'tmux ls` allows you to see the existing sessions you can attach to

### 4. Exit node and cancel job

When you are finished, you should exit the node using `exit` and then cancel the job using `scancel`.

```bash
[bendall@node004 ~]$ exit # exits from node
[bendall@login3 ~]$ scancel 2390150 # cancels the job
```
