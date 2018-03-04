# Logging on to Colonial One
Colonial One is GWU's high performance computing cluster that is available to all students and faculty. For more information and some helpful youtube videos, visit the [Colonial One wiki](https://colonialone.gwu.edu/)

### Getting access
To request access, email hpchelp@gwu.edu from your GW email account, letting them know what research group you're in, and (for students) CC your advisor / PI.

After you are approved, log in on the command line by typing:

`ssh <username>@login.colonialone.gwu.edu`

where `<username>` is your GWU Net ID, the part of your email before the @.

On your first connection to the HPC, you'll be prompted to accept the ssh keys and verify the fingerprint of ColonialOne. Every time you log in, you will be required to give your password, which is the same password you use to access your GW email account. Alternatively, if you want to save 40 minutes a year by not typing in your password every time, you can set up an [SSH key](https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys--2). Additionally, you can set up an [alias](alias.md) so that you don't have to type in `ssh <username>@login.colonialone.gwu.edu` every time.

To run a job on the cluster, use [SLURM](slurm.md), Colonial One's scheduler or run an [interactive job](interactive_jobs.md).

To transfer files from your computer to the Colonial One cluster, use a [file transfer](filetransfer.md) software like [Cyberduck](https://cyberduck.io/) or [Globus](https://www.globus.org/). 

There are four main directories or filesystems on Colonial One:
`/home/<user>`
This is your home directory where you can store your personal files, data, programs etc. 25GB 

`/groups/<group>` 
If you are a member of a lab or group on Colonial One, you can store things here. Accessible by anyone in your group. 250GB

`/lustre/<group>`
Used as a shared scratch space. Run jobs here, but do not store things as they will be purged at the beginning of each month.

`/import/<group>`
Longer term storage 

`/c1/apps/`
Where colonialone staff installs software/modules


Use `logout` to log out of Colonial One.
