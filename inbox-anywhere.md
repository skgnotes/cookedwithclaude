---
layout: post
title: "Inbox Anywhere"
permalink: /inbox-anywhere
---

# Inbox Anywhere

The thought arrives when you are away from your desk. You are walking, driving, mid-conversation.

So you do what most people do. You write it in WhatsApp, or the notes app, or a quick reminder — somewhere accessible — with the intention of moving it later. Except later means opening your documentation system, finding the right page, and manually transferring it across. That rarely happens cleanly. Sometimes it does not happen at all.

Or you try to capture it directly. You find the app on your phone, open it, navigate to the right section, and you type it into that.

Either way, too much friction. Too many hoops.

## What I set up

A Telegram bot that writes directly to my documentation system.

I text it a thought, a task, an idea — and it lands in the right place, timestamped, without me doing anything else. Like texting an EA who has it neatly organised and filed in my system. One message. Done. By the time I am back at my desk it is already waiting, in the right section, ready to be processed.

## The command structure

I have it set up with three commands — note, action, and idea — followed by whatever I want to capture. These are the keywords that work for me. You can set yours up with whatever makes sense for how you think and work.

Everything lands in a single inbox file. But the file is organized into sections: notes in the notes section, tasks in the actions section, ideas in the idea bank. The command you use determines where in the file it sits. When you open your inbox at your desk, its already sorted. You just process it.

Different commands, different sections — all from the same place. Lesser apps on my phone, not having to think which app for which, and nothing falls through the cracks.

I use Obsidian for most of this, with Notion as a secondary destination for some captures. The bot can write to both.

## What is actually happening

A small script runs quietly in the background on my computer. It listens to my Telegram bot. When I send it a message, it parses the command, identifies the destination, and appends the text to an Inbox section of the file I want it to be in. I got it set up end to end using Claude Code — including the testing to confirm it was working correctly.

## Why Telegram specifically

Its already on my phone. The bot appears in my chat list like any other contact. No new app, no new habit to build — just a different recipient for a message I already know how to send.

Systems fail when they ask too much of you. It should just work.

## You can have this too

If you find this useful and want it for yourself — its fairly easy and straightforward to get done. Claude Code can do it for you. You will need a Telegram bot — and that too, Claude Code will set up for you. You just need to ask it to do it for you.

## Ubiquitous

There is a word I first came across in a Shakespeare class in 12th grade — ubiquitous. Here and there and everywhere. Omnipresent.

That is what your capture system becomes after this is set up. Ubiquitous. It is on your phone, it is in your pocket, it is wherever you are. The thought arrives — anywhere, anytime — and there is a place for it, instantly, without effort. You stop losing things not because you got more disciplined, but because the system stopped asking you to be.

This alone should feel close to magical.

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/setting-up-obsidian" style="text-decoration: none; color: #0366d6;">Next: Setting up Obsidian and why →</a>
  </div>
  <div>
    <a href="/using-claude-as-a-thinking-partner" style="text-decoration: none; color: #0366d6;">← Previous: Using Claude as a Thinking Partner</a>
  </div>
  <div>
    <a href="/" style="text-decoration: none; color: #0366d6;">Home</a>
  </div>
</nav>
