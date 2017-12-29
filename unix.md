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
Executed by itself will bring you to your home directory, while adding a path after cd will bring you to that directory.  

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
Does the same thing as cp, but does not make a copy and just moves the file.  

