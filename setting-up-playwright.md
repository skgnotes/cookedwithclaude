---
layout: post
title: "Setting up Playwright and why it matters"
permalink: /setting-up-playwright
---

# Setting up Playwright and why it matters

There's a moment where Claude Code stops feeling like a smart text tool and starts feeling like a capable assistant. For most people, that moment happens when they add Playwright.

Without it, Claude Code operates in files, terminals, and APIs. With it, Claude Code can open a browser, click things, fill in forms, log in to websites, retrieve information, and navigate the web — all without you touching a mouse. That's the shift. And for non-developers, it's the most important add-on you can install.

## Why it matters before it's set up

Most of the workflows documented on this site use Playwright somewhere. Web check-ins. LinkedIn profile updates. Order placements. Shopify store setup. Email filing. Every task that involves a website — not an API, an actual website — goes through Playwright.

The operators who can't yet use it hit a wall. There's a whole category of automation that's simply unavailable to them. They're limited to tasks where everything has a clean API or a CLI command. Which rules out most of the internet.

Playwright gives Claude Code a browser. And giving Claude Code a browser means almost anything a human can do on a computer — Claude Code can do too.

## The one design decision to make first

Before installation, decide which browser Claude Code will use. This is not a technical decision; it's a systems one.

If you use a browser for personal work — saved logins, personal accounts, bookmarks — do not let Claude Code near it. The automations will interrupt sessions, blow out cookies, and create conflicts you don't want.

The pattern that works: use Chrome exclusively for Claude Code automation. Use a different browser (Edge, Firefox, Brave — anything) for everything personal. Keep them completely separate.

Once Chrome is reserved for automation, everything runs cleaner. Playwright knows where to find it. Sessions don't interfere with each other. You stop having to think about it.

## Installation

Playwright for Claude Code runs through the MCP (Model Context Protocol) layer — which is how Claude Code connects to external tools. The installation is a single command:

```bash
npm install -g @playwright/mcp@latest
```

Then add it to your Claude Code config. Open `~/.claude/claude_desktop_config.json` (create it if it doesn't exist) and add the Playwright MCP server:

```json
{
  "mcpServers": {
    "playwright": {
      "command": "npx",
      "args": ["@playwright/mcp@latest", "--browser", "chrome"]
    }
  }
}
```

If you want Claude Code to use a specific Chrome profile — which you do, to keep a persistent session — add the profile path:

```json
{
  "mcpServers": {
    "playwright": {
      "command": "npx",
      "args": [
        "@playwright/mcp@latest",
        "--browser", "chrome",
        "--user-data-dir", "/Users/yourusername/Library/Application Support/Google/Chrome/Default"
      ]
    }
  }
}
```

Replace `yourusername` with your actual macOS username. This is the default Chrome profile location on a Mac.

Restart Claude Code. Done.

## How to verify it's working

Open a new Claude Code session and ask it to take a screenshot of a webpage. Something like:

> "Open google.com and take a screenshot."

If Playwright is connected, Claude Code will open Chrome, navigate to Google, and return a screenshot. You'll see it happen — the browser window appears, navigates, and closes.

If it doesn't work, the most common issue is Node.js not being installed. Run `node --version` in a terminal. If nothing comes back, install Node.js first (nodejs.org has a standard installer), then run the Playwright install command again.

## What becomes possible

Once Playwright is running, Claude Code can:

- Log in to websites using credentials you provide
- Navigate multi-step web forms
- Click buttons, select dropdowns, upload files
- Extract data from pages that don't have APIs
- Take screenshots to verify that actions completed
- Handle popups, alerts, and modal dialogs

The things that used to require a developer — or just your own manual time — are now Claude Code tasks.

A founder I know asked Claude Code to check in for a flight, select a seat, and forward the boarding pass to WhatsApp. It did all three without any help. The only thing required: Playwright installed, Chrome profile active.

Another used it to place an order on a grocery delivery app — navigating the site, adding items to cart, entering the address, completing checkout — without opening a browser manually.

Neither of these people writes code.

## The thing I didn't expect

Playwright is not just useful — it changes how you think about delegation. Once you know Claude Code has a browser, you stop asking "can Claude do this?" and start asking "where is the browser session I need?"

Most tasks that stalled previously stalled because there was a website in the way. Playwright removes the website as a blocker. The internet becomes part of the task space.

## Where to start

After installation, run one simple test: ask Claude Code to open a website and describe what's on it. Not a complex task — just navigation and observation.

Once that works, pick one recurring task in your week that involves a website. A check-in, a form, a report you have to pull manually. Write a clear instruction. Let Claude Code try it.

The first successful end-to-end browser automation is the moment it clicks. Not theoretically — in practice, watching something you've done manually thirty times happen on its own.

Everything else builds from there.

<nav style="margin-top: 48px; padding-top: 24px; border-top: 1px solid #eee; font-size: 14px;">
  <div>
    <a href="/claude-md-setup">← Previous: The CLAUDE.md setup that makes everything work</a>
  </div>
  <div style="margin-top: 16px;">
    <a href="/">↑ Home</a>
  </div>
</nav>
