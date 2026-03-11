---
layout: post
title: From idea to live site in one session
permalink: /idea-to-live-site
---

# From idea to live site in one session

The site you're reading right now was built in one session.

Domain purchased. DNS configured. GitHub repo created. GitHub Pages enabled. SSL provisioned. First article published. All of it — in a single conversation with Claude Code, in an afternoon.

Most sites don't get built. They stay as ideas in Notion, or domain names that were purchased and then pointed nowhere for years. The thing that separates a live site from a parked idea is usually not skill. It's that no one sat down and just did it.

Here is how to sit down and just do it.


## What you need before you start

Three things:

1. A rough idea of what the site is for (one sentence is enough)
2. A domain name you want (or a willingness to pick one in the session)
3. A GitHub account (free)

That's it. No hosting account. No credit card for a CMS. No developer.

GitHub Pages hosts the site for free. Your domain registrar handles the domain. Claude Code handles everything else.


## The session

Start with a single prompt:

"I want to build a simple website. It's for [describe it in one sentence]. I want to use GitHub Pages with a custom domain. Help me set it up from scratch — I'll need: a domain purchased through [your registrar], DNS configured, a GitHub repo created, GitHub Pages enabled, and a simple first page live. Walk me through it or do it directly wherever you can."

Claude Code will ask what it needs. It may handle some steps directly — creating the repo, writing the config files, pushing the first commit. For things that require your credentials (domain registrar, GitHub login), it will tell you what to do and why.

The conversation is the spec document. By the time the site is live, you'll have made every decision that matters, in plain English, without touching a terminal yourself.


## What the setup looks like

For a simple content site, the stack is:

- **GitHub Pages** — free hosting, automatic SSL, deploys on every push
- **Jekyll** — static site generator, built into GitHub Pages, no setup required
- **Custom domain** — four DNS A records pointing to GitHub's servers, one CNAME for www

The DNS records are always the same:

```
A    @    185.199.108.153
A    @    185.199.109.153
A    @    185.199.110.153
A    @    185.199.111.153
CNAME    www    your-username.github.io
```

SSL provisions automatically within minutes of the domain connecting. You don't configure it. It just appears.


## What surprised me

The whole thing took less time than I expected, and the part I expected to be hard — the DNS — was the most mechanical. Four records, copy-pasted. Done.

The hard part, such as it was, was deciding what the site was actually for. That conversation happened inside the session too. Claude Code asked questions that sharpened the answer. By the time the first page was live, I knew what the site was trying to do in a way I hadn't before I started.

Building the site clarified the idea. I don't think I could have gotten that clarity just by thinking about it.


## How to start

Open Claude Code. Type one sentence about what you want to build. Then say: "Help me get it live today."

The infrastructure is trivial. The decision to start is the thing.

<nav style="margin-top: 48px; padding-top: 24px; border-top: 1px solid #eee; font-size: 14px;">
  <div>
    <a href="/first-automation">← Previous: The first automation I built with Claude Code</a>
  </div>
  <div style="margin-top: 16px;">
    <a href="/">↑ Home</a>
  </div>
</nav>
