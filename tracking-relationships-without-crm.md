---
layout: post
title: "How I track birthdays and follow-ups without a CRM"
permalink: /tracking-relationships-without-crm
---

# How I track birthdays and follow-ups without a CRM

Every morning, my phone gets a Telegram message that looks something like this:

> **Upcoming:** A founder I've been advising turns 40 on Thursday. Last spoke 6 weeks ago — he was mid-fundraise. Check in.
>
> **Overdue:** Connected with a product lead at an education startup 3 months ago. Said you'd introduce him to someone in edtech. Still pending.

No app open. No CRM to log into. No reminder I had to manually set. The context just arrives.

This is what relationship management looks like when you stop trying to systematize it and start treating it as an information retrieval problem.

## Why CRMs fail founders

CRMs are built for sales pipelines, not relationships. The mental model is wrong from the start. You're not moving people through stages — you're maintaining a web of connections that matters in ways you can't predict in advance.

The other problem is maintenance overhead. A CRM only works if you feed it. Every contact logged, every note added, every follow-up scheduled — that's time and attention spent on the system instead of the relationships. Most founders I know have half-empty CRMs within six months.

The "who do I need to follow up with?" problem doesn't go away. It just goes unmanaged.

## The setup: a flat file and a daily check

The core of this system is a single markdown file — `people.md` — and a daily automated check that reads it and sends you a Telegram if anything's coming up.

### people.md

Each person gets a short entry:

```
## [Name or identifier]
- Context: [How you know them, in one line]
- Birthday: [MM-DD or YYYY-MM-DD]
- Last contact: [YYYY-MM-DD]
- Next follow-up: [YYYY-MM-DD or a note like "when they close the round"]
- Notes: [What matters to them, what you've discussed, what you promised]
```

No more than that. The constraint is intentional. If you can't summarize why someone matters in three sentences, you haven't thought clearly about the relationship.

A typical entry looks like this:

```
## Founder, SaaS startup (met at conference, March 2025)
- Context: Building B2B analytics tool, intro'd to two potential customers
- Birthday: 09-14
- Last contact: 2025-12-10
- Next follow-up: 2026-03-01
- Notes: Fundraising Series A, skeptical of AI hype, values directness
```

### The daily check

A LaunchAgent runs every morning at 7 AM. The script reads `people.md` and checks two things:

1. **Birthdays in the next 7 days** — pulls the entry, sends name and context
2. **Overdue follow-ups** — any `Next follow-up` date that's today or past

The Telegram message formats the alert with the person's context notes, so you're not just getting a name — you're getting the context you need to actually act.

Here's the core of the check script:

```python
import re
from datetime import datetime, timedelta
import requests

PEOPLE_FILE = "/path/to/people.md"
TELEGRAM_BOT_TOKEN = "your_token"
CHAT_ID = "your_chat_id"
TODAY = datetime.today()

def send_telegram(message):
    url = f"https://api.telegram.org/bot{TELEGRAM_BOT_TOKEN}/sendMessage"
    requests.post(url, data={"chat_id": CHAT_ID, "text": message})

with open(PEOPLE_FILE) as f:
    content = f.read()

# Parse entries and check dates
# [parsing logic reads each ## section, extracts Birthday and Next follow-up fields]
# Birthday match: within 7 days (ignoring year)
# Follow-up match: date is today or in the past
```

The full implementation is straightforward — roughly 80 lines of Python. Claude Code wrote the first working version in a single prompt when I described the file format and what I wanted.

### Automation via LaunchAgent

On macOS, a plist file in `~/Library/LaunchAgents/` runs the script at 7 AM daily:

```xml
<key>StartCalendarInterval</key>
<dict>
    <key>Hour</key>
    <integer>7</integer>
    <key>Minute</key>
    <integer>0</integer>
</dict>
```

On Linux, a cron job at `0 7 * * *` does the same.

## What surprised me

The discipline the flat file imposes is more valuable than the automation.

When you only have a few lines per person, you get ruthless about what actually matters. You stop tracking noise and start tracking signal. The act of deciding what to write forces you to think about why the relationship matters.

I've also noticed that the system catches things I would have missed entirely — not because I forgot to log a follow-up, but because I never had a forcing function to surface what I'd promised three months ago. The Telegram message makes those commitments visible again.

The other thing: writing `Next follow-up: when they close the round` is more useful than a date. The system treats it as a human-readable note rather than a scheduled task. I review these entries periodically and check in when the condition is likely met.

## How to start

Don't build the full system yet. Start with the file.

Open a blank markdown file and add ten people you should be in contact with. For each one, write: how you know them, when you last spoke, and the one thing you'd want to remember before reaching out.

That's it. The file is useful before you automate anything.

Once you have twenty or thirty entries, the pattern of what's overdue becomes obvious even on a manual read. That's when the automation starts earning its place.

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/playwright-google-business-profile" style="text-decoration: none; color: #0366d6;">← Previous: How we fixed a Google Business Profile with Playwright — without touching the API</a>
  </div>
  <div>
    <a href="/" style="text-decoration: none; color: #0366d6;">Home</a>
  </div>
</nav>
