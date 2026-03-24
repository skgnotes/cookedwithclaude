---
layout: post
title: "How I use Claude Code to prep for important meetings"
permalink: /meeting-prep-brief
---

# How I use Claude Code to prep for important meetings

Thirty seconds before a call with an investor I'd met twice, I got a Telegram message. It had their background, what we'd discussed last time, two things they'd mentioned caring about, and three questions I should probably ask.

I hadn't written any of that. Claude had.

This is how I wired that up.

## The problem with meeting prep

Meeting prep is one of those tasks that feels important but almost never happens well. You have good intentions. You open LinkedIn, maybe scroll through old emails, try to remember what you talked about last time. Then someone pings you and the call starts and you're improvising.

The cost isn't the bad call. The cost is the cumulative effect — relationships that feel thinner than they should, deals that don't close because you didn't ask the right questions, partnerships that drift because you never followed up on the thing that mattered.

Good meeting prep takes 15–20 minutes when done properly. Most people either skip it or do a weak version of it. I was one of those people.

Now I'm not. And I didn't change my habits — I changed my system.

## What the brief contains

Before I describe the setup, here's what a generated brief looks like. For a one-on-one with an operator I've worked with before, it includes:

- Who they are (role, company, how we know each other)
- What we discussed last time
- What they said they were working on or worried about
- Any open threads from our last conversation
- Two or three suggested questions based on the context

For a new contact, it pulls their background from my notes if I have any, or flags that I should look them up before the call.

The whole thing is 10–15 lines. Dense, useful, specific.

## The setup

Three things power this:

**1. `people.md` — my contact file**

I keep a running file of people I interact with. For anyone I meet more than once, I write a short note: who they are, what their context is, what we've talked about. It's not comprehensive — it's just enough to orient me. A few lines per person, updated after meaningful conversations.

**2. Calendar access**

Claude Code can read my calendar via a script that pulls today's and tomorrow's meetings — title, attendees, time. Nothing complex. Just enough to know who I'm meeting.

**3. A Claude Code skill**

I have a skill called `meeting-brief` that I can trigger from the command line or via a Telegram bot. When run, it:

- Reads my calendar for upcoming meetings
- For each meeting, looks up the attendee(s) in `people.md`
- Cross-references any related notes in my notes folder
- Generates a brief for each meeting and sends it to my Telegram

The skill prompt is explicit: pull from these files, structure the brief like this, keep it under 200 words per person, flag if you have no context on someone.

## How to trigger it

I have two trigger paths.

**Automatic:** A cron job runs the skill each morning at 7 AM. By the time I open my phone, the briefs for the day are already in Telegram.

**Manual:** If I add a meeting last-minute or want a brief for tomorrow's calls, I type `/meeting-brief` in my Claude Code session and it runs immediately.

Both use the same underlying skill file. The cron job calls it via a background session script; the manual trigger runs it directly.

## The honest version of how this went

The first version was not clean. My `people.md` file was inconsistent — some entries were detailed, some were names with a company and nothing else. The briefs reflected that. For people I'd written real notes on, they were genuinely useful. For the thin entries, they were just formatted versions of almost no information.

That was actually useful feedback. It made me take `people.md` more seriously. Now I update it after almost every meaningful conversation, because I know it's the source the brief will pull from. The system created the habit.

The other surprise: the suggested questions are often the most valuable part. Claude isn't guessing — it's pattern-matching from what the person has said they care about. Most of the time, the questions it surfaces are better than the ones I'd have thought of on my own.

## How to start

You don't need a full `people.md` to begin. Start with five people you meet with regularly. Write two or three lines on each: what they do, what you've worked on together, anything that would help you show up better prepared.

Then write a simple Claude Code skill that reads that file and the output of a `cal` or calendar API call, and asks Claude to generate a brief for each person you're meeting today.

Run it manually a few times. See what the output looks like. Fill in the gaps in your notes file as they become obvious.

Within a few weeks, you'll have a contact file that actually captures your relationship context — and a system that makes it useful before every meeting that matters.

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/playwright-google-business-profile" style="text-decoration: none; color: #0366d6;">Next: How we fixed a Google Business Profile with Playwright — without touching the API →</a>
  </div>
  <div>
    <a href="/per-client-ai-contexts" style="text-decoration: none; color: #0366d6;">← Previous: Running separate AI contexts for each client</a>
  </div>
  <div>
    <a href="/" style="text-decoration: none; color: #0366d6;">Home</a>
  </div>
</nav>
