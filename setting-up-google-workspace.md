---
layout: post
title: "Setting up Google Workspace with Claude Code"
permalink: /setting-up-google-workspace
---

# Setting up Google Workspace with Claude Code

The first time Claude Code checked my calendar and told me I had a conflict on Thursday, I had to sit with it for a second.

Not because it was surprising — I had just set it up, I knew what it was supposed to do. But because something shifted. It wasn't answering a general question anymore. It was answering *my* question, with *my* data. It knew what Thursday looked like. It knew the 11 AM slot was already taken. It responded like someone who had actually looked at the schedule, not like a tool generating a plausible response.

That's the difference Google Workspace makes. Without it, Claude Code knows how scheduling generally works. With it, Claude Code knows when you're free.

## What you're actually connecting

Google Workspace for our purposes is four things:

**Gmail** — Claude can read emails, draft replies in your voice, file messages, search threads by context, summarise an inbox, and send on your behalf.

**Calendar** — Claude can check availability, create events, reschedule meetings, look at the week ahead, and answer questions like "when did I last speak to this person?"

**Drive** — Claude can read documents, create new files, search across folders, pull context from meeting notes or proposals, and update sheets.

**Contacts** — Claude can look up phone numbers, emails, and company context — so when you say "send this to the agency team", it knows who that is.

None of these require you to tell Claude the information at the start of every session. Once connected, it's just available. You ask, it checks.

## Before you start: one credential setup, all four tools

Every Google MCP server uses the same authentication flow — OAuth 2.0 via a Google Cloud project you control. Set this up once, and all four connections use the same credentials file.

It sounds technical. It's about fifteen minutes.

### Step 1 — Create a Google Cloud project

Go to [console.cloud.google.com](https://console.cloud.google.com) and create a new project. Name it something obvious — "Claude Code" works fine. This project is just a container for the credentials.

### Step 2 — Enable the APIs you need

Inside the project, go to **APIs & Services → Library** and enable:

- Gmail API
- Google Calendar API
- Google Drive API
- People API (for Contacts)

Enable all four now, even if you only plan to use one initially. The setup effort is the same.

### Step 3 — Create OAuth credentials

Go to **APIs & Services → Credentials → Create Credentials → OAuth client ID**.

If you haven't set up a consent screen yet, Google will prompt you to do that first. Set it to **Internal** if you're using a Google Workspace account (company email), or **External** if you're on a personal Gmail. For External, add yourself as a test user.

When creating the OAuth client:
- Application type: **Desktop app**
- Name it anything

Download the credentials JSON file. Save it somewhere permanent — a folder like `~/.google-creds/` works well. You'll reference this path in your Claude Code config.

## Configuring the MCP servers

Open your Claude Code config file at `~/.claude/claude_desktop_config.json`. You'll add one entry per Google tool under `mcpServers`.

The MCP ecosystem for Google Workspace is active and evolving — a few packages have become the standard:

```json
{
  "mcpServers": {
    "google-drive": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-google-drive"],
      "env": {
        "GOOGLE_CREDENTIALS_FILE": "/Users/yourusername/.google-creds/credentials.json",
        "GOOGLE_TOKEN_FILE": "/Users/yourusername/.google-creds/token.json"
      }
    },
    "gmail": {
      "command": "npx",
      "args": ["-y", "@gptscript-ai/gmail-mcp"],
      "env": {
        "CREDENTIALS_FILE": "/Users/yourusername/.google-creds/credentials.json",
        "TOKEN_FILE": "/Users/yourusername/.google-creds/gmail-token.json"
      }
    },
    "google-calendar": {
      "command": "npx",
      "args": ["-y", "@gptscript-ai/google-calendar-mcp"],
      "env": {
        "CREDENTIALS_FILE": "/Users/yourusername/.google-creds/credentials.json",
        "TOKEN_FILE": "/Users/yourusername/.google-creds/calendar-token.json"
      }
    }
  }
}
```

Replace `yourusername` with your actual macOS username throughout. Each MCP uses its own token file so the sessions don't interfere — the credentials file is shared.

Note: the specific package names above reflect the state of the ecosystem as of early 2026. If a package has moved or been superseded, a quick search for "Gmail MCP server" or "Google Calendar MCP" will surface the current recommendation. The configuration pattern — credentials file, token file, npx launch — stays the same regardless of which package you use.

## First-time authentication

On the first run of each connected tool, Claude Code will prompt you to authenticate. A browser window will open, asking you to sign in to Google and grant the permissions your app is requesting.

This is standard OAuth — you're authorising your own app (the one you just created in GCP) to access your own data. Grant access, close the browser, and the token file gets written automatically.

You'll do this once per tool. After that, the tokens refresh silently in the background.

If Google shows a warning about an "unverified app" — this is expected. You created the app yourself in GCP; Google just doesn't know it. Click **Advanced → Go to [app name] (unsafe)** to proceed. You're authorising your own credentials.

## What becomes possible

Once all four are connected, the character of your Claude Code sessions changes.

You stop giving Claude context it should already have. Instead of saying "I have a call with the startup on Thursday at 2pm, can you prepare a brief", you say "I have a call Thursday — prepare a brief." It finds the event, reads the company name, checks if there are related emails, and builds context from what's already there.

You start delegating things that previously required you to open multiple tabs. "Draft a reply to the last email from the agency, decline politely but leave the door open." It finds the thread, reads the history, writes the reply in your voice.

Calendar management becomes conversational. "Find 45 minutes next week for a catch-up with the team lead." It checks your calendar, checks theirs if they're in your Contacts, and proposes slots.

A founder I know summarised it well: before the integration, she was the one who knew things. Claude would assist. After the integration, Claude started knowing things too — and the dynamic shifted from assistant to collaborator.

## The thing I didn't expect

Connecting Gmail was the one I thought I'd use least. I'm faster at email than at most things. But it turned out to be the one that paid back the fastest.

Not for writing emails — for finding them. Years of threads, across dozens of threads. Being able to say "when did we last discuss the pricing model, and what was the outcome?" and get an actual answer, with the thread pulled up and summarised. That's not something I was doing before. The search was too slow and too imprecise. Now I just ask.

The value isn't always in the new action. Sometimes it's in making an old one fast enough to actually do.

## Where to start

Set up the Google Cloud credentials first — that's the only step that has real friction. Give it fifteen minutes with the GCP console open.

Then connect one tool, not all four. Calendar is usually the easiest first — the permissions are simple, the first useful interaction is quick, and it immediately changes how you plan your day.

Once Calendar works and you've asked it a few real questions, add Drive. Then Gmail. By the time you add Contacts, you'll already know what you want to do with it.

The integration compounds. Each new data source makes every other one more useful. Claude Code knowing your calendar is useful. Claude Code knowing your calendar *and* your emails *and* the documents from last quarter's planning session — that's a different class of assistant entirely.


<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/your-content-team-is-now-an-org-chart" style="text-decoration: none; color: #0366d6;">← Previous: Your content team is now an org chart</a>
  </div>
  <div>
    <a href="/" style="text-decoration: none; color: #0366d6;">Home</a>
  </div>
</nav>
