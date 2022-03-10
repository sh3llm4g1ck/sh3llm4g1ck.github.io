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

