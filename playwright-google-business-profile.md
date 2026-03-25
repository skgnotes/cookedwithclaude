---
layout: post
title: "How we fixed a Google Business Profile with Playwright — without touching the API"
permalink: /playwright-google-business-profile
---

# How we fixed a Google Business Profile with Playwright — without touching the API

The business description was wrong. The phone number was outdated. The hours were from two years ago.

A founder I work with asked me to fix it. I opened the Google Business Profile API docs, got three pages deep into OAuth scope verification and API access request forms, and closed the tab.

Then I opened Playwright.

Twenty minutes later, every field was correct. No API credentials. No agency. No waiting.

## Why the API is the wrong tool here

The Google Business Profile API exists. It is documented. It works — for teams building integrations, managing hundreds of locations, syncing with CRMs.

For a founder who needs to update their business hours once, it is a bureaucratic wall. You need OAuth consent screen setup, API project configuration, the right scope, verified access for certain fields, and a working understanding of the resource hierarchy before you can PATCH a single field.

The UI has none of that friction. You log in, you click, you update. The only problem is you have to do it yourself — until you don't.

## The pattern

Playwright isn't just for testing. It is a browser that your code controls.

Wherever a human can log in and click through a UI to accomplish something, Playwright can do the same thing — faster, repeatably, and without your attention.

When an API is missing, inaccessible, or buried behind setup cost that doesn't justify a one-time task, the UI is the API. Playwright is the client.

## How we did it

The Google Business Profile owner panel lives at `business.google.com`. From there, you can edit every public-facing field on your profile: name, description, phone, website, hours, attributes.

Here's what the Playwright script does:

**1. Launch and authenticate**

We used an existing Chrome profile that was already logged into the Google account. No credential handling, no cookies to manage — just point Playwright at the profile directory and launch.

```javascript
const browser = await chromium.launchPersistentContext(
  '/path/to/chrome/profile',
  { channel: 'chrome', headless: false }
);
```

Running headless is fine once you've confirmed the flow works. We kept it headed the first time to watch what was happening.

**2. Navigate to the edit panel**

```javascript
const page = await browser.newPage();
await page.goto('https://business.google.com/');
```

From the dashboard, there's an "Edit profile" button. We clicked it:

```javascript
await page.getByText('Edit profile').click();
```

**3. Update the fields**

Each field in the edit panel is a standard input or textarea. For the business description:

```javascript
await page.getByLabel('Business description').click();
await page.getByLabel('Business description').fill('');
await page.getByLabel('Business description').type('Updated description here.');
```

Clear first, then type. Filling directly sometimes leaves ghost characters in fields that already have content.

For phone number:

```javascript
await page.getByLabel('Phone').click();
await page.getByLabel('Phone').selectAll();
await page.keyboard.type('+91 98000 00000');
```

For hours, the UI uses dropdowns per day. We iterated:

```javascript
const days = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday'];
for (const day of days) {
  await page.getByRole('group', { name: day }).getByLabel('Opens at').selectOption('09:00');
  await page.getByRole('group', { name: day }).getByLabel('Closes at').selectOption('18:00');
}
```

**4. Save**

```javascript
await page.getByRole('button', { name: 'Save' }).click();
await page.waitForSelector('text=Changes saved');
```

We waited for the confirmation text before considering it done. Running without verification is how you think it worked and discover three days later it didn't.

## What surprised us

The selectors were stable. Google Business Profile is a mature product, and the edit panel's labels and roles matched exactly what you'd expect. We didn't need to inspect the DOM or hunt for data-testid attributes — the accessible labels were clean.

The second thing: it took longer to read the API docs than to write and run the Playwright script. That gap is bigger than most founders realise. The API is theoretically more powerful. In practice, for a single task with a logged-in account already in hand, Playwright is faster start to finish.

## Where else this applies

Any admin panel where you have credentials and the API is either nonexistent, requires OAuth setup you haven't done, or needs permissions you'd have to request.

Common candidates:

- Updating a Shopify storefront detail that isn't exposed in the standard API tier
- Editing a supplier portal that has no API at all
- Submitting a form on a government or regulatory site
- Bulk-updating fields in any SaaS dashboard that makes changes one at a time

The pattern is always the same: you have access as a human user, the task is defined, and the only variable is attention. Playwright removes attention from the equation.

## How to start

Pick one admin task you do manually, on a schedule or on demand, where you have a login and the outcome is predictable.

Write the Playwright script headed, watching what it does. Once it works once, run it headless. If you do it more than twice a year, the script already paid for itself.

The Google Business Profile was a twenty-minute fix. The next one will be ten.

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="/tracking-relationships-without-crm" style="text-decoration: none; color: #0366d6;">Next: How I track birthdays and follow-ups without a CRM →</a>
  </div>
  <div>
    <a href="/meeting-prep-brief" style="text-decoration: none; color: #0366d6;">← Previous: How I use Claude Code to prep for important meetings</a>
  </div>
  <div>
    <a href="/" style="text-decoration: none; color: #0366d6;">Home</a>
  </div>
</nav>
