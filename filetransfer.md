## File Transfer
### Transferring files between directories on the Cluster
While logged in to Pegasus, you may want to move files from your home directory (where you are automatically when you log into the cluster) to a group directory. You can see what groups you are a part of when you log in to Pegasus. You can also transfer files to the high speed lustre file system to run jobs, but be careful because data on lustre is not backed up, and is purged at the beginning of each month. Although you can use the `mv` or `cp` commands to move files on the cluster, using `rsync` is more secure and will give you more flexibility.

The general format for [rsync](https://www.linux.com/learn/get-know-rsync) commands is `rsync [option] source destination`. A good option to use is `-avh` which will apply the archive, verbose, and human-readable options to your copy. When you use the `-a` option, rsync will automatically do recursive, copy symlinks, preserve permissions, preserve time stamps, preserve group ownerships and preserve owner. For copying folders, do not include the slash `folder/` or it will only copy the contents of the folder over, not the folder itself. 

### Transferring files from your computer to Colonial One (Pegasus)
`rsync` can transfer files between your computer and Pegasus. It has the advantage of being able to resume fails. From the command line on your computer, use the following commands to transfer files from your computer to Pegasus:

`rsync -avh localsourcefile  username@pegasus.colonialone.gwu.edu:destinationfile`

To transfer files from Pegasus to your computer:

`rsync -avh username@pegasus.colonialone.gwu.edu:sourcefile localfile`

You can alsouse scp to securely copy files from your computer to a secure shell (SSH) and back as follows:

`scp localsourcefile  username@pegasus.colonialone.gwu.edu:destinationfile`

`scp username@pegasus.colonialone.gwu.edu:sourcefile localfile`

These commands must be run from your local computer. If you are logged in to Pegasus already, open up a new terminal window and copy local files to the cluster.

Both of these commands only work on a Mac or Linux machine. If you are working on a windows machine, or if you like the nice graphical user interface, you can use Cyberduck or Globus for file transfer. 

+ Note: for a really big transfer that will take a lot of time, if your computer goes to sleep, it will stop copying. To keep your computer awake, use the command `caffeinate -dims -t 100000`. When you finish, just enter control `c` to cancel the caffeination. Alternatively, you can use `tmux` to keep your computer running for an rsync when you're not there. 

#### Cyberduck
1. [Download Cyberduck](https://cyberduck.io/) and open it on your computer.
2. In the top left corner, click "Open Connection"
4. Select "SFTP (SSH File Transfer Protocol)"
4. Fill in the server: pegasus.colonialone.gwu.edu and your GW username and password.
5. Press "Connect" and you can see the files in your home directory on Colonial One.
6. Drag and drop files to and from your finder window on a Mac or windows explorer on a windows machine. 

#### Globus
Globus is the industry standard for transferring large amounts of science
and engineering research data between datacenters and endpoints.

1. Go to the [Globus](https://www.globus.org/) website, and click "Log In" in the top right corner
2. Select "The George Washington University" at the organizational login
3. Log in with your GW username and password
1. Go to EndPoints
2. Add globus personal connect endpoint and name it
3. Generate and copy set up key
4. Download installer and install.
5. Open app and paste setup key
6. Go back to webpage and find endpoint
7. Colonial One's public endpoint is gw#colonialone
8. Push the arrow to to transfer files from one endpoint to the other.

If you are working on a project as a group, you should also learn to use [github](github.md) to do collaborative projects.

#### Verifying Copy using Checksum
If you want to verify that a copy has worked, you can do this with a checksum. Many datasets will include a .md5sum file or some other file that has an md5 hash (a string of numbers and letters that is calculated by the contents of a file) and a filename. If you run the command `md5sum -c *.md5sum` in a folder with your .md5sum files and your files you want to see if copied correctly and it gives you the same md5 hashes as is in the .md5sum files, you can know that the file has not been changed or corrupted since the .md5sum file was created. 

To create a .md5sum file with a hash and a file, use the command `md5sum filetohash.txt > hashfile.md5sum`	

