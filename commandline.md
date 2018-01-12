# Navigating the Command Line
Although it may seem intimidating at first, using command line allows you to quickly perform tasks in a non-cumbersome way.

## Accessing Unix

First navigate to the command line. If you are using a Mac, open Terminal (in Applications in the Utilities folder).

If you are using a windows machine, use [Putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) or another terminal emulator.

You should see a black window that has a command prompt that looks like this:

```bash
Usernames-Macbook-Pro:~ Username$
```
## BASH Commands

There are hundreds of different commands you can use to perform a variety of different functions (hold ESC and press the "y" key for a complete list), but here are a few of the most useful. By typing "man" before the name of each command, you can get information about how to use them.

`cd`  
Executed by itself will bring you to your home directory, while adding a path after cd will bring you to that directory. A directory is basically a folder that holds your files or other directories.  

`cd ..`  
Changes directory to one-up the directory hierarchy  

`ls`  
Lists the files and directories in the current directory.

`ls -a`  
Lists the files and directories in the current directory including the hidden (dot) files.

`pwd`  
Returns the path to the current directory

`cp file_name path_to_new_directory`  
Copies a file from you current directory and places in a different directory.  

`mv file_name path_to_new_directory`  
Moves the file to a new directory.  

`cat` 
Concatenates files to standard output. Will print the contents of the file on the screen. `cat file1.txt file2.txt > newfile.txt` will concatenate 2 files into a third file.

`rm` 
This will remove or delete a file (be careful--cannot undo)

`mkdir` 
Makes a directory

`rm -rf` 
Removes a directory and all its contents

control `c` 
Kills the current process

control `z` 
Stops or pauses current process

`fg` 
Resumes last stopped job in the foreground

tab: autocompletes while typing

tab tab: see available autocomplete

`ls -ll` 
Lists the files in a directory as well as their dates and permissions

`du -sh` 
This tells you the disk usage--what is taking up space in a directory

`chmod` 
Change permissions

`exit` 
Disconnect form Colonial One or current node
Once you feel comfortable with these commands and moving around using the command line, you can create and edit files using a text editor like [vim](https://coderwall.com/p/adv71w/basic-vim-commands-for-getting-started) or [nano](https://www.howtogeek.com/howto/42980/the-beginners-guide-to-nano-the-linux-command-line-text-editor/), or [log onto Colonial One](colonialone.md).
