---
layout: post
title: "My Day with Claude Code — March 17, 2026"
permalink: /claude-code-days-march-17
---

# My Day with Claude Code — March 17, 2026

Two tracks ran in parallel all day: rebuilding the system that tells Claude how to work, and using that system to do the largest single automation job I've attempted.

<div style="background: #f0f0f7; border-radius: 6px; padding: 16px 20px; margin-bottom: 24px;" markdown="1">

**Quick read**

March 17 was a day of infrastructure and scale. While one part of the morning was spent rebuilding the instruction system from the ground up, another was migrating an entire 118-article archive for a non-profit client — scraped, converted, published, images added, a cache bug found and fixed, sections organised. Both tracks finished. Here's what happened:

- Rebuilt the core instruction file from scratch — cut from 236 lines to 90, split into two clear parts
- Created a communications log — every message sent on my behalf is now tracked
- Wrote knowledge files for all 16 skills in the system
- Migrated 118 articles from a non-profit client's blog to Substack — fully automated
- Added images to 108 posts, then hit a cache bug: data updated, pages not showing the changes
- Fixed the cache, re-published everything — 183 images rendering correctly across the archive
- Organised the archive into two sections with working navigation

A day where the system got rebuilt and did serious work at the same time.

</div>

<p style="margin-bottom: 32px;"></p>

### Rebuilding the brain

There's a file at the centre of how I work with Claude Code — the global instruction file. Think of it as the standing brief: who I am, what I'm trying to do, how Claude should behave, where things live. Over months of active use, it had grown to 236 lines and become difficult to maintain. Principles were buried under specifics. Things were in the wrong place.

March 17 started with rebuilding it from scratch.

The new version is 90 lines. Two sections: the first is philosophy — mental model, how to act, standing instructions. The second is execution reference — the commands and patterns that actually do things. The distinction matters. When a file mixes principle and procedure, both get worse. When they're separated, both get cleaner.

While we were at it: a new log was created to track every message sent on my behalf. Not a draft file — an append-only record of every WhatsApp and Telegram message that Claude sent for me. When you're running a hundred conversations a week and some of them are sent by an AI, you need to know exactly what was said.

Then: knowledge files. Every skill in the system — all 16 of them — now has a corresponding document explaining how it works, when to use it, what it expects. Before this, the skills existed but the reasoning behind them didn't. Now it does.

### The archive project

In the afternoon: a completely different kind of work. A non-profit client had years of published articles on their website — 118 of them — that they wanted archived on Substack. Not a few posts. An entire content history.

The approach: scrape every article from the source site, convert the HTML to the format Substack expects internally, publish each one via an authenticated browser session (the only reliable method at this scale), then go back and add images in a second pass.

The scraping and publishing ran cleanly. 118 articles, done. Then the second pass for images — 108 posts updated with their original images. The API confirmed each one. Done, right?

### The cache that lied

Loading the actual pages told a different story. No images.

The data had been written correctly. The platform's own API said so. But the pages were serving a cached version that didn't include the updates — the rendered output and the stored data had gotten out of sync.

This is a pattern that shows up in any system that stores data in one place and renders it somewhere else. The fix isn't to update the data again. It's to trigger a re-render — force the platform to regenerate the page from the updated source. A second publish pass, with nothing changed except the instruction to re-render.

After that pass: 183 images rendering correctly across 108 posts. Then the archive was organised into two sections — one for the client's main content, one for press releases — with navigation that actually worked.

Final state: 118 articles, correct images, two sections, clean nav. Zero failures.

### The day that was.

An instruction file rebuilt. A communications log created. Knowledge files for every skill. A 118-article archive migrated, imaged, fixed, and organised.

What strikes me about this day is that both tracks ran at the same time without getting in each other's way. Rebuilding how the system thinks didn't slow down what the system was doing. Doing a large piece of client work didn't push the maintenance to another day. In a normal working day, one of these would have crowded out the other. Here, they just ran in parallel.

That's not a feature of any particular tool. It's what happens when the overhead of switching between tasks goes to near zero.

You can build this. Not all at once. Not in a day. But piece by piece, the way I've been doing it — one automation, one workflow, one small win at a time. And if you want help getting started, that's exactly what this site is for.

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/claude-code-days-march-18" style="text-decoration: none; color: #0366d6;">Next day →</a>
  </div>
  <div>
    <a href="/claude-code-days-march-16" style="text-decoration: none; color: #0366d6;">← Previous day</a>
  </div>
  <div>
    <a href="/claude-code-days" style="text-decoration: none; color: #0366d6;">Series Home (Claude Code Days)</a>
  </div>
</nav>
