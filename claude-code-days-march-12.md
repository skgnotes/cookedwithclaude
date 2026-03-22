---
layout: post
title: "My Day with Claude Code — March 12, 2026"
permalink: /claude-code-days-march-12
---

# My Day with Claude Code — March 12, 2026

Some days you build in one direction. March 12, we built in four.

<div style="background: #f0f0f7; border-radius: 6px; padding: 16px 20px; margin-bottom: 24px;" markdown="1">

**Quick read**

A day spread across the blog, client work, a real estate proposal, and AI infrastructure — all in the same session. Here's what happened:

- Published the first two articles on this site — site formatting polished, content pipeline restructured
- Reconstructed a client's full-year financials from bank statement data — P&L built, shared with them
- Built a complete financial model for a real estate project — 6-tab Google Sheet, plus a GitHub Pages site with proposal and investor deck
- Discovered and fixed a permissions issue in the AI agent system
- Created a dedicated vault for consulting work — client projects separated from personal OS

A day that covered a lot of ground without losing the thread.

</div>

<p style="margin-bottom: 32px;"></p>

### The blog

March 12 was the day this site got its first real articles.

The site had been live for a day — domain, DNS, GitHub Pages, SSL all sorted on March 11. But the content needed polish: formatting inconsistencies across articles, footer links in the wrong order, a few draft articles that weren't ready. We worked through the list. Consistent headers, consistent footers, footer order fixed to Next → Previous → Home. Six articles moved to drafts, not yet ready for publish.

Then the content pipeline. The backlog of ideas had been a flat list. It got restructured into a level progression — Level 0 through 9, from "what is this" to "the bigger picture." 55 ideas organised, each tagged by source and type. The pipeline now has a shape.

And then: two articles published. The first two pieces on cookedwithclaude.com.

### Client finances

In the same day, completely different work: a client's full-year financials needed to be reconstructed.

The source material was a bank statement — transactions going back twelve months. Claude read the statement, identified consulting income, categorised expenses, and built the P&L. January and February went in first; the rest followed. Net position calculated. The output was shared with the client the same day.

There's something notable about how this works. Reconstructing a P&L from a bank statement used to be a full-day accounting exercise — each transaction checked, coded, totalled. Here it was a session. The output is the same. The time is not.

### The real estate model

Also in the same day: a real estate project proposal that needed a financial model.

Not a simple projection. A 6-tab Google Sheet — formula-linked, with revenue, costs, funding structure, and investor returns all connected. Then a GitHub Pages site: a proposal page, the financial model as HTML, a ten-slide investor deck. The whole thing deployed and live.

These are the kinds of deliverables that, in a traditional professional services context, take a team a week. Here they took a session.

### The AI agent issue

Late in the day: a permissions problem in the AI agent system. One of the agents was trying to assign tasks to other agents and failing. The root cause: the agent was using its own API key, which didn't have the right permission level for task assignment. Fix: use the right key for that operation.

Small fix. But finding it required understanding how the permission model works, which is exactly the kind of thing that gets documented so it doesn't need to be re-discovered.

### The day that was.

Two articles published. A client P&L reconstructed and shared. A real estate financial model built and deployed. An AI agent permissions bug fixed. A consulting vault created.

What strikes me about a day like this is the range — finance, publishing, proposals, infrastructure — all handled with the same tools, in the same session, without switching modes in the way that usually costs you momentum. The generalist quality of Claude Code is something I keep noticing. It doesn't have a domain. It just has capabilities.

You can build this. Not all at once. Not in a day. But piece by piece, the way I've been doing it — one automation, one workflow, one small win at a time. And if you want help getting started, that's exactly what this site is for.

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/claude-code-days-march-13" style="text-decoration: none; color: #0366d6;">Next day →</a>
  </div>
  <div>
    <a href="/claude-code-days-march-11" style="text-decoration: none; color: #0366d6;">← Previous day</a>
  </div>
  <div>
    <a href="/claude-code-days" style="text-decoration: none; color: #0366d6;">Series Home (Claude Code Days)</a>
  </div>
</nav>
