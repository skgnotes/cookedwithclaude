---
layout: post
title: "My Day with Claude Code — March 18, 2026"
permalink: /claude-code-days-march-18
---

# My Day with Claude Code — March 18, 2026

Some days you don't plan to be productive. You just start doing one thing, and then the momentum takes over.

March 18 started with the kind of unglamorous but necessary work that separates a system that actually functions from one that just looks organised on the surface. My quick actions list had become a disaster — a flat pile of 35-something items with no structure, no priority signal, no way to know what was urgent versus what I'd been meaning to do for three months. So Claude and I tore it down and rebuilt it from scratch. Six sections: Time Critical, Entrusted, Active Projects, Exploratory, Things To Do, Dues Follow Up. Every item triaged and slotted. Then we updated the facts file with some bank details I'd been meaning to capture, and turned to lifemap.md — a Dubai trip that had been sitting in the plan got officially cancelled, subscription reminders were set, and Dad's next cardiology check got noted for mid-year. When it was done, the system felt clean in a way it hadn't in weeks. That feeling — of things being where they're supposed to be — is rarer than it should be.

From there, somehow, we got the home printer working the way I'd always wanted. It sounds trivial. It isn't. The workflow is now: markdown file → HTML → Chrome headless → PDF → lp command → paper in the printer tray. Hit a command, your to-do list comes out of the printer. Documented it in ops.md so I don't have to reconstruct it next time. The fact that this took maybe twenty minutes and now it just works is the kind of thing that makes you wonder why you didn't do it years ago.

The bulk of the day, though, belonged to a friend's project. She has an ethnic wear business — close to 47,000 followers on Instagram — and wanted to move it into a proper online store. We'd been building out a Shopify store for her over a few sessions, and today was about finishing the infrastructure: removing a duplicate hero banner that had mysteriously appeared, writing and publishing the About page, Contact page, and policy pages from scratch, and verifying every footer link. Then I drafted a briefing for her family contact — the person coordinating from their side — laying out exactly what's needed to go live: product photos, descriptions, five items to start. Professional but plain. Here's what we built, here's what we need from you.

That project triggered something else. I have a nephew who's learning development and looking for real work to sink his teeth into. It struck me that this Shopify store — already half-built, real client, live brief — was exactly the kind of hands-on engagement that teaches more than any tutorial. So I reached out. Explained what was built, why it mattered, what the opportunity looked like if he wanted to take it on. A live paid engagement to learn Claude Code on actual client work. The message was warm, not transactional. A door being opened, not a task being assigned.

Before that could go anywhere, I needed to get the payment picture right. The friend's family contact had questions about how Razorpay settlements worked in the context of a Shopify store. So I went and found out properly — Shopify Sidekick, Razorpay's own documentation, Razorpay Assist, all three. Confirmed: T+2 for domestic payments, T+7 for international, Instant Settlements available on request but off by default. Compiled it into a clean knowledge note and shared it with both the client contact and the nephew. Research as work product. That feels right.

On the automation side, the day brought a meaningful addition to the Telegram bot. I added an `action` command — now if I send anything to the bot prefixed with "action", it gets appended directly to the Inbox section of quick actions.md as an unchecked task. Capture from anywhere, land in the right place. Testing it involved some fiddling with Telegram Web via Playwright — learned the hard way that you have to select from the country code dropdown first, then use pressSequentially for the number. Fill() picks up the wrong country code entirely (Iran instead of India — not ideal). Also built a health check for the bot's core commands and wired it into the 8am daily-ops run. The check tests the commands end-to-end using the same code paths the real bot uses. Programmatic confidence.

Eight articles went live on cookedwithclaude.com across the day. I don't even fully know how that happened — some were queued, some were finishing existing drafts, and the momentum just carried them through. Also password-gated the personal resume site using a JavaScript overlay with a SHA-256-hashed password, a robots.txt block, and noindex meta. Private without paying for auth infrastructure. Clean solution.

Personal errands ran in parallel the way they always do. A mobile recharge done. A pharmacy order placed — medications, expected delivery in a few days. First real run of a Swiggy Instamart automation I'd built — it hit a snag when the OTP step failed mid-flow and I had to enter it manually. Fixed the polling logic afterward. The interval had been too aggressive and conflicted with the Telegram listener.

And then, because it was that kind of day, two family messages. A WhatsApp to Mom in Malayalam, updating her on a settlement call happening over the weekend. A WhatsApp to my sister, looping her in on the nephew outreach, with a link to the blog post.

It was the kind of day where real things happened — systems got cleaner, a client's store moved forward, someone got an opportunity, automations got smarter — and yet it never felt like grinding. More like the day had direction and you were just following it where it wanted to go.

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/claude-code-days-march-19" style="text-decoration: none; color: #0366d6;">Next: My Day with Claude Code — March 19 →</a>
  </div>
  <div>
    <a href="/claude-code-days" style="text-decoration: none; color: #0366d6;">← My Day with Claude Code (series)</a>
  </div>
  <div>
    <a href="/" style="text-decoration: none; color: #0366d6;">Home</a>
  </div>
</nav>
