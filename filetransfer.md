## File Transfer
### Transferring files between directories in Colonial One
While logged in to Colonial One, you may want to move files from your home directory (where you are automatically when you log into the cluster) to a group directory. You can see what groups you are a part of when you log in to Colonial One. You can also transfer files to the high speed lustre file system to run jobs, but be careful because data on lustre is not backed up, and is purged at the beginning of each month. Although you can use the `mv` or `cp` commands to move files in Colonial One, using `rsync` is more secure and will give you more flexibility.

The general format for [rsync](https://www.linux.com/learn/get-know-rsync) commands is `rsync [option] source destination`. A good option to use is `-avh` which will apply the archive, verbose, and human-readable options to your copy.

### Transferring files from your computer to Colonial One

You can use scp to securely copy files from your computer to a secure shell (SSH) and back as follows:

`scp localsourcefile  username@login.colonialone.gwu.edu:destinationfile`

`scp username@login.colonialone.gwu.edu:sourcefile localfile`

rsync can also transfer files between your computer and Colonial One, but both of these commands only work on a Mac or Linux machine. If you are working on a windows machine, or if you like the nice user interface, you can use Cyberduck or Globus for file transfer. 

#### Cyberduck
1. [Download Cyberduck](https://cyberduck.io/)
2. set it up
4. use it

#### Globus
1. [Download Globus](https://www.globus.org/)
