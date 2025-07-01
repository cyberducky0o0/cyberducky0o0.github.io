---
date: 2025-07-01 08:39:30
layout: post
title: XSS Found in Asian Arts Talent Foundation
description: XSS Vulnerability Found in OSS
image: /assets/img/uploads/20250626_0723_cyberducky-s-hack-adventure_remix_01jyp9s1snernbzybyvg427ck9.png
optimized_image: /assets/img/uploads/20250626_0723_cyberducky-s-hack-adventure_remix_01jyp9s1snernbzybyvg427ck9.png
category: "{{slug}}"
tags:
  - security
  - research
  - xss
  - javascript
  - hacking
  - oss
author: CyberDucky
paginate: false
---
# 🐤 CyberDucky Strikes Again: Critical XSS Vulnerability Discovered on AATF Website

**Date Discovered:** June 20, 2025\
**Target:** [Asian Arts Talents Foundation (aatf.us)](http://aatf.us/)\
**Severity:** 🔥 High\
**Vulnerability Type:** Reflected Cross-Site Scripting (XSS)\
**Author:** Juan Soberanes – aka *CyberDucky* 🧠💻

## 🕵️ Discovery Story

During a routine local assessment using the public Docker container from the [Asian Arts Talents Foundation](http://aatf.us/), I uncovered a high-risk vulnerability in one of their endpoints. This wasn't just any bug – this was a textbook case of **Reflected XSS**, ripe for exploitation by malicious actors.

No login needed. No fancy bypass. Just a single unsanitized header away from browser-based chaos.

Let’s dive into the details...

- - -

## 💥 Vulnerability Summary

* **Endpoint:** `/ip.php`
* **Vector:** `X-Forwarded-For` HTTP header
* **Impact:** Arbitrary JavaScript execution in victim browsers
* **Tested Via:** Local Docker environment + Burp Suite

### 📜 Vulnerable Code Pattern

The script appears to output the X-Forwarded-For header directly without escaping HTML special characters.

- - -

## 🧪 Proof of Concept (Non-Malicious)

Launch this cURL request from your local machine:

```bash
curl -H "X-Forwarded-For: <script>alert('XSS, CyberDucky was Here.')</script>" http://localhost/ip.php


```

Or intercept and modify the header in Burp Suite to inject the payload directly in-browser.

Once triggered, the browser pops an alert — proving that **JavaScript execution is possible**.

- - -

## 🚨 Potential Impact

If exploited on a live environment, attackers could:

* 🥷 Steal session cookies or auth tokens
* 🪝 Inject keyloggers, redirect scripts, or phishing payloads
* 🔐 Hijack accounts or escalate privilege
* 📉 Damage user trust and brand reputation

- - -

## 🛡️ Recommendations

### ✅ Quick Fix

Sanitize all dynamic output using:

```php
// Instead of: print($_SERVER["HTTP_X_FORWARDED_FOR"]);

// Use: print(htmlspecialchars($_SERVER["HTTP_X_FORWARDED_FOR"], ENT_QUOTES, 'UTF-8'));
```

### 📦 Hardening Tips

* Add security headers like:

  * `X-Content-Type-Options: nosniff`
  * `X-Frame-Options: DENY`
  * `Content-Security-Policy: default-src 'self';`
* Enforce HTTPS sitewide
* Log and monitor header values that deviate from expected IP formats

## ✉️ Final Thoughts

This research was conducted **ethically** with no harm to production systems or user data. The goal? To make the internet a safer place — one bug at a time.

If you represent AATF or a security team member reading this: I’m here to collaborate, not criticize. Thank you to Felix for promptly getting this resolved over at AATF! I appreciate your efforts in resolving this. 

F﻿ix Found [here](https://github.com/AATF/aatf.us/commit/a3854c4041699ea6aab5914eb4552e87d223264a)

![](/assets/img/uploads/xxs-aatf.png)

- - -

**“Hack the bugs before the bad guys do.” – CyberDucky** 🐤💥

- - -