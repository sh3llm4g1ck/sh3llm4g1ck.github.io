---
layout: post
title: "Python discord.py Bot - Commands"
tags: [python, discord.py, linux, commands]
---

Ηere we are again with the 2nd tutorial. Commands.. commands I believe one of the most important things, what is a bot without commands?
In this tutorial I'll cover like everything about commands, basic format, user-specific commands, role-specific commands and more.

# Command definition

Its really easy to create a command. The below code create a command called `cmd` when we execute it prints `This is my first command!`, add this to your code - save it - run the file.

If you remember from the previous tutorial we set the `command_prefix` to `!` so now we will execute the command like this: `!cmd`

```python
@client.command()
async def cmd(ctx):
    await ctx.send("This is my first command!")
```

![](https://raw.githubusercontent.com/sh3llm4g1ck/sh3llm4g1ck.github.io/main/_posts/python-discord.py-bot-commands/images/1.png)

Let's take it a step further now, we can use [Context Attributes](https://discordpy.readthedocs.io/en/stable/ext/commands/api.html?highlight=author#discord.ext.commands.Context){:target="_blank"}. With context attributes we can get who called the command, the channel that command executed and many more things. 

For example let's see who called the command.

```python
@client.command()
async def cmd(ctx):
    await ctx.send(f"Hello {ctx.author.name} \O")
```

![](https://raw.githubusercontent.com/sh3llm4g1ck/sh3llm4g1ck.github.io/main/_posts/python-discord.py-bot-commands/images/2.png)

Υou may feel confused now, what is `{ctx.author.name}`!? I'll share the logic with you how to read the documentation.

`ctx` is the parameter always have to be first then is the attribute `author`. If we click on `author` tell us that is a `Member` and member has other attributes like the `name`. Check the screenshot below.

![](https://raw.githubusercontent.com/sh3llm4g1ck/sh3llm4g1ck.github.io/main/_posts/python-discord.py-bot-commands/images/3.png)

![](https://raw.githubusercontent.com/sh3llm4g1ck/sh3llm4g1ck.github.io/main/_posts/python-discord.py-bot-commands/images/4.png)
