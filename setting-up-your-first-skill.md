---
layout: post
title: "Setting up your first skill"
permalink: /setting-up-your-first-skill
---

# Setting up your first skill

The third time you explain the same task to Claude, you start to feel the waste.

Not wasted time — the explanation takes thirty seconds. Wasted setup. You're rebuilding the context every time: here's what this is, here's who's involved, here's the format, here's what not to do. Claude gets it right each time. But you had to get it there.

A skill solves this. Write the instructions once, save them as a file, and invoke the whole thing with a slash command. From that point, Claude knows what to do without being told.

This is how you write your first one.

## What a skill actually is

A skill is a markdown file. One file, one folder, one command name. That's the whole structure.

Inside the file: frontmatter at the top with a name and description, followed by instructions for how to execute the task. Same format as any brief you'd give a new assistant — except Claude reads it every time you invoke it, not just the first time.

The file goes here:

```
~/.claude/skills/<skill-name>/SKILL.md
```

The folder name becomes the command. Create a folder called `morning-brief`, and `/morning-brief` becomes a valid command in Claude Code.

## The anatomy of a skill file

Here's the minimal structure:

```markdown
---
name: morning-brief
description: Compile and send my daily morning summary. Usage: /morning-brief
---

# Morning Brief

Compiles a daily brief and sends it via Telegram.

## Steps

1. Pull the three most recent unread emails and summarise each in one line
2. Check the calendar for today's meetings
3. Format as:

   **Morning Brief — [date]**
   - Emails: [list]
   - Today: [meetings]

4. Send via tg.sh
```

That's a working skill. The frontmatter gives Claude Code the name and the description shown when you list available skills. Everything below the `---` is instruction.

## What the instructions should cover

Think of the SKILL.md as the brief you'd give a capable new assistant who doesn't know your setup yet. Include:

**What the task is.** One sentence. What outcome are you producing?

**Any inputs.** If the skill accepts arguments (like `/morning-brief clients` for a focused version), document what each variant does. A small table works well here.

**The steps.** Ordered. Specific. Each step is an instruction, not a category. "Check email" is a category. "Search inbox for unread messages from the last 24 hours and summarise subject and sender" is an instruction.

**Notes and exceptions.** What should Claude never do? What should it do if something fails? What's the right fallback? This is where you encode the judgement calls you'd otherwise be making in the moment.

The more specific the skill, the fewer surprises at runtime.

## A real example (trimmed for length)

Here's a lightly simplified version of one I use to post a daily group poll:

```markdown
---
name: daily-poll
description: Post the daily availability poll in the team group. Usage: /daily-poll [yes|no|maybe]
---

# Daily Poll

Posts the daily attendance poll in the team WhatsApp group. Optionally votes on my behalf.

## Input

| Command | Behaviour |
|---------|-----------|
| `/daily-poll yes` | Post poll + vote yes |
| `/daily-poll no` | Post poll + vote no |
| `/daily-poll` | Post poll only |

## Steps

1. Generate today's date string: `date '+%-d %b, %a'`
2. Open WhatsApp Web via Playwright
3. Navigate to the group
4. Post the poll with the date in the question
5. If a vote argument was provided, cast that vote
6. Send a Telegram confirmation

## Notes

- Do not post on Sundays
- If WhatsApp shows a QR code, abort and send a Telegram alert
- On any Playwright failure: retry once before giving up
```

This runs in under two minutes, every time, without re-explaining the date format or the group name or what to do when the session has expired.

## Where things go wrong

The most common mistake with first skills: writing the goal instead of the steps.

"Post the message" is a goal. A skill file contains instructions for how to achieve it. If you'd give a new assistant verbal guidance about this task, that guidance belongs in the file.

The second mistake: no error handling. Real tasks fail. A page doesn't load. An API is down. A file is missing. The skill should say what to do — retry once, send an alert, or abort with a message. Without this, Claude will improvise. Sometimes fine. Often not.

## What surprised me

Skills don't just save time. They change what you trust.

When a task is written down in a skill file, I know what Claude will do before I run it. The behaviour is encoded. I've already thought through the edge cases. The result is consistent in a way that ad-hoc prompting never quite is.

That predictability is underrated. Most of the value in a documented process isn't the automation — it's that the process exists, is written down, and doesn't require a fresh judgement call every time it runs.

## Where to start

Pick one recurring task that you've explained to Claude more than twice. Doesn't need to be complex. Doesn't need to save hours. Just something you've re-explained.

Write a SKILL.md for it. Five to ten steps. Add a notes section. Create the folder, drop the file in, restart Claude Code.

Run it once. See what happens. Edit until it works exactly as intended.

After that first skill, the second one takes half the time. The pattern becomes obvious. And the list of things worth encoding gets longer the more you use Claude.

That's how the system compounds.

---

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/advice-is-not-action" style="text-decoration: none; color: #0366d6;">← Previous: Advice Is Not Action</a>
  </div>
  <div>
    <a href="/" style="text-decoration: none; color: #0366d6;">Home</a>
  </div>
</nav>
