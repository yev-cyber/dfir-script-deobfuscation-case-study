# Script Deobfuscation and Payload Analysis: DFIR Case Study

This repository presents a sanitized DFIR case study focused on multi-stage script deobfuscation and payload analysis. Starting from an obfuscated script, the investigation follows repeated Base64 decoding, XOR transformations, and AES decryption to reconstruct the payload and assess its behavior.

## Overview

This project demonstrates a practical malware-analysis workflow for unpacking a layered script and reviewing the resulting payload in a portfolio-safe format.

## What this project covers

- Multi-stage script deobfuscation
- Base64 decoding and string replacement
- XOR loop analysis
- AES decryption review
- Intermediate and final payload analysis
- IOC extraction
- Malware behavior assessment

## Key findings

- The script used several layers of obfuscation
- Decoding required Base64, XOR, and AES-based processing
- The downloaded `.ko` stage was an intermediate layer, not the final payload
- The final payload requested broad browser permissions
- The payload removed browser security headers such as CSP and X-Frame-Options
- Extracted indicators suggested suspicious infrastructure and staged malware delivery

## Tools and methods

- Static script review
- CyberChef
- Base64 and XOR analysis
- AES key / IV review
- Payload inspection
- IOC extraction
- Comparative malware research

## Skills demonstrated

- DFIR
- Malware analysis
- Script deobfuscation
- PowerShell analysis
- Payload reconstruction
- IOC analysis
- Technical reporting
