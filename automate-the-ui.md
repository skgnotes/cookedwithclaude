---
layout: post
title: "When the API says no, automate the UI"
permalink: /automate-the-ui
---

# When the API says no, automate the UI

The command ran. No error. No output. Nothing changed.

I was trying to delete SMS messages programmatically — the obvious approach, a single command to clear the inbox. The command accepted the request, returned nothing, and the messages sat exactly where they were.

What looked like a bug was a permission model.

## What the platform was protecting

Android 4.4 introduced a rule: only the default SMS app can write to the SMS database. Third-party callers — including the ADB debugging interface — can read messages fine. They cannot delete them. The system silently ignores the write request. No error. No acknowledgment. Just nothing.

The right reaction to this is not to find a way around the permission. The permission exists for good reasons — it prevents malicious apps from silently wiping your messages. The right reaction is to go through the authorised channel.

The authorised channel, in this case, was the Messages app itself.

## Automating the authorised path

The Messages app can delete messages. It has the permission. So instead of calling the database directly, I automated the app.

Android's UI testing framework lets you dump the current screen state as an XML tree, read which elements are visible and where, and send input events — taps, long presses, swipes — to specific coordinates. Each step is a shell command over ADB.

The sequence:
1. Wake the screen and open the Messages app
2. Dump the UI tree to get the current position of the target conversation
3. Long press (2500ms) on the conversation — this enters selection mode
4. Tap the delete icon that appears in the toolbar
5. Confirm

The result is identical to doing it manually. Because it is doing it manually — just without a human hand.

## Why this pattern matters beyond SMS

The specific use case is not the point.

Every locked system has an authorised interface. A SaaS tool without an API can be automated through its web UI. A desktop application with no scripting support can be driven through its windows. A mobile app that exposes no external access points can be controlled through its own screens.

When the direct path is blocked — by permissions, by authentication, by a platform design decision — the UI path is almost always open. And automating the UI is using the system the way the system was designed to be used.

This is not a workaround in the pejorative sense. The permission model said: go through the app. Automating the app is going through the app.

## The honest tradeoff

UI automation is fragile in ways API calls are not.

A layout change breaks the coordinate logic. An app update moves a button. A new confirmation dialog appears. You are coupling your automation to a visual representation that the platform can change without notice.

The right mental model: UI automation is a fallback, not a first choice. Reach for it when the direct path is unavailable — and know that you are trading brittleness for capability.

Sometimes that trade is worth making.

The test I use: if I had to do this manually every day, would the friction matter? If yes, the fragility of the automation is worth tolerating. Build it, note the dependency, and accept that it might need occasional repair.

That is a better outcome than doing it by hand indefinitely.

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/two-minute-tasks" style="text-decoration: none; color: #0366d6;">Next: The two-minute task you should automate anyway →</a>
  </div>
  <div>
    <a href="/phone-as-api-endpoint" style="text-decoration: none; color: #0366d6;">← Previous: Your phone is now an API endpoint</a>
  </div>
  <div>
    <a href="/" style="text-decoration: none; color: #0366d6;">Home</a>
  </div>
</nav>
