---
layout: post
title: "Context engineering, not prompt engineering"
permalink: /context-engineering
---

# Context engineering, not prompt engineering

Every operator I know who uses Claude effectively has stopped talking about prompts. Not because prompts don't matter — they do. But because they've moved the work upstream.

The shift is subtle. You stop asking "how do I phrase this?" and start asking "what does this model need to know before I say anything?" One question is about wordsmithing. The other is about infrastructure.

That difference compounds fast.

## The problem with prompt engineering

Prompt engineering frames AI collaboration as a communication problem. The model is smart; you just need to learn its language. Write clearer instructions. Add examples. Use chain-of-thought. Be specific about the format you want.

This advice isn't wrong. It's just the wrong level of abstraction.

A better prompt gets you a better output from that specific interaction. Context engineering gets you better outputs from every interaction, including the ones where your prompt is vague or rushed or half-finished — which is most of them.

Here's the practical difference: I run Claude Code dozens of times a day. I'm not going to write a crafted prompt every time I need a draft email or a quick decision summarised or a document formatted. The value of AI assistance collapses if every use requires careful prompt construction.

What I have instead is context.

## What context actually is

Context is everything the model knows about your world before you type a single word. It has three layers, and each one does different work.

**Persistent instructions** — the `CLAUDE.md` files that live in your project directories. These tell the model who you are, how you work, what decisions have already been made, what not to do. A well-built `CLAUDE.md` means the model carries your operating principles into every session without you restating them.

The key is specificity. A `CLAUDE.md` that says "be concise" does almost nothing. One that says "lead with the answer, not the reasoning — no preamble, no summaries at the end of responses, short sentences over long explanations" does real work. It changes the shape of every output you receive.

**Persistent memory** — the `MEMORY.md` file or equivalent system for carrying hard-won knowledge across sessions. Proven CLI patterns. Tools you prefer. Approaches that have failed. Gotchas specific to your setup. The things you'd otherwise re-explain, re-discover, or re-debate every time.

This is where most people leave leverage on the table. They build good session-level prompts but have no mechanism for carrying learning forward. Every session starts cold. The model is stateless by design; your job is to build the infrastructure that makes it effectively stateful.

**Domain context files** — the deeper files that give the model genuine understanding of your world. Your communication style and preferences. The people you work with and how to address them. Your current projects, priorities, and constraints. The vocabulary of your industry. How decisions get made in your organisation.

When these exist, you can say "draft a follow-up to last week's meeting" without explaining who you are, what you work on, what your tone should be, or who receives the message. The model already knows.

## The systems design framing

Think about it as a design problem, not a communication problem.

The input you're designing for is: how much of every interaction can be implicit instead of explicit? The output you're optimising for is: minimum prompt, maximum useful output.

Every piece of context you build is leverage. Not just for the next prompt, but for every prompt that follows it. A good `CLAUDE.md` is a one-time investment that pays out indefinitely. A well-built memory file means you never re-explain a preference you've already stated.

The operators I've seen get the most value from Claude Code are, almost without exception, the ones who treated this as an infrastructure problem early. They spent time building context before they needed it. They maintained it the way you'd maintain any other system that your work depends on.

The ones who didn't are still rewriting the same context into each new session.

## The honest version

Context engineering is not hard. The files are just markdown. The principles are just: write down what the model needs to know, keep it specific, keep it current.

What makes it feel hard is that it requires a different frame. You're not talking to a model. You're building a system that talks to a model on your behalf, efficiently, every time. The system includes you, your context files, and the model. Most of the leverage is in the middle layer — the one people skip.

Prompt engineering asks: how do I explain this better? Context engineering asks: how do I build something that doesn't require me to explain this at all?

That's a different kind of work. It takes maybe a few hours to set up properly. And then it quietly multiplies everything that comes after it.

Start with a `CLAUDE.md` in your main working directory. Write down how you want to be communicated with. What you're working on. What the model should and shouldn't do. Keep it honest rather than aspirational.

That file is not a prompt. It's infrastructure. The difference is that you build infrastructure once and then use it forever.

Most people are still trying to write better prompts. The operators pulling ahead are building better context.

<nav style="margin-top: 48px; padding-top: 24px; border-top: 1px solid #eee; font-size: 14px;">
  <div>
    <a href="/tool-priority-hierarchy">← Previous: The Tool Priority Hierarchy</a>
  </div>
  <div style="margin-top: 16px;">
    <a href="/claude-md-setup">Next: The CLAUDE.md setup that makes everything work →</a>
  </div>
  <div style="margin-top: 16px;">
    <a href="/">↑ Home</a>
  </div>
</nav>
