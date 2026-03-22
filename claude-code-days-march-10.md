---
layout: post
title: "My Day with Claude Code — March 10, 2026"
permalink: /claude-code-days-march-10
---

# My Day with Claude Code — March 10, 2026

The day the blog got its name. Also the day the tax liability went to zero. Not a coincidence — both were about getting clarity on something that had been vague for too long.

<div style="background: #f0f0f7; border-radius: 6px; padding: 16px 20px; margin-bottom: 24px;" markdown="1">

**Quick read**

A day of foundations — naming the blog, locking the tax strategy, fixing broken automations, auditing telecom plans, and publishing a first draft for a client. Here's what happened:

- Renamed the blog from "Claude Code Notes" to "Cooked with Claude" — domain decided, vault created, branding settled
- Confirmed the tax strategy for the year: a combination of two provisions wipes the liability and recovers withheld tax
- Fixed a Telegram bot that had been stuck on an unprocessed message since early morning
- Audited two mobile plans — one expiring in two days; recharged via Playwright
- Published a client's first blog post to their CMS as a draft
- Reorganised the task list — finance section added, structure cleaned

A day where setup was the work.

</div>

<p style="margin-bottom: 32px;"></p>

### The name

The blog had been called "Claude Code Notes" since it started. It was a working title — accurate but flat. Not a brand. Not something you'd share.

March 10 was when that changed. The new name: Cooked with Claude. The subtitle: *The business leader's playbook for getting things done in the AI age.* The domain: cookedwithclaude.com — not yet purchased, but checked and confirmed available.

The naming conversation is worth noting because it's an example of Claude Code's less obvious value: not as an executor, but as a thinking partner. Working through the "by vs with" distinction, the implications of different audience words in the subtitle, the feel of different domain options — that's not task execution. It's ideation, back and forth, until something lands right.

A dedicated Obsidian vault was created for the project. Content ideas, voice guide, branding document — the foundation was built in one session.

### Tax clarity

In the same session: the year's tax position.

The question was whether a specific combination of two tax provisions — one for professional income, one for small earners — would interact the way I hoped. My CA confirmed it. Together, they clear the full liability and result in the full withheld tax coming back as a refund.

That confirmation changes the financial picture for the year. Not dramatically, but meaningfully. Carrying uncertainty about a significant number is a background cost. Resolving it is relief.

### The stuck bot

In the morning, before any of the above: a Telegram bot had been unresponsive since 7:52 AM. An unprocessed message had gotten stuck in the queue and the bot had stopped handling new ones.

The fix: find the stuck process, stop it, restart it via the LaunchAgent (the right restart method — killing the process directly would have caused two instances to run and fight each other). Message queue cleared. Bot back online.

Small incident. But it illustrates something about running automations: they break in quiet ways. Nothing announces the failure. You notice it when you expect something to have happened and it hasn't.

### Telecom audit

Also in the session: a Jio plan audit. Two SIM cards, two plan expiry dates. The automation navigated to the carrier's site, logged in, checked both accounts. One plan: good for another two months. The other: expiring in two days.

Recharged immediately via Playwright. Problem resolved before it became a problem.

### Client work

Late in the session: a client's first blog post, published to their CMS as a draft. Not yet live — image pending, a few FAQs incomplete — but staged for review. The workflow for publishing to that CMS had been automated in a prior session; this was the first real use of it.

### The day that was.

A name. A tax position confirmed. A stuck bot fixed. A SIM recharged. A blog post drafted and staged.

What strikes me about March 10 is how much of it was setup — and how that setup *was* the work, not the preamble to it. The blog name mattered because it determined the domain, the brand, the voice. The tax clarity mattered because it freed attention. The bot fix mattered because the system wasn't working. None of it produced something visible or impressive. All of it made the next session start from a better place.

You can build this. Not all at once. Not in a day. But piece by piece, the way I've been doing it — one automation, one workflow, one small win at a time. And if you want help getting started, that's exactly what this site is for.

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/claude-code-days-march-11" style="text-decoration: none; color: #0366d6;">Next day →</a>
  </div>
  <div>
    <a href="/claude-code-days-march-09" style="text-decoration: none; color: #0366d6;">← Previous day</a>
  </div>
  <div>
    <a href="/claude-code-days" style="text-decoration: none; color: #0366d6;">Series Home (Claude Code Days)</a>
  </div>
</nav>
