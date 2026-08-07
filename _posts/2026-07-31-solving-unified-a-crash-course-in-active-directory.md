---
title: "Solving Unified: A Crash Course in Active Directory"
date: 2026-07-31 09:00:00 +0000
categories: [Learning]
tags: [active-directory, ldap, ctf, hack-the-box, log4j]
description: "A narrow question about LDAP led nowhere until I realized I was missing the bigger picture — how Active Directory and its protocols fit together."
image:
  path: /assets/img/thumb-ldap.webp
  alt: A simple icon representing directory services and networked computers
---

As a beginner going through HTB's Starting Point boxes, I've been running into protocols that are still new to me. LDAP was one of them. I went looking for YouTube videos that would explain the concept just enough to confidently solve the box in front of me, and came up empty.

The machine I was working on is called Unified. One of the services it runs is UniFi Network Controller version 6.4.54 on port 8443, which turned out to be vulnerable to Log4j — CVE-2021-44228. That vulnerability allows remote code execution, typically triggered by making a request to a remote server via LDAP.

## Why the shortcuts didn't work

I could have just followed a walkthrough, or copy-pasted a payload I found while googling the vulnerability. That didn't sit right with me. I actually needed to understand the LDAP protocol, not just paste around it.

The YouTube search wasn't a total waste, though — it taught me that Active Directory relies on LDAP to function. And that was about it. Understanding one protocol meant learning the rationale behind Active Directory's existence in the first place: what other services and protocols live inside that environment, and how they work together to solve the problem every AD environment exists to solve — managing tens or hundreds of computers efficiently.

## Changing how I asked the question

I still used Claude to learn all of this — but differently than before. Instead of asking "what is LDAP?" and getting an explanation full of other protocols I didn't understand yet, I asked it to generate a guide to the entire Windows enterprise ecosystem instead: the rationale behind its existence, and the protocols it uses to make that happen.

That single change — asking for the map instead of directions to one point on it — was what actually got me unstuck. Armed with an actual sense of how Active Directory fits together, going back to Unified's LDAP-triggered Log4j injection finally clicked, and the box fell within the hour.

## The guide

You can download the guide down below if you're interested in the Windows ecosystem and how to approach CTF challenges built around it. It won't answer every question, but it's a solid starting point — you can fill in the gaps afterward with follow-up questions to your AI agent of choice.


[Download: The windows enterprise ecosystem (PDF)](/assets/downloads/windows_ecosystem_rationale.pdf)

 