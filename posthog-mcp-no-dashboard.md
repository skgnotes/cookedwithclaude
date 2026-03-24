---
layout: post
title: "How I Query My Product Analytics Without Opening a Dashboard"
permalink: /posthog-mcp-no-dashboard
---

# How I Query My Product Analytics Without Opening a Dashboard

The last time I opened a PostHog dashboard was weeks ago.

That's not because I stopped caring about the numbers. It's because I no longer need the dashboard to get the numbers.

## What Changed

PostHog has an MCP server. Claude Code has MCP support. When you connect the two, you can ask questions about your product in plain language and get answers back — no tab switching, no filter menus, no waiting for a chart to load.

I run a SaaS product. I want to know things like: how many users activated this week, where they're dropping in the onboarding funnel, whether a specific feature is being used. Before, that meant opening PostHog, navigating to the right insight, adjusting the date range, maybe building a new query from scratch. It was never fast, and I almost never remembered how I'd set up the filters last time.

Now I type it into Claude Code and get an answer in seconds. The answer comes back with context, not just a number.

## The Setup

You need the PostHog MCP server running in your Claude Code config. PostHog ships an official MCP server — add it to your `claude_desktop_config.json` or `settings.json` depending on your setup. You'll need a PostHog API key and your project ID.

Once it's connected, Claude has access to a set of tools that can query your PostHog project: trends, funnels, retention, feature flags, event definitions, user lists. The full product analytics surface, callable from a conversation.

No extra infrastructure. No custom scripts. The MCP server handles authentication and the query translation.

## What I Actually Ask

The queries I run most often are things like:

- "How many unique users triggered the signup event this week versus last week?"
- "Show me the funnel from signup to first project created — where's the biggest drop-off?"
- "Which users activated in the last 7 days but haven't returned since?"
- "Is the new onboarding feature flag enabled for more than 50% of users?"

Claude calls the right PostHog MCP tool, runs the query, and returns the result in plain text with a short interpretation. If the result is ambiguous, it says so. If the query needs refinement — wrong date range, unclear event name — it asks one clarifying question and tries again.

What I didn't expect: it's often faster to describe what I want than to know which PostHog insight type I need. I sometimes wouldn't remember if I wanted a Trend, a Funnel, or a Retention view. I'd just ask the question and Claude would figure out the right query structure.

## The Operator Shift

The insight here isn't that Claude is smarter than PostHog. PostHog is excellent software. The insight is that the bottleneck in using analytics isn't the data — it's the attention cost of switching contexts and navigating a UI.

When I have a question in the middle of a working session — a draft, a strategy call, a review — opening a dashboard costs me the thread. I don't always recover it. So I'd often defer the question, which meant the question never got answered, which meant the decision got made without the data.

Now the question gets answered right where the question occurred. No tab, no thread loss, no deferral.

The data habit forms because the friction is gone.

## What to Watch For

A few things worth knowing before you assume it works perfectly:

Event naming matters more than you'd expect. If your PostHog events are inconsistently named — some with spaces, some with underscores, some abbreviated — Claude will sometimes query the wrong event. Spend time on clean event definitions and it pays dividends here.

Complex cohort queries sometimes require iteration. Simple trends and funnels work immediately. If you want a segmented retention analysis with multiple filters, you might need two or three rounds of clarification before the query matches what you meant. This is fine — it's still faster than doing it manually — but set expectations accordingly.

It reads your existing insights too. You can ask Claude to retrieve a saved PostHog insight by name, interpret it, and tell you what it means in context. This is useful when you have insights a previous analyst set up and you've never been sure what they actually track.

## How to Start

Connect the PostHog MCP server. Ask one question about something you already know the answer to — a metric you check manually — and compare the response to what you'd get from the dashboard.

If the answer matches, you now have a new habit: analytics by conversation. Questions get answered in context, without the context switch. The data stops being something you schedule time to look at and starts being something you consult as you work.

That's the shift. It sounds small. The compounding effect on decision quality isn't.

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/memory-across-sessions" style="text-decoration: none; color: #0366d6;">← Previous: How to Give Claude Code Memory Across Sessions</a>
  </div>
  <div>
    <a href="/" style="text-decoration: none; color: #0366d6;">Home</a>
  </div>
</nav>
