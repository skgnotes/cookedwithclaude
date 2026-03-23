---
layout: post
title: "The One-Word Trigger"
permalink: /the-one-word-trigger
---

# The One-Word Trigger

One word. That's what it takes now.

I type a topic into Telegram — something like "write about morning routines" or even just a two-word subject line — and five agents wake up, coordinate, write, review, and publish a full article to my blog. By the time I've put my phone down, the pipeline is already running.

That's the outcome. Here's how it works, and why the design pattern matters for anything you want to automate at this level.

## Why This Matters Before We Get to How

Most automation stops at task automation. You wire up a Zapier or a shell script, and something that used to take ten minutes now takes one. Useful, but not the same thing.

What a multi-agent pipeline does is different. It's not automating a task — it's automating a workflow that requires judgment at multiple points. Research. Editorial decisions. Voice calibration. Quality review. Publishing mechanics. Each one of those used to require me. Now they don't.

The reason the trigger matters is that the trigger is the only thing that does. If you have to hand-hold the process at any point, you haven't built a pipeline — you've built a longer to-do list.

## The Pipeline

Five agents, running in sequence:

**Researcher** gets the topic. Searches the web, reads related articles, gathers context. Produces a research brief.

**COO** acts as editorial coordinator. Reads the brief, checks the content backlog, decides the angle. Creates a task for the Content Writer with a specific frame — not just "write about X" but "write about X from this angle, at this level, for this reader."

**Content Writer** writes the full draft. Reads the voice guide before every article. Follows the site style. Saves to `_drafts/`.

**Content Publisher** picks up the draft. Validates front matter, checks formatting, anonymizes where needed, updates the navigation, commits, and pushes to GitHub. The article goes live.

**Telegram Bot** closes the loop. Sends me a link when it's done.

The whole thing runs without any human in the loop after that first message.

## The Design Pattern

Here's what makes this replicable for your own workflows.

**One canonical entry point.** All triggers come in through Telegram. Not email, not a web form, not a direct API call — one channel, one protocol. This is the lesson I keep relearning: the simpler the trigger surface, the more reliably you'll use it.

**Structured handoffs.** Each agent passes a specific artifact to the next. The Researcher doesn't just "finish" — it produces a brief with a specific shape. The COO doesn't just "decide" — it creates a Paperclip task with a title, description, angle, and level. The Writer doesn't just "write" — it saves to a known path and marks done with the path and word count in the completion comment.

Agents don't hand off vibes. They hand off structured data.

**The COO as traffic cop.** This is the piece most people skip. You don't go from trigger directly to execution. There's a coordination layer in the middle that reads context, makes editorial decisions, and routes work to the right agent with the right frame. Without this, you get five agents doing five things that don't cohere. With it, you get a pipeline.

**Blocking, not calling.** Each agent in the chain waits for the previous one to mark its task done before picking up work. This isn't asynchronous fire-and-forget — it's a sequential queue with checkpoints. Slower, but reliable. The COO creates a task for the Content Writer, marks its own task done, and the Writer's heartbeat picks it up on the next cycle.

**Paperclip as the coordination layer.** The agents don't talk to each other directly. They talk through a shared task system. The COO creates a task, the Writer reads it. The Publisher knows to look for `_drafts/` because the Writer's completion comment always contains the path. The shared protocol is what makes the handoffs work even across agents that were built independently.

## What Surprised Me

The research agent is the one that changed the output quality most.

Before adding it, I was relying on my own framing when I sent the trigger — "write a how-to about setting up Obsidian" — and the pipeline would execute faithfully against whatever I had in my head. Often fine. Occasionally thin.

With a research pass first, the COO has actual material to work with when it frames the article. It can see what's already been covered, what angles are overdone, what's missing from the conversation. The editorial decision gets better because it's informed.

That's a general principle: the more context flows into each handoff, the better the output. The agents themselves haven't changed. What changed is what they have to work with.

## The Other Thing

There's a failure mode worth naming. When I first built this, the pipeline would occasionally produce an article that was technically correct — right voice, right structure, right word count — but that I didn't actually want to publish. Not because it was bad, but because the topic had come in too loose, and the COO had made reasonable choices I disagreed with after the fact.

The fix wasn't to add more human checkpoints. It was to tighten the trigger. "Morning routines" is a bad trigger. "How I use a 6 AM Telegram brief to start the day without touching email" is a good trigger. The more specific the input, the less interpretation the pipeline has to do, and the more the output matches what you wanted.

Garbage in, garbage out hasn't stopped being true just because the process is autonomous.

## How to Start

You don't need five agents to use this pattern.

Start with one handoff. Pick a task you do regularly that has two distinct steps — one that produces a document, and one that does something with that document. Wire a trigger to the first. Have the first agent hand off a structured artifact. Have the second agent pick it up.

That's a pipeline. Not because of the technology, but because of the structure: one trigger, one artifact, one handoff, one outcome.

Add agents when you find the bottleneck. The reason I have five is that each one was added to remove a point where I was still in the loop. That's the only good reason to add another agent: because there's somewhere in the workflow where you're still being asked to show up.

When you're not being asked to show up anywhere, you've built what I mean by a pipeline.

The word goes in. The article comes out. Everything in between runs itself.

---

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/editorial-calendar-that-runs-itself" style="text-decoration: none; color: #0366d6;">Next: Building an editorial calendar that runs itself →</a>
  </div>
  <div>
    <a href="/personal-operating-system-flat-files" style="text-decoration: none; color: #0366d6;">← Previous: How I Built a Personal Operating System with Flat Files</a>
  </div>
  <div>
    <a href="/" style="text-decoration: none; color: #0366d6;">Home</a>
  </div>
</nav>
