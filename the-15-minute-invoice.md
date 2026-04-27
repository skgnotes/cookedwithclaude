---
layout: post
title: "The 15-Minute Invoice"
permalink: /the-15-minute-invoice
---

# The 15-Minute Invoice

A client wraps up. You need to send an invoice. A real one — not a plain text email with a bank transfer note, but something that looks like you run a business.

The old version of this problem took most of a day. Get the logo from the client (they take two hours to send a low-res PNG). Pass it to a designer or freelancer. Wait for a draft. Mark up the draft. Wait again. Export it. By the time you send it, two days have passed and the goodwill from the engagement is starting to cool.

Last month I needed to invoice a company I'd done advisory work for. I had their website. I had the numbers. I had no design file, no designer on call, and no patience for the old process. I opened Claude Code and said: make me a professional invoice.

Fifteen minutes later I had a PDF with their logo, matched brand colors, clean typography, and a proper table of services. I sent it the same day. The client replied within the hour.

Here's how it works.

## Why This Is Worth Knowing

The barrier to professional output has always been tooling and people. You needed Illustrator or Figma or InDesign. You needed someone who knew how to use them. Or you used a generic invoice tool that branded itself all over your document.

What changed: Claude Code can write Python. Python has PIL and reportlab. PIL can extract pixels from an image and identify dominant colors. reportlab can generate a PDF that looks like it cost money. The entire pipeline from "client website" to "finished invoice" runs in a single session, in your terminal, without a creative subscription or a freelance dependency.

The cost: your time to review and approve. That's it.

## The Actual How

**Step 1: Get the logo.**

Point Claude Code at the client's website. Ask it to find and download the logo. Typically this means fetching the page, parsing the HTML for `<img>` tags or CSS background references, and downloading the highest-resolution version it can find. If their site uses SVG logos, even better — scalable without quality loss.

```
Find the logo from [client website URL] and save it locally.
```

Claude will write the scraping code, run it, and tell you what it found. Usually takes under a minute.

**Step 2: Extract the brand color.**

This is the part that surprised me most. PIL can read pixel values from an image. Claude Code writes a short script that loads the logo, samples pixels across the image, clusters them by frequency, and returns the dominant non-white, non-transparent color. You end up with a hex value — the actual brand color — without asking the client for their style guide.

```python
from PIL import Image
from collections import Counter

img = Image.open("logo.png").convert("RGBA")
pixels = [
    p[:3] for p in img.getdata()
    if p[3] > 200 and not all(c > 230 for c in p[:3])
]
color_counts = Counter(pixels)
dominant = color_counts.most_common(1)[0][0]
hex_color = "#{:02x}{:02x}{:02x}".format(*dominant)
```

The result feeds directly into the invoice design. Headers, rule lines, and accent colors all pull from the extracted value. The document feels native to their brand without you ever opening a design tool.

**Step 3: Generate the PDF.**

reportlab is a Python library that draws PDFs programmatically. It handles fonts, tables, colors, and layout. Claude Code writes the invoice template: your name and contact details at the top, their logo, a line item table with services and amounts, payment terms, bank details.

The key prompt is specific:

```
Generate a professional invoice PDF using reportlab. 
Use [extracted hex color] as the accent color.
Include: invoice number, date, client name, 
services rendered (table), subtotal, tax, total, 
payment terms, bank transfer details.
Use the downloaded logo in the header.
```

Claude writes the full script, runs it, and produces a PDF. You open it. If something's off — spacing, font size, column widths — you say so and it adjusts. Three or four rounds of feedback and it's done.

**Step 4: Verify visually.**

Don't skip this. Open the PDF before you send it. Claude can also help: ask it to take a screenshot of the rendered PDF and describe what it sees. I had one run where the logo was rendering at 10% opacity because reportlab was treating transparency differently than expected. Caught it in review, not in the client's inbox.

## What Surprised Me

The color extraction is better than it sounds. I expected it to return something close to the brand color — good enough. What it actually returned was exact. I checked it against the client's public brand guidelines afterward: the hex matched their primary brand color to within a few points.

The other thing: this took me fifteen minutes including the back-and-forth feedback on the layout. Not fifteen minutes of typing. Fifteen minutes total — describe what I wanted, watch it run, review the output, request a tweak, done. The wall-clock time from opening Claude Code to sending the invoice was shorter than writing this paragraph.

## How to Start

You don't need to build this ahead of time. The next time you need to send an invoice, open a Claude Code session and say:

```
I need to generate a professional invoice as a PDF. 
The client's website is [URL]. 
Extract their logo, identify their brand color, 
and produce a clean invoice with these line items: [your items].
My details are [your name, address, bank info].
```

It will figure out the rest. PIL and reportlab are standard Python libraries — Claude can install them if they aren't already present. The entire thing runs locally.

The only thing you supply: the numbers, your bank details, and five minutes to review the output before sending.

That's the leverage. Not "AI generated your invoice." You generated the invoice. In fifteen minutes. Without asking anyone else.

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/ai-legal-first-pass" style="text-decoration: none; color: #0366d6;">Next: The AI Legal First Pass →</a>
  </div>
  <div>
    <a href="/retiring-an-automation" style="text-decoration: none; color: #0366d6;">← Previous: The Automation You Should Have Retired Six Months Ago</a>
  </div>
  <div>
    <a href="/" style="text-decoration: none; color: #0366d6;">Home</a>
  </div>
</nav>
