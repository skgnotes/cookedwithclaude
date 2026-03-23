---
layout: post
title: "How to Run Your Weekly Review with AI"
permalink: /weekly-review-with-ai
---

# How to Run Your Weekly Review with AI

The weekly review used to take me two hours and leave me feeling vaguely guilty about everything I hadn't done. Now it takes twenty minutes and ends with a clear list of what actually matters this week.

The difference: Claude does the processing. I make the calls.

## Why the weekly review usually doesn't happen

GTD practitioners know the weekly review is the keystone habit. Without it, your system degrades within days. Open loops accumulate. Priorities drift. You start operating on vibes instead of data.

And yet most operators don't do it consistently. Not because they don't believe in it — they do — but because doing it properly requires pulling together information from a dozen places: email threads, notes apps, calendar, Slack, half-finished documents, mental notes you made in the car. By the time you've assembled the inputs, you're exhausted and the review never really happens.

The problem is the assembly cost. If you can eliminate that, the review becomes trivial.

## What the system looks like

The weekly review prompt assumes three files exist:

- `actions.md` — your running list of open tasks, commitments, and things to watch. One file, plain text, updated as things come in.
- `session-log.md` — a dated log of what actually happened each week. What was completed, what was started, what shifted.
- `lifemap.md` — upcoming items: scheduled commitments, deadlines, things that are coming but haven't landed in your task list yet.

You don't need all three to start. Even with just `actions.md`, this works.

## The review prompt

This is the prompt I run at the end of the week:

```
Read actions.md, session-log.md, and lifemap.md.

Do the following:
1. List everything in actions.md that has been open for more than 2 weeks with no movement.
2. List commitments I made to others (things I said I'd send, do, or follow up on).
3. List anything in lifemap.md coming up in the next 14 days.
4. Look at the session logs for this week — what got done, what didn't, what carried forward.
5. Based on all of the above, propose a prioritised focus list for next week: the 5 things that actually need to move.

Then ask me: what did you ship this week that isn't captured here?
```

That last question is the one that matters most.

## What Claude does vs what you do

Claude reads the files and surfaces the picture. It's good at this — it doesn't get tired halfway through `actions.md`, doesn't skip the uncomfortable item, doesn't forget the thing from three weeks ago.

What it can't do: decide what matters. It doesn't know that the meeting with your investor is more strategically loaded than it appears on the calendar. It doesn't know you've been avoiding a particular decision because the answer is going to be difficult. It doesn't know your energy levels or what kind of week you can actually run.

So the review has two parts. Claude assembles. You adjudicate.

Read what Claude surfaces. Then answer: Is this the right list? What's missing? What on this list is actually someone else's problem?

The output is a revised `actions.md` — trimmed, prioritised, with anything genuinely dead removed.

## The thing I didn't expect

The stale items list is brutal.

The first time I ran this, Claude pulled up seven things that had been sitting in my actions list for more than a month. Some I'd genuinely forgotten. One I'd been telling myself I'd get to. Two I'd already decided not to do — but hadn't removed from the list because removing things from a task list feels like admitting defeat.

Seeing them listed neutrally, without judgment, made it easy to cut. I archived four of them in thirty seconds. They'd been generating low-level anxiety for weeks.

This is the real value of the weekly review done properly: not the planning, but the clearing. The system working as intended.

## How to start

Don't build the whole system first. Start with one file.

Create `actions.md`. Write down everything you're tracking in your head right now — every open loop, every thing you said you'd do. Don't organise it. Just get it out.

Then run a simple version of the prompt above: *Read this file. What's been open longest? What involves a commitment to someone else? What can be cut?*

Do that once. See what it surfaces. Then add the session log next week, and the lifemap the week after.

The weekly review is a habit before it's a system. Get the habit first.

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/the-memo-you-never-wrote" style="text-decoration: none; color: #0366d6;">Next: The Memo You Never Wrote →</a>
  </div>
  <div>
    <a href="/second-brain-works-now" style="text-decoration: none; color: #0366d6;">← Previous: The Second Brain Actually Works Now</a>
  </div>
  <div>
    <a href="/" style="text-decoration: none; color: #0366d6;">Home</a>
  </div>
</nav>
