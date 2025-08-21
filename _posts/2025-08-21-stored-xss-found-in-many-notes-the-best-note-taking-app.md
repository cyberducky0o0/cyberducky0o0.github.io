---
date: 2025-08-20 19:16:18
layout: post
title: Stored XSS FOUND! In Many Notes, The Best Note Taking APP!
description: "Blind SQL Injection Found! In Tirreno : Security Analytics"
image: /assets/img/uploads/capture.png
optimized_image: /assets/img/uploads/capture.png
category: research
tags:
  - research
  - xss
  - web
  - security
  - hacking
  - cybersecurity
  - manynotes
  - php
author: CyberDucky
paginate: false
---
# How I Found a Stored XSS in Markdown Rendering

Severity: High (CVSS 7.3)

- - -

## The Discovery

I was testing the markdown rendering feature in the Many Notes application when something caught my eye. It looked like the application was running user content through a markdown parser and then trying to clean it with DOMPurify. On paper, that sounds safe enough. In practice, it wasn’t.

After a couple of quick checks, I realized I could sneak in a script tag and get it to execute. That meant the app was vulnerable to a classic stored XSS.

- - -

## Where It Happens

The issue shows up when viewing files like this:

```
http://localhost/files/2?path=test2.md
```

If you upload a malicious markdown file, the contents get stored and later displayed without proper sanitization.

- - -

## Under the Hood

Here’s the relevant code path:

```
if (options.content) {
    content = DOMPurify.sanitize(
        markedService.parse(options.content),
    );
}

```

The problem is that DOMPurify doesn’t catch everything. It’s good at blocking obvious stuff, but more creative payloads (SVG tricks, DOM clobbering, mutation XSS) can still get through.

- - -

## Proof of Concept

The simplest test payload worked right away:

```
<script>alert("Cyber Ducky was Here")</script>

```

Open the file in the browser, and sure enough, the alert popped.

- - -

## Why It Matters

This isn’t just a harmless pop-up. Once an attacker has XSS in the application, they can:

* Steal cookies or tokens to hijack sessions.
* Act as the logged-in user (full account takeover).
* Read sensitive data out of the vault.
* Inject malware or phishing redirects into pages other users trust.

- - -

## Fixing It

If I were patching this, here’s what I’d do right away:

* Don’t just sanitize in the browser — add server-side sanitization before saving content.
* Enforce a strong Content Security Policy so rogue scripts can’t run.
* Revisit the DOMPurify configuration and enable stricter settings.
* Validate uploaded files properly instead of just trusting the parser.

- - -

## Timeline

* Day 0 – I discovered and reproduced the issue.
* Day 1 – Sent the report to the vendor.
* Day 30 – Plan to go public if it isn’t fixed.

- - -

## Closing Thoughts

This was a straightforward find, but it highlights a bigger point: relying solely on client-side libraries like DOMPurify isn’t enough. XSS is sneaky, and even well-known tools can miss certain payloads.