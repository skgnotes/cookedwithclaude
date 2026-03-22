---
layout: post
title: "My Day with Claude Code — March 11, 2026"
permalink: /claude-code-days-march-11
---

# My Day with Claude Code — March 11, 2026

At some point in the afternoon, a domain name resolved. The SSL certificate turned green. The site was live.

<div style="background: #f0f0f7; border-radius: 6px; padding: 16px 20px; margin-bottom: 24px;" markdown="1">

**Quick read**

The day this site came into existence — and several other things happened alongside it. Here's what happened:

- Purchased cookedwithclaude.com — DNS configured, GitHub Pages set up, SSL provisioned
- Hit an SSL cert that got stuck after the domain switch — found the fix (reset via API), verified live
- Closed the full year's consulting accounts — P&L completed, shared with my EA
- Benchmarked AI usage against a national framework — produced a styled PDF report, shared with a contact
- Ran an AI agent orchestration system for the first time — 4 agents, 6 tasks
- Added a Telegram command that captures ideas directly to the content backlog

A day where a project became a thing that exists in the world.

</div>

<p style="margin-bottom: 32px;"></p>

### The site goes live

The domain: cookedwithclaude.com. Purchased on March 11. The thinking behind the name, the branding, the subtitle — all of that had been worked out over the previous day. What remained was the technical part: buy the domain, point it at GitHub Pages, wait for DNS to propagate, watch the SSL certificate provision.

It mostly went smoothly. DNS resolved. GitHub Pages built. But the SSL certificate got stuck — a known issue that sometimes happens when a custom domain is added to an existing Pages site. The cert was provisioned for the old domain but hadn't updated for the new one.

The fix: clear the custom domain via API, wait, re-add it. The cert re-provisioned. Verified via Playwright — HTTPS, green padlock, correct page content.

That moment — checking the URL in a browser and seeing the site load correctly on its permanent domain — is different from all the sessions leading up to it. Everything before is draft. That moment is when it becomes real.

### The year's accounts

In the same afternoon: the year's consulting accounts needed to be closed.

The full-year numbers: income tallied, expenses categorised, tax withheld broken out, net position calculated. The output — a P&L summary and the supporting details — was compiled into a document and shared with my EA. Payables identified. TDS position noted for the accountant.

This is the kind of financial admin that accumulates until someone forces the close. Having it done in a session, with accurate figures, in a shareable format, is the difference between carrying the uncertainty forward and actually knowing where you stand.

### The benchmark

Also in the afternoon: a benchmark. Anthropic had published an India Economic Index — a framework for measuring how individuals use AI across several dimensions: how much of their work it handles, how autonomous their usage is, how it changes the quality of their output.

I ran the benchmark against my own usage data. Scored across five dimensions. The output was formatted into a styled PDF report. Shared with a contact who works in the AI space.

The exercise is useful even without the sharing. Putting a number on how you're using something forces an honest assessment of what "active use" actually means.

### The agents

Late in the day: the first run of an AI agent orchestration system.

The system is called Paperclip — open source, runs locally. The idea: instead of one AI assistant handling everything sequentially, a team of agents each with a specific role, handing off to each other. For the blog: a strategist decides what to write, a writer drafts it, a publisher puts it live.

The first run: four agents, six tasks. It worked. Not perfectly — there were misfires and adjustments. But the basic loop ran. Tasks were created, assigned, picked up, completed.

That's the beginning of the publishing pipeline that, by March 21, would be running articles while I was at lunch.

### The day that was.

A domain live. A certificate fixed. Accounts closed. A benchmark run and shared. Agents running for the first time. An idea capture command added.

What strikes me is the SSL cert turning green. It's a technical event — a certificate provisioned, a protocol handshake succeeding — but it marks something. Before that moment, the site existed in potential. After it, the site existed in the world. The work that preceded it was building. That moment was arriving.

You can build this. Not all at once. Not in a day. But piece by piece, the way I've been doing it — one automation, one workflow, one small win at a time. And if you want help getting started, that's exactly what this site is for.

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/claude-code-days-march-12" style="text-decoration: none; color: #0366d6;">Next day →</a>
  </div>
  <div>
    <a href="/claude-code-days-march-10" style="text-decoration: none; color: #0366d6;">← Previous day</a>
  </div>
  <div>
    <a href="/claude-code-days" style="text-decoration: none; color: #0366d6;">Series Home (Claude Code Days)</a>
  </div>
</nav>
