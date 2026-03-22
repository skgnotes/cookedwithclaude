---
layout: post
title: "My Day with Claude Code — March 22, 2026"
permalink: /claude-code-days-march-22
---

# My Day with Claude Code — March 22, 2026

There's something a little strange about spending a day writing articles called "My Day with Claude Code" while Claude Code is, in the background, ordering your lunch.

<div style="background: #f0f0f7; border-radius: 6px; padding: 16px 20px; margin-bottom: 24px;" markdown="1">

**Quick read**

March 22 was a day of infrastructure, meta-work, and one very good biryani. The morning started with AI agents checking their own email. The afternoon ended with a fully automated lunch order. In between, I spent most of the day writing the articles you may have read before this one. Here's what happened:

- Confirmed that a connection automation from the previous night had worked — checked one profile, found "1st degree"
- Gave agents their own dedicated email addresses — three inboxes, one per project
- Set up a job alert on a hiring platform end-to-end: agent created the account, read its own verification code, confirmed signup — no manual steps
- Spent most of the morning writing the Claude Code Days articles in plain English — translating technical logs into business stories
- Found an invisible bug silently breaking 1,600 lines of notes
- Ordered lunch: beef biryani, ₹225, fully automated — restaurant, item, card, OTP read off the phone, zero keystrokes after the first command

A day where the thing being documented and the thing doing the documenting were running at the same time.

</div>

<p style="margin-bottom: 32px;"></p>

### First things first

The morning started with a check. The previous day had ended with a browser automation that completed a LinkedIn connection through a method I wasn't entirely sure would hold. I opened the profile. 1st degree. It had worked.

This is one of the quiet satisfactions of building automations — you set something in motion, close the laptop, and come back the next morning to find out if it ran. This one did.

### Giving agents their own addresses

One of the things that makes practical automation possible — placing orders, completing verifications, receiving confirmations — is that the agents working on your behalf need somewhere to receive information. The same way a new employee needs an email address before they can actually do the job.

We formalised that properly on March 22. Each major project now has its own agent inbox: one for general tasks, one for a client project, one for this site. When an agent signs up for a service, receives a verification email, gets a receipt — it lands in the right inbox, neatly separated from everything else. Three addresses. Zero overlap with mine.

To test it properly: we set up a job alert on a hiring platform I'd been meaning to check. The agent navigated to the site, created an account using its own email address, waited for the verification code to arrive in that inbox, read it, entered it, and confirmed the signup. I got a Telegram notification when it was done. I didn't touch any of it.

### Writing about the writing

Most of the morning was spent on something that felt a bit unusual: writing these articles.

The Claude Code Days series — the one you're reading right now — started with session logs. Technical notes: what ran, what broke, what was learned. Useful to me, but not really readable by anyone who isn't already deep in the work. The goal was to translate those logs into something a founder or professional could actually read. Not a tutorial. Not a sales pitch. A story.

That turns out to be its own craft. The same day that produced a line like "confirmed CDP relay via authenticated browser session" becomes "set up a connection through the platform's own interface, without triggering the usual blocks." Same outcome. Very different sentence.

Getting that translation right — across four articles, with consistent structure, TL;DR cards, section headers, the right closing note — took most of the morning. By the end of it, the articles were rewritten, the structure was settled, and a guide document existed so the same approach could be applied to any future article without starting from scratch.

That document is being used right now, for this one.

### The invisible bug

Later in the morning, a small investigation. The session log — 1,600+ lines of notes spanning months — had a rendering problem. Something was breaking the display in my notes app from a certain point downward. But everything looked fine in other tools. Classic invisible bug: wrong in one place, looks correct everywhere else.

The culprit: a stray tag that the notes app tried to interpret as formatting code. It couldn't, and quietly stopped displaying everything below it. One tag. 1,600 lines affected.

Fixing it was quick once found. Finding it — cross-checking between tools, narrowing down the line, understanding why only one app was affected — that's the diagnostic work that used to take an hour and now takes five minutes.

### Lunch

At some point in the afternoon, I wanted beef biryani.

One command.

Claude navigated to Swiggy, found the restaurant, selected the item, confirmed the address, and moved to payment. The card was already on file. When the verification code arrived as an SMS on my phone, Claude read it directly — not by asking me, but by querying the phone's SMS inbox automatically — entered it into the payment form, and the order was placed. ₹225. Delivered to the door. I was at my desk the whole time.

That's not a prototype. That's just how lunch works now.

### The day that was.

A connection confirmed. Agent inboxes created. A job alert set up end-to-end without touching it. Four articles translated from technical logs to readable stories. An invisible bug found and fixed. Lunch ordered hands-free.

What strikes me about this day is the meta quality of it — spending most of it writing about past days of using Claude Code, while Claude Code was doing things in the background: placing orders, setting up accounts, confirming what had run overnight. The documentation and the work were happening at the same time. The story about the tool, and the tool itself, running side by side.

I've been writing these articles so that someone else can read them and think: I could do that. What I didn't expect is that writing them would feel like doing the work twice — once when it happens, and once when you put it into words.

You can build this. Not all at once. Not in a day. But piece by piece, the way I've been doing it — one automation, one workflow, one small win at a time. And if you want help getting started, that's exactly what this site is for.

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/claude-code-days-march-21" style="text-decoration: none; color: #0366d6;">← Previous day</a>
  </div>
  <div>
    <a href="/claude-code-days" style="text-decoration: none; color: #0366d6;">Series Home (Claude Code Days)</a>
  </div>
</nav>
