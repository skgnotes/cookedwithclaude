---
layout: post
title: "The Silent Failure Problem"
permalink: /silent-failure
---

# The Silent Failure Problem

Three days into a trip, I noticed I hadn't received the daily digest my automation was supposed to be sending every morning. I opened the server logs and found the script had been failing since day one — silently, cleanly, without a word. No error email. No alert. Nothing. The job ran, hit an error, and stopped. Meanwhile I had been assuming it was working.

That's the silent failure problem. And it's the most dangerous failure mode in automation.

## The Anti-Pattern

When you start building automations — scheduled jobs, daily reports, background syncs, agentic workflows — the natural instinct is to check that the logic works. You write the code, test it once, verify the output looks right, and ship it.

What most people don't build is the part that tells you it ran.

The result is a class of automations I now call **silent failures**: processes that fail without alerting you. No noise, no red flag, no message. Just the quiet absence of something you were expecting.

Silent failures are worse than broken automations. With a broken automation, you know it's broken. With a silent failure, you think it's running. You make decisions based on data that isn't arriving. You stop doing the manual version of the task because you believe the automated version is handling it. By the time you notice something is wrong, it's been wrong for a while.

## The Fix: Heartbeat Bookends

The pattern that solved this for me is simple. Every automated workflow gets two Telegram messages: one at the start, one at the end.

```bash
bash ~/Documents/scripts/tg.sh "🔄 Daily digest — starting"

# ... the actual work ...

bash ~/Documents/scripts/tg.sh "✅ Daily digest — done"
```

That's it. The start message tells you the job fired. The end message tells you it completed. If you get the start message but not the end message, something failed between them. If you get neither, the job didn't fire at all — a cron issue, a machine that was off, a misconfigured LaunchAgent.

Two lines. Nothing complex.

## Why This Works

The failure mode it's protecting against isn't usually the logic failing. It's the infrastructure: the machine wasn't on, the environment variable wasn't set, a dependency silently changed. These are failures that don't surface in your code — they surface in the absence of output.

Telegram messages are zero-latency proof of execution. When the message arrives in your phone at 7 AM, you know the job ran. When it doesn't arrive and you notice at 8 AM, you've caught a failure with a one-hour lag instead of a three-day lag.

The key word is *notice*. Most silent failures persist not because they're hard to fix but because there's nothing prompting you to look. The heartbeat creates the prompt.

## What Surprised Me

I expected this to become background noise — notifications I'd start ignoring. It didn't.

The start/end pair creates a rhythm you actually notice when it's absent. After a few weeks of seeing the pattern, your brain starts expecting it. On days when the message doesn't arrive, you notice the gap. The notification itself becomes less important; the *absence* of the notification becomes the signal.

This is the counterintuitive part: you're training yourself to notice silence, not noise.

I also found that the start message does something useful beyond logging. When Claude Code agents run multi-step workflows, the start message anchors the execution in time. If something goes wrong three steps in, I know exactly when the run started and can correlate it with anything else that was happening at that time.

## The Minimal Implementation

Here's the full pattern for a scheduled workflow:

```bash
#!/bin/bash

SCRIPT_NAME="your-workflow-name"

# Heartbeat: start
bash ~/Documents/scripts/tg.sh "🔄 ${SCRIPT_NAME} — starting"

# Your actual work here
# ...
# ...

# Heartbeat: end
bash ~/Documents/scripts/tg.sh "✅ ${SCRIPT_NAME} — done"
```

For agentic workflows run by Claude Code, the same structure applies in the agent instructions:

```
### 1. Notify start
bash ~/Documents/scripts/tg.sh "✍️ Agent name — starting: [task]"

### [steps 2–N: actual work]

### Last step. Notify completion
bash ~/Documents/scripts/tg.sh "✅ Agent name — done: [outcome]"
```

The format matters less than the commitment: every workflow, without exception, gets both messages.

## How to Start

Pick one automation you're currently running — a daily report, a scheduled sync, a recurring job. Add the two Telegram lines. Run it for a week.

Within a few days, you'll develop the habit of noticing the messages. Within a week, you'll probably catch something that would have been a silent failure.

After that, you won't build another automation without them.

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/orchestration" style="text-decoration: none; color: #0366d6;">← Previous: Orchestration is the new programming</a>
  </div>
  <div>
    <a href="/" style="text-decoration: none; color: #0366d6;">Home</a>
  </div>
</nav>
