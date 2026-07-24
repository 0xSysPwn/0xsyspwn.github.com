---
title: "A Beginner's Guide to Two-Factor Authentication"
date: 2026-07-21 09:15:00 +0000
categories: [Auth]
tags: [2fa, totp, authentication]
image:
  path: /assets/img/thumb-2fa.png
  alt: Diagram showing a phone and server both deriving the same TOTP code
---

A password is one thing you know. Two-factor authentication (2FA) adds a second, different kind of proof — usually something you have, like your phone. Even if your password leaks in some breach you'll never hear about, that second factor is what stops it from becoming an actual account takeover.

## How TOTP codes actually work

TOTP stands for Time-based One-Time Password. When you scan a setup QR code, both your phone and the server agree on a shared secret. From that point on, each side independently computes a six-digit code from that secret plus the current time, refreshed roughly every 30 seconds. Nothing is transmitted between them at login — the two sides simply arrive at the same number, which is why it works without an internet connection on your phone.

```python
import pyotp

secret = pyotp.random_base32()   # generated once, during setup
totp = pyotp.TOTP(secret)
print(totp.now())                # the current 6-digit code
```

## Choosing a method, roughly ranked

- **Hardware security key** — the strongest option, and resistant to phishing since it checks the site's actual domain before responding.
- **Authenticator app (TOTP)** — the good default: no cell signal needed, not tied to your phone number.
- **SMS codes** — better than nothing, but vulnerable to SIM-swap attacks where an attacker ports your number to their own device.

## Where to turn it on first

Start with email and your password manager — both of those protect everything else, so they're worth securing before anything else on your list. Save the backup codes somewhere offline when you set it up; they're the only way back in if you lose the device.

[Download: 2FA Setup Guide (PDF)](/assets/downloads/2fa-setup-guide.pdf)
