---
layout: post
title: "The remote control of Claude Code"
permalink: /remote-control
---

# The remote control of Claude Code

On my phone, I type "new". A Claude Code session starts on my laptop.

I don't open the laptop. I don't switch contexts. I send a Telegram message, and a session initialises — with a fresh terminal, the relevant context loaded, ready to work.

This is the Telegram command interface: Claude Code running on your machine, reachable from anywhere.

## Why this matters

Claude Code runs locally. That is one of its strengths — it has access to your files, your tools, your environment. But it also means that traditionally, using it requires being at your desk.

The command interface changes that.

Any instruction you can type in a terminal, you can send from your phone. The work happens on the machine. The result comes back to your phone. You are the remote, not the operator.

This is useful for anything that arises when you are away from your desk: a thought you want captured, a status you want checked, a session you want running before you get home, an automation you want triggered while you are in a meeting.

The AI runs while you are elsewhere. You check in on it the same way you check a message.

## How it works

Three components:

**A Telegram bot.** A bot you create through Telegram's BotFather that receives messages from you and only you. It is the input interface.

**A listener process.** A script running on your machine that polls the bot for incoming messages, matches them against a command list, and executes the corresponding action. The script runs persistently as a background process, managed by a system daemon so it restarts if it ever stops.

**A command map.** The definitions that connect a word you type to an action on the machine. This is where you decide what the interface can do.

When you send a command, the listener catches it, runs the associated shell command, and optionally sends confirmation back via Telegram.

## The commands I use most

**`new`** — starts a fresh Claude Code session in a terminal window. Useful when I have a task I want handled and want a session ready when I'm back at the desk, or want to hand off work that will run unattended.

**`note [text]`** — appends whatever follows to the inbox section of my actions file. Fast capture without opening a laptop. A thought, an idea, a task — it lands in the right place.

**`action [text]`** — same as note but adds it as a checkbox to my quick actions list. One word difference, different destination.

**`idea [text]`** — sends a capture directly to the inbox of my ideas file. Not a task, not a note — a spark. It goes somewhere I will actually review it.

**`check`** — runs a health check across all my automations and sends the results back to Telegram within a few minutes. I know the state of the whole system without opening anything.

**`close`** — kills all running sessions. Clean slate.

## The architecture underneath

When a session is started via `new`, it runs in tmux — a terminal multiplexer that keeps the session alive and accessible even when the initiating connection closes. If I want to interact with the session directly, I can connect via the Claude mobile app or attach to the tmux session remotely.

This means sessions can be triggered on-demand, run unattended, and deliver results back to Telegram — all from a message sent on a phone. The work happens without the machine being in front of me.

## Where to start

Start with `note`. It is the lowest-stakes command and provides immediate value: a way to send any thought directly to your working inbox without opening a laptop.

Once that works, the pattern is established. Adding other commands is a matter of extending the map. The listener is already running. The channel is already open.

The harder part is usually deciding what commands you want. Ask: what do I find myself wishing I could trigger from my phone? That is your command list.

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/different-kind-of-power-user" style="text-decoration: none; color: #0366d6;">Next: A different kind of Claude Code power user →</a>
  </div>
  <div>
    <a href="/two-minute-tasks" style="text-decoration: none; color: #0366d6;">← Previous: The two-minute task you should automate anyway</a>
  </div>
  <div>
    <a href="/" style="text-decoration: none; color: #0366d6;">Home</a>
  </div>
</nav>
