---
layout: post
title: "From screenshots to board report in one session"
permalink: /screenshots-to-board-report
---

# From screenshots to board report in one session

Eight screenshots sitting in a folder. Each one a snapshot from a different dashboard — revenue, pipeline, headcount, burn. No API access. No export button that works. Just images.

By the end of the session, there was a clean PDF on the board's Telegram group.

## What this replaces

Every quarter, someone on the team would spend half a day on this. Open each dashboard. Screenshot it. Paste the numbers into a spreadsheet manually. Hunt down the duplicates where the same metric showed up in two places. Build the summary table. Export to PDF. Send it.

That half-day is now a single Claude Code session.

## The actual workflow

### Step 1 — Dump the screenshots into a folder

Start simple. All eight screenshots in one directory. Nothing renamed, nothing organised. Claude handles that.

```
Read all screenshots in /reports/q1-dashboards/ and extract every numeric metric you can identify. For each metric, note the source screenshot filename and what the metric appears to represent.
```

Claude reads each image and returns a structured list: metric name, value, source file. It's not perfect — some labels are ambiguous, some numbers appear to be the same metric pulled from different views — but the extraction is fast and surprisingly accurate.

### Step 2 — Reconcile duplicates

This is the part that used to take longest. Three different screenshots all showing some version of "active users." Which one is correct? Which time period applies?

```
Looking at the extracted data, identify metrics that appear more than once across different screenshots. For each duplicate group, flag which values differ and hypothesize which is most likely canonical (e.g. most recent date visible, most specific label).
```

Claude surfaces eight duplicate groups. Five are trivially resolvable — same number, different screenshots. Three need human judgment: a daily vs. monthly active user figure, two different pipeline stage definitions, a headcount number that may or may not include contractors.

Those three get flagged with a note. The rest get resolved automatically.

### Step 3 — Build the conversion table

The board wants a single-page summary. Not raw numbers — a table showing metric, current period value, prior period value, and direction of change.

Problem: the screenshots don't all include prior period data. Some do. Some don't.

```
Build a summary table with these columns: Metric | Current | Prior | Change. Where prior period data is available in the screenshots, include it. Where it's not, mark as "—". Flag any metrics where the change calculation requires clarification.
```

The output is a markdown table. Clean, consistent, with honest gaps flagged rather than left blank or filled with guesses.

### Step 4 — Generate the PDF

Claude Code can't generate PDFs natively. But it can write the HTML, and a headless browser can render it.

```
Take the summary table and convert it to a clean, minimal HTML document styled for printing. Use a system font, black on white, adequate margins. No branding needed — this is an internal report.
```

Then:

```bash
/usr/bin/wkhtmltopdf --page-size A4 report.html board-report-q1.pdf
```

Or, if `wkhtmltopdf` isn't available, Playwright works:

```javascript
const browser = await chromium.launch();
const page = await browser.newPage();
await page.goto('file:///path/to/report.html');
await page.pdf({ path: 'board-report-q1.pdf', format: 'A4' });
```

The PDF renders in under two seconds.

### Step 5 — Deliver to Telegram

One script call. The Telegram Bot API handles the rest.

```bash
curl -s -F "chat_id=-100XXXXXXXXXX" \
  -F "document=@board-report-q1.pdf" \
  -F "caption=Q1 Board Report — $(date +%d %b %Y)" \
  "https://api.telegram.org/bot$BOT_TOKEN/sendDocument"
```

The file lands in the group within seconds.

## What surprised me

Two things.

First, the image reading was more capable than I expected. These weren't clean charts — they were full dashboard screenshots with navigation menus, filter dropdowns, annotation overlays, and varying font sizes. Claude correctly ignored the surrounding UI noise and extracted the signal. The occasional miss was obvious and easy to correct.

Second, the duplicate reconciliation framing changed how I thought about the problem. I expected to spend time reviewing conflicts. Instead, most of the "duplicates" turned out to be non-conflicts — same metric, same value, just appearing in two places for different audience views. The real conflicts were the ones I genuinely needed to think about. Claude's output made that separation visible instead of burying it.

## Where to start

You probably have a version of this problem somewhere. A recurring report that involves pulling numbers from multiple places, assembling them manually, and sending them to a group that could have received them automatically.

The threshold for trying this is low: a folder with the screenshots and a rough description of what you want in the output. You don't need to script the whole thing first. Start with step one — just ask Claude to extract the data and tell you what it sees. The rest follows naturally.

The half-day task doesn't need to be a half-day task.

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/morning-automation-stack" style="text-decoration: none; color: #0366d6;">Next: Your morning automation stack →</a>
  </div>
  <div>
    <a href="/tracking-relationships-without-crm" style="text-decoration: none; color: #0366d6;">← Previous: How I track birthdays and follow-ups without a CRM</a>
  </div>
  <div>
    <a href="/" style="text-decoration: none; color: #0366d6;">Home</a>
  </div>
</nav>
