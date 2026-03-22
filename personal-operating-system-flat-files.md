---
layout: post
title: "How I Built a Personal Operating System with Flat Files"
permalink: /personal-operating-system-flat-files
---

# How I Built a Personal Operating System with Flat Files

Claude Code knows that my EA briefs via Telegram, not email. It knows which clients have active engagements and which are on hold. It knows my travel preferences, payment details, and how I like messages drafted before they're sent.

None of this is trained into the model. It's in a folder of plain markdown files on my laptop.

This is how I built a personal operating system — and why flat files turned out to be the right substrate for it.

## The Problem It Solves

Every AI assistant starts from zero. You give it context in the chat window, it uses it for the session, then it's gone. The next time you start, you explain everything again.

For casual tasks, this is tolerable. For someone using Claude Code as their primary execution layer — running workflows, drafting comms, managing clients, tracking actions — it's a constant tax. The tool is capable. The friction is context.

The insight I kept returning to: the context itself is valuable, and it can be made persistent.

## The Architecture

Everything lives in a single folder: `~/Documents/PersonalOS/`. It's a vault of flat markdown files, each with a clear scope.

| File | What it holds |
|------|--------------|
| `people.md` | Contacts, relationships, communication preferences |
| `actions.md` | Active to-do list, structured by GTD quadrants |
| `facts.md` | Payments, credentials, travel preferences, form-filling data |
| `ops.md` | How things get done — EA cadence, workflow logic, recurring processes |
| `comms.md` | Communication infrastructure and tone guidelines |
| `lifemap.md` | Upcoming commitments, scheduling context, horizon planning |
| `quick actions.md` | Fast-access list for triage and review |

Each file is human-readable and human-editable. There's no database. No sync service. No app layer sitting in front of it. Just markdown.

The files load on demand. For a communication task, Claude reads `comms.md`. When processing the inbox, it reads `ops.md` and `actions.md`. When drafting a message to a specific person, it reads `people.md`. When filling in a form or booking travel, it reads `facts.md`.

This is the entire system.

## Why Flat Files

The obvious question: why not a proper database? A CRM? A task manager with an API?

Three reasons.

First, **durability**. Markdown files don't go away. No startup risk. No pricing changes. No deprecated API. The files I have today are readable by any tool, forever.

Second, **editability**. I can open any file and change it in ten seconds. No interface to navigate. No fields to locate. I find the line, update it, save it. The AI picks it up on the next read.

Third, and most important: **they work natively with how Claude Code reads context**. The model doesn't query a database. It reads. Give it a well-structured markdown file and it extracts exactly what it needs. The file format and the AI's reading behavior are matched.

## How Claude Uses It

The CLAUDE.md file in my home directory is the entry point. It tells Claude which files exist, what each one contains, and when to load them. It's essentially a table of contents for the operating system.

When Claude starts a task, it checks whether any of the relevant context files apply. Communication task — load `comms.md`. Session start — load `ops.md`. Booking something — load `facts.md`. This is explicit in the instructions, not inferred.

The result is that Claude Code behaves like an assistant who knows the context, not a tool that has to be re-briefed every time.

A practical example: when I ask it to draft a message to a contact, it knows how that person prefers to receive communication, what project we're currently working on together, and what my last action with them was. All of that comes from `people.md` and `actions.md`. I don't explain any of it in the message.

## The GTD Layer

The actions file follows a loose GTD structure. Items are organized into quadrants: things to do now (Q1), things that are important but not urgent (Q2), things to delegate, and things to defer. Claude reads this file when processing my inbox or when I run a review session.

The key thing GTD gave me was the distinction between *capture* and *processing*. Items land in `actions.md` as captures. A review session processes them — moving them between quadrants, delegating to my EA, clearing what's done. Claude handles the processing; I handle the judgment calls.

This is what separates a system from a pile. Flat files are just a pile until there's a structure that tells the AI what to do with them.

## What Surprised Me

The system's value isn't the information it stores. It's the behavior it enables.

The most useful thing that happened wasn't Claude knowing my EA's name. It was Claude knowing *not to send a WhatsApp to a client before showing me a draft first*. That instruction lives in `comms.md`. It's a two-line policy. But it means I don't have to think about it — or remember to say it — ever again.

Standing instructions are more powerful than stored facts. The facts make Claude accurate. The instructions make it trustworthy.

## The Practical Part

Start with one file.

`facts.md` is the easiest entry point. Start with: your preferred payment methods, a few form-filling defaults (address, phone, email), and any travel preferences you use regularly. Then tell Claude in your CLAUDE.md to load this file when booking anything or filling in a form.

That's it. Within a week you'll notice that tasks which required three back-and-forth exchanges now require zero. That's when you start adding the other files.

The architecture can grow indefinitely. But start with the one file that would save you the most repetition right now. Build the system around the friction that actually costs you time.

The files are doing one thing: making sure your AI knows your world before you ask it to act in it.

---

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/setting-up-your-first-skill" style="text-decoration: none; color: #0366d6;">← Previous: Setting up your first skill</a>
  </div>
  <div>
    <a href="/" style="text-decoration: none; color: #0366d6;">Home</a>
  </div>
</nav>
