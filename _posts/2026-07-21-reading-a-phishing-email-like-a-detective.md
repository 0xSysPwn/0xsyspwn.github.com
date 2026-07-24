---
title: "Reading a Phishing Email Like a Detective"
date: 2026-07-21 09:10:00 +0000
categories: [Email]
tags: [phishing, social-engineering, email-security]
image:
  path: /assets/img/thumb-phishing-email.png
  alt: Example email header showing a From address mismatch with Reply-To and Return-Path
---

Most phishing advice stops at "don't click suspicious links," which is true but not very actionable — the whole point of a good phishing email is that it doesn't look suspicious at a glance. The tell is usually sitting in fields nobody reads: the headers.

## Three fields worth checking every time

```text
From:        "IT Support" <support@yourcompany.com>
Reply-To:    it-helpdesk@mail-secure-update.info
Return-Path: <bounce@mail-secure-update.info>
```

The **From** display name is whatever the sender typed — it proves nothing. What matters is where a reply, or a bounce, actually goes. When **Reply-To** or **Return-Path** point to a domain unrelated to the claimed sender, that mismatch is one of the most reliable signals available, and it's invisible unless you go looking.

## The pressure tactics that usually ride along

- **Urgency** — "act within 24 hours" or "your account will be suspended." Urgency is designed to short-circuit the pause where you'd normally check.
- **Borrowed authority** — impersonating IT, HR, or an executive, so the request feels like it can't be questioned.
- **A credential-shaped ask** — "verify your account," "re-enter your password," anything that ends in typing a password into a form.

## Before you click anything

Hover the link and look at where it actually points, not the display text layered over it. If something still feels off, reach the sender through a separate channel you already know — a phone extension, a Slack DM, not a number or link in the email itself — and confirm before acting.

[Download: Phishing Red Flags Checklist (PDF)](/assets/downloads/phishing-red-flags.pdf)
