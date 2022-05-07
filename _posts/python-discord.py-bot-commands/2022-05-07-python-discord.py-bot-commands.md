---
layout: post
title: "Python discord.py Bot - Commands"
tags: [python, discord.py, linux, commands]
---

Ηere we are again with the 2nd tutorial. Commands.. commands I believe one of the most important things, what is a bot without commands?
In this tutorial I'll cover like everything about commands, basic format, user-specific commands, role-specific commands and more.

# Command definition

Its really really easy to create a command. The below code create a command called `cmd` when we execute it prints `This is my first command!`, add this to your code - save it - run the file.

```python
@client.command()
async def cmd(ctx):
    await ctx.send("This is my first command!")
```

If you remember from the previous tutorial we set the `command_prefix` to `!` so now we will execute the command like this: `!cmd`

```python
client = commands.Bot(command_prefix = '!')
```

![](https://raw.githubusercontent.com/sh3llm4g1ck/sh3llm4g1ck.github.io/main/_posts/python-discord.py-bot-commands/images/1.png)
