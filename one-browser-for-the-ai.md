---
layout: post
title: "One browser for the AI"
permalink: /one-browser-for-the-ai
---

# One browser for the AI

At some point I made a decision that I didn't recognise as a decision at the time.

I stopped using Chrome for my personal browsing. I handed it over — entirely, deliberately — to Claude Code. My personal browser became Edge. Chrome became the AI's browser.

It felt minor when I did it. It turned out to be one of the more consequential setup choices I've made.

## What was breaking

When I first started using Playwright for browser automation, the sessions were unreliable. Not always. Not in an obvious pattern. But often enough that I'd start an automation task and spend twenty minutes diagnosing why it wasn't working, only to find that Chrome had been open, or a tab had something loaded, or a login session had expired because I'd used Chrome personally and cleared something.

The problem was that I was treating Chrome as a shared resource. My automation scripts and my personal browsing were both writing to the same browser profile, fighting over the same state, creating interference in ways that were hard to trace and harder to prevent.

The symptoms were maddening. Something would work fine one day and fail the next. I'd make no changes and get different results. I'd spend more time debugging the environment than doing the work.

## The separation that fixed it

The solution wasn't technical. It was architectural.

I moved all personal browsing to Edge. I configured Chrome with a dedicated profile for automation — a profile that nothing else touches. Claude Code's Playwright automation always uses Chrome. I never open Chrome personally. Edge is untouched by any automation.

Two browsers. Clean lines. No shared state.

Since making that change, I can count on one hand the number of times automation has failed because of a browser environment issue. Before the change, it happened regularly.

## Why this is a systems decision, not a preference

Most people treat browser choice as a preference — which one you like, which one is faster. That's a consumption decision.

This is different. It's a resource allocation decision.

When you run automation, you're running a process that depends on a browser being in a predictable state. It needs to know which profile is loaded. It needs to know which sessions are active. It needs to be able to open, navigate, interact, and close — without something else having modified the environment between runs.

If your automation browser is also your personal browser, you're introducing a variable that you can't control. Every time you browse personally, you're potentially changing the state that your automation depends on. You may clear cookies, log out of something, open a tab that interferes, update a setting.

The automation doesn't know any of this happened. It just fails.

Separating the two removes that variable completely. The automation browser exists in a known state, always. The personal browser is yours — use it however you like, no constraints, no risk of breaking anything.

## The compounding effect

There's a second-order benefit that I didn't anticipate.

When your automation environment is stable, you stop questioning it. When something breaks, you know immediately that the issue is in the automation logic — not in the environment. That changes how you debug. You're looking at the right things from the start.

More than that: you start trusting the system. And trust compounds. When you trust your tools, you're willing to build more on top of them. When you're not sure your tools are reliable, you hold back. The unreliability creates a kind of anxiety that limits how far you're willing to go.

Stable environment, more ambitious automations. That's the compounding effect.

## The practical setup

The decision has two parts: the rule and the infrastructure.

The rule is simple — one browser per purpose. Pick which is which and stick to it. The infrastructure is minor: set up a dedicated profile in the automation browser, make sure your automation tooling points to that profile, and never open the automation browser personally.

On a Mac, this is a few configuration lines. The friction of maintaining the separation is essentially zero once it's set up. You just use Edge for personal browsing. Chrome stays off. The automation runs in its own clean lane.

It costs nothing to maintain. It saves a class of debugging problems that would otherwise appear randomly, resist diagnosis, and eat time that should be going elsewhere.

## The broader principle

There's a version of this that applies beyond browsers.

Whenever automation and human activity share an environment, you get interference. Shared files, shared accounts, shared APIs — all of these create the same class of problem. Something changes for reasons that have nothing to do with the automation, and the automation breaks.

The general fix is the same: separate the environments. Give the automation its own resources. Keep the human and the machine out of each other's way.

The browser separation is just the most visible instance of this principle. Once you see it here, you see it everywhere.

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/daily-login-health-check" style="text-decoration: none; color: #0366d6;">Next: The daily login health check →</a>
  </div>
  <div>
    <a href="/the-system-that-checks-itself" style="text-decoration: none; color: #0366d6;">← Previous: The system that checks itself</a>
  </div>
  <div>
    <a href="/" style="text-decoration: none; color: #0366d6;">Home</a>
  </div>
</nav>
