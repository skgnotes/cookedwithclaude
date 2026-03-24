---
layout: post
title: "Institutional Memory Is a Skill"
permalink: /institutional-memory
---

# Institutional Memory Is a Skill

Three months into using Claude Code seriously, I asked it to draft a message to my EA.

It wrote something reasonable. Polite, clear, professional. Then I asked it again the next week. Same message, same tone, same adequate-but-generic result. Nothing wrong with it. Just nothing right with it either.

The problem wasn't the model. The problem was that I hadn't told it anything real. My EA and I have a shorthand. There are things she handles without being asked. There are things I handle before she can ask. There's a rhythm. Claude had no idea any of that existed.

That's when I understood what I was actually building.

## The ops file is not documentation

When I first started writing context files — a file about my EA, a file about how I communicate, a file about what I'm working on — I thought of it as setup. A one-time configuration task. Do it once, move on.

That framing was wrong.

The ops file is not documentation. It's not a README for a project. It is a live representation of how your world works, updated as your world changes. And building it well is a skill — one that most people never develop because they don't realize they need it.

The difference is this: documentation is written for someone who needs to understand a finished thing. Context files are written for an agent that needs to act in an ongoing world.

## What Claude actually needs to know

Not everything. That's the first mistake — trying to write down everything. You'll produce a wall of text that gets ignored.

What Claude needs is the operational skeleton: who's who, how things move, what the defaults are, where the exceptions live.

When I briefed my EA about a meeting, Claude used to ask me who she was every time. Not literally — but it had no idea of the relationship, the tone, the standing instructions. After I wrote a single file documenting her role, our communication pattern, and the key standing arrangements, the briefs it drafted stopped being adequate and started being useful.

The file is maybe 400 words. It has changed almost nothing since I wrote it. But it means Claude doesn't have to ask, and I don't have to explain. Every message it drafts from that point forward reflects something real.

That's the ROI calculation: time spent writing the file versus time spent re-explaining across every interaction forever. It's not even close.

## The compounding starts when you maintain it

The first iteration of my context files was rough. Incomplete. Wrong in places. It didn't matter, because rough and wrong is better than absent.

What matters more is maintaining the files — updating them when the world changes. When my EA started handling a new category of decisions, I added two sentences. When I moved to a different communication channel with one of my teams, I updated the comms file. When a new project became active, I added it to the overview.

None of these updates took more than five minutes. But each one meant Claude's model of my world stayed accurate. And an accurate model means fewer mistakes, fewer corrections, fewer moments where I have to say "no, that's not how we do things here."

The compounding is quiet. You don't notice it happening. You just notice that drafts need fewer edits, that Claude asks fewer clarifying questions, that it can operate rather than having to be supervised.

## The skill is knowing what to write

Here's where most people get stuck. They understand they should document their world, but they don't know what level of abstraction to aim for.

Too abstract and it's useless. "I run several businesses and work with a small team" tells Claude nothing it can act on.

Too detailed and it becomes noise. A five-page biography of every person in your life will never get read in full.

The right level is operational. What does Claude need to know to make a good decision on your behalf?

For people: their role, the standing arrangements, the tone defaults, the things that need to go through them versus around them.

For communication: the channels you use, the format preferences, the standing instructions like "always draft before sending" or "send directly, don't show me."

For projects: what it is, what's active, who's involved, what the current priorities are.

Write for a capable person who just started working with you. What would you tell them in the first week? That's your context file.

## The honest version

I didn't build my context files because I had a system in mind. I built them because I kept running into the same friction — asking Claude to do something, it doing it slightly wrong, me correcting it, and then the next time it doing it slightly wrong again.

At some point I realized the problem wasn't the model. The model was doing its best with the information it had. I was the one withholding the information.

The ops file is a transfer of knowledge — from your head into a place where an agent can act on it. That transfer takes time and attention. But it pays back every time you don't have to re-explain something you've already explained.

Institutional memory is a skill. You have to learn to build it. And once you do, the agent stops being a tool you use and starts being a system that operates.

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/per-client-ai-contexts" style="text-decoration: none; color: #0366d6;">Next: Running separate AI contexts for each client →</a>
  </div>
  <div>
    <a href="/posthog-mcp-no-dashboard" style="text-decoration: none; color: #0366d6;">← Previous: How I Query My Product Analytics Without Opening a Dashboard</a>
  </div>
  <div>
    <a href="/" style="text-decoration: none; color: #0366d6;">Home</a>
  </div>
</nav>
