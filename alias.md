## Creating aliases

If you're like some people and have a hard time remembering exactly how to ssh into ColonialOne, it may be a good idea for you add an alias to your .bash_profile.

An alias is a substitute for a complete command, like a shortcut. 

You can make an alias so that you only have to type `colone` instead of typing `ssh username@login.colonialone.gwu.edu` every time you log in to ColonialOne.

First, make sure you are in the home directory of your own computer (not on ColonialOne). Use the command `cd ~`.

Use the command `ls -a` to see your hidden files (those with `.` in front of them). You should see a file called `.bash_profile`.

Use a text editor like [vim](https://coderwall.com/p/adv71w/basic-vim-commands-for-getting-started) or [nano](https://www.howtogeek.com/howto/42980/the-beginners-guide-to-nano-the-linux-command-line-text-editor/) to add the following line to the file `.bash_profile`:

`alias colone='ssh username@login.colonialone.gwu.edu'`

Type `. .bash_profile` to reload .bash_profile and update any functions you add.

You should now be able to type `colone` and get into ColonialOne.
