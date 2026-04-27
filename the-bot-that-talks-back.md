---
layout: post
title: "The Bot That Talks Back"
permalink: /the-bot-that-talks-back
---

# The Bot That Talks Back

From your phone, you open Telegram and message your bot: "What are the three most urgent things in my actions file right now?"

It reads the file. It thinks. It tells you.

Not a command. Not a lookup. An actual answer, from a system that has read your actual files and understands what you mean by "most urgent."

That's what Claude Code's `--channels` flag gives you. And it's different from everything that came before it.

## Why This Is Different

Previous articles on this site cover how to build a Telegram bot that routes commands to your local system — `note`, `action`, `idea`, each one mapped to a handler that writes to a file. Useful. I still use those commands every day.

But that approach requires you to pre-define every interaction in advance. You have to know what questions to ask before you know what you need to ask. The bot is a lookup table, not a mind.

The `--channels` flag does something different. When you run it, Claude Code itself becomes the Telegram bot. Your messages go directly to the AI. The AI has access to your local files through its tools — it can read them, write to them, run scripts, search the web. When you send a message, you're not routing a command. You're having a conversation with something that can actually do things.

The difference is the difference between a menu and a colleague.

## What You're Building

A session where Claude Code listens to your Telegram bot and responds directly — no routing logic, no pre-defined commands, just the full intelligence of Claude operating on your local environment from your phone.

## Step 1: Get the Plugin Token

Claude Code uses a plugin system for channels. The Telegram plugin is available through Claude's official plugin registry.

When you run the command for the first time, Claude Code will prompt you to authenticate the plugin:

```bash
claude --channels 'plugin:telegram@claude-plugins-official'
```

Follow the auth flow — it will guide you to link your Telegram bot token. You'll need a bot token from BotFather if you don't have one already. (If you've set up the control layer from the previous article, you already have this.)

## Step 2: Point It at Your Working Directory

The context Claude operates in is wherever you run the command from. If you run it from your home directory, it can see your home directory. If you run it from a specific project folder, that's its world.

I run it from the folder where most of my working files live — my PersonalOS folder. That gives it access to my actions file, my notes, my context files. Everything it needs to actually help me.

```bash
cd ~/Documents/PersonalOS
claude --channels 'plugin:telegram@claude-plugins-official'
```

## Step 3: Message Your Bot

Open Telegram. Find the bot you linked in Step 1. Send it a message.

Anything you'd normally ask Claude, you can ask here. The difference is what it can see and do.

"What's in my inbox?" — it reads the file.  
"Draft a reply to the email I forwarded to my notes yesterday." — it finds the note, drafts the reply.  
"Add an action to follow up with the designer on Thursday." — it writes to your quick actions file.  

There's no command syntax. You write normally. The AI figures out what you need.

## Step 4: Keep It Running

The session stays live as long as the terminal is open. For anything you want available across the day, run it in a persistent tmux session:

```bash
tmux new-session -d -s telegram-channel -c ~/Documents/PersonalOS \
  'claude --channels "plugin:telegram@claude-plugins-official"'
```

Add that to a startup script or a LaunchAgent if you want it live from boot.

## What Surprised Me

I expected it to be a smarter version of my command bot. It's not — it's a different category of thing entirely.

The command bot answers questions I pre-defined. This answers questions I haven't thought to define yet. I asked it things I would have just held in my head before — "where did I put the notes from that call last Tuesday?" — and it found them. I asked it to draft a message I'd been putting off, gave it one line of context, and it produced something I sent with minimal edits.

The phone-to-local-files loop is the part that changes things practically. I'm not sitting at my desk when I realize I need to brief someone on something. I'm between meetings, or in a car, or half-awake at 7 AM. The channels session means Claude is already running, already knows my files, and is reachable from my pocket.

The sessions also have memory within a conversation. You can say "based on what we just discussed" and it knows what you mean. That's not how a command router works. That's how a colleague works.

## Where to Start

Pick one workflow you do from your phone that currently requires you to get to a laptop.

Run the channels session pointed at the folder that workflow depends on. Message the bot the way you'd message a person. See what comes back.

Don't try to make it your complete mobile command center from day one. Find the one thing where the phone-to-AI-to-files loop saves you a trip to the desk. That alone will tell you whether you want to go further.

The bot talks back. Let it.

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/ai-legal-first-pass" style="text-decoration: none; color: #0366d6;">← Previous: The AI Legal First Pass</a>
  </div>
  <div>
    <a href="/" style="text-decoration: none; color: #0366d6;">Home</a>
  </div>
</nav>
