---
date: 2025-08-05 23:03:28
layout: post
title: "Blind SQL Injection Found! In Tirreno : Security Analytics"
description: "Blind SQL Injection Found! In Tirreno : Security Analytics"
image: /assets/img/uploads/20250425_0751_retro-room-duck_remix_01jspptv0hfrhv52pyy0zrwnf6.png
optimized_image: /assets/img/uploads/20250425_0751_retro-room-duck_remix_01jspptv0hfrhv52pyy0zrwnf6.png
category: research
tags:
  - security
  - research
  - sqli
  - javascript
  - hacking
  - sql
  - cybersecurity
  - postgres
author: CyberDucky
paginate: false
---
<!--StartFragment-->

**Uncovering a Blind SQL Injection in v0.9.5: A Deep Dive**

- - -

## Overview

In my latest security audit of **v0.9.5**, I discovered a **Blind SQL Injection** that allows attackers to infer—and eventually extract—arbitrary data from the database. This blog post walks through:

* **Vulnerability details**
*  **Proof of Concept**
*  **Recommended Fixes**
* **Our Vulnerability Disclosure Policy**

Read on to learn how this flaw works and how you can protect your own applications.

- - -

## 1. What Is Blind SQL Injection?

Blind SQL Injection is a variant of SQL Injection where the application does not directly return database errors or query results to the attacker. Instead, the attacker infers data based on application behavior—like response delays or conditional responses. In a **time-based** attack, malicious payloads introduce deliberate delays (e.g., using `pg_sleep()`) to confirm the presence of injectable parameters.

- - -

## 2. Affected Version

* **Package:** Admin API “loadUsers” endpoint
* **Version:** v0.9.5 (latest at time of discovery)

- - -

## 3. Impact

An attacker exploiting this vulnerability can:

* Extract **database metadata** (e.g., server version)
* Enumerate **user accounts**, **roles**, and **permissions**
* Steal or modify **sensitive application data**
* Pivot to further attacks against your infrastructure

This is a **high-severity** issue: although it doesn’t immediately leak data, it provides a reliable mechanism to retrieve any information stored in the database—one character at a time.

- - -

## 4. Proof of Concept (Time-Based)

Below is an example payload that causes a **5-second delay** when the first character of the database version is **not** “W”:

```http
GET /admin/loadUsers?columns%5B0%5D%5Bdata%5D=(CASE%20WHEN%20SUBSTRING((SELECT%20version())%2c%201%2c%201)%20%3d%20'W'%20THEN%201%20ELSE%20(SELECT%201%20FROM%20pg_sleep(5))%20END)&order%5B0%5D%5Bcolumn%5D=0&order%5B0%5D%5Bdir%5D=asc&token=<replace with your admin token>
```

* **Normal Response:** ~200 ms
* **With Payload:** ~5 s delay

This delay confirms that the database engine is executing our injected `CASE` statement. By iterating this technique (checking each character of version, table names, user names, etc.), an attacker can fully enumerate your schema and data.

- - -

## 5. Root Cause

The injection vector lies in the **`ORDER BY`** clause of the query used for the api.

Because the application directly interpolates user-supplied sorting parameters into the SQL query—without validation or sanitation—an attacker can inject arbitrary SQL expressions.

- - -

## 6. Recommended Fix

1. **Parameterize All Queries**\
   Use prepared statements or an ORM’s parameter binding—even for sorting fields. For example, in PostgreSQL with `pg-promise.`
2. **Whitelist Input**\
   Maintain a server-side list of allowable columns and directions (`ASC`/`DESC`), rejecting anything else.
3. **Use Query Escaping Helpers**\
   Leverage your database driver’s built-in escaping functions rather than manual string concatenation.
4. **Adopt Security Middleware**\
   Consider libraries such as [sqlstring](https://www.npmjs.com/package/sqlstring) (Node.js) or [`psycopg2.sql`](https://www.psycopg.org/docs/sql.html) (Python) to build safe SQL identifiers.

- - -

## 7. CyberDucky Vulnerability Disclosure Policy

We believe **responsible disclosure** protects users and strengthens open-source communities. Our policy:

| Tier                 | Timeline                                                                         |
| -------------------- | -------------------------------------------------------------------------------- |
| **Standard**         | 90 days to patch; public disclosure after deadline.                              |
| **0-Day Exploited**  | 7 days to publish a fix; details released thereafter.                            |
| **Weekend/Holiday**  | Deadline shifts to next business day.                                            |
| **Patch Within 14d** | If a patch arrives within 14 days post-deadline, disclosure waits until release. |
| **Equal Treatment**  | All vendors receive the same deadlines—no exceptions for size or notoriety.      |

> *Feel free to adopt or adapt our policy: together, we can build a safer internet.*

- - -

## 8. Get Involved

*  **Share this post** if you found it useful!
* **Comment below** with your experiences or questions.
* **Subscribe** to CyberDucky for the latest security reports and in-depth analyses.

Stay safe, and happy hunting! 🦆

<!--EndFragment-->