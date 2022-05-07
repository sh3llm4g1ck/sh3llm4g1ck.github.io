---
layout: post
title: "Python discord.py Bot - Setup"
tags: [python, discord.py, linux, pip, nano]
---

Welcome, welcome. There are ton of tutorials on how to make a discord bot with python but most of them are fucked up, missing things, outdated, forget to explain things, they make you to join their server to get the code etc you got the point. So I decided to make some 1337 tutorials on how to make one with full explanation that will cover everything and share the logic of how to search and do things. 

The tutorials will be based on GNU\Linux, if you're a windows user then bad for you. Use your search engine to find a way to do the corresponding things.
I don't know how many tutorials I'll make until we cover everything, I'll see. At the end of the tutorials you will be an 1337 bot developer, I guess.

- [Make a Guild/Server](#make-a-guildserver)

# Make a Guild/Server

You can't do shit without a guild/server. I bet the majority already know how to make one but I'll show it for those who don't know.

1) Click on the plus symbol.

![](https://raw.githubusercontent.com/sh3llm4g1ck/sh3llm4g1ck.github.io/main/_posts/python-discord.py-bot-setup/images/1.png)

2) Click on `Create My Own`.

![](https://raw.githubusercontent.com/sh3llm4g1ck/sh3llm4g1ck.github.io/main/_posts/python-discord.py-bot-setup/images/2.png)

3) Now you can choose `For me and my friends` `For a club or community` or just `skip`, does not matter.

![](https://raw.githubusercontent.com/sh3llm4g1ck/sh3llm4g1ck.github.io/main/_posts/python-discord.py-bot-setup/images/3.png)

4) Choose your server name and press `Create`.

![](https://raw.githubusercontent.com/sh3llm4g1ck/sh3llm4g1ck.github.io/main/_posts/python-discord.py-bot-setup/images/4.png)

5) Abracadabra you have a server.

![](https://raw.githubusercontent.com/sh3llm4g1ck/sh3llm4g1ck.github.io/main/_posts/python-discord.py-bot-setup/images/5.png)

# Create a Bot Account

In order to work with discord API we need to have a bot account, first go to discord.com and log in then move to [Developer Portal/Applications](https://discord.com/developers/applications){:target="_blank"}

1) First let's create a new application.

![](https://raw.githubusercontent.com/sh3llm4g1ck/sh3llm4g1ck.github.io/main/_posts/python-discord.py-bot-setup/images/6.png)

![](https://raw.githubusercontent.com/sh3llm4g1ck/sh3llm4g1ck.github.io/main/_posts/python-discord.py-bot-setup/images/7.png)

2) Now let's create a bot user. Under settings click on `Bot` then `Add Bot`.

![](https://raw.githubusercontent.com/sh3llm4g1ck/sh3llm4g1ck.github.io/main/_posts/python-discord.py-bot-setup/images/8.png)

Click on `Yes, do it!`

![](https://raw.githubusercontent.com/sh3llm4g1ck/sh3llm4g1ck.github.io/main/_posts/python-discord.py-bot-setup/images/9.png)

You have a bot account now. From this page you can change things like your bot username/profile etc.

![](https://raw.githubusercontent.com/sh3llm4g1ck/sh3llm4g1ck.github.io/main/_posts/python-discord.py-bot-setup/images/10.png)

# Invite Bot to the server

We have a server, we have a bot account now we need to invite the bot to the server.

1) Under settings click on `OAuth2` then `URL Generator` and check the `bot` scope.

![](https://raw.githubusercontent.com/sh3llm4g1ck/sh3llm4g1ck.github.io/main/_posts/python-discord.py-bot-setup/images/11.png)

2) Now you can choose what permissions your bot want to have, personally I always choose Administrator to have them all but be careful. The generated URL allows us to invite the bot into the server.

![](https://raw.githubusercontent.com/sh3llm4g1ck/sh3llm4g1ck.github.io/main/_posts/python-discord.py-bot-setup/images/12.png)

3) Copy the generated URL and paste into your browser, choose in which server you want to add the bot and press continue. Now the bot is in the server.

![](https://raw.githubusercontent.com/sh3llm4g1ck/sh3llm4g1ck.github.io/main/_posts/python-discord.py-bot-setup/images/13.png)

![](https://raw.githubusercontent.com/sh3llm4g1ck/sh3llm4g1ck.github.io/main/_posts/python-discord.py-bot-setup/images/14.png)

# Coding the bot

Τhis is where the magic begins, first we have to install the [discord.py](https://github.com/Rapptz/discord.py){:target="_blank"} library. We're going to use pip, pip is the standard package manager for python it allows us to install/uninstall etc python modules.

Let's install pip first. Fire up your terminal and run:

```
$ sudo apt install python3-pip -y
```

```
$ pip3 -V
pip 20.3.4 from /usr/lib/python3/dist-packages/pip (python 3.9)
```

Now we can install discord.py:

```
$ pip3 -q install discord.py
$ pip3 freeze | grep discord.py
discord.py==1.7.3
```

Good, good. Let's create a space now to work:

```
$ cd Documents/
$ mkdir 1337bot; cd 1337bot
$ touch main.py
```

Before we start coding the bot we need to take our bot Token. Token is a string that contains letters,numbers,symbols that connects our code to the application. Always remember **never share your token with someone else!** Imagine if a kiddo connects his code to your application and do malicious things like banning all members, delete all channels.. got it? 

Now go again to your [applications](https://discord.com/developers/applications){:target="_blank"} and go under Bot setting and click `Reset Token` and copy it.

![](https://raw.githubusercontent.com/sh3llm4g1ck/sh3llm4g1ck.github.io/main/_posts/python-discord.py-bot-setup/images/15.png)

You can use now your favorite text editor sublime,atom,vsc etc. I prefer command line text editors, I'll use `nano`.

Below is the simplest code for our bot to start running. I wrote comments to understand what each line does.

```
$ nano main.py
...
```

```python
import discord
from discord.ext import commands

#Here we set the command prefix. We set it to '!' so we will execute a command this way '!testcommand'
client = commands.Bot(command_prefix = '!')

#Here we set an event. An event is when you want your bot to do something when a event happens like when a member join/leave the server etc 
#Then we use the on_ready() function, this function called after user login successfully 
#Then we use the .user and .guilds attributes. The .user prints the connected user (our bot) and the .guilds prints the servers that the bot is member of
@client.event
async def on_ready():
        print(f"{client.user} is online!")
        print(f"Bot is connected to the following servers: {client.guilds}")

#Here we specify our token
client.run('PLACE_YOUR_TOKEN_HERE')
```

Now save it and run it.

```
$ python3 main.py 
1337 bot#4314 is online!
Bot is connected to the following servers: [<Guild id=972128183732297798 name='1337@server' shard_id=None chunked=False member_count=2>]
```

We can now see that bot is online!

![](https://raw.githubusercontent.com/sh3llm4g1ck/sh3llm4g1ck.github.io/main/_posts/python-discord.py-bot-setup/images/16.png)

That was it, that was the "hard" part because we had to setup ton of shits. From now on we can enjoy writing code. ;)
Bookmark the [discord.py Documentation](https://discordpy.readthedocs.io/en/latest/){:target="_blank"}, trust me you will need it a lot.
If you need any help you can contact me on discord `sh3llm4g1ck#0853`.

See you in the next tutorial.
