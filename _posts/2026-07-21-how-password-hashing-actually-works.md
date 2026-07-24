---
title: "How Password Hashing Actually Works"
date: 2026-07-21 09:05:00 +0000
categories: [Auth]
tags: [passwords, bcrypt, hashing]
image:
  path: /assets/img/thumb-password-hashing.png
  alt: Diagram comparing bcrypt password hashing against plaintext storage
---

Almost every major breach headline includes some version of the same sentence: "passwords were stored using outdated hashing" or, worse, "in plaintext." The difference between those two outcomes is a few lines of code and a well-chosen library.

## The right way

A password never needs to be stored in a form you could read back. Instead, it's run through a slow, deliberately expensive hashing function, and only the result is stored:

```js
const bcrypt = require('bcrypt');

// on signup
const hash = await bcrypt.hash(plainPassword, 12);
await db.users.save({ email, passwordHash: hash });

// on login
const valid = await bcrypt.compare(candidatePassword, storedHash);
```

Notice there's no step where the plaintext password is ever written to storage — it exists only briefly in memory during the comparison.

## Why "slow" is the whole point

Generic hash functions like SHA-256 are built for speed, which is exactly the wrong property for password storage — it means an attacker with a stolen hash list can try billions of guesses per second. Algorithms built for passwords (bcrypt, scrypt, Argon2) are deliberately slow and tunable, so cracking attempts stay expensive even after a breach.

## What "salt" solves

A salt is random data mixed into each password before hashing, unique per user. Without it, two users with the same password would produce identical hashes, and an attacker could crack every matching pair at once using a precomputed table. Modern libraries like bcrypt generate and store the salt for you automatically — it's part of the output string, not something you manage by hand.

[Download: Password Hashing Cheat Sheet (PDF)](/assets/downloads/password-hashing-cheatsheet.pdf)
