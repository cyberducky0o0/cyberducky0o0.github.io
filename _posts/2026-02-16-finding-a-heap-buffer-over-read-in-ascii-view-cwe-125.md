---
date: 2026-02-16 08:41:45
layout: post
title: Finding a Heap Buffer Over-Read in ascii-view (CWE-125)
description: Finding a Heap Buffer Over-Read in ascii-view (CWE-125)
image: /assets/img/uploads/coverphoto-1.jpg
category: research
tags:
  - security
  - research
  - bufferoverflow
  - heap
  - hacking
  - oss
  - c
  - heap-overread
author: CyberDucky
paginate: false
---
Security research isn’t always about flashy exploits or instant remote code execution. Sometimes, the most valuable work is finding small, quiet bugs *before* they become serious problems.

While reviewing the open-source project **ascii-view**, I identified a **heap buffer over-read vulnerability (CWE-125)** affecting the image grayscale conversion logic. Although the issue is not practically exploitable today, it represents a real memory safety flaw that could become exploitable if future changes alter how the leaked data is processed.

This article documents the vulnerability, explains why it happens, demonstrates how it can be reproduced, and shows how it was fixed following responsible disclosure practices.

- - -

### Vulnerability Summary

* **Project:** ascii-view
* **Vulnerability Type:** Heap Buffer Over-read (CWE-125)
* **Severity:** Medium
* **CVSS 3.1 Score:** 4.3
* **Location:** `src/image.c`, `make_grayscale()`
* **Impact:** Heap memory disclosure
* **Exploitability:** Low (high difficulty in extracting useful data)

- - -

### Quick Overview

The `make_grayscale()` function assumes that all images contain at least three color channels (RGB). When a grayscale PNG (single channel) is processed, the function reads beyond the allocated heap buffer, pulling unintended memory into the grayscale calculation.

While the output does not directly expose raw memory, it *does* incorporate heap data into computations — making this a genuine memory safety issue.

- - -

### Technical Breakdown

### Vulnerable Code

```
double grayscale = 0.2126 * pixel[0]
                 + 0.7152 * pixel[1]
                 + 0.0722 * pixel[2];
```

### Why This Is a Bug

* **Grayscale images:** 1 channel → `pixel[0]` is valid
* **RGB images:** 3 channels → `pixel[0..2]` are valid
* **Bug:** The code assumes all images are RGB

When a grayscale image is passed in, `pixel[1]` and `pixel[2]` access memory **past the allocated buffer**, resulting in a heap over-read.

- - -

### Memory Impact

Because the function iterates over every pixel, the leak scales with image size:

Image SizeAllocatedAccessedLeaked3×124 bytes72 bytes48 bytes10×10800 bytes2,400 bytes1,600 bytes100×10080 KB240 KB160 KB

Each pixel leaks approximately **16 bytes of heap memory**.

- - -

### Proof of Concept

### Step 1: Create a Grayscale Image

```
python3 -c "from PIL import Image; Image.new('L', (3, 1), 128).save('poc.png')"

```

### Step 2: Run ascii-view

```
./ascii-view poc.png

```

### Step 3: Observe the Output

You’ll typically see corrupted grayscale values such as:

```
-2147483648

```

These values are a strong indicator that unintended heap data has been read and incorporated into floating-point calculations.

- - -

### Impact Assessment

### What Can Be Leaked?

* Heap memory contents
* Previously freed data
* File paths
* Environment variables
* Potentially sensitive strings

### Why Exploitation Is Difficult

* Leaked bytes are interpreted as **IEEE 754 doubles**
* Values overflow when converted to integers
* Output is lossy and transformed
* Original memory contents cannot be reliably reconstructed

**Real-world risk:** Low to Medium\
**Security classification:** Legitimate vulnerability, low exploitability

- - -

### Recommended Fix

The correct approach is to validate the number of channels before accessing pixel data.

```
double grayscale;

```

```
if (original->channels == 1) {
    grayscale = pixel[0];  // Already grayscale
} else if (original->channels >= 3) {
    grayscale = 0.2126 * pixel[0]
              + 0.7152 * pixel[1]
              + 0.0722 * pixel[2];
} else {
    fprintf(stderr, "Unsupported channel count: %zu\n", original->channels);
    free(data);
    return (image_t){0};
}
```

This ensures memory safety while preserving existing behavior.

- - -

### Responsible Disclosure Timeline

The issue was handled following standard disclosure best practices:

* **Day 0:** Private disclosure to the maintainer
* **Patch:** Implemented and reviewed
* **Fix Released:** Merged into the project
* **Public Disclosure:** After remediation



- - -

### References

* **Patch (Pull Request):**\
  <https://github.com/gouwsxander/ascii-view/pull/13>
*  **Fix Commit:**\
  <https://github.com/gouwsxander/ascii-view/commit/a8d6c42bc2bd702ddb80c8d19f73a2d62f1adec0>

- - -

### Final Thoughts

This vulnerability is a good example of why **memory safety issues should be taken seriously even when exploitation seems unlikely**. Today, it’s a low-risk heap over-read. Tomorrow, with a small refactor or new feature, it could become something far more dangerous.

Security research isn’t just about breaking things — it’s about strengthening them *before* attackers get the chance.

If you’re a maintainer, patch early.\
If you’re a researcher, keep digging.