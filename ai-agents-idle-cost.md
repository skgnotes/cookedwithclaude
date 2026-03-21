---
layout: post
title: "Your AI team is burning money while it sleeps"
permalink: /ai-agents-idle-cost
---

# Your AI team is burning money while it sleeps

The bill showed up on a Thursday morning. Four agents. Seven days. Nothing assigned to any of them for most of that week.

The spend wasn't enormous — but it was there, and it had no business being there. These agents had done nothing. No tasks assigned. No work completed. The queue was empty. And they had still, quietly, cost money.

I dug in and found the problem immediately: polling intervals.

## What "always on" actually means

Every agent in the system had a default configuration that said: wake up every hour. Check for work. If there's nothing, exit.

That exit costs something.

Not much per wake. A little context loading. A quick API call. A short inference run that terminates before doing any real work. But four agents waking hourly for seven days — that's 672 idle wake cycles. At scale, it adds up. Even at a small operation, it's waste you didn't sanction.

The thing is, nobody set this up deliberately. "Wake every hour" was the default. Nobody had a reason to change it. The agents were assigned work manually, so the polling felt like a safety net — what if an assignment came in between heartbeats?

That reasoning sounds fine until you notice that the assignments don't come in randomly. They come in because a person created them. And that person could just as easily trigger a wake directly.

## The fix is one config change

Every serious agent orchestration system has a way to switch from polling to event-driven wakes. In the one I was using, the config key was `intervalSec`. The default was `3600` — once an hour. Setting it to `0` disables polling entirely. The agent only wakes when explicitly triggered: a new assignment, a comment mention, an approval event.

That's it. One value, one file, per agent.

After the change: zero idle spend. Agents wake when there's work. They finish, exit, and cost nothing until they're needed again. Response time didn't change — event-driven wakes are just as fast as the next scheduled poll, and usually faster.

## Why this happens

There's an assumption baked into most default configs: agents should be responsive. The fear is that if something is assigned and the agent is asleep, there'll be a delay. So the default is "wake frequently." It feels like the safe choice.

But "frequently" and "idle" are the same thing when there's nothing to do. You've built a system that checks in hourly to discover it has nothing to do — and you pay for that discovery.

The more honest framing: agents don't need to check for work. Work needs to go find the agents. That's what event-driven dispatch does. When a task is created and assigned, the system pings the agent. The agent wakes, does the work, exits. Nothing polls. Nothing idles.

This is how any sane infrastructure works. You don't keep a server processing loop running when no requests are coming in. You don't pay for a Lambda that's just waiting. The same logic applies to AI agents.

## What to check in your setup

If you're running agents on any kind of scheduled heartbeat, find the interval config and ask: does this agent need to wake when nothing is assigned?

For most agents, the answer is no. If assignments come through a system that can send a trigger on creation, polling is redundant. Turn it off.

The agents that might need polling: ones that check external state you don't control. An agent watching an inbox that doesn't emit events. A monitor checking a third-party API. For those, polling makes sense. Set a sensible interval — maybe every 15 or 30 minutes instead of hourly.

Everything else: event-driven.

## The bill you weren't watching

The honest version of this story is that I had set up an AI team, assigned them roles, and then stopped thinking about the infrastructure. The work was getting done. The system was running. I assumed that meant it was running cleanly.

It wasn't. It was running with the training wheels still on — defaults that made sense at setup, when you want responsiveness before you've figured out the triggering model, but that should've been tightened weeks earlier.

This is the hidden cost of "always on": it's not about the agents being on. It's about the agents being on when they have nothing to do. The spend is small enough per cycle that it never screams at you. It just accumulates, quietly, in a line item you weren't watching.

One config change fixed it. The only cost was the week before I looked.

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/command-vocabulary" style="text-decoration: none; color: #0366d6;">← Previous: Your command vocabulary</a>
  </div>
  <div>
    <a href="/" style="text-decoration: none; color: #0366d6;">Home</a>
  </div>
</nav>
