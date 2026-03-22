---
layout: post
title: "My Day with Claude Code — March 20, 2026"
permalink: /claude-code-days-march-20
---

# My Day with Claude Code — March 20, 2026

Some days have a shape to them. March 20 had the shape of a wall — and everything happening around it.

<div style="background: #f0f0f7; border-radius: 6px; padding: 16px 20px; margin-bottom: 24px;" markdown="1">

**Quick read**

The main project hit a regulatory wall. Everything around it kept moving. And the day ended with a live demonstration — for an accountant exploring AI for their firm — that turned abstract into witnessed. Here's what happened:

- Built a working voice AI for delivery agents: they call a number, the AI answers and gives the exact address and directions in natural language
- Hit the wall: every Indian phone number provider requires full government KYC — no self-serve path, no sandbox. Email sent. Waiting.
- Diagnosed why the morning health check had gone completely silent: a one-line fix. Expanded from 9 checks to 14 while in there.
- Discovered that the mobile control feature I'd been planning to build already ships natively with Claude Code — saved a day's work
- Built a skill that logs into the Income Tax portal, pulls the latest notice for a given entity, and forwards it to the accountant on WhatsApp with a summary
- Ran it live for two entities in the same session. The accountant was watching.

Some days you build. Some days you fix. Some days you clear a path for something that'll land later. This was all three.

</div>

<p style="margin-bottom: 32px;"></p>

### The voice AI

The main project was something I'd been genuinely excited about: a voice AI for a client that handles inbound calls from delivery agents. The need is real and simple — a delivery person is standing outside an unfamiliar building at 8pm, trying to reach the customer. Instead of a missed call and a failed delivery, they call a number, the AI picks up, and gives them the exact address and directions in natural language. The whole thing was built and working: voice handling, speech recognition, AI reasoning, natural speech output. A complete system.

### The wall

The only thing missing was a real Indian phone number. And that, it turned out, was the wall.

Every provider I went to — four of them — requires full government KYC before they'll issue an Indian number. Not a quick ID check. Full KYC, manual process, no self-serve path. One provider requires a minimum twelve-month commitment just to begin. It's a regulatory reality, not anyone's fault. But the AI was sitting there, working, waiting for a phone to ring, and the phone didn't exist yet.

I sent a KYC initiation email to the provider that looked most workable and documented the full project state — what's built, what's blocked, what the path forward looks like. The MVP exists. It just needs a number to live on. Sometimes the last five percent is the hardest five percent.

### When the automation went quiet

While that email was in flight, I turned to something quieter but equally important: figuring out why the morning health check had gone completely silent for the past few days.

No errors. No reports. Just nothing. When an automation disappears without making any noise, the instinct is to assume something complex broke. The actual cause was simpler: the scheduled automation was running in an environment where most of the tools it needed weren't visible to it. One line added to the script. The failure had been quietly logging to an error file the entire time. It was there, waiting to be read.

The lesson that keeps coming up: when an automation goes quiet, check the error log before assuming anything. The system almost always tells you what's wrong. You just have to ask.

After the fix, I ran the health check directly to confirm — and expanded it while I was in there. Nine checks became fourteen. One of the additions corrected a check that had been hitting the wrong URL for months, quietly passing when it shouldn't have been. Fourteen out of fourteen now passing cleanly.

### Already built

Then something that shifted how I think about a piece of work I'd been planning: I discovered that the mobile control feature I was intending to build as a custom skill already ships with Claude Code as a native command. It exists, it works, and it creates an interactive session you can connect to from the Claude mobile app or a shareable web link. The mobile app finds it automatically. What I needed to work out was the startup pattern — how to launch it cleanly from a background session. Small thing. Saved a day's work.

### The notice run

The day ended with something that felt genuinely significant. I built and ran a skill that logs into the Income Tax portal, navigates to the notices section, pulls the latest notice PDF for a given entity, and forwards it to the accountant on WhatsApp with a brief summary of what it is.

Ran it live for two entities. Both notices pulled. Both PDFs named cleanly. Both forwarded with context — in the same session.

The reason this mattered beyond the operational value: the accountant who handles tax matters for several entities I'm involved with has been exploring AI enablement for their firm. The notice run was partly a demonstration. There's a difference between describing what AI can do and watching it log in, pull a notice, and forward it on WhatsApp while you're sitting in the room. That difference — between abstract and witnessed — is where adoption actually happens.

### The day that was.

A voice AI built and waiting for a phone number. A regulatory wall documented and queued. A silent automation diagnosed and fixed. Health checks expanded to 14. A day's planned work discovered to already exist. Two income tax notices pulled and forwarded, live.

What strikes me about a day like this is what happened around the wall. The voice AI is real. The notice skill is real. The health check is running cleanly. A planned day's work turned out to already exist. The regulatory blocker is frustrating — but it's one email in flight, one process started. Everything else moved anyway. That's the thing about working this way: even when the main thing is stuck, the rest doesn't stop.

You can build this. Not all at once. Not in a day. But piece by piece, the way I've been doing it — one automation, one workflow, one small win at a time. And if you want help getting started, that's exactly what this site is for.

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/claude-code-days-march-21" style="text-decoration: none; color: #0366d6;">Next: My Day with Claude Code — March 21 →</a>
  </div>
  <div>
    <a href="/claude-code-days-march-19" style="text-decoration: none; color: #0366d6;">← Previous: My Day with Claude Code — March 19</a>
  </div>
  <div>
    <a href="/claude-code-days" style="text-decoration: none; color: #0366d6;">Go to My Day with Claude Code (series) Home</a>
  </div>
</nav>
