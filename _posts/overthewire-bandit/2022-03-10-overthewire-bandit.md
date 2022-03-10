---
layout: post
title: "OverTheWire: Bandit writeup"
tags: [overthewire, linux, ssh]
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
