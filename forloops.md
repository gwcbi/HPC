# For Loops in Bash

A lot of times when you are moving and renaming files, you need to do things repeatedly. Using 'For loops' can help you do this more effectively. Here are some examples of what you can do with for loops.

### Repeat a command a number of times
This for loop will iterate through the numbers 1-5 and print a message to the screen
```
for i in 1 2 3 4 5; do
   echo "Welcome $i times"
done
```
You can do the same thing if you replace `1 2 3 4 5` with `{1..5}`

The same thing can be done with files.
### List all of the files in all of the folders in a directory
```
for file in /directory/*
   ls $file
done
```

### Change names of multiple files in a directory to have directory name in them, and move them to another file
```
for f in *; do
   cp $f/flexcleaned_1*.html fastqc_cleaned/${f}_flexcleaned_1.html
done
```
