---
layout: post
title: "Use Google Antigravity to set up Claude Code on your machine"
permalink: /setup-claude-code-antigravity
---

# Use Google Antigravity to set up Claude Code on your machine

Most setup guides assume you're comfortable in a terminal. This one doesn't.

If you've been reading about Claude Code and want to try it — but the installation instructions read like they were written for someone else — this is for you. You're going to use Google Antigravity, a free AI development environment, to handle the technical setup. You do the directing. Antigravity does the installing.

By the end, Claude Code will be running on your Mac.

## Why setup has always been the barrier

Installing Claude Code the standard way requires Node.js, npm, and a working terminal session. None of those are hard for someone who does this regularly. For everyone else, they're three separate rabbit holes, each with its own version of "it depends."

Google Antigravity changes that. It ships as a proper Mac app — you download it, drag it to Applications, and it opens. Inside, there are AI agents that can run terminal commands, handle errors, and explain what's happening in plain language. You use those agents to complete the Claude Code installation instead of figuring it out yourself.

This is the setup process for non-developers. It takes about fifteen minutes.

## Step 1: Install Google Antigravity

Go to antigravity.google and download the Mac version. You'll need a personal Gmail account to log in — Workspace accounts aren't supported in the current preview.

Once downloaded, open the `.dmg` file, drag Google Antigravity to your Applications folder, and open it. Sign in with your Gmail. You're now inside Antigravity.

The interface will look familiar if you've ever seen a code editor, but you don't need to use most of it. The part you care about is the chat panel — that's where Antigravity's agent lives.

## Step 2: Let Antigravity install your dependencies

Claude Code needs Node.js (version 18 or higher) and npm to run. These are technical prerequisites. You're going to ask Antigravity to check for them and install them if they're missing.

In the Antigravity chat panel, type:

> "Check if Node.js and npm are installed on my Mac. If they're not installed, install them. Use Homebrew if it's available, or install it first if needed."

The agent will open a terminal, run the checks, and handle whatever it finds. If you don't have Homebrew, it installs that first. If Node.js isn't present, it installs it. Watch what it does — you don't need to intervene, but reading the output builds familiarity with what's happening on your machine.

When it finishes, you'll see versions confirmed. Something like `node v22.x.x` and `npm 10.x.x`.

## Step 3: Install Claude Code

Once Node.js is in place, the Claude Code installation is one command. In the same Antigravity chat panel:

> "Install Claude Code globally using npm."

Antigravity will run `npm install -g @anthropic-ai/claude-code` and confirm when it's done.

## Step 4: Set up your Anthropic API key

Claude Code needs an API key from Anthropic to run. Go to console.anthropic.com, create an account, and generate an API key from the API Keys section. Copy it.

Back in Antigravity, ask:

> "Add my Anthropic API key to my shell environment so Claude Code can use it. The key is [paste your key here]."

The agent will add it to your `.zshrc` or `.bash_profile` — whichever your Mac uses — and tell you to restart your terminal or run `source` to reload the configuration.

## Step 5: Start Claude Code

Open a new terminal window. Navigate to a folder where you want to work — your Desktop, Documents, wherever. Then type:

```
claude
```

Claude Code starts. You're done.

## What surprised me about this approach

The first time I tried explaining Claude Code setup to someone without a development background, I spent a full hour working through terminal errors with them. Node version conflicts. PATH issues. Shell configuration quirks. Things that are genuinely tedious to debug and have nothing to do with what they were trying to accomplish.

Using Antigravity to handle the setup changes that experience entirely. The agent narrates what it's doing, handles errors without needing you to understand them, and confirms success before moving on.

The unexpected thing: Antigravity keeps a record of every command it ran. You can scroll back through the session and see the full installation history. For someone new to all of this, that log is more useful than most tutorials — it shows you exactly what was done, in order, in plain view.

## Where to start

Download Google Antigravity from antigravity.google. Use a personal Gmail account. Follow the steps above in order.

The rest of this series assumes you're already running Claude Code. This is how you get there.

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/setting-up-google-workspace" style="text-decoration: none; color: #0366d6;">← Previous: Setting up Google Workspace with Claude Code</a>
  </div>
  <div>
    <a href="/" style="text-decoration: none; color: #0366d6;">Home</a>
  </div>
</nav>
