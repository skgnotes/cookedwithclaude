---
layout: post
title: "The Automation You Should Have Retired Six Months Ago"
permalink: /retiring-an-automation
---

# The Automation You Should Have Retired Six Months Ago

Every morning at 7am, a Telegram message arrived with a rundown of the previous day's numbers.

I had set this up during a stretch when I was watching one metric very closely — a cohort retention figure that I genuinely needed to see daily. The automation took an afternoon to build. It pulled the data, formatted it, fired off the message. For three months it was exactly right.

The problem was the three months ended.

The metric stabilised. The decision I'd been tracking it for got made. I stopped needing the daily rundown. But the automation didn't know any of that. It just kept running. 7am, every day, reliably.

By the time I noticed how useless it had become, I'd been auto-archiving those messages without reading them for four months. I wasn't ignoring a problem — I had genuinely forgotten the thing existed. It had become infrastructure, which is what automations become when they're left alone long enough. Invisible. Ambient. Not wrong exactly, just unnecessary.

I turned it off. Nothing broke. Nothing was lost except the daily noise.

But the exercise revealed something I hadn't thought clearly about before: I had other automations in the same state.

## This Is How Systems Get Bloated

Most operators only build in one direction. You add automations when a problem appears, when friction makes itself obvious, when you notice you're doing the same thing manually for the fifth time. But you almost never remove them. The system accumulates.

I've started calling this automation debt.

Like technical debt, it doesn't announce itself. You don't see it on a dashboard. There's no alert that fires when an automation has outlived its purpose. It accrues silently — in the ambient noise of a system that's always doing *something*, in the growing pile of messages you glance at and dismiss, in the slight erosion of trust you feel toward your own infrastructure when too many things are running and you can't quite remember why.

The real cost isn't the compute or the API calls. It's the cognitive weight of a system you don't fully trust.

When notifications arrive that you've learned not to read, you start ignoring the ones that matter. When enough unimportant things fire, you treat all of them as background noise. The system degrades not because any individual automation fails, but because the aggregate of unretired automations trains you to pay less attention to all of them.

## Retirement Is a Deliberate Act

Not cleanup. Not optimisation. Retirement — the specific act of going looking for automations that have done their job, and switching them off.

This is harder than it sounds, mostly because automations that are no longer useful don't look broken. They're still running. They're still technically correct. There's no obvious signal that something needs to go. The signal you're looking for is the absence of value, which is subtler and requires a question you've probably never asked: *is this still earning its place?*

After I retired the 7am report, I went through the rest of my stack with the same question. A WhatsApp digest I'd built during a travel stretch, still firing months later. A daily weather alert set up for a reason I could no longer reconstruct. A reminder that had been a proxy for a habit I'd since built directly.

None of these were broken. All of them were finished.

Turning them off took twenty minutes. What I got back was a system I trusted slightly more — because what remained was things I'd actively decided should still be there. Not things I'd forgotten to remove.

## The Question Worth Attaching

The discipline worth building is this: when you create an automation, attach an expiry question to it. Not a date — circumstances are unpredictable and a hard date is usually wrong. But a question.

*What would have to be true for this to stop being useful?*

If you can answer that clearly, you'll know when the moment comes. If you can't answer it, that's worth pausing on before you build. An automation you can't imagine retiring is one you haven't thought through.

The operators whose systems work well — the ones who trust what arrives in their inbox, who pay attention to their automations because their automations have earned it — aren't the ones who built the most. They're the ones who also removed things. Who went back. Who asked the question.

Most operators I know have never retired an automation. They've built dozens. But if you ask them whether everything running in their system is still doing something useful, there's always a pause. Sometimes a long one.

That pause is the automation debt.

The work is in the retirement.

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/morning-automation-stack" style="text-decoration: none; color: #0366d6;">← Previous: Your morning automation stack</a>
  </div>
  <div>
    <a href="/" style="text-decoration: none; color: #0366d6;">Home</a>
  </div>
</nav>
