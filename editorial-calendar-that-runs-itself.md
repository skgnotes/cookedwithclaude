---
layout: post
title: "Building an editorial calendar that runs itself"
permalink: /editorial-calendar-that-runs-itself
---

# Building an editorial calendar that runs itself

The last editorial meeting I ran lasted 47 minutes. We decided to publish two articles that week, argued about angles, and scheduled a follow-up to align on tone. A week later, I had a Telegram message waiting for me at 7 AM: "Draft ready — _drafts/editorial-calendar-that-runs-itself.md. Ready for Publisher."

No meeting. No scheduling. No calendar. A single trigger the previous evening, and by morning the queue had moved itself forward.

Here's how that works.

## Why editorial calendars fail operators

Most content calendars fail not because the content is bad but because the system requires constant human attention to keep it moving. Someone has to choose the next topic, brief the writer, review the draft, schedule the publish, and update the tracker. Each handoff is a decision point. Each decision point is a potential stall.

For a founder or operator running multiple things, that overhead is the actual cost — not the writing time. Writing is delegatable. Decision fatigue is not.

The fix isn't a better spreadsheet. It's removing the decisions from the loop entirely.

## The architecture: three agents, one orchestrator

The system has four components:

**A leveled content roadmap.** Topics are scored and tagged by type (essay vs. how-to) and complexity (1–10). This isn't just a backlog. Level 1–3 are standalone, self-contained pieces. Level 7–9 require lived context — the kind of article that can only be written by someone who's actually built the thing. The leveling tells the COO agent what to assign and when.

**A COO agent.** This is the orchestrator. It wakes on a schedule or on a Telegram trigger, checks the roadmap for the next appropriate item, and creates a task assigned to the Content Writer agent. It doesn't write. It doesn't judge angles. It reads a prioritized list and moves the queue.

**A Content Writer agent.** It receives the task, reads the brief and voice guide, writes the article to spec, anonymizes it, saves it to `_drafts/`, and marks the task done with the draft path and word count in the completion comment.

**A Content Publisher agent.** When the COO sees the Writer's task is done, it creates a new task for the Publisher. The Publisher reads the draft, runs the publishing checklist, updates navigation links, moves the file to the repo root, commits, pushes, and verifies the live URL loads correctly.

The whole chain runs on Paperclip — a task coordination layer that routes work between agents. Each agent wakes on assignment, does its job, and posts a completion comment. The COO reads those comments and moves the queue forward.

## What the trigger looks like

A single Telegram message to the bot:

```
/cooked
```

That's it. The COO agent wakes, checks the roadmap for the next queued item, creates a Writer task with the brief, and exits. The Writer picks it up in the next heartbeat. An hour or two later — or by morning if triggered in the evening — there's a draft in `_drafts/`.

If you want the queue to run on a schedule without any trigger, you add a cron. The COO checks every morning at 8 AM, sees if there's an open slot this week, and fires the pipeline if there is. You never think about it again.

## The roadmap structure that makes it work

The system only works if the roadmap is actually usable by an agent. That means:

- Each item has a title, a one-paragraph brief describing the angle
- Each item has a type tag (essay / how-to)
- Each item has a level (1–10 complexity)
- Items are roughly ordered by priority

The COO agent doesn't have opinions. It takes the next unclaimed item that fits the current brief (type balance, level appropriateness) and assigns it. You do the curation once — adding briefs, ordering, tagging — and then you step back.

The curation work is real. That's the part you can't fully automate. But you do it on your own schedule, in a single session, not distributed across dozens of small decisions embedded in your week.

## Something unexpected

The thing I didn't anticipate: the articles got better.

When I was running the calendar manually, I'd often pull topics forward because they felt timely or because I'd been thinking about them that week. That meant skipping the brief, improvising the angle, and hoping the draft landed. Sometimes it did. Often the articles felt reactive and undercooked.

The agent doesn't have moods. It takes the next prepared brief and executes to spec. The preparation I'd done when building the roadmap — the thinking about angle, the clarity about what the reader should take away — was all there in the brief. The writing was better because the thinking had been done at a different time, without deadline pressure.

Boring inputs, better outputs.

## How to start

You don't need to build the full pipeline on day one.

Start with the roadmap. Take your existing content backlog — wherever it lives — and add a brief, a type tag, and a rough level to each item. Ten items is enough to start. This is the work that unlocks everything else.

Once the roadmap exists, the COO agent has something to work from. The writer just needs the brief and the voice guide. The publisher just needs the draft and the checklist.

Build the orchestrator last. The hard part isn't the code — it's having a roadmap that's genuinely ready to be consumed by an agent that doesn't ask follow-up questions.

If a brief requires clarification, the system stalls. So make the briefs clear. Everything else follows from that.

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/delegation-vs-abdication" style="text-decoration: none; color: #0366d6;">Next: The Difference Between Delegation and Abdication →</a>
  </div>
  <div>
    <a href="/the-one-word-trigger" style="text-decoration: none; color: #0366d6;">← Previous: The One-Word Trigger</a>
  </div>
  <div>
    <a href="/" style="text-decoration: none; color: #0366d6;">Home</a>
  </div>
</nav>
