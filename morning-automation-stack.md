---
layout: post
title: "Your morning automation stack"
permalink: /morning-automation-stack
---

# Your morning automation stack

The brief arrived before I was done with my first coffee.

Today's meetings. A call in the afternoon I'd almost forgotten. A birthday coming up in three days. Four items on my action list. A quick note that the inbox was clear.

All of it, already assembled and waiting in Telegram at 8 AM. I had not opened a single app.

If you've read the essay on the morning brief, you know why it matters. This is the technical walkthrough — the full stack, laid out so you can replicate it in one session.

## What you're building

A scheduled Claude Code skill that wakes up every morning, pulls from five data sources, assembles a single digest, and delivers it before you pick up your phone to check anything.

The five sources:

- **Google Calendar** — today's meetings and a five-day look-ahead
- **Cadences file** — recurring touchpoints and commitments tracked in a flat file
- **Birthdays** — upcoming dates pulled from your personal facts store
- **Actions file** — the GTD-style task list, filtered to today and high-priority
- **Inbox status** — a snapshot of whether anything urgent is sitting in email

You can start with just calendar. Add the others as you understand what you actually need to know before the day starts.

## The architecture

One shell script. One Claude Code skill. One LaunchAgent.

**The shell script** (`morning-digest.sh`) kicks off the whole run. It calls `claude` with the skill command and passes any needed context. A run takes about 30 seconds.

**The skill file** (`~/.claude/skills/morning-digest.md`) contains the instructions: what to read, what to look for, how to format the output, where to send it. It is a plain markdown file. You update it like a document.

**The LaunchAgent** (`com.user.morningdigest.plist`) is the macOS equivalent of a cron job. It fires the shell script at 8 AM every day, whether you are at your desk or not.

That is the entire stack. Everything else is data sources.

## The skill file

Create `morning-digest.md` in your Claude Code skills folder (`~/.claude/skills/`). Here is the structure of mine, stripped down to the essential pattern:

```markdown
# Morning Digest

You are generating the morning brief.

Read the following:
1. Google Calendar — events for today and the next 5 days
2. ~/Documents/PersonalOS/cadences.md — recurring reminders and touchpoints
3. ~/Documents/PersonalOS/facts.md — birthdays section, look 7 days ahead
4. ~/Documents/PersonalOS/actions.md — today's items and anything high-priority
5. ~/Documents/PersonalOS/inbox-status.md if it exists — one-line inbox summary

Format as:

**Today** — [day, date]
[Today's meetings with times]

**This week**
[Notable items in next 5 days]

**Upcoming**
[Birthdays or cadences due in next 7 days]

**On your plate**
[Today's actions, high-priority first]

**Inbox**
[Status line if available]

Send the formatted digest to Telegram using tg.sh.
```

Intentionally sparse. Claude Code is good at matching a format from minimal instruction. You do not need elaborate templates.

## Calendar access

The standard route is the Google Calendar API. The setup:

1. Enable the Google Calendar API in Google Cloud Console
2. Create a service account for headless automation
3. Download the credentials JSON file
4. Point your skill at the credentials path

A simpler route if you prefer: the `gcal` command-line tool. If you have it installed, the skill can call `gcal list --format=json` and parse the output. Less setup, equally reliable.

The goal is getting calendar data into a format Claude Code can read. Once that works, everything else is formatting instructions.

## The cadences file

This is the most underrated input in the stack. A flat markdown file of recurring commitments:

```markdown
# Cadences

- Monthly: Review pipeline — first week of month
- Weekly: Team sync — Mondays
- Quarterly: Review pricing — next due: June 2026
- Annual: Subscription renewals — various (April)
```

The skill reads this file and flags anything relevant to the current period. No API, no integration, no setup beyond writing the file once.

Birthdays work the same way. A section in your personal facts file:

```markdown
## Birthdays
- [Name]: March 15
- [Name]: April 3
```

Real names and dates in yours. The skill checks whether any fall in the next seven days and includes them if they do. This one change has turned "did I remember to send a message?" from an occasional miss to a zero-miss record.

## The inbox status file

This section does not require polling email in real-time. The simpler approach: a file that your email-triage automation updates whenever it runs.

Create `inbox-status.md` in your PersonalOS folder. Your email script (or a separate Claude Code skill that runs after each triage session) writes a single line to this file:

```
Inbox: 0 unread — last checked 07:45
```

or

```
Inbox: 3 unread — flagged for review
```

The morning digest skill reads whatever is in the file. It does not have to be live. Even a status from the previous evening is useful context before the day starts.

## The delivery script

If you have not set up a Telegram bot, do that first — it takes ten minutes and you only do it once. Create a bot via BotFather, get the token, note your chat ID.

Then create `tg.sh`:

```bash
#!/bin/bash
TOKEN=$(python3 -c "import json; print(json.load(open('/path/to/config.json'))['telegram_bot_token'])")
curl -s -X POST "https://api.telegram.org/bot$TOKEN/sendMessage" \
  -d "chat_id=YOUR_CHAT_ID" \
  -d "text=$1" \
  -d "parse_mode=Markdown"
```

Store the token in a config file, not in the script itself. The skill ends every run by calling `bash ~/Documents/scripts/tg.sh "message"`.

## The LaunchAgent

Create `~/Library/LaunchAgents/com.user.morningdigest.plist`:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN"
  "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>com.user.morningdigest</string>
    <key>ProgramArguments</key>
    <array>
        <string>/bin/bash</string>
        <string>/Users/yourusername/Documents/scripts/morning-digest.sh</string>
    </array>
    <key>StartCalendarInterval</key>
    <dict>
        <key>Hour</key>
        <integer>8</integer>
        <key>Minute</key>
        <integer>0</integer>
    </dict>
    <key>StandardOutPath</key>
    <string>/tmp/morning-digest.log</string>
    <key>StandardErrorPath</key>
    <string>/tmp/morning-digest-error.log</string>
</dict>
</plist>
```

Load it once:

```bash
launchctl load ~/Library/LaunchAgents/com.user.morningdigest.plist
```

It will run every morning at 8 AM. Check `/tmp/morning-digest.log` if it ever goes quiet.

## What surprised me

I expected the calendar section to be the most useful. It is not.

The cadences and birthdays section does more cognitive work per line than anything else in the brief. The calendar tells you about today. The cadences file tells you about relationships and commitments that would otherwise drift without ever appearing as urgent. The birthday flag has eliminated an entire category of social error from my life.

The brief is a system for noticing. Once you see what it surfaces, you realise how much was not being noticed before — not because it was invisible, but because it was competing with louder things for a limited amount of attention.

## Where to start

Build the calendar section first. Get it working, get it delivering to Telegram, let it arrive one morning.

Then spend a week noticing what you manually check, or wish you had been reminded of. That is what goes in next.

The cadences file is the easiest second step — no API, no integration, just a markdown file you write once and update when things change.

The full stack takes an afternoon to build. The return starts the next morning and compounds from there.

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/screenshots-to-board-report" style="text-decoration: none; color: #0366d6;">← Previous: From screenshots to board report in one session</a>
  </div>
  <div>
    <a href="/" style="text-decoration: none; color: #0366d6;">Home</a>
  </div>
</nav>
