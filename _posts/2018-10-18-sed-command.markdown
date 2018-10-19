---
layout: post
title:  "sed command"
date:   2018-10-18 18:23:45 +0530
categories: unix/linux commands
permalink: /commands/sed.html
comments: true
---

## sed -- stream editor

`sed` command is used in unix/linux like operating system for editing the file or stream and it does a lot of functions
like find and replace, insertion, deletion but it is mainly used for substitution of word. you can used `sed` to substitue
words without opening the file. it scans the file or stream line by line and executes command on each line.

## Syntax

```cmd
sed options [script] [inputfile]
```

## Examples

Consider the text file `rk.txt` as input with the following content

```cmd
java is a programming language, java has a good developer community  
java is easy learn java, java follows oo principles
java uses simple syntax, python uses simple syntax
```
# 1. Replacing or substituting a string

```cmd
$sed 's/java/python/' rk.txt
```
By default sed replaces only the first occurance, so the above command will replace first occurrence of 'java' with 'python'.  
**output:**
```log
python is a programming language, java has a good developer community  
python is easy learn java, java follows oo principles
python uses simple syntax, python uses simple syntax
```
# 2. Replace or substitute nth occurrence of a pattern in each line
```cmd
$sed 's/java/python/2' rk.txt
```
The above command will replace 2nd occurrence of 'java' with 'python' in each line if the 2nd occurrence is present.  
**output:**
```log
java is a programming language, python has a good developer community  
java is easy learn python, java follows oo principles
java uses simple syntax, python uses simple syntax
```

# 3. Replace or substitute all occurrences of a pattern in each line
```cmd
$sed 's/java/python/g' rk.txt
```

The above command will replace all the occurrences of 'java' with 'python'  
**output:**
```log
python is a programming language, python has a good developer community  
python is easy learn python, python follows oo principles
python uses simple syntax, python uses simple syntax
```

# 4. Use sed with pipe
```cmd
$cat rk.txt | sed 's/java/python/g'
```
As with all the other linux commands you can use sed in a pipe and it's where is actual power lies. you can use
sed command in a pip instead of giving the file name as argument.  
**output:**
```log
python is a programming language, python has a good developer community  
python is easy learn python, python follows oo principles
python uses simple syntax, python uses simple syntax
```

# 5. Replacing string on a particular line number
```cmd
$sed '2 s/java/python/g' rk.txt
```
The above command replaces 'java' with python only on 3rd line of the file.  
**output:**
```log
java is a programming language, java has a good developer community  
python is easy learn python, python follows oo principles
java uses simple syntax, python uses simple syntax
```

# 6. Replacing string in a range of line
```cmd
$sed '1,2 s/java/python/g' rk.txt
```
**output:**
```log
python is a programming language, python has a good developer community  
python is easy learn python, python follows oo principles
java uses simple syntax, python uses simple syntax
```

```cmd
$sed '2,$ s/java/python/g' rk.txt
```
The above command will replace occurrence of 'java' with 'python' from 2nd line to last line  
**output:**
```log
python is a programming language, python has a good developer community  
python is easy learn python, python follows oo principles
python uses simple syntax, python uses simple syntax
```

# 7. 


