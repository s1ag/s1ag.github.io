---
layout: single
title: "Hack The Box: art Writeup"
categories: [Challenge, HTB]
header:
    overlay_image: /assets/images/homepageHeader.jpg
toc: true

---


## Overview

> Can you find the flag?

## Files of Interest
- `art.zip`: container of contents
- `art.png`: image file which contains flag

## Tools Needed

- `piet interpreter`: preferably an online service like https://www.bertnase.de/npiet/npiet-execute.php 

## Step-by-Step Solution 
---

### Step 1: WTF is This?
- After attempting to use stego tools, I determined it didn't contain hidden metadata
- I had to reference the forums because of how vague the instructions were
- A user hinted to "Look up obscure and crazy programming languages" as a clue (mfw this challenge is incredibly obscure)

### Step 2: Identification
- After some brief searching, determined a graphical bitmap-based language called `piet`
- The .png is a compiled program and each square represents some obscure form of data
- Determined that I needed some form of interpreter or compiler

### Step 3: Solution
- After googling, found an online interpreter for piet at https://www.bertnase.de/npiet/npiet-execute.php 
    - Its an extremely obscure language, so documentation is limited
- After uploading the png file, we're presented with a flag
```
HTB{p137_m0ndr14n}? ? ??$? ?...
```
- done :)

