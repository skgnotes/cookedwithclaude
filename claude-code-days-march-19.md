---
layout: post
title: "My Day with Claude Code — March 19, 2026"
permalink: /claude-code-days-march-19
---

# My Day with Claude Code — March 19, 2026

There's a particular kind of day in work where you're not building anything new — you're making everything you've already built actually work. March 19 was that day, and by the time it was done, the system felt like it had aged two years in the right direction.

<div style="background: #f0f0f7; border-radius: 6px; padding: 16px 20px; margin-bottom: 24px;" markdown="1">

**Quick read**

A day spent making everything that was already built actually work — better, more reliably, with less chance of breaking quietly. Not glamorous. Completely necessary. Here's what happened:

- Permanently separated the automation browser from the personal browser — no more silent session drift
- Learned the only reliable way to check if a session is alive: navigate to the page and see. Everything else lies.
- Consolidated five scattered health check scripts into one, running automatically every morning at 7:45am
- Set up fully automatic recovery for expired Google logins — no intervention, no login screen
- Fixed a calendar bug that had been pulling yesterday's evening into today's schedule
- Documented every automation and script in the system for the first time (18 scripts, 13 scheduled jobs)
- Cleaned up the website: fixed a formatting issue collapsing all article links, converted 14 old-style nav footers
- Published five new articles — 25 to 30 total — including the front-door piece for first-time readers
- Shared the blog in the family WhatsApp group

Some days you build things. This day you made sure things stayed built.

</div>

<p style="margin-bottom: 32px;"></p>

### Hardening the setup

It started with something that had been nagging at me: the way my two browsers were coexisting too casually. The browser I use for automations — running tasks in the background, managing sessions, doing real work — and my personal browser had started to blur. Automations were occasionally picking up temporary profiles that lose their sessions without warning. So I spent the first part of the morning drawing a clean line. Chrome is now exclusively for automations. Edge is my personal browser. Sessions migrated, paths locked in, the separation made permanent.

The more interesting lesson came from tracing why a WhatsApp session had silently broken. The session looked fine on the surface — the stored credential existed, the local record said everything was in order. But the session was dead, and nothing was telling me that. The fix sounds obvious in retrospect: don't inspect the stored record, just open the page and see if it loads logged in. That's the only check that actually tells you what's true. Looking at the stored credential is a lie detector that believes everything.

### One health check to rule them all

That insight went straight into the morning health check. The WhatsApp check was rewritten to actually navigate to the page. A check for the Shopify Partners account was added alongside it. The health check had been five separate scripts scattered in different places. By afternoon it was one consolidated routine — checking email authentication, the command-line tools I rely on, the Telegram bot, GitHub access, WhatsApp, Shopify, and the database, all in sequence. It now runs automatically every morning at 7:45am, fifteen minutes before the morning digest, so everything is confirmed working before the day's summary arrives.

The most satisfying part: if a Google login expires overnight, the system now fixes it by itself. It detects the authentication prompt, opens the browser, clicks through the consent screen, and closes the loop — without me ever seeing a login page.

### The digest and the bug

Around midday I ran the monthly Shopify payout check. While I was thinking about the morning digest, I also pulled the recurring revenue figures into it automatically — the numbers that matter now arrive with the morning summary without me doing anything to retrieve them. Small change. Significant upgrade.

There was also a calendar bug I'd been meaning to trace. The daily schedule had been showing the previous evening's events at the top of today's list. A timezone miscalculation was pulling in a window that started 5.5 hours earlier than it should. Fixed. These are the bugs that make you feel both stupid and clever at the same time.

### Everything documented

Late afternoon shifted to documentation. The automation stack had 18 scripts and 13 scheduled jobs running across the system. None of it was written down anywhere — it existed in practice, not on paper. Knowledge files now exist for all of them. Two automations that were doing redundant overlapping work were merged into one. The system didn't get bigger. It got cleaner.

### The site

Meanwhile, the website got a full audit. A formatting issue had caused all the article links on the homepage to collapse into one long run-on line. Fixed. Fourteen article footers were still using the old navigation style — different link ordering, no explicit styling on the links. All converted to the current standard. One article was missing its Next link entirely. And then I published a site style guide so none of this happens again.

### Thirty articles

Five new articles went up that day, bringing the site from 25 to 30. The most important was a front-door piece for readers who've never written a line of code and aren't sure what they're even looking at. That one had been the highest-priority gap for weeks. Getting it done felt like finally placing the welcome mat.

In the evening I built something completely different: an automated way to clear old SMS conversations from my phone in bulk. Useful house-cleaning when a device accumulates months of noise.

The day ended with sharing the blog in the family WhatsApp group. It took a couple of rounds of editing to get the tone right. No hype, no positioning language. Just: 30 articles up, writing and publishing both done with Claude Code, take a look if you're curious. Low-key. Direct. That's the register that felt right.

### The day that was.

A browser setup made permanent. A morning health check that now heals itself. A calendar bug fixed. An automation stack documented for the first time. Fourteen pages cleaned up. A front-door piece for first-time readers. Thirty articles on the site. The blog shared with family.

What strikes me about a day like this is how invisible the value is. Nobody sees a health check that runs cleanly every morning. Nobody notices a browser profile that never loses its session. Nobody reads the documentation for an automation stack. And yet all of it is the difference between a system that holds and one that quietly falls apart at inconvenient moments. The unglamorous work is the load-bearing work. What surprised me was how much of it got done in a single day — and how much lighter the whole thing felt afterward.

You can build this. Not all at once. Not in a day. But piece by piece, the way I've been doing it — one automation, one workflow, one small win at a time. And if you want help getting started, that's exactly what this site is for.

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/claude-code-days-march-20" style="text-decoration: none; color: #0366d6;">Next: My Day with Claude Code — March 20 →</a>
  </div>
  <div>
    <a href="/claude-code-days-march-18" style="text-decoration: none; color: #0366d6;">← Previous: My Day with Claude Code — March 18</a>
  </div>
  <div>
    <a href="/claude-code-days" style="text-decoration: none; color: #0366d6;">Go to My Day with Claude Code (series) Home</a>
  </div>
</nav>
