---
layout: post
title: "OverTheWire: Bandit writeup"
tags: [overthewire, linux, ssh, find]
---

Our journey will begin with [Bandit](https://overthewire.org/wargames/bandit/){:target="_blank"} wargame, as the page says will teaches us the basics we need to be able to play other wargames. We will learn various linux commands and much more. This post will contain all the solutions for each level with explanation. I'll update daily, till all the levels get pwned. Let's get started!

## level 0

We have to connect into bandit using SSH. It gives us the all information we need, the credentials `bandit0:bandit0` the host `bandit.labs.overthewire.org` and the port `2220`.

SSH (Secure Shell) is a protocol used to securely connect to a remote system. So using the above info we connect.

```
$ ssh bandit0@bandit.labs.overthewire.org -p 2220
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames
bandit0@bandit.labs.overthewire.org's password:

bandit0@bandit:~$ 
```

We can simply find the password for the next level in the current working directory:

```
bandit0@bandit:~$ ls
readme
bandit0@bandit:~$ cat readme 
boJ9jbbUNNfktd78OOpsqOltutMc3MY1
```

## level 1

Now we can connect as bandit1, I'll show it just for this time then you can apply it for each level. Sadly we can't use `su (su - bandit1)` so we do have to use the SSH way again.

```
$ ssh bandit1@bandit.labs.overthewire.org -p 2220
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames
bandit1@bandit.labs.overthewire.org's password: 

bandit1@bandit:~$ 
```

Running `ls`, we see a dash file that we can't read it if we try. Traditionally `-` means stdin (standard input) accepts text as input. If we try to read it using cat will wait for our input.

```
bandit1@bandit:~$ ls 
-
bandit1@bandit:~$ cat -
```

After a quick google-fu we can read it using the left-angle bracket `<` which redirect a file into a command.

```
bandit1@bandit:~$ cat < -
CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9
```

## level 2

Now we can see a file with spaces if we run `ls`.

```
bandit2@bandit:~$ ls
spaces in this filename
```

We can read this file using different ways, the most simple one is by pressing TAB for auto completion.

```
bandit2@bandit:~$ cat spaces\ in\ this\ filename 
UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK
```

Other way that will also work is using single/double quotes:

```
bandit2@bandit:~$ cat "spaces in this filename"
UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK
```

## level 3

This level is a really simple one, running `ls` we can see a directory named `inhere`.

```
bandit3@bandit:~$ ls
inhere
bandit3@bandit:~$ cd inhere/
bandit3@bandit:~/inhere$ 
```

There is a hidden file (.) here which we can see it using `ls -la`.

```
bandit3@bandit:~/inhere$ ls -la
total 12
drwxr-xr-x 2 root    root    4096 May  7  2020 .
drwxr-xr-x 3 root    root    4096 May  7  2020 ..
-rw-r----- 1 bandit4 bandit3   33 May  7  2020 .hidden
bandit3@bandit:~/inhere$ cat .hidden 
pIwrPrtPN36QITSp3EQaw936yaFoFgAB
```

## level 4

There is another `inhere` directory, we enter into it and we see lot of dashed files again.

```
bandit4@bandit:~$ cd inhere/
bandit4@bandit:~/inhere$ ls -la
total 48
drwxr-xr-x 2 root    root    4096 May  7  2020 .
drwxr-xr-x 3 root    root    4096 May  7  2020 ..
-rw-r----- 1 bandit5 bandit4   33 May  7  2020 -file00
-rw-r----- 1 bandit5 bandit4   33 May  7  2020 -file01
-rw-r----- 1 bandit5 bandit4   33 May  7  2020 -file02
-rw-r----- 1 bandit5 bandit4   33 May  7  2020 -file03
-rw-r----- 1 bandit5 bandit4   33 May  7  2020 -file04
-rw-r----- 1 bandit5 bandit4   33 May  7  2020 -file05
-rw-r----- 1 bandit5 bandit4   33 May  7  2020 -file06
-rw-r----- 1 bandit5 bandit4   33 May  7  2020 -file07
-rw-r----- 1 bandit5 bandit4   33 May  7  2020 -file08
-rw-r----- 1 bandit5 bandit4   33 May  7  2020 -file09
```

If we try to read one of them we can see that contains unreadable characters.

```
bandit4@bandit:~/inhere$ cat < -file00
�/`2ғ�%��rL~5�g��� �����
```

Now we will use the command `file` with wildcard `*` that matches any character to check which file contains readable data. Because these are dashed files we have to use a little trick `./`:

```
bandit4@bandit:~/inhere$ file ./*
./-file00: data
./-file01: data
./-file02: data
./-file03: data
./-file04: data
./-file05: data
./-file06: data
./-file07: ASCII text
./-file08: data
./-file09: data
```

Bingo! File `-file07` has the password.

```
bandit4@bandit:~/inhere$ cat < -file07
koReBOKuIDDepwhWk7jZC0RTdopnAYKh
```

## level 5

We have another `inhere` directory that contains a lot of directories and files. OTW gives us a hint that file is:

```
human-readable
1033 bytes in size
not executable
```

I crafted the following `find` command and gave me the password.

```
bandit5@bandit:~/inhere$ find . -type f -size 1033c -exec cat {} \;
DXjZPULLxYr17uwoI01bNLQbtFemEgo7
```

`.` = Search in current directory.
`-type f` = Search for regular file.
`-size 1033c` = Search for 1033bytes.
`-exec cat {} \;` = Execute cat once you find the file.

## level 6

Coming soon..
