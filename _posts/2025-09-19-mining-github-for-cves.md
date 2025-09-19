---
date: 2025-09-19 08:00:04
layout: post
title: Mining Github for CVEs!
description: Mining Github for CVEs!
image: /assets/img/uploads/2.png
optimized_image: /assets/img/uploads/2.png
category: code
tags:
  - security
  - research
  - tech
  - talk
  - cybersecurity
  - osint
  - github
author: CyberDucky
paginate: false
---
# Tech Talk: Mining GitHub for CVE Research with an Enhanced Vulnerability Scanner

## Abstract

Security research often begins with patterns — where do vulnerabilities come from, what practices make them more likely, and how can we spot them earlier? In this talk, I’ll walk through how I built an OSINT-powered vulnerability scanner for GitHub repositories that blends CVE trend analysis, Semgrep static analysis, and repository health metrics into a unified framework. You’ll see how this approach helped me identify bug-prone projects, optimize scanning for scale, and improve my own CVE research workflow.

- - -

## Talk Outline

### 1. Why GitHub OSINT for Vulnerability Research (5 min)

* Repositories as living ecosystems of security practices (or mispractices).
* Quick case study: One of my CVEs came from spotting a repo with weak security hygiene and poor code review patterns.

- - -

### 2. Building the Enhanced Vulnerability Scanner (10 min)

* Motivation: traditional scanners miss “social signals” (maintenance, documentation, contributor activity).
* Architecture:
* * GitHub OSINT collector → Metadata & repo stats.
  * Semgrep engine → Static analysis for known bug patterns.
  * Scoring framework → Combines repository health, security hygiene, development practices, and vulnerability findings.
* Optimization Challenges:
* * API rate limits (5k/hour with token).
  * Tradeoffs between data-only mode vs deep static analysis.
  * Why I added a two-stage process: screen wide, then deep dive.

- - -

### 3. Demo: From 1000 Repos to a Shortlist of Vulnerability Candidates (10 min)

* Stage 1: Run --skip-semgrep mode → Fast OSINT-based filtering.
* Show results in CSV with scores (health, security, development).
* Stage 2: Feed top repos into Semgrep-only scan.
* Show Semgrep findings → e.g., insecure deserialization, weak crypto, bad auth checks.
* Highlight how the scoring system prioritizes “most promising for bugs.”

- - -

### 4. Real Case Study: Turning OSINT into a CVE (5 min)

* Walk through a repo where your scanner surfaced weak security hygiene.
* Show how a Semgrep finding (or manual review after OSINT) led to a bug.
* Tie it back to  published CVE  — explaining the research path from GitHub metadata → pattern spotting → vulnerability discovery.

- - -

### 5. Lessons Learned & Future Work (5 min)

* Patterns matter: poor repo health often predicts bad security practices.
* Automation helps: large-scale scanning + static analysis = faster trend detection.
* Research directions:
* * Expanding beyond GitHub (GitLab, Bitbucket, DockerHub).
  * Enriching scoring with commit-level NLP (e.g., security-related commit messages).
  * Mapping findings to MITRE ATT&CK or CWE categories.
  * Use of LLMs and MCPs