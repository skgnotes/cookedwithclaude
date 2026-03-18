---
layout: post
title: Your capture system should work from your phone
permalink: /capture-from-anywhere
---

# Your capture system should work from your phone

Most personal productivity systems are designed for the desk.

You set them up on your laptop. You review them on your laptop. The whole thing assumes you're sitting down, focused, with a keyboard in front of you. And for the moments when you're not — when something occurs to you in the car, or on a walk, or between meetings — you're supposed to remember it until you get back.

This is a flaw. Not a minor one.

**Where ideas actually happen**

The things I need to remember don't arrive on schedule. A follow-up I forgot surfaces while I'm having lunch. An action item from a call stays in my head for two hours after the call ends. Something I read triggers a thought about a project that has nothing to do with what I was reading.

None of this happens at my desk.

The standard workaround is to type it into your phone's notes app, then remember to move it to your actual system later. In practice, "later" is unreliable. Items sit in phone notes for days. Some never make it. The capture happened but the integration didn't.

**What frictionless looks like**

A while back, I set up a bot that I can message from anywhere. I send it `note <text>` and it drops the item into my inbox. No app switching. No remembering to transfer later. No friction between the thought and the system.

I recently added a second command: `action <text>`. Same mechanic, different destination. Actions go directly into my quick actions list — the page I review every morning to decide what the day looks like.

The technical implementation is about 20 lines of code. The change it made to how I work is disproportionate to those 20 lines.

**The transfer problem**

Every productivity system has a transfer problem. You capture something somewhere and then you have to move it somewhere else before it becomes actionable. Email to task manager. Voice memo to note. Phone photo to document.

Each transfer is friction. Each transfer is a moment where things can fall through.

The goal isn't to eliminate capturing. It's to collapse the distance between capture and the system you actually use. If the thing you captured goes directly into the list you review, there's no transfer. There's no "I'll add it properly later."

The item is in the system the moment you think of it.

**Why Telegram specifically**

I use a messaging app rather than a purpose-built capture app for a few reasons.

First, it's already open. I'm in Telegram multiple times a day. There's no switching cost, no app to find, no screen to unlock and navigate. I'm already there.

Second, it's on every device. Whatever I'm holding when the thought arrives, I can send it.

Third, it goes somewhere real. This isn't a second inbox I have to process separately. The bot writes directly to the files I use. When I open my task list, the things I sent from my phone are already there.

**The system works when you don't have to think about it**

The measure of a good capture system is how little you think about it.

A system that requires you to decide where to put something is already asking too much. In that moment of indecision, the thought fades, you choose the path of least resistance, or you pick the wrong place and lose it anyway.

A system that requires one command — `action follow up with the client about pricing` — is asking almost nothing. You type, you send, it's in the system. The decision-making happens later, when you're at your desk and reviewing, not at the moment of capture.

The desk is where you process. The phone is where you capture. Your system should work both places.

<nav>
  <div>
    <a href="/telegram-command-interface" style="text-decoration: none; color: #0366d6;">Next: A few commands that changed how I work →</a>
  </div>
  <div>
    <a href="/when-to-trust-the-ai" style="text-decoration: none; color: #0366d6;">← Previous: When to trust the AI, when to check the source</a>
  </div>
  <div>
    <a href="/" style="text-decoration: none; color: #0366d6;">Home</a>
  </div>
</nav>
