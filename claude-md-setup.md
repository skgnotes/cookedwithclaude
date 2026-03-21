---
layout: post
title: "The CLAUDE.md setup that makes everything work"
permalink: /claude-md-setup
---

# The CLAUDE.md setup that makes everything work

Every session with Claude Code starts from zero.

No memory of last week. No knowledge of how you like things done. No context about who your EA is, which GitHub account to push from, or the fact that you never want em dashes in your writing. You start clean, you re-explain, you get generic output.

Unless you've built a CLAUDE.md.

This is the one setup task that compounds across everything else. Every automation, every how-to on this site, every workflow you build — it all works better once Claude Code has permanent standing instructions. The CLAUDE.md is how you give it those instructions.

Here's how to build one that actually does the job.

## What CLAUDE.md is

Claude Code reads CLAUDE.md automatically at the start of every session. No prompt required. Whatever is in that file becomes Claude's operating context for the duration of the session.

There are two levels:

- **Global** (`~/.claude/CLAUDE.md`) — applies to every session, regardless of project
- **Project-level** (a `CLAUDE.md` in any folder) — applies when Claude Code is run from that directory

Most of what makes Claude Code useful day-to-day lives in the global file. The project-level file is for folder-specific context: repo structure, publishing workflow, specific rules for that codebase.

Start with the global file. Everything else follows.

## What to put in it

The goal is to answer three questions Claude Code can't answer on its own: who you are, how you work, and where things live.

### Who you are

Not a biography. The operational facts that change how Claude Code interprets your requests.

Your name. Your email. Your role. The businesses you run or advise. The assistant or EA relationship you have. Whether you're technical or not. What city you're in. These aren't vanity — they change how Claude Code frames its output and who it mentions things to.

A founder running four businesses wants different default assumptions than a developer working on a single product.

```
## Who you are
[Your name] — [role], [location].
Email: your@email.com
Currently [brief description of what you're working on].
```

### How you work

This is where most of the leverage is.

Write out the standing preferences that you'd otherwise repeat every session. The operating principles that should never require re-stating. For example:

- **Action bias.** Do things, don't ask permission. Only pause for irreversible, destructive actions.
- **Verify before confirming done.** After any task, check the result. Don't declare success based on a command not throwing an error.
- **Preferred tools.** Which CLI tools you have set up. Which browser automation should use. Which accounts belong to which services.
- **Communication rules.** Draft before sending any message. Exception: messages to your own assistant — send those directly.
- **Tone preferences.** Short sentences. No preamble. Lead with the answer.

These are the instructions you'd give a new EA on day one. Write them down once, and Claude Code follows them in every session.

### Where things live

The most underrated section.

Claude Code can read files. It cannot know which files matter or where to find them. A context file map removes that friction entirely.

List the files that contain critical context and when to load them:

```
| File | Load when |
|------|-----------|
| contacts.md | Any communication task |
| facts.md | Payment details, form-filling, account credentials |
| actions.md | Every planning or triage session |
| [project]/overview.md | Any session in that project folder |
```

When Claude Code knows where things live, it fetches them. When it doesn't, it either halts to ask or makes something up. The context map eliminates both.

## The structure that works

Here's the outline that makes a global CLAUDE.md functional:

```markdown
# Global Claude Instructions

## Primary Objective
[One paragraph: what you use Claude Code for, the operating mental model]

## Who you are
[Name, role, email, current work focus]

## How to act
[Your standing preferences — autonomy level, verification requirements, tool choices]

## Standing instructions
[Specific recurring rules: communication protocols, account choices, tone]

## Where things live
[File and folder map by task type]

## Technical reference
[Script paths, CLI tools, API keys locations, common commands you want accessible]
```

Keep each section tight. This isn't documentation — it's operating instructions. If a sentence doesn't change Claude's behaviour, cut it.

## The project-level CLAUDE.md

Once the global file is working, add project-level files for any folder where you do recurring work.

A project-level CLAUDE.md should cover what the global one can't: the specific repo structure, the publishing workflow, the rules unique to that project. It inherits the global context automatically — you only need to add what's different.

For a blog, that means: how to structure a post, where drafts live, what anonymization rules apply, which GitHub account handles the push. For a client project: the architecture decisions, the deployment pipeline, what's in scope.

A good project CLAUDE.md is 50–150 lines. If it's longer, it's probably documenting things that belong in the code or in separate reference files — not in the instructions file.

## What changes when you have it

The first session after building a real CLAUDE.md feels different.

Claude Code stops asking what you want and starts doing it. It knows which account to use. It knows not to send messages without drafting first. It knows to send you a Telegram notification at the start of every long task. It knows your EA's name and where to reach them.

The honest version of this: you still have to write the file. That means an hour of thinking through how you actually work and what you'd want an autonomous assistant to know. Most people skip this and wonder why their Claude Code sessions feel like starting from scratch every time.

Write it once. Every session that follows starts with an operator, not a blank slate.

## How to start

Create `~/.claude/CLAUDE.md` and add three things: your name and role, one standing instruction about how you like to work, and one context file you reference regularly.

That's the minimum. Ship it. Then add to it every time you catch yourself re-explaining something you've explained before.

The file compounds. An hour of setup returns that hour — plus margin — on every session that follows.

<nav style="margin-top: 48px; padding-top: 24px; border-top: 1px solid #eee; font-size: 14px;">
  <div>
    <a href="/context-engineering">← Previous: Context engineering, not prompt engineering</a>
  </div>
  <div style="margin-top: 16px;">
    <a href="/">↑ Home</a>
  </div>
</nav>
