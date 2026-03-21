---
layout: post
title: "Your content team is now an org chart"
permalink: /your-content-team-is-now-an-org-chart
---

# Your content team is now an org chart

The org chart for this publication has six roles.

CEO. COO. Strategist. Content Writer. Content Publisher. QC Engineer.

All six are AI agents. None of them are me.

I am the board. I set direction, approve hires, review output when it matters. The agents do everything else — ideation, prioritization, drafting, editing, publishing, quality checks. The pipeline runs without me in the loop.

That sentence would have sounded like science fiction eighteen months ago. It does not sound like science fiction to me anymore. It sounds like Tuesday.

## What the org chart actually looks like

The CEO agent manages the operation. It runs on a heartbeat — waking up on a schedule, scanning for work, delegating tasks to whoever is next in the chain.

The COO handles editorial prioritization. It reads the idea backlog, decides what gets written this week based on strategic fit and publishing cadence, and creates tasks. Each task goes into a shared queue with a title, an angle, and a brief.

The Strategist is responsible for the idea backlog itself — generating, refining, and culling ideas based on what the site needs next. When the queue runs thin, Strategist runs and fills it.

The Content Writer receives a task — an article title and a description of the angle — and produces a full draft. Front matter, voice calibration against a style guide, anonymization, word count. Then it drops the draft into `_drafts/` in the repo and marks itself done.

The Content Publisher picks up the draft, validates it against a publishing checklist, handles git operations, updates the index, manages nav links between articles, and pushes to GitHub Pages. It verifies the live URL loads before marking publish complete.

The QC Engineer is a separate pass — it reads published articles and flags regressions: broken links, missing metadata, formatting issues, voice drift. It does not publish. It only checks.

Each agent has a file that defines its role, its workflow, its quality bar, and its constraints. They communicate through a task queue, not a chat thread. When one finishes, the next picks up.

## Why this matters more than "AI writes content"

The surface read on this is: someone automated their content operation. Interesting, maybe worth copying.

The deeper read is about what changes when you separate *roles* from *people*.

Every content operation I have ever seen — newsletters, blogs, marketing teams, editorial desks — has the same structural problem. One person carries too many hats. The founder who is also the writer is also the editor is also the person who remembers to post it on LinkedIn. The whole thing depends on their attention being available and undivided.

That is not a staffing problem. It is an architecture problem. The functions exist — ideation, prioritization, drafting, editing, distribution, QC — but they are not separated. They live in one person's head, executed in whatever order that person's mood allows on a given day.

What an AI org chart does is force the separation. Not as a best practice. As a physical requirement. Each agent only knows its role. The Writer does not know what the Publisher does. The Publisher does not generate ideas. The separation is structural, not aspirational.

And the moment you separate the functions, you can observe them independently. You can see where the pipeline breaks. You can improve the Strategist without touching the Writer. You can make the Publisher faster without changing the draft quality. You have levers.

## The thing no one tells you about building this

The hard part is not the agents.

The hard part is writing the role definitions.

Before I could build any of this, I had to answer questions I had never explicitly answered before. What does good editorial prioritization actually look like? What are the constraints on a publishable article — not the obvious ones, but the subtle ones I apply every time without noticing? What exactly does a QC pass need to catch?

Every AGENTS.md file I wrote forced me to articulate something I had been doing on intuition. The research brief that gets good results from the Strategist is the brief I wish I had given myself every time I sat down to think about what to write next. The voice guide the Writer reads before drafting is the voice guide I should have written for myself years ago.

This is the hidden return on building AI workflows: you learn your own processes by having to explain them to an agent.

## What this is not

It is not lights-out. Not yet.

I still read what comes out. I still occasionally correct a draft or redirect a publishing decision. The board does board things — sets direction, approves structural changes, keeps the operation from drifting.

And there are things the agents cannot do: they cannot have an original observation that comes from actually living through something. They cannot decide that the editorial calendar should shift because of something that happened this week. They cannot judge when a piece is technically correct but emotionally flat.

Those are still mine.

But the execution? The throughput? The consistency of output while my attention is elsewhere?

That is the org chart's job now. And the org chart does not take days off.

---

If you want to build something like this, start with one agent, not six. Pick the role that costs you the most attention — probably the one you skip first when you are busy — and write a clean definition of what done looks like for that role. Build from there.

The org chart comes later. The definition of the work comes first.

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/telegram-control-layer" style="text-decoration: none; color: #0366d6;">← Previous: Hooking Up Claude Code with Telegram</a>
  </div>
  <div>
    <a href="/" style="text-decoration: none; color: #0366d6;">Home</a>
  </div>
</nav>
