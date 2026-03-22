---
layout: post
title: "My Day with Claude Code — March 21, 2026"
permalink: /claude-code-days-march-21
---

# My Day with Claude Code — March 21, 2026

Some days feel like you've lived three of them back to back. Yesterday was that day.

It started with housekeeping — the kind that doesn't feel glamorous but you know matters. The Cooked with Claude content system had grown messy over the past few weeks. The Idea Bank had become a dumping ground: backlog entries, book chapter candidates, published articles, discarded ideas, fresh captures — all jostling in one file. So Claude and I untangled it. We moved the level-structured backlog into its own Article Roadmap file, stripped the Idea Bank back to a pure running inbox, and shuffled the book chapter candidates and discarded ideas over to the roadmap where they belonged. Then we chased the knock-on effects — updated the CLAUDE.md for the Cooked project, fixed a broken voice guide path, cleaned up the /cooked skill file, and fixed the tg-listener marker text so it still knew where to write when ideas come in from Telegram. None of this was exciting. All of it needed to happen.

While we were in the Cooked codebase anyway, we updated the remote-control article on the live site — added `idea [text]` to the commands section, deployed, and verified it live using Playwright with a cache-busting query param to make sure we were actually looking at the new version and not a cached one. Small thing. Done.

Then we built something I'd been meaning to set up for a while: Notion MCP. I created a "Claude Code" integration in my Notion workspace, retrieved the API token, added the server to `~/.claude.json`, and granted it access to all 15 pages. By mid-morning, `/mcp` was showing it green — ✓ Connected. From there, we extended it: created a Capture Logs page in Notion, wired up tg-listener.js so every note/idea/action capture now dual-writes to Notion silently alongside the local markdown files. Notion failures don't break the local capture — the whole thing is designed so the Telegram bot keeps working regardless.

Somewhere in the middle of all this, I ran the /cigs skill. Classic Connect Cigarettes, Swiggy Instamart, ₹431 to the home address. The OTP part failed mid-flow — had to enter it manually, which is exactly the kind of thing that irritates me about automation that's almost working. So after the order went through, we went back into the skill and fixed it properly: the swiggy-otp-poll.py script had a `&timeout=3` parameter causing a 409 conflict with tg-listener, the polling interval was too aggressive, and the price in the documentation was wrong by ₹90. Fixed all three. Now it should just work next time.

Then we spent time on something I'd been putting off: the infrastructure layer for agents.

If you're going to deploy a team of AI agents that act in the world, they need to exist in the world — not just as processes on your laptop but as entities with actual presence. So we set that up. AgentMail inboxes — purpose-built email addresses designed for code to operate, not humans to read. A phone number for OTP handling. And critically, we re-paired the ADB wireless connection to my Android phone so that agents can read incoming SMS messages directly — specifically bank OTPs that arrive during purchases or account verifications. The setup sounds obscure but the implication is significant: an agent can now complete a payment flow end-to-end without needing me to relay a six-digit code.

That last point came in handy almost immediately. I ordered a Boldfit 2.2L gallon water bottle from Amazon.in — army green, ₹898, arriving Tuesday. Claude handled the entire flow: navigated to the product, added to cart, selected the card, and when the OTP arrived on my phone, read it off the SMS inbox via ADB and entered it into the checkout iframe automatically. Fully hands-free after login. The last SMS in the inbox at that point was a ₹1,061 charge at a local café from 6:42 PM — visible confirmation that the ADB connection was live and current. A water bottle, ordered without me lifting a finger. That's what the infrastructure layer makes possible.

The main event of the afternoon was the agent team.

We put a full publishing team to work on Cooked with Claude. A CEO agent that delegates. A COO that routes. Three content agents — Strategist, Writer, Publisher — each with STOP gates so they can't run without being explicitly tasked. It took several iterations to get right. There were frustrating runs where agents would act without being asked, or where a "default to action" bias buried deep in the CEO's core instructions kept overriding the delegation gate I'd added. I moved the delegation gate to the top of the primary instructions file so it would be the first thing the agent read. Rewrote the CEO's heartbeat logic — clean step-by-step, no ambiguity. Added a self-trigger: the CEO now checks its own git log on every heartbeat and creates a task for the COO automatically if nothing's been published in three hours and no pipeline is running.

Then I went to lunch with my parents.

And here's the thing. While I was sitting at the table — talking, eating, just being present — my phone kept buzzing. The Strategist had picked an article. The Writer had drafted it. The Publisher had deployed it. Each stage completing, each one pinging me on Telegram. Articles going live on a website I was nowhere near, driven entirely by a team of agents I'd spent the morning wiring up. By the time I got back, four articles had been published.

That's the most surreal thing that happened yesterday. Not any single technical trick. Just sitting across from my parents at lunch while a publishing team ran without me.

After getting back, we kept going. We built the selection logic — a dual-source system where the Strategist draws from the Article Roadmap for level structure and the Idea Bank Inbox for freshness, with a priority table that prefers Level 3, then 4–5, then 2, then 6+. Added mention-based wakeup to all three content agents so they trigger immediate COO routing on completion instead of waiting for the next polling interval. The pipeline dropped from ~20 minutes to ~11 minutes end-to-end.

We also hired a QC Engineer — a fourth content agent whose job is to check every article after the Publisher deploys it. Spacing, front matter, navigation style, link integrity. Appends its findings to a log. Commits fixes. Hands back to the COO. The first QC run on a live article came back clean. We also created a LinkedIn persona for one of the agents — full profile, headshot, headline — and sent its first connection request to a contact using CDP WebSocket automation to get around LinkedIn's shadow DOM limitations. The agent now has a real professional presence.

Then Claude flagged the site audit. I'd been so focused on the pipeline that I hadn't checked the site itself in days. Turned out index.md had all 47 articles running inline — single newlines instead of blank lines, which in Jekyll means they all render as one continuous paragraph. We fixed the formatting across all 47 entries, then found six articles still using a legacy navigation pattern. Converted all six to the current standard. The site is now consistent end-to-end for the first time.

Late in the day, we ran /insights — a usage report across all my Claude Code sessions from February 19 to March 21. **1,056 sessions. 239 hours. 26 commits. 89% satisfaction.** Uploaded the report to a public GitHub repo. The final pipeline run of the day — for an article called "Your content team is now an org chart" — was kicked off before I closed the laptop. Telegram would tell me when it was done.

What do you call a day like this? Sixteen things, some deeply technical, some mundane, some genuinely novel. A content system reorganization. An agent team that publishes. A LinkedIn persona. A water bottle. A cigarette order and its post-mortem. Notion integration. Site cleanup. ADB phone reads. Usage analytics.

What strikes me, sitting with it now, is how much of this was just... done. Not planned across a week. Not delegated to a team. Done in a single day, with one AI assistant and a decent amount of coffee — and some of it from my phone, while the agents pinged me on Telegram from the other room. There's something quietly extraordinary about that — and also something that makes me wonder what it'll feel like in six months when days like this are just normal.

I think they already almost are.

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/claude-code-days" style="text-decoration: none; color: #0366d6;">← My Day with Claude Code (series)</a>
  </div>
  <div>
    <a href="/" style="text-decoration: none; color: #0366d6;">Home</a>
  </div>
</nav>
