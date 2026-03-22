---
layout: post
title: "My Day with Claude Code — March 20, 2026"
permalink: /claude-code-days-march-20
---

# My Day with Claude Code — March 20, 2026

Some days have a shape to them. Yesterday had the shape of a wall — beautiful, interesting, occasionally frustrating, and ultimately educational. Also: a lot got done on either side of it.

The main project was something I'd been genuinely excited about: a voice AI agent for a client that handles inbound calls from delivery agents. The idea is simple and the need is real — a delivery person is standing outside an unfamiliar building at 8pm, trying to reach the customer, and instead of a missed call and a failed delivery, they call a number, the AI picks up, and gives them the exact address and directions in natural language. The technical stack was already live: Vapi for voice orchestration, Deepgram for speech recognition, GPT-4o doing the reasoning, Azure TTS for the voice. Clean, solid, working.

The only thing missing was a real Indian phone number. And that, it turned out, was the wall.

Every virtual number provider I went to — Twilio, Vonage, Exotel, Telnyx — requires TRAI KYC before they'll issue an Indian number. Not a simplified form, not a quick ID check. Full KYC. And there's no self-serve path. No sandbox environment that lets you test with a real number. Telnyx requires a minimum 12-month commitment just to get an Indian number at all. It's a regulatory reality, not anyone's fault, but it's a genuine blocker when you've built the AI layer and it's sitting there, working, waiting for a phone to ring.

I sent a KYC initiation email to Exotel and documented the full project state — architecture, what's built, what's blocked, what the path forward looks like. The MVP exists. It just needs a number to live on. Sometimes the last five percent is the hardest five percent.

While that email was in flight, I turned to something quieter but equally important: figuring out why the health check automation had gone silent.

The daily health check is supposed to run every morning and send a Telegram report — all systems green, or not. For the past few days, nothing. No errors either. Just silence. When an automation goes quiet without any noise, the instinct is to assume something broke in the skill logic. The actual culprit was more elemental: macOS LaunchAgents inherit a stripped PATH when they run. Homebrew binaries — tmux, claude, all the tools I rely on — simply aren't visible to the script unless you explicitly export the PATH at the top. One line added to the script. The failure had been logging to an error file the entire time. It was there the whole time, waiting to be read.

The lesson that keeps coming up: when an automation goes quiet, check the error logs before assuming the skill failed. The system almost always tells you what's wrong. You just have to ask.

After the fix, I ran the health check directly to confirm — and took the opportunity to expand it. It had been checking 9 things. I pushed it to 14, including fixing the Shopify Partners check, which had been hitting the root URL. Turns out the root URL redirects to a marketing page regardless of whether you're logged in. The right URL is the organizations path. Both runs: 14 out of 14 passing cleanly.

Then something that shifted how I think about a piece of infrastructure I'd been treating as custom work: I learned that `/remote-control` is a native Claude Code command. I'd been planning to build it as a skill file. It already exists, ships with the tool, and creates an interactive session accessible from the Claude mobile app and a shareable web URL. The mobile app connects automatically to the tmux-hosted session. What I did need to work out was the injection pattern — to send a slash command into a running tmux session, you need three separate send-keys calls: the command text, then Enter for autocomplete, then Enter again to execute, with a sleep between each. Small thing. Took a while to land on.

The session ended with something that felt genuinely significant — building and running a new skill that logs into the Income Tax portal, navigates to e-Proceedings, downloads the latest notice PDF for a given PAN, and forwards it to the CA on WhatsApp with a brief summary.

I ran it live for two entities. Both notices pulled. Both PDFs named cleanly. Both forwarded with context in the same session.

The reason this mattered beyond the operational value: the CA who handles tax matters for several entities I'm involved with has been exploring AI enablement for their firm. The notice-check run was partly a demonstration. There's a difference between describing what AI can do and watching it log in, pull a notice, and forward it on WhatsApp while you're sitting in the room. That difference — between abstract and witnessed — is where adoption actually happens.

Some days you build things. Some days you fix things. Some days you clear a path for something that'll land later. Yesterday was all three.

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/claude-code-days-march-21" style="text-decoration: none; color: #0366d6;">Next: My Day with Claude Code — March 21 →</a>
  </div>
  <div>
    <a href="/claude-code-days-march-19" style="text-decoration: none; color: #0366d6;">← Previous: My Day with Claude Code — March 19</a>
  </div>
  <div>
    <a href="/claude-code-days" style="text-decoration: none; color: #0366d6;">← My Day with Claude Code (series)</a>
  </div>
  <div>
    <a href="/" style="text-decoration: none; color: #0366d6;">Home</a>
  </div>
</nav>
