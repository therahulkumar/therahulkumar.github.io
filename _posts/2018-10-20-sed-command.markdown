---
layout: post
title:  "Sed command in  Unix/Linux with examples"
date:   2018-10-20 18:23:45 +0530
categories: unix-linux-commands
permalink: /unix-linux-commands/sed.html
comments: true
navname: "Sed command"
---

`sed` command is used in unix/linux like operating system for editing the file or stream and it does a lot of functions
like find and replace, insertion, deletion. it scans the file or stream line by line and executes command on each line. 
In this post I am exploring some useful sed command with examples.

## Syntax

```cmd
sed options [script] [inputfile]
```
Make `man` your friend, for reference or in doubt use the command `$man sed` 
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

# 7. Print only modified lines
```cmd
$sed -n '2,$ s/java/python/gp' rk.txt
```
Above command will replace 'java' with 'python' from second line to last line and print only the modified lines in which
the substitution performed. look for `-n' flag  
**output:**
```cmd
python is easy learn python, python follows oo principles
python uses simple syntax, python uses simple syntax
```

# 8. Print modified lines twice
```cmd
$sed '2,$ s/java/python/gp' rk.txt
```
Above command will replace 'java' with 'python' from second line to last line and print twice the modified lines in which
the substitution performed.   
**output:**
```log
java is a programming language, java has a good developer community  
python is easy learn python, python follows oo principles
python is easy learn python, python follows oo principles
python uses simple syntax, python uses simple syntax
python uses simple syntax, python uses simple syntax
```

# 9. Deleting nth line
```cmd
$sed '2d' rk.txt
```
Above command will delete 2nd line from rk.txt  
**output:**
```log
java is a programming language, java has a good developer community  
java uses simple syntax, python uses simple syntax
```

# 10. Deleting lines in a range
```cmd
$sed '1,2d' rk.txt
```
Above command will delete lines from 1 to 2.  
**output:**
```cmd
java uses simple syntax, python uses simple syntax
```

```cmd
$sed '2,$d' rk.txt
```
Above command will delete lines from 2 to last.  
**output:**
```log
java is a programming language, java has a good developer community
```

# 11. Insert a blank line after each line
```cmd
$sed G rk.txt
```
**output:**
```log
java is a programming language, java has a good developer community  

java is easy learn java, java follows oo principles

java uses simple syntax, python uses simple syntax


```
For inserting two blank lines use following command
```cmd
$sed 'G;G' rk.txt
```
# 12. View/Print lines in a range
```cmd
$sed -n '2,3p' rk.txt
```
Above command will print 2nd to 3rd line from rk.txt  
**output:**
```log
java is easy learn java, java follows oo principles
java uses simple syntax, python uses simple syntax
```
For print nth line use following
```cmd
$sed -n '2p' rk.txt
```
Above command will print 2nd line from rk.txt  
**output:**
```log
java is easy learn java, java follows oo principles
```

# 13. View/Print lines except a given range
```cmd
$sed '2,3d' rk.txt
```
Above command will print all lines from file rk.txt except lines from 2nd to 3rd  
**output:**
```log
java is a programming language, java has a good developer community
```

# 14. View/Print non-consecutive lines/range from a file
```cmd
$sed -n -e '1p' -e '3p' rk.txt
```
Above command will print 1st and 3rd line from file rk.txt  
**output:**
```log
java is a programming language, java has a good developer community  
java uses simple syntax, python uses simple syntax
```

Notice the `-e` flag, using this flag we can append multiple editing command and each command will be executed in
sequence

# 15. Inplace editing of a file
```cmd
$sed -i 's/java/python/g' rk.txt
```
Above command will do the substitution inplace directly in rk.txt file, notice the `-i' flag, without this flag the 
edit operation does not affect the original file.

# 16. Inplace editing of a file with backup
```cmd
$sed -i '.original' 's/java/python/g' rk.txt
```
Above command will make changes in original file rk.txt and will make a backup of file with '.original' extension,
After executing the above command there will be two files rk.txt and rk.txt.original. This is recommended way of 
doing inplace editing, in case if we do any mistake we will have a backup file.  

# 17. Regular expression: print line which matches a pattern
```cmd
$sed -n '/programming/ p' rk.txt 
```
Above command will print all the lines which has 'programming' in it.  
**output:**
```log
java is a programming language, java has a good developer community
```
# 18. Delete lines which matches a pattern
```cmd
sed  '/programming/ d' rk.txt
```
Above command will delete all the lines which has 'programming'.  
**output:**
```log
java is easy learn java, java follows oo principles
java uses simple syntax, python uses simple syntax
```

# 19. Replace in lines which matches given pattern
```cmd
$sed '/programming/ s/java/python/g' rk.txt
```
Above command will replace 'java' with 'python' in each line which has 'programming' in it.  
**output:**
```log
python is a programming language, python has a good developer community  
java is easy learn java, java follows oo principles
java uses simple syntax, python uses simple syntax
```








