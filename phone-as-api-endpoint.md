---
layout: post
title: "Your phone is now an API endpoint"
permalink: /phone-as-api-endpoint
---

# Your phone is now an API endpoint

My AI assistant read my phone's SMS inbox this morning without me touching it.

Not a notification. Not an integration through some app. My AI — running on my laptop, connected to my phone over WiFi — queried the SMS database directly, summarised what was there, and reported back in plain text.

I hadn't opened the Messages app. I hadn't looked at my phone at all.

This is not hard to set up.

## How it works

Android exposes its internal data — SMS messages, call logs, contacts — through a system called the content provider. Normally this is used by apps running on the phone itself. But Android also supports ADB, a debugging protocol that lets a connected computer send commands to the phone over USB or WiFi.

Once your phone is paired to your computer over WiFi via ADB, you can query its content providers from a terminal.

```
adb shell "content query --uri content://sms/inbox \
  --projection address,body,date --sort 'date DESC'"
```

That command returns your SMS inbox — every message, with sender, body, and timestamp — as structured text that an AI can read and reason about.

## What this enables

Reading the inbox is the obvious use. The more useful capability is targeted extraction.

I run a secondary number for signups and third-party services. Verification codes arrive on that number constantly. With ADB WiFi set up, Claude Code can retrieve any OTP autonomously — filter for the relevant sender, extract the code, use it — without me switching apps or picking up the phone.

Any signup or verification flow that used to require me to interrupt myself to check a code can now be handled entirely by the AI.

The phone stops being a device I have to look at. For that category of task, it becomes a data source the AI reads on my behalf.

## The setup

Three things required:

**An Android phone on the same WiFi network as your computer.** The phone does not need to be rooted. Standard Android works.

**ADB paired over WiFi.** Enable developer options on the phone — tap Build Number seven times in Settings — then enable Wireless Debugging. Pair using the code shown on screen. Once paired, ADB connects automatically whenever both devices are on the same network.

**A query pattern.** The content provider returns raw rows. A small script that extracts the field you need — the OTP code, a specific sender, a date range — turns the raw output into something useful.

## What surprised me

I expected this to feel fragile. It doesn't.

Once the pairing is done, querying the phone is indistinguishable from querying any other data source. The phone is just another endpoint. The SMS inbox is just another table.

The category of interruption that disappeared — "check your phone for the code" — is small per instance. Across a week of signups, verifications, and two-factor flows, it adds up. More than the time: it is the switching cost, the picking-up, the putting-down, the return to whatever you were doing.

Removing a category of interruption is not the same as saving the sum of its instances. It is cleaner than that.

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/automate-the-ui" style="text-decoration: none; color: #0366d6;">Next: When the API says no, automate the UI →</a>
  </div>
  <div>
    <a href="/personal-os-status-page" style="text-decoration: none; color: #0366d6;">← Previous: Your personal OS needs a status page</a>
  </div>
  <div>
    <a href="/" style="text-decoration: none; color: #0366d6;">Home</a>
  </div>
</nav>
