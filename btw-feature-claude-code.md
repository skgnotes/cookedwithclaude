---
layout: post
title: "Off the record"
permalink: /btw-feature-claude-code
---

# Off the record

Not every question needs to become part of the session.

There's a category of question that surfaces mid-session that isn't really a task or a direction change. It's a sanity check. A quick clarification. A "does this approach make sense before I keep going." You want an answer, but you don't need Claude to carry that exchange for the rest of the session.

Before `/btw`, asking that question meant adding it to the conversation history. It joined the context window, factored into everything Claude calculated going forward, and inflated the cost of the session slightly — for a question that was essentially transient.

`/btw` is the off-the-record version.

## What it actually does

`/btw` is a side question. You prefix your query and ask it as a normal message. Claude reads it from your current session context and answers. Then the exchange disappears. The question and answer don't get written into the conversation history. The context window doesn't grow. The session continues where it left off.

The distinction matters:

- A normal question goes on the record. It shapes context going forward.
- A `/btw` question is answered, then gone. The session doesn't know it happened.

It's a recent addition to Claude Code — shipped in early 2026 — and it's a small feature that addresses something real for anyone running long sessions.

## Why long sessions care

Context accumulates. Every question, clarification, and instruction you've asked sits in the window and adds to what Claude is carrying. For operators running Claude Code across involved workflows — coordinating tasks, building automations, running multi-step processes — sessions can run long and context can bloat.

Some of that bloat is unavoidable. A lot of it is questions that didn't need to persist but did, because there wasn't another way to ask them.

## Where it earns its place

A few situations where `/btw` is the right tool:

**Sanity checks.** You're part way through a workflow and want to ask: does the approach I'm taking here make sense? You get an answer from Claude's knowledge of your session without the check itself becoming part of the session's running context.

**Quick clarifications.** You're drafting something and want to ask whether the tone is right for this contact, or whether a particular term means what you think it means in this context. Transient question, transient answer.

**Reference lookups.** You remember something vague mid-session — how a setting works, what format is correct, what the right pattern is for something. `/btw` is faster than switching context and doesn't add noise to the conversation.

What these have in common: the question is one-off. It doesn't need to be carried.

## The constraint to know

`/btw` answers from your current session context only. It has no tool access — it won't check a file, run a command, or fetch anything. If your question requires Claude to look something up or take an action, you need to ask that normally.

Think of `/btw` as: questions Claude can answer from what it already knows in this session. Use it for checks and clarifications, not for requests.

## The cost angle

The side question reuses the parent conversation's prompt cache. The additional token cost is minimal — far less than asking the same question as a regular message and having it baked into every subsequent prompt in the session.

For anyone running sessions long enough to think about cost, this matters. Every question that doesn't need to be in the permanent context is overhead you don't have to pay.

## How to start

The syntax is simple: prefix your question with `/btw` and send it.

```
/btw Is the approach I'm taking here going to cause formatting issues downstream?
```

You get the answer. The session moves on.

The habit worth building: before asking a question mid-session, pause for two seconds and ask whether it needs to be on the record. Sanity checks, clarifications, quick references — they usually don't. `/btw` gives you somewhere to put them.

The questions that matter for the session, ask normally. The rest — ask off the record.

<nav style="margin-top: 48px; padding-top: 24px; border-top: 1px solid #eee; font-size: 14px;">
  <div>
    <a href="/curiosity-and-a-mentor" style="text-decoration: none; color: #0366d6;">Next: Curiosity and a mentor →</a>
  </div>
  <div>
    <a href="/company-that-runs-itself" style="text-decoration: none; color: #0366d6;">← Previous: The company that runs itself</a>
  </div>
  <div>
    <a href="/" style="text-decoration: none; color: #0366d6;">Home</a>
  </div>
</nav>
