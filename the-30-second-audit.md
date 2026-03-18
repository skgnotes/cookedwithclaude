---
layout: post
title: "The 30-second audit"
permalink: /the-30-second-audit
---

# The 30-second audit

After setting up a Shopify store for a friend, I needed to verify the billing plan — the exact tier, the current rate, the trial end date.

The old way: open a browser, log in, navigate to Settings → Plan, read the screen. Five minutes if everything loads cleanly.

What I did instead: one instruction to Claude Code. Playwright navigated to the admin page and snapshotted it. Plan name, rate, trial end date, annual savings option — all in the response. Thirty seconds.

## Playwright as an inspection tool

Most of the conversation about Playwright frames it as automation. You use it to fill forms, click buttons, submit things. It does the repetitive work so you don't have to.

Inspection is a different use. Not "do this" — "tell me what's here."

The question that comes up constantly in running anything is not "do this task." It's "what's the current state of this thing." Payment method configured or just set up. Page rendering or returning a 404. Record saved or silently failed. Setting applied or still pending.

These are checks, not tasks. Playwright handles them as easily as it handles tasks.

## What changes when verification is instant

When checking something costs five minutes — logging in, navigating, locating the right screen — you often don't do it. You assume. You trust the process and move on.

When it costs thirty seconds, you don't skip it. The cost of checking drops below the cost of assuming.

The habit this builds: before closing out any action, verify the outcome directly. Not by reading the terminal. By looking at the actual thing.

Most operators have had the experience of learning about a problem three days after it happened, when someone else pointed it out. The issue was always findable in thirty seconds. What was missing was the habit of looking.

The only thing that's changed is that looking is no longer the friction it used to be.

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/what-done-means" style="text-decoration: none; color: #0366d6;">Next: What done actually means →</a>
  </div>
  <div>
    <a href="/curiosity-and-a-mentor" style="text-decoration: none; color: #0366d6;">← Previous: Curiosity and a mentor</a>
  </div>
  <div>
    <a href="/" style="text-decoration: none; color: #0366d6;">Home</a>
  </div>
</nav>
