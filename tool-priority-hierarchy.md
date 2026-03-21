---
layout: post
title: "The Tool Priority Hierarchy"
permalink: /tool-priority-hierarchy
---

# The Tool Priority Hierarchy

At some point I started noticing a pattern in how Claude Code was failing me.

Not failing dramatically. Failing in small, annoying ways. A task that should take three seconds taking forty-five. A browser window spinning open to send a Telegram message. Playwright navigating to a page to check something that a one-line API call could return instantly. The results were correct. But the path to them was wrong.

I had 29 of these friction incidents logged over six weeks. Same root cause every time: Claude chose the heavy tool when a lighter one was available.

## The Wrong Tool Is the Problem

When a task involves sending a message, there are several ways to do it. You could open a browser, navigate to the web app, find the compose button, type the message, send it, close the browser. Or you could call the API. Or run a script you already have.

All three produce the same result. The difference is everything else: speed, reliability, side effects, and whether the approach feels coherent or cobbled together.

An AI assistant that reaches for the browser every time because it "works" is like a contractor who uses a sledgehammer for every nail. Technically functional. Practically exhausting.

The problem gets worse because AI assistants don't default to the lightest tool — they default to the most visible one. Browser automation is demonstrable. You can watch it work. A curl call is invisible and instant. Invisibility looks like nothing happened. Demonstrability looks like capability. The wrong incentive structure, if you're trying to build something fast and reliable.

## The Hierarchy

The fix was simple: encode a priority rule in CLAUDE.md.

```
Tool priority: Direct API → CLI/scripts → Playwright (browser automation)
Never use Playwright for something a shell script can do.
Never use browser automation when a CLI tool exists.
```

Three lines. One rule. The whole category of friction disappeared.

The hierarchy has a logic to it. APIs are the authoritative interface — fast, unambiguous, designed for programmatic use. CLIs and scripts are the next layer — they abstract the API into something human-runnable, with sensible defaults, error handling, existing patterns. Browser automation is the fallback for systems that have no API and no CLI — legacy web apps, authentication flows that resist automation, anything that only works in a browser.

Moving up that chain in the wrong direction — using Playwright to call what should be an API — is not just inefficient. It's fragile. Browsers break on DOM changes. Headless flows fail on CAPTCHA. A selector that worked last week stops working this week. You've built something brittle when something solid was available.

## What Changes When You Write It Down

The interesting thing is that this rule isn't controversial. Any developer would agree with it immediately. The problem isn't knowledge — it's recall at the moment of decision.

When an AI assistant is mid-task and needs to send a notification, it doesn't stop and reason through the hierarchy. It pattern-matches on "how do I do this" and reaches for whatever it has seen succeed before. If the most reinforced pattern is browser automation, it uses browser automation.

Writing the hierarchy into CLAUDE.md changes what gets pattern-matched. It makes the rule part of the operating context, not something that has to be reasoned through from scratch each time.

This is a broader point about CLAUDE.md that I've come back to repeatedly: the file isn't for things Claude doesn't know. It's for things Claude knows but won't prioritise without being told.

The hierarchy was obvious once I named it. The problem was that obvious things don't get applied consistently unless they're encoded.

## Friction Compounds

Twenty-nine friction incidents over six weeks is roughly one per day. Each individual incident is minor — a few seconds of extra load time, a browser window that shouldn't have opened. But each one also breaks flow. You notice the wrong tool was used. You feel the drag of an inefficient system.

Worse: you start working around it. You add notes about specific tasks. You add exceptions. You build a patchwork of corrections instead of a single governing rule.

The hierarchy replaced the patchwork. After I added it, I stopped logging friction incidents in that category entirely. Not because I stopped paying attention — because there was nothing to log.

One rule, stated plainly, applied consistently. That's the ceiling of what a three-line addition to a config file can do.

The meta-lesson is harder to encode: most recurring friction has a governing principle behind it. You can fix it incident by incident, or you can find the principle and fix the whole category at once.

The second approach takes longer once and saves time forever.

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/context-engineering" style="text-decoration: none; color: #0366d6;">Next: Context engineering, not prompt engineering →</a>
  </div>
  <div>
    <a href="/skip-cowork" style="text-decoration: none; color: #0366d6;">← Previous: What you're actually paying for at a coworking space</a>
  </div>
  <div>
    <a href="/" style="text-decoration: none; color: #0366d6;">Home</a>
  </div>
</nav>
