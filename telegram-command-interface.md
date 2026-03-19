---
layout: post
title: A few commands that changed how I work
permalink: /telegram-command-interface
---

# A few commands that changed how I work

There's a bot I message every day.

I don't think of it as a bot, exactly. I think of it as the front door to my system. When I want to capture something, I send it there. When I want to start a task, I send it there. When I have an idea for an article, I send it there.

It does one thing: it takes what I send and puts it in the right place.

**What it started as**

The original version was simple. You could send `new` to spin up a Claude Code session on my desktop, and send `close` to shut it down. Remote control, basically. Useful, but narrow.

Then I added `note`. Send `note <text>` and the text goes into my inbox in my main actions file. Timestamped. Formatted correctly. Already there when I open it.

Then `idea`. Ideas go directly into my idea bank for the blog.

Then `action`. Actions go into my quick actions list — the short list I review every morning.

Each command is a single addition. Each one took less than an hour to build. Together, they've changed something fundamental about how input gets into my system.

**Why commands rather than a form or an app**

There are apps for this. Notion has a mobile app. Obsidian has a mobile app. Most task managers have mobile apps.

The problem isn't the absence of mobile apps. The problem is that every app is its own context to switch into. Find the app. Open it. Navigate to the right place. Type. Save.

A message is faster than that. I'm already in a messaging app. I type the command and the text. I send. Done. No navigation, no context switch, no decision about where in the app to put it.

The command is the navigation.

**The friction that matters**

People talk about friction as if any friction is bad. That's not quite right. The friction that matters is the friction at the moment of capture — when the thought arrives and you have to decide what to do with it.

That moment is already fragile. You're usually doing something else. The thought is competing with whatever you were thinking before. If the next step requires three taps and a choice about which list to add it to, you've already lost attention to the task.

If the next step is type and send, you almost always complete it.

I've noticed that the items I capture via the bot are qualitatively different from items I capture via an app. The app captures are things I deliberately sat down to add. The bot captures are things I actually thought of in the moment — the follow-ups, the half-formed ideas, the things that would have evaporated otherwise.

**What happens on the other end**

The other half of this is what happens after you send.

The bot isn't just storing text in a message thread somewhere. It's writing to files I already use. When I send `action <text>`, the text appears in my quick actions list — the same file I open every morning. It's not in a separate inbox. It's not waiting to be processed into the right system. It's already there.

This matters because it closes the loop. There's no "I'll move this properly later." Later doesn't happen reliably. If the item needs to move from capture to system, there's a gap where things disappear.

The bot eliminates the gap.

**What you actually need to build this**

A Telegram bot takes about ten minutes to create. Add a polling script that listens for messages. Add a few command handlers that write to files. Run it as a background process that starts automatically.

The complexity is low. The surface area is small — one script, a handful of commands, files it writes to.

What takes longer is deciding what the commands should be. That's not a technical question. It's a question about how your system actually works — what you capture, where things need to go, what the review process looks like.

The bot just implements that. The thinking is yours.

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/inbox-is-not-where-things-get-done" style="text-decoration: none; color: #0366d6;">Next: The inbox is not where things get done →</a>
  </div>
  <div>
    <a href="/capture-from-anywhere" style="text-decoration: none; color: #0366d6;">← Previous: Your capture system should work from your phone</a>
  </div>
  <div>
    <a href="/" style="text-decoration: none; color: #0366d6;">Home</a>
  </div>
</nav>
