## Permissions

In order to run shell scripts (programs that you run on shell), you have to give the shell permission to execute the file.

Use `ls -l` to list files and directories and tell you the permissions they currently have. You should see something that says -rwxrwxr--. The r’s indicate who can read to it, the w’s indicate who can write to it, and the x’s indicate who can execute it. These are grouped in order of who they apply to: user (u), group members (g), and all other users (o). A dash indicates that permission is not granted to that category of user.

To change the mode of the permissions on a file so that a user can execute it, use the command `chmod u+x file.sh`. To take away write permissions from users not in the group, use `chmod o-w file.sh`. To take away write permissions from everyone, use `chmod a-w file.sh`. 

You can also change permissions using the unix numeric system where read is 4, write is 2 and execute is 1. To change the permissions so that a user and group can read, write and execute, use the command `chmod 774 file.sh`



To change a file so that anyone can execute it, use the command `chmod 777 file.sh`


