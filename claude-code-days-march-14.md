---
layout: post
title: "My Day with Claude Code — March 14, 2026"
permalink: /claude-code-days-march-14
---

# My Day with Claude Code — March 14, 2026

Some days are about building the infrastructure that makes everything else possible. March 14 was one of those.

<div style="background: #f0f0f7; border-radius: 6px; padding: 16px 20px; margin-bottom: 24px;" markdown="1">

**Quick read**

A day of bot improvements and agent planning — closing gaps in the Telegram infrastructure and designing a full AI agent company for personal operations. Here's what happened:

- Built unknown sender detection into the Telegram bot — it now logs and identifies anyone who contacts the bot unexpectedly
- Designed a full AI agent company for personal operations — planned, not yet executed

A day where the foundation got stronger.

</div>

<p style="margin-bottom: 32px;"></p>

### The Telegram bot

An improvement to the Telegram bot that runs as my notification and control layer. The original bot handled messages from known contacts. But it had a gap — if anyone else messaged the bot, nothing happened. No response, no record, no alert.

The new behaviour: when someone the bot doesn't recognise sends a message, it logs their name, their handle, and their chat ID. It checks whether they match any contact in the contacts file. It sends me a notification. And it replies to the unknown sender with a polite message explaining that this is a private bot.

Small addition. But now nothing that touches the bot disappears silently.

### The agent company

Late in the day, a planning session: design an AI agent company for personal operations. The idea — a set of agents, each with a specific role, that handles recurring tasks: scheduling, briefings, triage, daily digest — running on a schedule without requiring a session to be started.

The design is complete. The execution is not — that's for another day. But having the design documented means the build, when it happens, starts informed.

### The day that was.

The Telegram bot improved. An agent company designed.

What strikes me about this day is that the most important work is often invisible. Closing a gap in the bot means no interaction ever goes unlogged. Designing the agent company means the build, when it starts, won't start from scratch. Neither of these produced a visible output today. Both of them make every future session easier.

You can build this. Not all at once. Not in a day. But piece by piece, the way I've been doing it — one automation, one workflow, one small win at a time. And if you want help getting started, that's exactly what this site is for.

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/claude-code-days-march-15" style="text-decoration: none; color: #0366d6;">Next day →</a>
  </div>
  <div>
    <a href="/claude-code-days-march-13" style="text-decoration: none; color: #0366d6;">← Previous day</a>
  </div>
  <div>
    <a href="/claude-code-days" style="text-decoration: none; color: #0366d6;">Series Home (Claude Code Days)</a>
  </div>
</nav>
