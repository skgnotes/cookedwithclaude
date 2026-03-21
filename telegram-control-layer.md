---
layout: post
title: "Hooking Up Claude Code with Telegram"
permalink: /telegram-control-layer
---

# Hooking Up Claude Code with Telegram

Most people run Claude Code and then stare at the terminal until it finishes.

That's not a system. That's babysitting.

What I have instead: Claude sends me a Telegram message when it starts something, updates me midway through, and pings me when it's done. I reply from my phone if I need to redirect it. The whole thing runs in the background while I do other work.

This is what that setup looks like.

## Why Telegram

You could use desktop notifications, a log file, or a dashboard. But Telegram is already on your phone, already in your pocket, already part of how you communicate. Adding Claude Code to it means you're working the same channel where your EA sends you updates and your clients send questions. It's not a new tool — it's just a new sender.

The two-way piece matters more than people expect. Once you can *reply* to Claude from your phone, your whole relationship with long-running tasks changes. You don't hover. You go do something. The task runs. Your phone buzzes. You check, reply if needed, and put it back down. That's the loop I was actually trying to build.

## What You're Building

- A Telegram bot that belongs to Claude Code
- A `tg.sh` script that sends messages to your chat from any command or agent prompt
- A listener process that polls your Telegram inbox and routes incoming messages back to Claude

## Step 1: Create the Bot

Open Telegram and start a conversation with `@BotFather`.

Send `/newbot`. Give it a name and a username. BotFather will return a token that looks like this:

```
7891234567:AAFxyz_some_long_random_string_here
```

Copy it. This is your bot token. Keep it somewhere secure — I store mine in a local JSON config file.

## Step 2: Get Your Chat ID

Start a conversation with your new bot (search for its username and send `/start`). Then visit this URL in your browser, swapping in your token:

```
https://api.telegram.org/bot<YOUR_TOKEN>/getUpdates
```

You'll see a JSON response. Find the `chat.id` field inside the `message` object. That number is your personal chat ID. Write it down.

If the response is empty, send the bot another message first and refresh.

## Step 3: Set Up the Config File

I keep my bot token and chat ID in a JSON config file:

```json
{
  "skg_bot_token": "7891234567:AAFxyz_your_token_here",
  "my_chat_id": 217000000
}
```

Replace the values with your own. The token key name is arbitrary — just stay consistent.

## Step 4: Write tg.sh

This is the script that does the sending. Drop it somewhere on your PATH or in a scripts folder:

```bash
#!/bin/bash
# tg.sh — send a Telegram message
# Usage: bash tg.sh "your message"
#        bash tg.sh "your message" "chat_id"  (optional override)

MESSAGE="$1"
CHAT_ID="${2:-$(python3 -c "import json; print(json.load(open('/path/to/your/config.json'))['my_chat_id'])")}"
TOKEN=$(python3 -c "import json; print(json.load(open('/path/to/your/config.json'))['skg_bot_token'])")

curl -s -X POST "https://api.telegram.org/bot${TOKEN}/sendMessage" \
  -d "chat_id=${CHAT_ID}" \
  -d "text=${MESSAGE}" \
  > /dev/null
```

Replace `/path/to/your/config.json` with your actual config file path.

Test it:

```bash
bash tg.sh "hello from claude"
```

Your phone should buzz.

## Step 5: Wire It Into Claude Code

Once `tg.sh` works, you can call it from anywhere Claude Code runs — agent prompts, CLAUDE.md instructions, post-task hooks.

In a CLAUDE.md file:

```
Always send Telegram updates at key points in every session via tg.sh —
start of task, key intermediate points, choke points, task completion.
```

In an agent prompt directly:

```
After completing the task, run:
bash /path/to/scripts/tg.sh "✅ Done — [brief summary]"
```

The pattern is simple: any time you'd want to know something, add a `tg.sh` call. Task started. File saved. API call succeeded. Error hit. Task done.

## Step 6: Set Up the Listener

The listener is a polling loop. It checks your Telegram inbox every few seconds, looks for new messages from you, and acts on them.

Here's a basic version:

```bash
#!/bin/bash
# tg-listener.sh — poll Telegram and print new messages

CONFIG="/path/to/your/config.json"
TOKEN=$(python3 -c "import json; print(json.load(open('$CONFIG'))['skg_bot_token'])")
OFFSET=0

while true; do
  RESPONSE=$(curl -s "https://api.telegram.org/bot${TOKEN}/getUpdates?offset=$OFFSET&timeout=10")

  MESSAGES=$(echo "$RESPONSE" | python3 -c "
import json, sys
data = json.load(sys.stdin)
for update in data.get('result', []):
    msg = update.get('message', {})
    text = msg.get('text', '')
    update_id = update.get('update_id', 0)
    if text:
        print(f'{update_id}|||{text}')
")

  while IFS='|||' read -r update_id text; do
    if [ -n "$update_id" ] && [ -n "$text" ]; then
      echo "Received: $text"
      # Your routing logic here
      OFFSET=$((update_id + 1))
    fi
  done <<< "$MESSAGES"

  sleep 2
done
```

What you do with the incoming message is up to you. Options:
- Write it to a file that a running Claude session polls
- Pass it as input to a new `claude` CLI invocation
- Post it into a tmux session where Claude is running

The simplest version I use: the listener writes incoming messages to a temp file. My agent prompts include an instruction to check that file periodically and treat any contents as a redirect or additional instruction.

## What Surprised Me

I expected the notifications to be useful. What I didn't expect was how much the *two-way* piece changed my behavior.

Before: I'd start a long Claude task, feel anxious about what it was doing, drift back to the terminal to check.

After: I start the task, my phone confirms it started, I go do something else. When it pings me done, I read the summary and decide next steps right there. If something's going sideways, the midway ping tells me before it gets worse.

The listener is the part that feels different. You stop watching the machine. The machine tells you when it needs you.

## Where to Start

Do Step 1 through Step 4 first. Get `tg.sh` working and add one `tg.sh` call to something Claude Code already does. See the message land on your phone. That alone is useful.

The listener can wait. One-way notifications solve 80% of the problem.

Once you want two-way, build the listener. The simplest version — write to a file, have your agent check the file — takes about an hour to set up and works reliably.

The more sophisticated setup (listener piping into an active Claude session) is real automation infrastructure. Build it when you've earned the need for it, not before.

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/setting-up-playwright" style="text-decoration: none; color: #0366d6;">← Previous: Setting up Playwright and why it matters</a>
  </div>
  <div>
    <a href="/" style="text-decoration: none; color: #0366d6;">Home</a>
  </div>
</nav>
