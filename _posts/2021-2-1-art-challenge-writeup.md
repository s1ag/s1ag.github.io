---
title: "HacktheBox: Art Challenge"
excerpt: "A fun little steganography challenge!"
author_profile: true
toc: true
---


## Overview

Art is a relatively simple steganography challenge that imploys an esoteric programming language. At first glance, it appears as if it looks like some form of QR code. Upon further research, you learn that this is in fact a POC programming language that uses colors to encode data. 

## Files of Interest

- `art.zip`: container of contents
- `art.png`: image file which contains flag

## Tools Needed

- `piet interpreter`: preferably an online service like https://www.bertnase.de/npiet/npiet-execute.php 

## Step-by-Step Solution 


### Step 1: First Glance: WTF is this?

- After attempting to use stego tools, I determined it didn't contain hidden metadata.
- At the time of solving this challenge, the instructions weren't very specific. A user on the formums hinted to "Look up obscure and crazy programming languages" as a clue (mfw this challenge is in fact, incredibly obscure)

### Step 2: Identification: Sneaky

- After some searching, I finally determined a graphical bitmap-based language called `piet`. Upon looking at some examples, it was clear that this is what our given picture was.
- The .png is actually a compiled program and each square represents some obscure form of data.
- Now that we know what this is, we also know that there is some form of interpreter or compiler we can use. 

### Step 3: Solution: Ayyye

- After some google-fu, I found an online interpreter for piet at https://www.bertnase.de/npiet/npiet-execute.php 
- After uploading the png file, we're presented with a flag

```
HTB{****_********}
```

## Conclusion
All in all, this was a fun little introduction into stego. I think the most important skill learned in this challenge is the power of research. Thinking outside the box, looking for patterns, this all can be circumvented through careful enumeration of the problem.
