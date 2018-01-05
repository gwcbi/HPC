## Permissions

In order to run shell scripts (programs that you run on shell), you have to give the shell permission to execute the file.

Use `ls -l` to list files and directories and tell you the permissions they currently have. the r’s indicate who can read to it, the w’s indicate who can write to it, and the x’s indicate who can execute it. These are grouped in order of who they apply to: user, group members, and all other users. A dash indicates that permission is not granted to that category of user.

To change the mode of the permissions on a file so that a user can execute it, use the command `chmod u+x file.sh`.

