---
layout: post
title: "My Day with Claude Code — March 14, 2026"
permalink: /claude-code-days-march-14
---

# My Day with Claude Code — March 14, 2026

There's a moment when automation stops feeling like a project and starts feeling like a service. March 14 was that moment.

<div style="background: #f0f0f7; border-radius: 6px; padding: 16px 20px; margin-bottom: 24px;" markdown="1">

**Quick read**

A day anchored by one task that mattered: a family member's flight check-in, handled end to end without them lifting a finger. Around that, bot infrastructure improvements and an agent planning session. Here's what happened:

- Completed a family member's IndiGo check-in — navigated the seat map, selected a seat, sent the boarding pass via Telegram and WhatsApp
- Worked through three automation gotchas along the way — each one fixed, each one documented
- Created a knowledge file covering check-in patterns for multiple airlines — reusable the next time
- Built unknown sender detection into the Telegram bot — it now logs and identifies anyone who contacts the bot unexpectedly
- Designed a full AI agent company for personal operations — planned, not yet executed

A day where the system proved it could handle something real.

</div>

<p style="margin-bottom: 32px;"></p>

### The check-in

The main task: check in a family member on an IndiGo flight from Bangalore to Calicut. Check-in opens 48 hours before departure. The automation should navigate to the airline's web check-in page, find the booking, work through the seat selection, and send the boarding pass.

In theory, straightforward. In practice, three things needed to be worked around.

First: checkboxes on the check-in page that wouldn't respond to a normal click because a label element was intercepting the interaction. The fix was to click the label directly rather than the checkbox.

Second: seat selection timing. The seat map loads asynchronously — it appears before the seats are actually interactive. Clicking too fast means clicking nothing. The fix was to wait for interactivity, not just visibility.

Third: the boarding pass. After seat selection, the flow moves to a print page with a different session state — the automation needed to handle that transition correctly or the boarding pass download would fail.

Three problems, three fixes. The check-in completed. Seat selected. Boarding pass downloaded. Sent via Telegram, then WhatsApp.

A family member got their boarding pass before they'd thought to check their email. That's not impressive as a technical achievement. It's impressive as a service.

### The knowledge file

After the check-in, we documented everything. Not just "here's how IndiGo works" — a proper knowledge file covering the patterns that apply across airlines: where check-in pages live, how seat maps typically load, how to handle the boarding pass step, what usually breaks.

IndiGo covered. Air India, Air India Express, Akasa — patterns documented based on prior experience. The file is live now. The next check-in starts from there, not from scratch.

This is something I try to do consistently: when you solve a problem that will recur, don't just solve it — write down how. The second time is always faster. The fifth time is nearly instant.

### The Telegram bot

In the background: an improvement to the Telegram bot that runs as my notification and control layer. The original bot handled messages from known contacts. But it had a gap — if anyone else messaged the bot, nothing happened. No response, no record, no alert.

The new behaviour: when someone the bot doesn't recognise sends a message, it logs their name, their handle, and their chat ID. It checks whether they match any contact in the contacts file. It sends me a notification. And it replies to the unknown sender with a polite message explaining that this is a private bot.

Small addition. But now nothing that touches the bot disappears silently.

### The agent company

Late in the day, a planning session: design an AI agent company for personal operations. The idea — a set of agents, each with a specific role, that handles recurring tasks: scheduling, briefings, triage, daily digest — running on a schedule without requiring a session to be started.

The design is complete. The execution is not — that's for another day. But having the design documented means the build, when it happens, starts informed.

### The day that was.

A family member checked in. Three gotchas worked through and documented. A knowledge file built. The Telegram bot improved. An agent company designed.

What strikes me about this day is the difference between a task being automated and a task being *handled*. The check-in wasn't just automated — it was done before anyone thought to ask. The boarding pass arrived before the question was raised. That's the shift you're building toward: not a faster way to do things, but a system where certain things just happen.

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
