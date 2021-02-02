---
title: "HacktheBox: fs0ciety Challenge"
excerpt: "A fun little steganography challenge!"
author_profile: true
toc: true

---


## Overview


## Files of Interest

- `fs0ciety.zip`: password encrpyted zip file; intial starting point
- `sshcreds_datacenter.txt`; located within zip file; accessed after password is found

## Tools Needed

- `fcrackzip`: zip file password cracking utility 
- `rockyou.txt`: a large wordlist used for dictionary attacks
- `unzip`: command line tool to deinflate zipped files
- `base64 decoder`: utilized an online web service 
- `binary-to-text converter`: utilized an online web service
- `gzip`: used for files with .txt.gz extension

## Step-by-Step Solution

### Step 1: Enumeration

- Given our zip file, our`unzip` command was unsuccessful. Seems like this zip file is password protected.
  -  Since we have no password, we must run some sort of password cracking utility to bruteforce/dictionary attack the zip file.

### Step 2: Cracking
- Find rockyou.txt.gz in `/usr/share/wordlists`, decompress it and move to your directory of choice with `gzip -d rockyou.txt.gz && mv ~/HTB`

- Run `fcrackzip -u -D -p rockyou.txt` where the `-u` flag shows successful attempts, `-D` means Dictionary mode, and `-p` is the path to the wordlist.
- Once we successfully find the password, we open the folder and are presented with some ciphertext. Looking at the very end, we can assume this to be a base64 cipher as indicated by the `=` at the end of the file.
  - This isn't 100% foolproof, but given the difficulty of the challenge we can safely assume this to be true.


```text
*****************************************************************************************
Encrypted SSH credentials to access Blume ctOS : 

MDExMDEwMDEgMDExMDAxMTAgMDEwMTExMTEgMDExMTEwMDEgMDAxMTAwMDAgMDExMTAx
MDEgMDEwMTExMTEgMDExMDAwMTEgMDEwMDAwMDAgMDExMDExMTAgMDEwMTExMTEgMDAx
MDAxMDAgMDExMDExMDEgMDAxMTAwMTEgMDExMDExMDAgMDExMDExMDAgMDEwMTExMTEg
MDExMTAxMTEgMDExMDEwMDAgMDEwMDAwMDAgMDExMTAxMDAgMDEwMTExMTEgMDExMTAx
MDAgMDExMDEwMDAgMDAxMTAwMTEgMDEwMTExMTEgMDExMTAwMTAgMDAxMTAwMDAgMDEx
MDAwMTEgMDExMDEwMTEgMDEwMTExMTEgMDExMDEwMDEgMDExMTAwMTEgMDEwMTExMTEg
MDExMDAwMTEgMDAxMTAwMDAgMDAxMTAwMDAgMDExMDEwMTEgMDExMDEwMDEgMDExMDEx
MTAgMDExMDAxMTE=

*****************************************************************************************
```
### Step 3: Decryption 
- Using an online base64 decryption site like  <a href="https://gchq.github.io/CyberChef/">CyberChef</a>, we get some binary. 

```
01101001 01100110 01011111 01111001 00110000 01110101 01011111 01100011 01000000 01101110
01011111 00100100 01101101 00110011 01101100 01101100 01011111 01110111 01101000 01000000 
01110100 01011111 01110100 01101000 00110011 01011111 01110010 00110000 01100011 01101011 
01011111 01101001 01110011 01011111 01100011 00110000 00110000 01101011 01101001 01101110 
01100111
```

- Once again, using CyberChef we can plug in this binary to spit out our incredibly long flag!

```
HTB{**_***_***_*****_****_***_****_*********}
```