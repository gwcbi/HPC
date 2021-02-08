# Logging on to GW's cluster Pegasus
Pegasus (formerly called Colonial One) is GWU's high performance computing cluster that is available to all students and faculty. For more information and some helpful youtube videos, visit the [Colonial One wiki](https://colonialone.gwu.edu/)

The Pegasus cluster is only available if you are on campus or have access to GW's VPN. To access the VPN, you need to first download [Cisco AnyConnect](https://my.gwu.edu/mod/downloads/?category=VPN), and then follow the instructions listed [here](https://seascf.seas.gwu.edu/vpn-access).

### Getting access
To request access, visit the [Getting Access](https://colonialone.gwu.edu/getting-access/) page, and let them know what research group you're in, and (for students) your advisor / PI.

After you get an email saying you are approved, log in on the command line by typing:

`ssh <username>@pegasus.colonialone.gwu.edu`

where `<username>` is your GWU Net ID, the part of your email before the @.

On your first connection to the HPC, you'll be prompted to accept the ssh keys and verify the fingerprint of ColonialOne. Every time you log in, you will be required to give your password, which is the same password you use to access your GW email account. Alternatively, if you want to save 40 minutes a year by not typing in your password every time, you can set up an [SSH key](https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys--2). Additionally, you can set up an [alias](alias.md) so that you don't have to type in `ssh <username>@login.colonialone.gwu.edu` every time.

To run a job on the cluster, use [SLURM](slurm.md), Colonial One's scheduler or run an [interactive job](interactive_jobs.md).

To transfer files from your computer to the Colonial One cluster, use a [file transfer](filetransfer.md) software like [Cyberduck](https://cyberduck.io/) or [Globus](https://www.globus.org/). 

There are four main directories or filesystems on Colonial One, three that you can use:

`/$SCHOOL/home/<user>`
This is your home directory where you can store your personal files, data, programs etc. When you first log on to pegasus, you will be in this partition until you navigate somewhere else. Can only store 25GB. Do NOT run jobs in this partition. Use lustre instead.

`/$SCHOOL/groups/<group>` 
If you are a member of a lab or group on Colonial One, you can store things here. Accessible by anyone in your group. Store up to 250GB. DO NOT run jobs here. Instead run on lustre. If you are part of CBI, you can navigate to this partition with the command `cd /groups/cbi/Users`. Then, create a directory with your username. For long term storage, use [GW Box](https://gwu.account.box.com/login).

`/$SCHOOL/lustre/<group>`
Lustre partition: Used as a shared scratch space. Run jobs here, but do not store things as they will be purged at the beginning of each month. For more information on GW's purge policy, see the [Colonial One purge page](https://colonialone.gwu.edu/quick-start/purge-policy-for-colonial-one-lustre-filesystem-lustregroups/). If you are a part of CBI, you can navigate to the lustre partition with the command `cd /lustre/groups/cbi/Users`. Then, create a directory with your username where you can perform your analyses, or perform analyses in the projects directory if it is a group project. 

To see if any of your analyses will be purged at the next monthly purge, search the text file with the purgeable data using grep: `grep "yourusername" /lustre/lustrePurge/cbi_purgeable.txt` .

`/c1/apps/`
Where colonialone staff installs software/modules


Use `logout` to log out of Colonial One.

