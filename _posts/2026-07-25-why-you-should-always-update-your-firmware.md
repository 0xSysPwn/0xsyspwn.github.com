---
title: "Why You Should Always Update Your Firmware"
date: 2026-07-25 09:00:00 +0000
categories: [Hardening]
tags: [firmware, thinkpad, hardware-security]
image:
  path: /assets/img/thumb-firmware.png
  alt: A simple icon representing firmware updates
---

The word "update" doesn't sound like much anymore. Your phone throws a notification at you now and then, you tap "update all," and you go back to scrolling. That kind of update is routine and easy to ignore.

Firmware updates are a different thing entirely, and they're a lot easier to overlook — most people have never dealt with one unless they've spent a weekend afternoon troubleshooting a hardware issue themselves.

## What firmware actually is

Firmware is code stored directly on the physical chips in your computer — motherboards, SSDs, Wi-Fi modules, battery controllers. It tells these components how to talk to each other, and it's OS-independent: the code is the same whether you're running Windows, Linux, or macOS. It doesn't disappear when you format your drive and install a new OS, and every so often, updates get pushed to fix real issues — including security vulnerabilities, and problems that can physically damage the component itself.

## A bug that could have bricked the laptop I'm writing this on

A while back, I bought a refurbished Lenovo ThinkPad X390, first released in 2019 — the same laptop I'm using to write this post. Seven years on, it's still a good machine, but seven years is also long enough that it needed real firmware attention along the way, including one update that mattered more than most.

That update was meant to patch the **Flash ROM "wear-out" vulnerability**, which affected a wide range of ThinkPads — T470 through T490, X1 Carbon Gen 5–7, X280, X390, and several P-series models. The bug was self-destructive by design: a flaw in the Intel Thunderbolt controller's firmware caused it to continuously write unnecessary data to a separate chip, the SPI Flash ROM.

That chip was physically built to hold firmware that rarely changes — it was never designed to withstand continuous write cycles. But that's exactly what the faulty firmware was doing to it, even while the laptop sat idle or ran basic tasks. Eventually the chip would fail, taking the Thunderbolt controller down with it. Since modern ThinkPads route USB-C power delivery, external displays, and high-speed data through that same controller, one dead chip could cascade into an entire laptop rendered unusable.

## What actually happened, and why it matters

When I first got the laptop and installed Ubuntu on it, one of the first things waiting in my notifications was a firmware update addressing this exact issue. Had I ignored it and kept using the laptop as-is, I'd likely have ended up with a bricked machine — a real possibility that had already happened to other ThinkPad owners before Lenovo shipped the fix.

That's the actual case for taking firmware updates seriously: they're not just routine housekeeping like an app update. Sometimes they're the only thing standing between your hardware working normally and a slow, silent failure you won't see coming until it's too late. A few minutes spent updating firmware is a lot cheaper than the alternative — a dead laptop and an unplanned repair bill.
