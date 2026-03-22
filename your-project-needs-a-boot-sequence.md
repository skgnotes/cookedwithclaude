---
layout: post
title: "Your project needs a boot sequence"
permalink: /your-project-needs-a-boot-sequence
---

# Your project needs a boot sequence

Every session with Claude starts clean.

No memory of last week's decisions. No awareness of who the stakeholders are, what's already been tried, or what conventions your project follows. If you've been re-explaining your setup at the top of every conversation, that's a tax you're paying that doesn't have to exist.

A boot sequence eliminates it.

## What a boot sequence is

It's a single file — typically `CLAUDE.md` or `AGENTS.md` — that lives in your project directory and gets loaded automatically at the start of every Claude Code session.

Not documentation. Not a README. A session initializer.

The difference is intent. Documentation explains what the project is. A boot sequence tells Claude how to work on it — what context to load, what conventions to follow, what to do first.

## Why it matters more than you think

The hidden cost of a missing boot sequence isn't the 30 seconds you spend re-explaining. It's the drift.

Every session without one, you explain slightly differently. Claude builds a slightly different mental model. Over time, inconsistency compounds — in tone, in approach, in decisions that should have been settled once.

A boot sequence is how you make your project decisions sticky.

## How to build one

Start with what you'd say at the top of every conversation if you were briefing someone new.

For a content project, that might be: who the audience is, what the publishing workflow looks like, which files hold the working context, what the conventions are for naming and structure.

For a client engagement, it might be: who the client is, what the goal of the engagement is, where the working documents live, what's been decided already, who to loop in on what.

Write it in plain language, in sections. Keep it under 500 words for most projects. The goal is loading context fast, not comprehensiveness.

Then save it as `CLAUDE.md` in the root of your project directory. Claude Code reads this file automatically at session start.

## What a real one looks like

For a multi-agent content pipeline — where different Claude agents handle writing, publishing, and coordination as separate roles — each agent has its own boot file.

The writer agent's file specifies: the working directory, the key context files (voice guide, brand overview, style guide), the exact workflow steps to follow on each session, the output format, where to save drafts, and how to report completion.

None of that context lives in the agent's memory. It lives in the file. Every session, the agent boots into the same operating context — same conventions, same workflow, same quality bar.

When you read that file, it doesn't look like documentation. It looks like standing orders.

## The thing that surprised me

The boot sequence surfaced decisions I hadn't consciously made.

Writing it forced me to answer: what does "done" look like? What files are authoritative? What does the workflow actually do, in sequence?

Some of those questions I'd been answering inconsistently across sessions without realizing it. The file made the inconsistency visible. That turned out to be half the value.

## Where to start

Pick your most active project — the one where you're in Claude Code most often.

Write one paragraph: what the project is, what you're currently working on, and what conventions matter. Save it as `CLAUDE.md` in that directory. Start the next session and see what changes.

That's the whole starting point. You can add to it as you notice what you keep re-explaining.

The file gets better every time you wish you didn't have to say something again.

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/setting-up-obsidian" style="text-decoration: none; color: #0366d6;">← Previous: Setting up Obsidian and why</a>
  </div>
  <div>
    <a href="/" style="text-decoration: none; color: #0366d6;">Home</a>
  </div>
</nav>
