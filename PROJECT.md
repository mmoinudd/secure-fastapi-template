# Secure FastAPI Template

Production-shaped secure API baseline that demonstrates OWASP mitigations.

**Status:** Planned — build after Python + OWASP training  
**Stack:** Python, FastAPI, Pydantic v2, SlowAPI, OAuth2, Bandit / Semgrep, Docker

## Goal

Ship a small but real API that shows secure application architecture, not just scanner usage. Second portfolio project and the stronger architecture demo.

## Why this project

- Proves OWASP knowledge in working code
- Shows auth, validation, rate limiting, logging, secret handling
- Easy to walk through in interviews with a simple diagram

## MVP features

1. Register / login with secure auth
2. Input validation with Pydantic
3. Rate limiting
4. CORS and security headers
5. No secrets in code
6. Structured logging (no sensitive data)
7. Optional Bandit/Semgrep in CI
8. Simple security status page

## Architecture

```
Client
  ↓
API layer (FastAPI)
  ↓
Auth / rate limit / validation
  ↓
Service layer
  ↓
Datastore (SQLite first)
```

Security controls live at the edge. Business logic stays separate.

## OWASP mappings

- A01 Broken access control — auth on protected routes
- A02 Cryptographic failures — hashed passwords, HTTPS in deploy notes
- A03 Injection — Pydantic validation, no string-built queries
- A04 Insecure design — threat notes in README
- A05 Security misconfiguration — headers, CORS allowlist
- A07 Auth failures — rate limit, token expiry
- A09 Logging failures — audit log without secrets

## Build order

1. Bare FastAPI app + health check
2. Pydantic models and validation
3. Auth (OAuth2 password bearer)
4. Rate limiting
5. Logging
6. One protected resource endpoint
7. Security README + short threat model
8. Docker + local run instructions
9. Optional later: AWS deploy

## Interview talking points

- Data flow and trust boundaries
- Why validation belongs at the edge
- What you would add for production (WAF, vault, observability)
- How other teams would reuse this template

## Do not commit

- Real passwords
- JWT signing keys
- `.env` with secrets
