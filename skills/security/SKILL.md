---
name: security-and-hardening
description: "Threat model first with STRIDE. Three-tier boundary system for security-sensitive operations. Apply before every code change."
---

# Security and Hardening

## When to Use

- Before writing code that handles user input, auth, or sensitive data
- When reviewing code that touches security boundaries
- Before deploying to production
- When adding new API endpoints or modifying existing ones
- When integrating third-party libraries or services

## Threat Model First: STRIDE

Always start with a threat model. Don't bolt security on after the fact.

| Threat | Description | Question to Ask |
|--------|-------------|-----------------|
| **S**poofing | Identity verification failure | Can an attacker pretend to be someone they're not? |
| **T**ampering | Data integrity violation | Can data be modified in transit or at rest? |
| **R**epudiation | Denying actions taken | Can a user deny performing an action? |
| **I**nformation Disclosure | Data exposure | Can sensitive data leak to unauthorized parties? |
| **D**enial of Service | Availability attacks | Can an attacker make the system unavailable? |
| **E**levation of Privilege | Unauthorized access | Can a user gain higher privileges than intended? |

## Three-Tier Boundary System

### Always Do (Green Zone)
These require no approval — just do them:

- Validate and sanitize all user input
- Use parameterized queries (never string concatenation for SQL)
- Hash passwords with bcrypt, argon2, or scrypt (never MD5/SHA1)
- Use HTTPS everywhere in production
- Set secure, HttpOnly, SameSite cookie flags
- Apply principle of least privilege to database access
- Never log secrets, tokens, or passwords
- Use established crypto libraries, never roll your own

### Ask First (Yellow Zone)
These need explicit approval or discussion before proceeding:

- Accepting credentials or secrets from users
- Modifying authentication or authorization logic
- Adding new external service integrations
- Changing session management
- Modifying CORS or CSP policies
- Storing data in new locations or with new encryption
- Adding admin-only endpoints or features

### Never Do (Red Zone)
These are always wrong — reject them immediately:

- Hardcode secrets, API keys, or passwords in source code
- Store passwords in plaintext or reversible encryption
- Use eval() or exec() with untrusted input
- Commit .env files, credentials, or private keys to repositories
- Skip CSRF protection on state-changing endpoints
- Disable security features for convenience
- Trust client-side validation as the only input validation
- Use deprecated crypto algorithms (MD5, SHA1, DES, RC4)

## Common Vulnerability Patterns

| Vulnerability | Prevention |
|---------------|------------|
| SQL Injection | Parameterized queries, ORM usage, input validation |
| XSS (Cross-Site Scripting) | Output encoding, Content Security Policy, input sanitization |
| Auth Bypass | Proper middleware, session validation, token verification |
| CSRF | CSRF tokens, SameSite cookies, origin validation |
| Path Traversal | Input sanitization, chroot, path canonicalization |
| Insecure Deserialization | Validate input types, avoid pickle/eval, use safe parsers |
| Sensitive Data Exposure | Encryption at rest/transit, minimal data collection |
| Broken Access Control | Server-side authorization checks, role-based access |

## Pre-Commit Security Checklist

- [ ] No secrets in source code?
- [ ] Input validation present for all user inputs?
- [ ] Parameterized queries used for database access?
- [ ] Authentication checks on all protected endpoints?
- [ ] No sensitive data in logs?
- [ ] Dependencies scanned for known vulnerabilities?
- [ ] Error messages don't leak internal details?
- [ ] File uploads validated (type, size, content)?

## Quick Decision Guide

```
User input → Validate → Sanitize → Use
Database query → Parameterize → Never concatenate
Password → Hash with argon2/bcrypt → Store hash only
Secret → Environment variable → Rotate if exposed
Error → Generic message to user → Detailed log server-side
```
