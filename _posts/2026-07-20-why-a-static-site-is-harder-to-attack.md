---
title: "Why a Static Site Is Harder to Attack"
date: 2026-07-20 09:00:00 +0000
categories: [Infra]
tags: [static-sites, github-pages, hosting]
image:
  path: /assets/img/thumb-static-sites.png
  alt: Diagram comparing a dynamic site's attack surface against a static site's
---

This blog is built from three files: an HTML page, a stylesheet, and nothing else. No database, no admin login, no server-side code executing on every request. That's not a limitation — for a small blog, it's the strongest security decision available.

## What a dynamic site exposes

A typical CMS like WordPress runs a server-side application on every page load: it queries a database, renders templates, and often exposes an admin panel at a predictable path. Each of those is a component that can have a vulnerability, and each one needs to be patched, monitored, and defended.

Common weak points include outdated plugins, exposed admin login pages, SQL injection through unsanitized inputs, and misconfigured database permissions. None of those exist if there's no database and no server-side code to begin with.

## What static hosting removes from the equation

A static site hosted on GitHub Pages is just files served over HTTPS. There's no application logic running per-request, so entire vulnerability classes — SQL injection, server-side template injection, most authentication bypasses — simply don't apply, because there's no server-side code path for them to exploit.

The hosting platform also handles HTTPS certificates and infrastructure patching, so that responsibility moves off your plate entirely.

## What it doesn't protect against

Static hosting isn't a complete security story. It's still worth thinking about:

- **Account takeover** — if someone compromises your GitHub account, they can edit your site. Use a strong password and enable two-factor authentication.
- **Supply chain risk** — if you later add third-party JavaScript (analytics, comment widgets, ad scripts), each one is code you didn't write, running on your visitors' browsers.
- **DNS hijacking** — if you add a custom domain, protect your domain registrar account the same way you'd protect any other login.

> The lesson generalizes past blogs: the safest component in any system is the one that doesn't exist. Every server, every database, every login form is something to defend. Removing one is worth more than hardening it.

## Try it yourself

Here's the entire request/response model of this page, for comparison against a typical dynamic stack:

```text
Browser  --GET /index.html-->  GitHub Pages CDN
Browser  <--HTML + CSS file--  GitHub Pages CDN
```

No step in between reads a database or executes your input. That's the whole attack surface: two files, over HTTPS.

[Download: Static Site Security Checklist (PDF)](/assets/downloads/static-site-checklist.pdf)
