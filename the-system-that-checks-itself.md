---
layout: post
title: "The system that checks itself"
permalink: /the-system-that-checks-itself
---

# The system that checks itself

Every morning at 8am, a message arrives before I've looked at my phone.

It lists every automation I have running — the morning brief, the customer email pipeline, the bot that handles commands from my phone — and next to each one, whether it worked. Green ticks down the list. Takes three seconds to read.

And it does something to the rest of the day that's hard to explain until you've experienced it.

## The problem with silent automations

Most automations fail silently. They run in the background, you stop thinking about them, and then one day you notice something didn't happen. The report wasn't there. The reminder never arrived. The order didn't go through. You trace it back and find it had been broken for two weeks.

Silent failure is the default mode of any automation you don't actively monitor. You build it, you test it once, it works — and then you trust it. Which is fine, until it isn't.

The worse version is when you don't even realise it's broken. You've reorganised your expectations around the automation. It was doing something you used to do manually. When it stops, you don't notice the absence immediately. You just experience the downstream effect — a dropped ball, a missed moment — and it takes time to connect it back to the broken pipe.

## The system that confirms it's alive

The alternative is simple. Build something that tests itself and reports back.

For me, this is a small check that runs every morning alongside everything else. It sends a test command to each automation I depend on, waits for the expected response, and confirms the result. Not just that the automation is switched on — that it actually did the thing. If anything in the chain breaks, the morning report tells me before 9am, before I might have needed it.

I find out when the failure is hypothetical, not when it's costing me something.

The check itself is lightweight. For each automation: trigger it, confirm the result, report pass or fail. For an email pipeline, send a test and verify it arrived. For a scheduled report, confirm the file was created. For any system with a command interface, send a command and check the response. The point is to test the actual path — not whether the machine is running, but whether it's working.

## What it does to how you carry the system

This is the part that surprised me.

The peace of mind isn't just about catching failures. It's about what happens to your relationship with the system once you know it checks itself.

Every automation you build lives somewhere in your attention. Not consciously — you've stopped thinking about it. But it's still there, carried at a low level. The background question of: *is that still working?* You don't ask it. But you're holding it.

When a system tells you every day that it's working, you stop holding it. It drops out of your mental inventory entirely. And that compounds. One automation checking itself is useful. A stack of them — each one self-reporting, each one dropping out of the background — changes the texture of the day.

You're not just saving time on the tasks. You're also not spending attention on the quiet worry that things might have broken. Those are different benefits. The second one is harder to measure and more valuable than it sounds.

The goal isn't just to automate the work. It's to build a stack where you wake up and already know everything is functioning. Before you've made a single decision. Before you've needed anything.

The systems have already checked. They're ready.

<nav style="margin-top: 48px; padding-top: 24px; border-top: 1px solid #eee; font-size: 14px;">
  <div>
    <a href="/when-tools-talk">← Previous: When your tools talk to each other</a>
  </div>
  <div style="margin-top: 16px;">
    <a href="/">↑ Home</a>
  </div>
</nav>
