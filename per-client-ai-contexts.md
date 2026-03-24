---
layout: post
title: "Running separate AI contexts for each client"
permalink: /per-client-ai-contexts
---

# Running separate AI contexts for each client

When you're managing multiple client engagements, your Claude setup starts to resemble your mental state: everything in one place, slightly unsorted, occasionally surfacing the wrong thing at the wrong moment.

The problem isn't Claude. The problem is that most operators set up one Claude environment and use it for everything. One config file. One set of connected tools. One working directory with folders for each client. It works until it doesn't — until Claude references a Notion page from the wrong engagement, or surfaces context from a project you're no longer actively working, or you realize you've been operating with three clients' worth of background noise in every session.

Clean client separation is architecture, not habit. Here's how to build it.

## What clean separation actually looks like

When it's working, switching clients means switching directories. That's it.

You open the folder for a client, Claude's context is scoped entirely to that engagement — their Notion workspace is the only one connected, their CLAUDE.md is the one being read, their project files are the only ones visible. When you close it and open a different client folder, everything resets.

No cross-contamination. No phantom context. No chance of Claude generating output that accidentally references information from another engagement.

## Why this matters

Context bleed is mostly invisible until it causes a problem. The risk isn't Claude hallucinating client A's details into client B's work — it's subtler than that. It's Claude drawing on the wrong Notion database when you ask about "the pipeline." It's instructions from one client's CLAUDE.md shaping how Claude responds in a different context. It's you spending mental energy managing what Claude does or doesn't know about each engagement.

For consultants, there's also a professional dimension. Your clients are paying for focused attention. An AI setup that treats all your engagements as one pool of context is not that.

## The architecture

The foundation is the working directory. Claude Code reads its instructions from a `CLAUDE.md` file in the current directory. That one fact is the whole mechanism.

Structure your consulting work like this:

```
~/Documents/Consulting/
  ClientA/
    CLAUDE.md
    project-facts.md
    ... working files
  ClientB/
    CLAUDE.md
    project-facts.md
    ... working files
```

Each `CLAUDE.md` contains only what's relevant to that client. Their tools, their contacts, their context. Nothing from anyone else.

**Per-client MCP configuration** is where this gets powerful. If you're using Notion MCP to connect Claude to your clients' workspaces, don't connect all workspaces at once. Each client's `CLAUDE.md` should reference their specific Notion integration token and only their databases. When you're in ClientA's directory, Claude can access ClientA's Notion. When you're in ClientB's directory, ClientB's Notion. Never both simultaneously.

Configure it in the project-level CLAUDE.md like this:

```yaml
# In ~/Documents/Consulting/ClientA/CLAUDE.md

## MCP Connections
- Notion: ClientA workspace (token: see project-facts.md)
- Scope: project-tracker, meeting-notes, decisions-log

## Off limits
Do not reference or access any other client's data or tools.
```

For the MCP server config itself, you can use Claude's settings.json to define named MCP servers and reference them conditionally — or manage separate MCP configs per client folder using Claude Code's project-level settings.

**Separate API tokens** are worth doing properly. If a client provides API access to their own tools — their CRM, their analytics, their Slack — store those credentials in that client's `project-facts.md`, not in a shared config. This also makes offboarding clean: when an engagement ends, you archive the folder and the credentials go with it.

**Context files scope tightly.** Each client's `CLAUDE.md` should explicitly name the files Claude can reference for that engagement:

- `project-facts.md` — credentials, key contacts, project background
- `context.md` — what's currently in motion, what's on hold, what matters this week
- `decisions-log.md` — things that have been agreed and shouldn't be re-litigated

None of these get shared between clients. They live in the folder. They stay there.

## What surprised me about this

The discipline required to build this forces you to be clearer about each engagement than you might otherwise be.

When you have to write a `CLAUDE.md` for a client, you have to answer questions you might have been leaving fuzzy: what are the boundaries of this engagement? What does Claude need to know? What should it never do here? The exercise of scoping Claude's context is also the exercise of clarifying your own mandate.

The second thing: once separation is in place, context-switching between clients becomes faster, not slower. You close one folder, open another, and Claude is already oriented. No recap. No "let me remind you what we're working on." The folder is the brief.

## How to start

Pick your most active client engagement. Create a clean folder for it. Write a `CLAUDE.md` that covers only that client's context. Connect only their Notion workspace (or whatever tools you're using for that engagement). Run a session from that folder and see what's different.

Then do the same for a second client.

The goal isn't to build the perfect multi-client architecture all at once. The goal is to get one clean separation working, observe how it changes the quality of your sessions, and replicate it.

Once you've done two, the third takes fifteen minutes.

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/meeting-prep-brief" style="text-decoration: none; color: #0366d6;">Next: How I use Claude Code to prep for important meetings →</a>
  </div>
  <div>
    <a href="/institutional-memory" style="text-decoration: none; color: #0366d6;">← Previous: Institutional Memory Is a Skill</a>
  </div>
  <div>
    <a href="/" style="text-decoration: none; color: #0366d6;">Home</a>
  </div>
</nav>
