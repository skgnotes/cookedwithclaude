---
layout: post
title: "Setting up Obsidian and why"
permalink: /setting-up-obsidian
---

# Setting up Obsidian and why

After setting up CLAUDE.md, most people run into the same wall. They've told Claude Code how to behave. They haven't told it what to know.

The standing instructions are there. But every time someone asks Claude to draft a message to a specific client, or check what's pending on a project, or reference the EA's contact details — it still has to ask. The instructions are persistent. The knowledge isn't.

That's the gap Obsidian closes.

## Why Obsidian and not something else

Obsidian is a note-taking app. What makes it relevant here is one design decision: it stores everything as plain markdown files in a regular folder on your computer.

Not a database. Not a proprietary format. Not a cloud sync service with its own API. A folder of `.md` files.

Claude Code reads markdown files. So when your knowledge lives in Obsidian, it also lives somewhere Claude Code can reach directly. No export, no integration, no copying and pasting. You reference the file path, Claude reads it.

Most knowledge tools create a barrier between what you know and what your AI can use. Obsidian removes that barrier entirely — not through any special integration, but because its format and Claude Code's capabilities happen to be the same thing.

## What to install

Go to obsidian.md and download Obsidian. It's a desktop app — Mac, Windows, and Linux are all supported.

On the first launch, Obsidian asks you to create a vault. A vault is just a folder. You can create a new one anywhere, or point it at a folder you already use.

For this setup, create a dedicated vault for your personal operating context. Something like `PersonalOS` in your Documents folder. The name doesn't matter. What matters is that the path is clean and consistent — because you'll be referencing it from Claude Code.

```
~/Documents/PersonalOS/
```

That becomes your vault. Everything inside it is accessible to Claude Code.

## The files that matter

You don't need an elaborate system on day one. Four files do most of the work.

**people.md** — everyone Claude Code might need to reference. Your EA's full name, WhatsApp number, email, preferred way to be reached. Key clients: who they are, what you're working on together, any context that changes how Claude should address them. Colleagues, business partners, anyone Claude might draft a message to or about.

**facts.md** — the operational facts of your life. Home address. Frequent flyer numbers. Standard email signature. Payment card last four digits. Any recurring detail that shows up in forms, bookings, or communications. Claude Code will stop asking and start knowing.

**actions.md** — what's currently on your plate. Not a complete task manager — just a running list of active items, sorted by priority. When you ask Claude to help you plan a day or check what's pending, it reads this file and answers from reality, not from vague context.

**projects/** — one file per active engagement. For a founder advising multiple companies, this means one file per company: current status, open questions, relevant contacts, recent decisions. A short file, updated regularly.

None of these need to be long. A 50-line `people.md` is more useful than a 500-line one that's never read. The goal is accuracy, not completeness.

## Wiring it to CLAUDE.md

Once the files exist, open your global CLAUDE.md (`~/.claude/CLAUDE.md`) and add a section that tells Claude Code where to find them.

The pattern from the CLAUDE.md article applies directly:

```markdown
## Where things live
| File | Load when |
|------|-----------|
| ~/Documents/PersonalOS/people.md | Any communication task — drafting messages, looking up contacts |
| ~/Documents/PersonalOS/facts.md | Payments, travel bookings, form-filling, addresses |
| ~/Documents/PersonalOS/actions.md | Planning sessions, triage, checking what's pending |
| ~/Documents/PersonalOS/projects/[client].md | Any session involving that client |
```

This is the connection. Claude Code now knows not just how to behave, but where to look for knowledge when a task requires it.

The effect is immediate. Ask Claude to draft a WhatsApp message to someone in `people.md` — it reads the file, uses the name correctly, and doesn't ask for the number. Ask it to help you prioritise your morning — it checks `actions.md` and works from your actual list. Ask it to reference a client's current status — it opens the right project file.

The sessions stop being generic. They start being specific to your world.

## The thing I didn't expect

When I built this setup, I thought I was making a better note-taking system.

What I actually built was external memory for an AI.

The frame shift matters. Notes are for you to read later. Context files are for Claude to read now. That changes what you put in them, how you structure them, and how often you update them. You're not journaling. You're maintaining an operating system.

The files that work well are the ones where Claude gets something useful from reading them — specific names, specific numbers, specific decisions. The files that sit unused are the ones that are either too vague to be actionable or too detailed to be worth the scan time.

Once you think of the vault as Claude's memory rather than your notes, it becomes obvious what belongs there and what doesn't.

## Where to start

Install Obsidian. Create a vault. Write a `people.md` with ten people Claude Code is likely to reference — names, emails, context.

Open your CLAUDE.md and add the path to that file with one line about when to load it.

Then start a Claude Code session and ask it to draft a message to one of those people.

Watch it stop asking for contact details and start writing.

That's the moment. The session is no longer starting cold — it's starting with context. Everything else is just adding more files.

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/inbox-anywhere" style="text-decoration: none; color: #0366d6;">← Previous: Inbox Anywhere</a>
  </div>
  <div>
    <a href="/" style="text-decoration: none; color: #0366d6;">Home</a>
  </div>
</nav>
