# Script Deobfuscation and Payload Analysis: DFIR Case Study

This repository presents a sanitized DFIR case study focused on multi-stage script deobfuscation and payload analysis. Beginning with an obfuscated script, the investigation traces each decoding stage through repeated Base64 transformations, XOR-based logic, and AES decryption before analyzing the resulting payload. The case study highlights execution flow reconstruction, malicious behavior identification, suspicious permission usage, browser security-control bypass techniques, IOC extraction, and an evidence-based malware assessment.

## Overview

This project documents a structured malware-analysis workflow used to unpack and understand a layered, staged payload delivery chain. The analysis starts with an obfuscated initial script, follows the intermediate decoding and decryption stages, and ends with inspection of the final payload and its observable behaviors.

The goal of this repository is to demonstrate practical DFIR and malware-analysis methodology in a portfolio-safe format without exposing internal operational details.

## What this project covers

- Multi-stage script deobfuscation
- Repeated Base64 decoding
- Character substitution and string replacement
- XOR loop analysis
- AES decryption workflow review
- Intermediate payload analysis
- Final payload behavior assessment
- IOC and URL extraction
- Browser-focused abuse analysis
- Malware-family hypothesis and reporting

## Investigation workflow

The analysis followed these major stages:

1. Review of the initial obfuscated script
2. Decoding of embedded Base64 content
3. Character replacement and XOR-based transformations
4. Extraction of intermediate URLs and downloaded payload stages
5. Review of secondary obfuscated content
6. Identification of AES decryption logic, key material, IV, mode, and padding
7. Reconstruction of the final payload
8. Behavioral review of payload capabilities, permissions, and infrastructure
9. Extraction of relevant indicators and production of an analyst assessment

## Key findings

- The script used multiple layers of obfuscation rather than a single encoding stage
- Decoding required repeated Base64 processing, XOR transformations, and AES decryption
- The downloaded `.ko` stage functioned as an intermediate step rather than the final payload
- The final payload showed browser-focused abuse patterns and extensive permission requests
- The payload removed multiple browser security headers, indicating clear malicious intent
- Extracted indicators suggested links to suspicious infrastructure and crypto-related activity
- The overall behavior was consistent with staged malware delivery and follow-on payload execution

## Technical highlights

### 1. Multi-layer obfuscation

The initial script did not rely on one simple obfuscation method. Instead, it chained together multiple techniques to slow analysis and hide the true execution flow.

Observed techniques included:

- Base64 encoding
- Character substitution
- XOR-based decoding loops
- Encrypted payload stages
- Further Base64-based wrapping in later stages

### 2. XOR-based transformations

The investigation identified several XOR operations used to decode embedded content. This helped reveal intermediate strings and URLs that were not visible in the raw script.

### 3. AES decryption stage

A later stage of the script introduced AES-based decryption using extracted key material and IV values. This stage was critical for reconstructing the actual payload logic and understanding what the malware was attempting to execute.

### 4. Intermediate payload staging

The downloaded `ComAm.ko` file was not the final payload. Instead, it acted as an intermediate deobfuscation and staging layer that had to be unpacked further before the final behavior could be assessed.

### 5. Final payload behavior

After reconstruction, the final payload exposed several high-risk behaviors, including:

- Broad browser permission requests
- Removal of browser-enforced security protections
- Suspicious use of hashing and encoding routines
- Access to browser and system context
- Potential persistence, exfiltration, and command-and-control activity

## Security-relevant behaviors identified

The reconstructed payload and associated logic suggested the following malicious or suspicious capabilities:

- Requests for extensive sensitive browser permissions
- Attempts to interact with cookies, history, tabs, clipboard, and scripting features
- Removal of browser security headers such as CSP and X-Frame-Options
- Possible persistence and replication behavior
- Potential registry modification
- Possible interaction with command-and-control infrastructure
- Potential exfiltration of sensitive information
- Social-media and Google-account related interaction patterns

## Why the browser security-header removal matters

One of the most important findings in this case was the removal of key browser-enforced protections, including:

- Content-Security-Policy (CSP)
- X-Content-Security-Policy
- X-WebKit-CSP
- Content-Security-Policy-Report-Only
- X-Frame-Options

These controls are important because they help prevent:

- Cross-site scripting (XSS)
- Clickjacking
- Unauthorized content injection
- Framing abuse
- Certain classes of malicious browser manipulation

Their removal strongly increased confidence that the payload was designed for malicious browser-centric activity.

## Indicators and infrastructure

During analysis, the investigation extracted suspicious URLs and related indicators from multiple decoding stages. Some infrastructure appeared related to cryptocurrency and mining ecosystems, while other elements were linked to payload delivery and staging.

In this public portfolio version, indicators are summarized at a high level and may be partially redacted or defanged where appropriate.

## Malware assessment

Based on the decoded logic, payload behavior, and observed infrastructure, the investigation produced a tentative malware-family assessment. While attribution was not treated as definitive, the behavioral overlap was consistent with a staged loader-style threat capable of delivering follow-on payloads, stealing information, and enabling broader malicious activity.

## Analyst approach

This project demonstrates how I approach malware analysis in practice:

- Break the script into logical stages instead of treating it as one block
- Identify where encoding ends and encryption begins
- Track variable relationships and execution flow
- Reconstruct intermediate artifacts before jumping to conclusions
- Focus on observable behavior, not just signatures or names
- Separate confidence-backed findings from tentative hypotheses
- Summarize technical outcomes in a format suitable for defenders and stakeholders

## Tools and methods

The workflow used in this case included:

- Static script review
- CyberChef-based decoding and transformation
- Base64 and XOR analysis
- AES key / IV extraction and decryption review
- Payload inspection
- IOC extraction and documentation
- Comparative malware research
- Supplemental scripting for validation and decoding support

