# TLS 1.3 Explained

## Goal

TLS provides:

- Confidentiality
- Integrity
- Authentication

## Identity

Servers prove identity using certificates.

## Key Establishment

TLS 1.3 uses ECDHE to establish a shared secret.

## Encryption

Once session keys are derived, AES-GCM encrypts traffic.
