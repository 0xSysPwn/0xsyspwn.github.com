---
title: "Setting Security Headers on a Static Site"
date: 2026-07-21 09:00:00 +0000
categories: [Hardening]
tags: [http-headers, csp, static-sites]
image:
  path: /assets/img/thumb-security-headers.png
  alt: Diagram showing a server sending security headers to a browser
---

HTTP response headers are instructions your server hands the browser alongside every page: what sources it's allowed to load scripts from, whether it can be embedded in someone else's page, how much referrer information leaks when a visitor clicks a link. None of this is visible on the page itself — it's a quiet layer of defense sitting underneath.

## The headers worth setting

- **Content-Security-Policy** — restricts which sources scripts, styles, and images are allowed to load from, which blunts a large class of injection attacks.
- **X-Content-Type-Options: nosniff** — stops the browser from guessing a file's type and executing it as something it isn't.
- **Referrer-Policy** — controls how much of your URL leaks to the next site when someone clicks a link away from your page.
- **Permissions-Policy** — explicitly turns off browser features (camera, mic, geolocation) your site has no business asking for.

## Where you actually set these

If you're on Netlify or Cloudflare Pages, it's a plain-text file at your site root:

```text
/*
  Content-Security-Policy: default-src 'self'
  X-Content-Type-Options: nosniff
  Referrer-Policy: strict-origin-when-cross-origin
  Permissions-Policy: geolocation=(), microphone=(), camera=()
```

GitHub Pages is different — you don't get server config access, so most of these can't be set as true response headers. CSP is the one exception: it can be delivered through a meta tag directly in your HTML instead.

```html
<meta http-equiv="Content-Security-Policy"
      content="default-src 'self'">
```

That's a real limitation worth knowing about. If headers become a priority, moving hosting to Cloudflare Pages or Netlify — both still free, both still static — gets you full header control without giving up anything else we've built here.

## Checking your work

After deploying, run your domain through a headers-scanning tool to see what's actually being sent, and start with a loose Content-Security-Policy before tightening it — an overly strict policy can silently break fonts, embeds, or scripts you do want to allow.

[Download: Security Headers Cheat Sheet (PDF)](/assets/downloads/security-headers-cheatsheet.pdf)
