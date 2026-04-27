---
layout: post
title: "The AI Legal First Pass"
permalink: /ai-legal-first-pass
---

# The AI Legal First Pass

Before you pay a lawyer to read an NDA, read it yourself — with Claude.

Not instead of a lawyer. Not as legal advice. As the thing that happens before you decide whether a lawyer is even necessary, and if so, what you're actually asking them to look at.

Most founders get this backwards. They receive a contract, feel a vague unease, and either sign it without reading it or send it to a lawyer without knowing what to ask. The lawyer review costs money. The blind signature costs more.

There's a third option.

## What you get at the end

Ten minutes after you receive an NDA, you have:

- A plain-English summary of what you're agreeing to
- The clauses that carry real risk — flagged and explained
- A list of the things you would want to negotiate if you were going to
- Specific questions to ask a lawyer, if the doc warrants one

That's it. Not a legal opinion. A structured read.

## Why this is worth doing

Standard mutual NDAs — the kind a potential partner sends before a conversation — are usually low-risk. You know this instinctively, but you don't know it specifically. You don't know which clause is the weird one, or whether the definition of Confidential Information is so broad it covers your existing product roadmap.

Lawyers know this. But at hourly rates, asking a lawyer to look at every incoming NDA is expensive. So founders skip the step and sign. Which is mostly fine. Until it isn't.

The first pass changes the calculus. You're not replacing legal judgment. You're replacing the step where you hand off a document you haven't read to someone who charges you to read it for you.

## How to do it

**Paste the full document text** into Claude (Claude.ai or Claude Code). Formatting doesn't matter — Claude handles it. Then send this prompt:

---

*You are reviewing an NDA I received. I am the receiving party. Treat me as a founder who understands business but is not a lawyer.*

*Please produce the following:*

*1. Plain English summary — what am I agreeing to in 3–5 sentences?*
*2. Key risk areas — which clauses have the most potential to create problems for me or my company? For each one: quote the relevant text, explain the risk in plain English, and rate the severity (low / medium / high).*
*3. Unusual or non-standard clauses — anything that deviates from a typical mutual NDA between two companies exploring a partnership. Explain why it's unusual.*
*4. Negotiation opportunities — what would I reasonably push back on if I wanted to negotiate? For each point: what to ask for and why.*
*5. Lawyer trigger — should I pay a lawyer to review this, and if so, what specifically should I ask them to focus on?*

*Here is the NDA:*

[paste document text]

---

That's the whole prompt. Don't overthink the framing. Claude knows what an NDA is; you're just telling it whose chair you're sitting in.

## What the output looks like

To illustrate, here's what came out of a fictional NDA I used as a test case — a mutual confidentiality agreement between two companies exploring a potential distribution partnership.

The plain English summary was accurate and readable. The risk section flagged three clauses: an unusually long confidentiality period (five years, not the standard two), a definition of Confidential Information that explicitly included information shared orally without requiring written confirmation, and a non-solicitation clause buried in the boilerplate that applied to employees — not just customers.

The non-solicitation clause was the useful one. Most founders skim that kind of boilerplate. Claude pulled it out, quoted it, explained what it meant in practice, and rated it medium severity with a note that it could create friction if the partnership dissolved and both companies wanted to hire from the same talent pool.

That's the kind of thing you miss when you sign without reading and only realise later.

## What surprised me

I expected Claude to be good at summarising. I didn't expect it to be useful on the non-obvious stuff.

The oral disclosure clause is a good example. It's not a dramatic risk on its own — but it means that anything you say in a pitch meeting, before you've thought about what you're disclosing, is potentially covered. That's worth knowing going in.

The output also distinguished between what was unusual versus what was risky. Some non-standard clauses are just stylistic choices by whoever drafted the document. Others are deliberate. Claude made that distinction cleanly, which made it easier to know where to focus.

## One thing to keep in mind

This is pattern-matching at scale, not legal reasoning. Claude is good at identifying what clauses say. It is less reliable on the question of what they would mean in a specific legal dispute in a specific jurisdiction. For anything with material stakes — a large partnership, an acquisition pre-NDA, anything involving IP you care about — use a lawyer.

The point is not to avoid lawyers. The point is to stop arriving at lawyer conversations without having read the document first.

## Where to start

Your next NDA. When it lands, paste it in before you sign it. You will know more in ten minutes than most founders know when they sign.

If you do this enough times, you will also start to recognise the standard boilerplate — and notice quickly when something isn't standard.

That calibration is worth building. It costs nothing to start.

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/the-15-minute-invoice" style="text-decoration: none; color: #0366d6;">← Previous: The 15-Minute Invoice</a>
  </div>
  <div>
    <a href="/" style="text-decoration: none; color: #0366d6;">Home</a>
  </div>
</nav>
