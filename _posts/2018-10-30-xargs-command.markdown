---
layout: post
title:  "Xargs command in Unix/Linux with examples"
date:   2018-10-30 18:23:45 +0530
categories: unix-linux-commands
permalink: /unix-linux-commands/xargs.html
comments: true
navname: "xargs command"
---

`xargs` command is used to build argument for and execute other utility commands. It is really useful command if you
want to pass a list of output from other commands and use that output as an argument for other commands. In this post I
am going to use most frequently used xargs command syntax with examples.


## Examples

```cmd
$ pwd
/Users/rahul/xargs-tutorial
$ echo 'one.txt two.txt three.java four.py' | xargs touch
```
above command will create four files named one.txt, two.txt, three.java and four.py in present working directory.

**_Note:_** The touch utility sets the modification and access times of files.  If any file does not exist, it is created with default permissions.

```cmd
$ ls
four.py		one.txt		three.java	two.txt
```

# Remove files ending with '.txt'
```cmd
$ find . -name "*.txt" | xargs rm
$ ls
four.py		three.java
```
# Deleting files with whitespace in there name
```cmd
$ find . -name "*.txt" | xargs rm
```
Above command will not delete files which has white space in there name, to delete those files use `-print0` flag with 
find command and `-0` flag with xargs
```cmd
$ find . -name "*.txt" -print0 | xargs -0 rm
```
# Prompt for user confirmation before executing the command
```cmd
$ echo 'one.txt two.txt three.java four.py' | xargs touch
$ ls
four.py		one.txt		three.java	two.txt
```
use `-p` flag with xargs, it will prompt for user input(y/n) before executing the command. `y` will execute the command
and `n` will do nothing. This is really helpful command if you want to execute some deletion operations and confirm 
before each command to be executed.
```cmd
$ find . -name "*.txt" | xargs -p rm
rm ./two.txt ./one.txt?...n
```
Since I have passed `n` it will not remove the files
```cmd
$ ls
four.py		one.txt		three.java	two.txt
```
# Print command before execution
use `-t` flag with xargs to print each command before execution.
```cmd
$ find . -name "*.txt" | xargs -t rm
rm ./two.txt ./one.txt
```
# Using xargs with grep command
```cmd
$ ls
five.java	four.py		three.java
```
```cmd
$ cat three.java 
class Simple{  
    public static void main(String args[]){  
       System.out.println("Hello Java");  
    }  
}  
```
```cmd
$ cat four.py
# This program prints Hello, world!

print('Hello, world!')
```
```cmd
$ cat five.java
class HelloWorld
{
   public static void main(String args[])
   {
      System.out.println("Hello World");
   }
}
```

Grep 'Hello' in all the files ending with java

```cmd
$ find . -name "*.java" | xargs grep Hello
```
output:  
./three.java:       System.out.println("<span style="color:red">Hello</span> Java");    
./five.java:class <span style="color:red">Hello</span>World  
./five.java:      System.out.println("<span style="color:red">Hello</span> World");  

