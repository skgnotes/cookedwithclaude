---
layout: post
title: "My Day with Claude Code — March 19, 2026"
permalink: /claude-code-days-march-19
---

# My Day with Claude Code — March 19, 2026

There's a particular kind of day in software work where you're not building anything new — you're making everything you've already built actually work. March 19 was that day, and by the time it was done, the system felt like it had aged two years in the right direction.

It started with something that had been nagging at me: the browser situation. Chrome and Edge had been coexisting a little too casually in my automation setup. Playwright was occasionally pointing to a hash-based temp Chrome profile — the kind that quietly changes location and loses all your sessions. I spent the first part of the morning hardening the separation for good. Chrome is now exclusively Claude Code's automation browser. Edge is my personal browser. The two don't touch. Playwright was pinned to a fixed, stable Chrome profile path. WhatsApp Web sessions and Shopify Partners sessions migrated over cleanly.

The more interesting learning came when I was tracing why a WhatsApp session had silently broken. The cookie existed. Chrome's SQLite database said it was there. But the session was dead on the server side, and nothing local was telling me that. The fix sounds obvious in retrospect: don't inspect the cookie, just navigate to the URL and see if it loads authenticated. That's the only check that actually tells you what's true. Cookie inspection is a lie detector that believes everything.

That insight fed directly into the health check overhaul. The WhatsApp check was rewritten to use Playwright navigation. A Shopify Partners check was added alongside it. All the old references to the personal browser were removed. Then I kept going. The health check had been five separate scripts running in different places. By afternoon it was one consolidated skill — checking Google tokens, the gws CLI, the Telegram bot, GitHub SSH, WhatsApp Web, Shopify Partners, and Supabase, all in sequence. A LaunchAgent now runs it at 7:45am every morning, fifteen minutes before the 8am digest, so tokens are always fresh when the digest fires. The most satisfying part: the gws OAuth re-authentication is fully unattended now. If Claude detects the auth URL, it opens Chrome, clicks through the Google consent flow, and fixes it without me ever seeing a login screen.

Around midday I ran the monthly Shopify payout skill — checked the monthly payout numbers and pushed results to the relevant WhatsApp groups. While I was thinking about the morning digest, I also pulled the recurring SaaS revenue figures into it automatically from the database. The morning brief now includes those numbers without me doing anything. Small change, significant upgrade.

There was also a bug I'd been meaning to track down in the calendar display. The daily digest was showing the previous evening's events at the top of today's schedule. This one took some digging. The culprit: on a Mac set to IST, calling `new Date(year, month, day)` already returns midnight IST interpreted as UTC. Then the script was subtracting the IST offset again — sliding the window 5.5 hours earlier, pulling in yesterday's evening. Fixed by constructing the time with `Date.UTC()` and then subtracting — not the local date constructor. These are the bugs that make you feel both stupid and clever at the same time.

Late afternoon shifted to documentation. The scripts folder had 18 scripts and the automation stack had 13 LaunchAgents, cron jobs, and hooks running across the system. None of it was documented. Knowledge files now exist for all of them. Two LaunchAgents that were doing redundant overlapping work were merged into one. The system didn't get bigger — it got cleaner.

Meanwhile, cookedwithclaude.com got a full audit. Trailing double-spaces in the index had been stripped somewhere along the way — Jekyll needs them for line breaks, so all the article links had collapsed into one long run-on line. Fixed with a quick Python pass. Then I found 14 article footers still using the old navigation style — the legacy one, with different link ordering and no explicit link styling. Converted all of them to the current standard. One article was missing its Next link entirely. And then I published a site style guide so none of this happens again.

Five new articles went up that day, bringing the site from 25 to 30. The most important was a Level 0 front-door piece for readers who've never written a line of code and aren't sure what they're even looking at. That one had been the highest-priority gap for weeks. Getting it done felt like finally placing the welcome mat.

In the evening I built something completely different: a Python script to bulk-clear SMS conversations on an Android phone using ADB and UIAutomator. The non-obvious parts: content deletion silently fails on non-rooted Android 10+ because only the default SMS app has write permission. Long-press needs 2500ms, not 1000ms — shorter and it doesn't register. And you have to long-press the conversation body, not the avatar circle, or you open a contact card instead.

The day ended with sharing the blog in the family WhatsApp group. It took two rounds of edits to get the tone right. No hype, no positioning language, no "built for busy business owners" framing. Just: 30 articles up, writing and publishing both done with Claude Code, take a look if you're curious. Low-key. Direct. That's the register that felt right.

Thirty articles. A hardened system. A documented automation stack. One fixed calendar bug. And a family group chat that now knows the blog exists.

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/claude-code-days-march-20" style="text-decoration: none; color: #0366d6;">Next: My Day with Claude Code — March 20 →</a>
  </div>
  <div>
    <a href="/claude-code-days-march-18" style="text-decoration: none; color: #0366d6;">← Previous: My Day with Claude Code — March 18</a>
  </div>
  <div>
    <a href="/claude-code-days" style="text-decoration: none; color: #0366d6;">← My Day with Claude Code (series)</a>
  </div>
  <div>
    <a href="/" style="text-decoration: none; color: #0366d6;">Home</a>
  </div>
</nav>
