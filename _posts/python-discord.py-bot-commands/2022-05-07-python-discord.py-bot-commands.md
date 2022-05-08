---
layout: post
title: "Python discord.py Bot - Commands"
tags: [python, discord.py, linux, commands]
---

Ηere we are again with the 2nd tutorial. Commands.. commands I believe one of the most important things, what is a bot without commands?
In this tutorial I'll cover like everything about commands, basic format, user-specific commands, role-specific commands and more.

* [Command definition](#command-definition)
* [Command arguments](#command-arguments)
* [Bot owner only command](#bot-owner-only-command)
* [DM only command](#dm-only-command)
* [Specific role(s) command](#specific-roles-command)
* [Specific user command](#specific-user-command)

# Command definition

Its really easy to create a command. The below code create a command called `cmd` when we execute it prints `This is my first command!`, add this to your code - save it - run the file.

```python
@client.command()
async def cmd(ctx):
    await ctx.send("This is my first command!")
```
If you remember from the previous tutorial we set the `command_prefix` to `!` so now we will execute the command like this: `!cmd`

![](https://raw.githubusercontent.com/sh3llm4g1ck/sh3llm4g1ck.github.io/main/_posts/python-discord.py-bot-commands/images/1.png)

Let's take it a step further now, we can use [Context Attributes](https://discordpy.readthedocs.io/en/stable/ext/commands/api.html?highlight=author#discord.ext.commands.Context){:target="_blank"}. With context attributes we can get who called the command, the channel that command executed and many more things. 

For example let's see who called the command.

```python
@client.command()
async def cmd(ctx):
    await ctx.send(f"Hello {ctx.author.name} \O")
```

![](https://raw.githubusercontent.com/sh3llm4g1ck/sh3llm4g1ck.github.io/main/_posts/python-discord.py-bot-commands/images/2.png)

Υou may feel confused now, WTF is `{ctx.author.name}` !? I'll share the logic with you how to read the documentation.

`ctx` is the parameter always have to be first then is the attribute `author`. If we click on `author` tell us that is a `Member` and member has other attributes like the `name`. Apply the same logic with the other attributes.

![](https://raw.githubusercontent.com/sh3llm4g1ck/sh3llm4g1ck.github.io/main/_posts/python-discord.py-bot-commands/images/3.png)

![](https://raw.githubusercontent.com/sh3llm4g1ck/sh3llm4g1ck.github.io/main/_posts/python-discord.py-bot-commands/images/4.png)

# Command arguments

Another important part is the arguments, we can define arguments like this:

```python
@client.command()
async def cmd(ctx, msg):
    await ctx.send(f"This is my argument: {msg}")
```

![](https://raw.githubusercontent.com/sh3llm4g1ck/sh3llm4g1ck.github.io/main/_posts/python-discord.py-bot-commands/images/5.png)

If we want to use words with spaces we should use quotes:

![](https://raw.githubusercontent.com/sh3llm4g1ck/sh3llm4g1ck.github.io/main/_posts/python-discord.py-bot-commands/images/6.png)

If we don't want to use quotes, we can use keyword-only arguments. Note that you can only have one keyword-only argument.

```python
@client.command()
async def cmd(ctx, *, msg):
    await ctx.send(f"This is my argument: {msg}")
```

![](https://raw.githubusercontent.com/sh3llm4g1ck/sh3llm4g1ck.github.io/main/_posts/python-discord.py-bot-commands/images/7.png)

Needless to say, you can have as many arguments as you want.

```python
@client.command()
async def cmd(ctx, msg, msg2, msg3):
    await ctx.send(f"All my arguments: {msg}, {msg2}, {msg3}")
```

![](https://raw.githubusercontent.com/sh3llm4g1ck/sh3llm4g1ck.github.io/main/_posts/python-discord.py-bot-commands/images/8.png)

Now that we've covered the basics, let's make a command that convert our argument to uppercase. We will use the `.upper()` method.

```python
@client.command()
async def cmd(ctx, msg):
    await ctx.send(f"Converted to uppercase: {msg.upper()}")
```

![](https://raw.githubusercontent.com/sh3llm4g1ck/sh3llm4g1ck.github.io/main/_posts/python-discord.py-bot-commands/images/9.png)

# Bot owner only command

Let's say now that you want a command only for the bot owner. You can do that using the `is_owner()` check.

```python
@client.command()
@commands.is_owner()
async def cmd(ctx):
    await ctx.send(f"hello owner")
```

# DM only command

For example what if we want a command to be used only in DM? We can use the `dm_only()` check.

```python
@client.command()
@commands.dm_only()
async def cmd(ctx):
    await ctx.send(f"hello from DM")
```
# Specific role(s) command

Specific role command means the member that execute the command must have the specific role. To do that we can use the `has_role()` check.
You can use the role name or ID. To get the role ID you should enable developer mode on discord, go to `User Settings` -> `Advanced` -> Enable `Developer Mode`. Well you're a developer now so you should have this setting on. :P

```python
@client.command()
@commands.has_role('Admin') #or 972797319672127518 (role id)
async def cmd(ctx):
    await ctx.send(f"hello admin")
```

What if we want to have multiple roles? We can use the `has_any_role()` check.

```python
@client.command()
@commands.has_any_role('Owner', 'Co-Owner', 972797319672127518)
async def cmd(ctx):
    await ctx.send(f"hello staff team")
```

# Specific user command

You might be wondering now, how to make a specific user command? We need basic python logic in combination with discord.py library. The below code check if the `ctx.author.name` is the user `sh3llm4g1ck` the command will run else give error. You can use ID also like `ctx.author.id`.

```python
@client.command()
async def cmd(ctx):
    if ctx.author.name == 'sh3llm4g1ck':
        await ctx.send(f"hello sh3llm4g1ck, this is your command!")
    else:
        await ctx.send(f"you cant execute this command")
```

You can add some many users as you want.

```python
@client.command()
async def cmd(ctx):
    if ctx.author.name == 'sh3llm4g1ck' or ctx.author.name == 'user2':
        await ctx.send(f"hello sh3llm4g1ck, this is your command!")
    else:
        await ctx.send(f"you cant execute this command")
```

We covered like everything about commands, I'll make a seperate tutorial for errors,cooldown etc. For more info check [Commands from discord.py documentation](https://discordpy.readthedocs.io/en/latest/ext/commands/commands.html?highlight=commands){:target="_blank"} Also here is all the [checks list](https://discordpy.readthedocs.io/en/latest/ext/commands/commands.html?highlight=commands#checks){:target="_blank"} I suggest you to bookmark them. If you need any help you can contact me on discord `sh3llm4g1ck#0853`.

See you in the next tutorial.
