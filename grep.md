## GREP
GREP (Global regular expression print) is a way of navigating text using regular expressions. It is similar to find and replace in a word document and has many very useful applications in computing.

The basic pattern for using a grep command is `grep <option> <search pattern> file'

The options are:
+ i: case insensitive 
+ n: gives the line number of the search term 
+ c: gives the count of the lines the search term is found in
+ v: gives the lines the search term is not found in
+ -A 5 gives the five lines that come after a search term
+ -B 5 gives the five lines that come before a search term
+ -w gives only the lines where the whole word is found
+ -l gives the filename where the match is found

# Wildcards
There are some symbols that can be used to represent more than one thing. For example, `.` is used to designate any character so the command `grep "b.g" filename` could return lines with the words big, bag or bog. 
