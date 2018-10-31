---
layout: post
title:  "Sort command in Unix/Linux with examples"
date:   2018-10-21 18:23:45 +0530
categories: unix-linux-commands
permalink: /unix-linux-commands/sort.html
comments: true
navname: "Sort command"
---

`sort` command is used to sort or merge lines of text and binary files. Comparisons are based on one or more sort keys 
extracted from each line of input, and are performed lexicographically. By default, if keys are not given, sort uses 
entire lines for comparison. In this post I am going to explore commonly used sort command with examples.

## Syntax
```cmd
sort [OPTION]... [FILE]...
```
Make `man` your friend, for reference or in doubt use the command `$man sort` 

## Examples
Consider the text file `rk.txt` as input with the following content

```cmd
Rahul
rahul
Aman
Nitish
01rk
```

# 1. Sort in lexicographical order
```cmd
$sort rk.txt
output:
01rk
Aman
Nitish
Rahul
rahul
```

By default sort uses entire line for comparison and sorts based on lexicographical order (number < alphabet and Uppercase < Lowercase).

# 2. Sort  in reverse order
`-r` flag is used to sort in reverse order
```cmd
$sort -r rk.txt
output:
rahul
Rahul
Nitish
Aman
01rk
```
# 3. Check wheter the file is already sorted
Use `-c` flag to check whether the file is already sorted.
```cmd
$sort -c rk.txt
output:
sort: rk.txt:3: disorder: Aman
```
Since the file is not sorted it prints line number with disorder message. If the file is sorted it does not print anything.

# 4. Writing output to a file
**_Note:_** input file does not change with sort command, content of input file remains in same order as before  
To save output of sort command in a file either use `>` redirection operator or `-o' flag

```cmd
$sort rk.txt > output.txt
```
```cmd
$sort -o output.txt rk.txt
```
The both the above command output of sort will be saved in output.txt file.

# 5. Using sort with pipe
sort command can be used directly on standard input with pipeline without giving the input file name as agrument.
```cmd
$cat rk.txt | sort
```
```cmd
$cat rk.txt | sort -r
```
```cmd
$cat rk.txt | sort -r -o  output.txt
```
```cmd
$cat rk.txt | sort -r > output.txt
```

# 6. Sorting numeric values
`-n` flag is used to sort numeric values,
Lets override the content of rk.txt with following values
```cmd
12
1
4
5.23
23.2
```

```cmd
$sort -n rk.txt
output:
1
4
5.23
12
23.2
```

```cmd
$sort -nr rk.txt
output:
23.2
12
5.23
4
1
```
# 7. Merge sorted files
Consider files a.txt and b.txt with following contents  
a.txt
```cmd
Aman
Rahul
```
b.txt
```cmd
Amit
Nishant
```
```cmd
$sort -m a.txt b.txt
output:
Aman
Amit
Nishant
Rahul
```
**_Note:_** If the input files are not sorted, the order of lines in output is not defined.

# 8. Sort and remove duplicates
Consider a.txt with following content
```cmd
Rahul
Aman
Rahul
Rohit
```
`-u` command is used to sort and remove duplicated.
```cmd
$sort -u a.txt
output:
Aman
Rahul
Rohit
```
# 9. Sort based on a specific column/field of each line
`-k` flag with column/field number is used to sort on based on that column.  
Consider a.txt with following content.
```cmd
Rahul 2
Rohit 21
Aman 10
Amit 15
```
Following command will sort content of a.txt based on second column
```cmd
$sort -n -k 2 a.txt
output:
Rahul 2
Aman 10
Amit 15
Rohit 21
```
Above command can also be written as `$sort -nk2 a.txt`. note `-n` flag is used for numeric sorting. By default white 
spaces used as field separator, for other types of delimiter use `-t` flag.

Consider b.txt with following content.
```cmd
Rahul,2
Rohit,21
Aman,10
Amit,15
```
Following command will sort content of b.txt on second column.
```cmd
$sort -t ',' -n -k 2 b.txt
output:
Rahul,2
Aman,10
Amit,15
Rohit,21
```
# 10. Ignore case while sorting
Use `-f` flag to ingore case, consider a.txt with following content
```cmd
rahul
Rohit
Amit
Aman
```
```cmd
$sort -f a.txt
output:
Aman
Amit
rahul
Rohit
```



