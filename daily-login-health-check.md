---
layout: post
title: "The daily login health check"
permalink: /daily-login-health-check
---

# The daily login health check

Every morning, before I've done anything, a message arrives on my phone.

It lists every integration that my automations depend on — the calendar connection, the email pipeline, the Telegram bot, the browser session for a tool I use regularly — and next to each one, a status. Working or not working. One line per integration.

Thirty seconds to read. I know the state of the whole system before I've opened a laptop.

I built this because I got tired of finding out the hard way.

## The failure mode it prevents

Integrations drift. Tokens expire. Sessions time out. An update rolls out to a third-party service and the authentication flow changes. You log in somewhere new and the existing session on the automation machine gets invalidated. A refresh token hits its ninety-day limit. A browser profile gets reset.

None of this announces itself. The integration just stops working, silently, and you find out when you needed it.

The classic version: you have an automation that pulls data from a service every morning. It's been running for months. One Tuesday, the token expires overnight. The automation runs, gets a 401, fails silently, produces no output. You don't notice because you stopped looking — you trust it. Three days later, something downstream is wrong, you trace it back, and find three days of missing data.

The time cost isn't just fixing the token. It's the downstream investigation. It's the decisions you made on bad data. It's the trust you lost in the system.

## What the health check does

The health check runs every morning before anything else. For each integration it cares about, it does the simplest possible test: can it actually do the thing?

Not "is the token present." That's a file check. The token could be present and expired.

Not "is the service responding." That's a ping. The service could be up and your credentials could be invalid.

The right test is: make the actual call, get the actual response, confirm the expected output. For a calendar integration, pull tomorrow's events. For an email connection, list the last message. For a Telegram bot, send a test command and confirm the reply arrives. For a browser session, navigate to the authenticated page and confirm you land on it logged in, not on the login screen.

If any of these fail, the morning message says so. By name. By what failed. Before I've started anything.

## The specific integrations worth checking

Not every tool needs to be in the health check. The candidates are the ones where a failure would be non-obvious or consequential.

A file on your local disk doesn't need a health check. If it's missing, you'll find out the moment you try to use it and you can fix it in thirty seconds.

An authentication token to a third-party API does. Those expire on their own schedule, often with no warning, and the failure can be silent and downstream.

Browser sessions are the ones most people overlook. They feel solid — you can see the browser, you know you're logged in. But the session the automation uses is a profile you don't touch day-to-day. It's the one running in a background context, with cookies that last as long as the service decides they last. When it expires, Playwright gets redirected to a login page, the expected element isn't there, the automation throws an error you don't see, and the task doesn't happen.

The places worth checking:
- OAuth tokens for calendar and email (they have explicit expiry dates — check while you still have days, not hours)
- Browser sessions for any service you automate with Playwright
- Bot connections (the Telegram bot, the webhook, whatever is listening for commands)
- API keys for any service that rotates them or has usage-based limits

## What to do when something fails

The health check catches the failure when it's a potential problem, not when it's an actual one.

That's the shift. You're not debugging a broken automation. You're doing routine maintenance on a working system. The emotional register is completely different. Fix it now, everything runs tomorrow. Fix it after it breaks, and you're also dealing with consequences.

For most failures, the fix is fast. Re-authenticate. Copy the new token. Log back into the browser profile. These are five-minute tasks when you're doing them proactively. They're twenty-minute tasks plus a debugging session when you're doing them reactively while something is broken.

The health check makes them proactive by default.

## The thing it does to your relationship with the system

There's a version of this that's about catching failures. That's the obvious value.

But the less obvious value is what happens to how you carry the system.

Every integration you depend on lives somewhere in your awareness. Lightly, in the background. You don't think about it consciously, but you're holding the question: is that still working? You trust it, mostly. But trust-mostly isn't the same as know.

When a system checks itself every morning and tells you the result, you stop holding that question. It gets answered daily, automatically. The background hum of vague concern about whether things are working — that goes quiet.

It's hard to describe until you've experienced it. The anxiety isn't loud. You only notice it when it stops.

## How to start

Start with the integration that has failed the most unpredictably. Not the most important one — the most unpredictable one. That's where you'll get the most immediate value, and it'll tell you how to structure the rest.

Write the simplest test: make the real call, check the real output, report pass or fail. Wire it into whatever morning routine you already have. If you get a morning message of any kind — a brief, a digest, a summary — add the health check output to it. Don't build a separate system. Attach it to something you already read.

Once you've done it for one integration, the pattern is clear. Adding the next one takes ten minutes. Within a week you can have the whole stack checked every morning before you've made a single decision.

The goal isn't to build a monitoring system. It's to wake up already knowing.

<nav style="margin-top: 48px; padding-top: 24px; border-top: 1px solid #eee; font-size: 14px;">
  <div>
    <a href="/personal-os-status-page">Next: Your personal OS needs a status page →</a>
  </div>
  <div>
    <a href="/one-browser-for-the-ai">← Previous: One browser for the AI</a>
  </div>
  <div style="margin-top: 16px;">
    <a href="/">↑ Home</a>
  </div>
</nav>
