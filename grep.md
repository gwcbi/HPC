# GREP
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

## Wildcards
There are some symbols that can be used to represent more than one thing. For example, `.` is used to designate any character so the command `grep "b.g" filename` could return lines with the words big, bag or bog. 

To search for a `.` you have to escape the function using `\.`

The `*` is used to search for as many of the previous character as there is. For example `grep "b.*g" would return things like bag, bog and bug, but also blog, berg and betting.

Additional search terms include
+ \w for searching for letters, numbers and _
+ \d will search for numbers
+ \r will search for return character
+ \s Space, tab or end of line
+ [A-Z] Single character in the given range
+ [aeiou] Single vowel
+ ^ Beginning of line character
+ $ Last position before end-of-line character

## Capturing and Replacing
+ () captures a search result for use in a replacement term
+ \1 Substitutes matched item into replacement term in numerical order

## Examples
If you want to extract particular rows from a file, that include the words "key words", you can use the following command:
```
grep "key words" filename
```
and it will list all the lines that include those words.
If you want to put those lines into a csv, use the command
```
grep "key words" filename > newfile.csv
```
