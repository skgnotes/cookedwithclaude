---
layout: post
title: "The Idea Bank: A Content Capture System That Runs Itself"
permalink: /the-idea-bank
---

# The Idea Bank: A Content Capture System That Runs Itself

Every session with Claude Code produces something worth writing about. A pattern you discovered. A workflow that clicked. A failure that taught you something. The problem isn't that you don't have ideas — it's that they evaporate the moment the session ends and you switch back to the thing you were actually supposed to be doing.

The Idea Bank solves this with one markdown file and a standing instruction to Claude.

## What you end up with

A structured, tagged backlog that grows automatically. Every session deposits its captures. When you sit down to write, you're not staring at a blank page — you're triaging a queue.

Ideas arrive tagged by type (how-to, essay, concept), level of effort, and angle. Some are two words. Some are full paragraphs. All of them are in one place.

You didn't do any of the filing.

## Why most content capture systems fail

They require a separate action. You finish a good session, you think "I should capture that," and then life intervenes. The context is gone within hours.

Any system that depends on you remembering to capture is a system that will fail at exactly the moments it matters most — the moments when you're deep in execution mode and your brain doesn't have capacity for meta-work.

The fix is to make capture a byproduct of sessions you're already running, not a task that competes with them.

## How the Idea Bank works

The whole thing lives in a single file — `Idea Bank.md` — in your project folder. It has three sections:

**Published** — a strikethrough list of articles you've shipped. Visible history, nothing more.

**Idea Backlog** — the queue. Each entry is a one-liner or short paragraph. Tagged with type, level, and angle. No formatting rules beyond that.

**Session Captures** — a raw append-only log. Date-stamped. Whatever came up in the session goes here first, before it gets refined into the backlog.

The distinction matters. Session Captures are messy. You're not editing while capturing. You're just dumping. The refinement happens later, during a dedicated session, when you move captures into the backlog with tags.

Or you let Claude do that too.

## Priming Claude to populate it

This is the step most people miss. The file alone doesn't do anything — you need Claude to know it exists and what to do with it.

Add a standing instruction to your project's CLAUDE.md (or wherever you keep your session-level instructions):

```
After any session that involves a new pattern, workflow, or insight, append a dated entry to Idea Bank.md under Session Captures. Include: what was built or discovered, why it matters, and a possible angle for an article. Don't editorialize — just capture.
```

That's it. Now every session that produces something interesting ends with an automatic deposit.

You'll also want a separate instruction for the refinement pass:

```
During content planning sessions, review Session Captures and move ready ideas into the Idea Backlog. Tag each with: Type (how-to / essay / concept), Level (1–5 for effort), Angle (one sentence on the specific framing). Archive the Session Captures entry once moved.
```

With both instructions in place, the system captures automatically and refines on demand.

## The tagging system

Level is the most useful tag. It isn't effort — it's how foundational the article is for the reader. Level 1 ideas need almost no Claude Code background. Level 5 assumes you're running a full multi-agent setup.

This matters because your audience grows with you. Early readers are curious beginners. Later readers are operators running systems. The tag tells you which article to write next depending on where your audience is.

Type distinguishes how-tos from essays. How-tos are replicable — specific setup, specific outcome. Essays are idea-driven — one observation, one principle. Both have their place, but they require completely different structures. Tagging the intention upfront saves you from a messy draft that doesn't know what it wants to be.

Angle is the most valuable tag. A topic without an angle is just a topic. "Claude Code prompting" is not an article. "Why your Claude prompts are failing because you're treating them like Google searches" is. The angle is the reason someone reads past the first paragraph.

## What surprised me

The Session Captures section turns out to be more valuable than the backlog.

The backlog is refined and ordered. But the captures are raw — and often the rawness is where the actual insight is. When I go back and read a capture from three sessions ago, I sometimes find a better angle than the one I'd originally tagged. The messy version remembered something the clean version edited out.

I've started treating Session Captures as a first draft of my thinking, not just an inbox.

## Where to start

Create `Idea Bank.md` with three headers: Published, Idea Backlog, Session Captures.

Add one line to your CLAUDE.md: "After sessions with new patterns, append a dated entry to Idea Bank.md under Session Captures."

Run a session. Check the file when you're done.

If Claude populated it — and it will — you have a system. Everything else is refinement.

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/advice-is-not-action" style="text-decoration: none; color: #0366d6;">Next: Advice Is Not Action →</a>
  </div>
  <div>
    <a href="/your-project-needs-a-boot-sequence" style="text-decoration: none; color: #0366d6;">← Previous: Your project needs a boot sequence</a>
  </div>
  <div>
    <a href="/" style="text-decoration: none; color: #0366d6;">Home</a>
  </div>
</nav>
