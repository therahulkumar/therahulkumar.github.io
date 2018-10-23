---
layout: post
title:  "Grep command in Unix/Linux with examples"
date:   2018-10-18 18:23:45 +0530
categories: unix-linux-commands
permalink: /unix-linux-commands/grep.html
comments: true
navname: "Grep command"
---

`grep` command is used in unix/linux like operating system for searching a pattern in files. It searches for a pattern 
line by line from a file or stream and prints the matched line. Having a good grasp on grep command will definitely make 
your life easier. In this post I am going to explore grep command with examples.

## Syntax
```cmd
$grep [OPTIONS] PATTERN [FILENAME]
```
Make `man` your friend, for reference or in doubt use the command `$man grep` 

## Frequently used OPTIONS with grep
```cmd
--color: Highlighting the search
-r: Recursively search in a directory
-i: For case insensitive match
-l: Display only filenames in which pattern is matched
-n: Display the matched lines and their line numbers.
-v pattern: This prints out all the lines that do not matches the pattern
-e pattern: Specifies expression with this option. Can use multiple times.
-f file: Takes patterns from file, one per line.
-E: Treats pattern as an extended regular expression
-w: Match whole word
```

## Examples

Consider the text file `rk.txt` as input with the following content

```cmd
java is a programming language, Java has a good developer community  
java is easy learn java, java follows oo principles
java uses simple syntax, Python uses simple syntax
```

# 1. Searching a pattern
```cmd
$grep "Java" rk.txt
```
Above command will search each line in file rk.txt and prints all the lines which has "Java".  
**output:**  
java is a programming language, Java has a good developer community

# 2. Highlighting search
```cmd
$grep --color "Java" rk.txt
```
**output:**  
java is a programming language, <span style="color:red">Java</span> has a good developer community  

**_Note:_** you can ignore `--color` flag from all other commands used in this tutorial, I have used just for 
readability purpose.

# 3. Case insensitive search
Use `-i` flag for case insensitive search
```cmd
$grep --color -i "Java" rk.txt
```
**output:**  
<span style="color:red">java</span> is a programming language, <span style="color:red">Java</span> has a good developer community  
<span style="color:red">java</span> is easy learn <span style="color:red">java</span>, <span style="color:red">java</span> follows oo principles  
<span style="color:red">java</span> uses simple syntax, Python uses simple syntax

# 4. Exclude a pattern 
```cmd
$grep -v "Python" rk.txt
```

**output:**  
java is a programming language, Java has a good developer community  
java is easy learn java, java follows oo principles

# 5. Search multiple expressions
Use `-e` flag multiple times   
```cmd
$grep --color -e "Python" -e "Java" rk.txt
```
Above command will match all the lines which either has 'Java' or 'Python'     
**output:**  
java is a programming language, <span style="color:red">Java</span> has a good developer community  
java uses simple syntax, <span style="color:red">Python</span> uses simple syntax

# 6. Search for exact word
By default grep searches for the substring, by using `-w` flag to match exact word and not substring
```cmd
$grep -w "program" rk.txt
```
Above command will not print anything because there is no word "program" in rk.txt file.
Now lets consider the word "programming", since this is present in one line that line will be printed.
```cmd
$grep --color -w "programming" rk.txt
```
**output:**  
java is a <span style="color:red">programming</span> language, Java has a good developer community

# 6. Recursively search for a pattern in all files inside a directory
```cmd
$grep -r "python" mydir
```
Above command will find "python" in all the files inside "mydir" directory

# 7. Using grep with pipe
You can use grep with other linux command's output instead of passing a filename.

```cmd
$cat rk.txt | grep --color "Python"
```
**output:**  
java uses simple syntax, <span style="color:red">Python</span> uses simple syntax

# 8. Colored output when using pipe with other commands
```cmd
$grep --color "java" rk.txt | sort
```
Above command will not print colored output, When you simply run grep --color it implies grep --color=auto which detects
whether the output is a terminal and if so enables colors. However, when it detects a pipe it disables coloring.
Now see the below command

```cmd
$grep --color=always "java" rk.txt | sort
```
Above command will print colored output  
**output:**  
<span style="color:red">java</span> is a programming language, Java has a good developer community  
<span style="color:red">java</span> is easy learn <span style="color:red">java</span>, <span style="color:red">java</span> follows oo principles  
<span style="color:red">java</span> uses simple syntax, Python uses simple syntax

# 9. Regular expression with grep
We can use regular expression as pattern with grep.

```cmd
$grep "^java" rk.txt
```
Above command will print all the lines starting with "Java". `^` used to specify the beginning of a line.

```cmd
$grep "syntax$" rk.txt
```
Above command will print all the lines ending with 'syntax'. `$` is used to specify end of a line.


