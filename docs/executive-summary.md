# Executive Summary

This project presents a sanitized DFIR case study focused on multi-stage script deobfuscation and payload analysis.

The investigation followed repeated Base64 decoding, XOR-based transformations, and AES decryption to reconstruct the payload and assess its behavior. Key findings included layered obfuscation, an intermediate `.ko` stage, suspicious browser permission requests, browser security-header removal, and indicators consistent with staged malware delivery.
