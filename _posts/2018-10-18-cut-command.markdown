---
layout: post
title:  "Cut command in Unix/Linux with examples"
date:   2018-10-18 18:23:45 +0530
categories: unix-linux-commands
permalink: /unix-linux-commands/cut.html
comments: true
navname: "Cut command"
---

`cut` command is used to cut out a seleted portions of each line from a file or standard output based on some given 
conditions and writes them to standard output. In this post I am going to explore cut command with examples.

## Synopsis
```cmd
cut -b list [-n] [file ...]
cut -c list [file ...]
cut -f list [-d delim] [-s] [file ...]
```

## Flags description
```cmd
-b: cut using byte position
-c: cut using char position
-f: selet fields after using cut with delimeters
-d: cut with delimeter
--output-delimiter=STRING, use STRING as the output delimiter the default is to use the input delimiter
--complement: complement the set of selected bytes, characters or fields
```
**_Note:_** Indexing starts from 1 and `--output-delimiter` and `--complement` are not available for BSD version OS.

## Examples
Consider the text file `rk.txt` as input with the following content

```cmd
Rahul,Kumar,20
Aman,Kumar,21
```
# 1. Cut bytes in a range
To cut bytes in a range, pass a `-` separated index values with `-b` flag.
```cmd
$cut -b 1-3 rk.txt
output:
Rah
Ama
```
```cmd
$cut -b 2-4,6-8 rk.txt
output:
ahu,Ku
manKum
```

# 2. Cut bytes at specific positions
To cut bytes at specific positions, pass a `,` separated index values with `-b` flag.
```cmd
$cut -b 1,3,5 rk.txt
output:
Rhl
Aa,
```
```cmd
$cut -b 2,4 rk.txt
output:
au
mn
```

# 3. Cut bytes at specific positions and range
```cmd
$cut -b 2-4,6,7-8,10 rk.txt
output:
ahu,Kua
manKumr
```

# 4. Cut char at specific positions and in a range
Use `-c` command to cut using char index. this is especially useful in cases where the characters are of multiple bytes.
```cmd
$cut -c 1-3 rk.txt
output:
Rah
Ama
```
```cmd
$cut -c 2-4,6,7-8,10 rk.txt
output:
ahu,Kua
manKumr
```
By looking above examples the output with `-c` and `-b` flags are same. Now lets see the output of these two flags with
multi bytes char.
```cmd
$echo "rahul😝" | cut -b 5,6
output:
l?
```
```cmd
echo "rahul😝" | cut -c 5,6
output:
l😝
```
In the above examples `😝` is a multi byte char hence the output with `-c` and `-b` are different.

# 5. Using delimiter to cut
Using delimiter to cut creates an array of tokens which can be printed with `-f` flag by giving the field number as
argument. following examples uses `,` as delimiter.

```cmd
$cut -d "," -f 1 rk.txt
output:
Rahul
Aman
```
```cmd
$cut -d "," -f 2 rk.txt
output:
Kumar
Kumar
```
```cmd
$cut -d "," -f 2-3 rk.txt
output:
Kumar,20
Kumar,21
```
# 6. Changing the output delimiter
```cmd
$cut -d "," -f 1,2,3 --output-delimiter ":" rk.txt
output:
Rahul:Kumar:20
Aman:Kumar:21
```
```cmd
$cut -c 1,2  --output-delimiter ":" rk.txt
output:
R:a
A:m
```
```cmd
$cut -b 1,2  --output-delimiter ":" rk.txt
output:
R:a
A:m
```
# 7. Inverting the output of cut command 
```cmd
$cut --complement -d ',' -f 1 rk.txt
output:
Kumar,20
Kumar,21
```
```cmd
$cut --complement -c 1,2 rk.txt
output:
hul,Kumar,20
an,Kumar,21
```
```cmd
$cut --complement -b 1,2 rk.txt
output:
hul,Kumar,20
an,Kumar,21
```



