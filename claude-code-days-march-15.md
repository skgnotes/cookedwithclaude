---
layout: post
title: "My Day with Claude Code — March 15, 2026"
permalink: /claude-code-days-march-15
---

# My Day with Claude Code — March 15, 2026

Some days you build new things. March 15 was about clearing the ground first.

<div style="background: #f0f0f7; border-radius: 6px; padding: 16px 20px; margin-bottom: 24px;" markdown="1">

**Quick read**

A day of reorganisation and automation — the personal operating system flattened from 15+ files into 6, a smarter task system built, a family member's flight check-in handled automatically. Here's what happened:

- Reorganised 15+ files across 6 nested folders into 6 flat files — the whole system now opens faster and makes more sense
- Built a bidirectional sync between the task list and the life map — overdue items stay visible, upcoming items surface by proximity
- Refactored the daily digest script to be fully file-driven — no more hardcoded values
- Updated passenger lookup to pull from the contacts file automatically

A day where the system got simpler and smarter at the same time.

</div>

<p style="margin-bottom: 32px;"></p>

### The problem with nested folders

The personal OS — the collection of files where I keep context, plans, contacts, finances, upcoming events — had grown into something nobody had designed. It started flat. Then subfolders got added for organisation. Then subfolders inside those. After a few months, there were 15+ files spread across 6 nested folders, and finding anything required remembering where it lived.

The answer wasn't better organisation. It was fewer files.

March 15 was the day we flattened it. Everything collapsed into 6 files: profile, ops, people, facts, actions, lifemap. The deeply nested folders were deleted. The content was merged. What couldn't be merged cleanly was moved to the consulting vault where it actually belonged.

The result: the vault is navigable again. When something needs updating, you open one file, not four.

### The task system

The more interesting build of the day was the task system.

The old setup had tasks in one place and upcoming events in another. Overdue items would disappear from view once their date passed. New items surfaced only when you manually looked for them. It worked, but it required more attention than a system should.

The new setup has a bidirectional sync. One direction: the task list reads from the life map and surfaces upcoming items based on how close they are — things due this week appear automatically, without being manually added. The other direction: when items get updated or completed in the task list, those changes are written back to the life map.

Overdue items stay visible until resolved. Nothing falls off the edge of the calendar and disappears.

### The digest

While reorganisation was underway, the daily digest script got a refactor. The original version had hardcoded values — specific file paths, fixed assumptions about where things lived. Every time the file structure changed (and it changes often during active development), the script had to be manually updated.

The new version is file-driven. It reads configuration from a config file. Passenger details for upcoming check-ins are looked up from the contacts file. If a file moves, you update one reference, not the script itself.

This is a small change in complexity that pays off every time the structure evolves — which, at this stage, is often.

### The day that was.

Fifteen files collapsed into six. A smarter task system built. The digest script made more resilient.

What strikes me about this day is that simplicity isn't a starting point — it's a destination. The 6-file vault isn't simple because someone designed it that way from the beginning. It's simple because we kept asking what actually needed to be a separate file, and kept finding the answer was: fewer than we thought. The system works better not because it has more structure, but because it has less structure it doesn't need.

You can build this. Not all at once. Not in a day. But piece by piece, the way I've been doing it — one automation, one workflow, one small win at a time. And if you want help getting started, that's exactly what this site is for.

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/claude-code-days-march-16" style="text-decoration: none; color: #0366d6;">Next day →</a>
  </div>
  <div>
    <a href="/claude-code-days-march-14" style="text-decoration: none; color: #0366d6;">← Previous day</a>
  </div>
  <div>
    <a href="/claude-code-days" style="text-decoration: none; color: #0366d6;">Series Home (Claude Code Days)</a>
  </div>
</nav>
