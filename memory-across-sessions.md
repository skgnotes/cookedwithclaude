---
layout: post
title: "How to Give Claude Code Memory Across Sessions"
permalink: /memory-across-sessions
---

# How to Give Claude Code Memory Across Sessions

Every new Claude Code session starts blank.

It doesn't know your name, your context, your preferences, your stack, your clients. It doesn't remember what you decided last week or what went wrong last month. You tell it once. You start a new session. You tell it again.

After the third or fourth time, you stop telling it things, because it's tedious. And that's when Claude Code becomes useful but not powerful — a capable assistant with no institutional memory.

The fix is simple, and it compounds. Once it's in place, every session starts informed. Instructions don't drift. Preferences don't need repeating. Claude Code carries context the way a good operator carries context — not just for the task in front of it, but for the world it's operating in.

Here's how to build it.

## The Two Layers

Memory in Claude Code works in two layers.

The first layer is **CLAUDE.md** — an instruction file Claude Code reads at the start of every session. This is where you put how you want it to behave: your response style preferences, standing instructions, recurring workflows, role definitions. Think of it as a permanent briefing document. It loads automatically, every time, before you type anything.

The second layer is a **/memory/ folder** — a set of individual files that capture accumulated knowledge about your world. Not instructions, but facts: preferences it's learned, feedback it received, projects it's been briefed on, people it's been introduced to. Each session, Claude Code reads these files and uses them to inform everything it does.

Together, these two layers mean the agent never starts from zero again.

## Setting Up CLAUDE.md

CLAUDE.md lives in your project root or your home directory. Claude Code reads it automatically when it starts. If you put it in `~/.claude/CLAUDE.md`, it applies globally across every project.

The format is plain markdown. Write it like you'd brief a new person on your team who's highly capable but knows nothing about you yet.

Useful things to include:

- **How you want responses structured.** Length, tone, level of preamble, whether you want reasoning shown or just the action.
- **Standing instructions.** "Always send a Telegram update when you start and finish a task." "Don't commit and push without confirming first." "Before writing any message to an external contact, draft it and show me."
- **Your context.** Who you are, what you work on, what systems you use, what tools are available.
- **Key file paths.** Where your contacts live, your notes, your scripts. The agent shouldn't have to search for things it will need every session.

Keep it factual. Don't explain why you want things — just state what you want. The agent will follow it.

## Setting Up the Memory Folder

The /memory/ folder is separate from instructions. It stores what Claude Code learns about you over time, not what you tell it upfront.

Create a folder — `/memory/` at the same level as CLAUDE.md — and inside it, create individual files by type:

- `user.md` — who you are, how you work, what you know, what you don't
- `feedback.md` — corrections and confirmations from past sessions (what not to do again, what worked well)
- `project.md` — ongoing initiatives, current priorities, deadlines, decisions made
- `reference.md` — where things live in external systems (databases, project trackers, communication channels)

Each file is just markdown. No special format required. Claude Code reads them and incorporates the context automatically.

The value isn't any single file. It's that these files grow. A feedback memory from three weeks ago still applies today. A project memory written when a new engagement started carries forward until the engagement ends. Over time, the agent's operating picture becomes more complete, not less.

## The Write-Back Loop

The memory folder only works if Claude Code writes to it, not just reads from it.

When something new is worth remembering — a preference stated, a decision made, a correction given — tell Claude Code to save it. Better yet, instruct it in CLAUDE.md to save relevant information automatically. "When you learn something non-obvious about how I prefer to work, save it to `/memory/feedback.md`." "When a new project or engagement is described, add a summary to `/memory/project.md`."

The discipline required is light: you write the initial files, and then you trust the system to accumulate. What you're building is institutional memory that compounds. Each session leaves the system slightly more calibrated than it found it.

## What Surprised Me

The first thing that surprised me was how much context I had been assuming Claude Code held.

I'd been treating it like a colleague who remembered our previous conversations. When it didn't respond in the way I expected, I'd correct it. Next session, same correction. I hadn't noticed the pattern until I started writing memory files — because writing them forced me to enumerate what I actually needed it to know. The list was longer than I expected.

The second surprise was how quickly the feedback file became the most valuable one. Not the project files, not the reference files — the feedback file. A single line like "Don't add trailing summaries to responses — the user can read the output" changes every interaction that follows. Accumulated over months, a well-maintained feedback file is a detailed model of how you think and work. It's more useful than any explicit instruction.

## Where to Start

Don't start by designing the perfect system. Start with one file.

Open `~/.claude/CLAUDE.md` and write ten lines: who you are, how you want responses delivered, and two or three standing instructions that you find yourself repeating across sessions. Save it. Start a new session. Notice what's different.

Then, after a few sessions, create the memory folder and add a `feedback.md`. Each time Claude Code does something you correct, add a line. Each time something works exactly as you hoped, add a line. Don't batch it — add it in the moment.

Within a few weeks, the system starts pulling ahead. Sessions start informed. The corrections accumulate as preferences. Instructions compound.

That's the thing about memory: you only have to give it once.

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/posthog-mcp-no-dashboard" style="text-decoration: none; color: #0366d6;">Next: How I Query My Product Analytics Without Opening a Dashboard →</a>
  </div>
  <div>
    <a href="/the-memo-you-never-wrote" style="text-decoration: none; color: #0366d6;">← Previous: The Memo You Never Wrote</a>
  </div>
  <div>
    <a href="/" style="text-decoration: none; color: #0366d6;">Home</a>
  </div>
</nav>
