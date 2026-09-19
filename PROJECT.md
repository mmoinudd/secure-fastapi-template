# Secure FastAPI Template

Secure API baseline that implements common OWASP mitigations in working code.

**Status:** Planned
**Stack:** Python, FastAPI, Pydantic v2, SlowAPI, OAuth2, Bandit / Semgrep, Docker, SQLite

## Goal

A small, reusable API that shows secure application architecture: auth, validation, rate limiting, headers, logging, and secret handling. Security controls live at the edge; business logic stays separate.

## MVP features

1. Register / login with hashed-password auth
2. Input validation with Pydantic
3. Rate limiting
4. CORS allowlist and security headers
5. No secrets in code
6. Structured logging with no sensitive fields
7. Optional Bandit / Semgrep in CI
8. Security status page

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

## OWASP mappings

- A01 Broken access control — auth on protected routes
- A02 Cryptographic failures — hashed passwords; HTTPS in deploy notes
- A03 Injection — Pydantic validation; no string-built queries
- A04 Insecure design — threat notes in README
- A05 Security misconfiguration — headers, CORS allowlist
- A07 Auth failures — rate limit, token expiry
- A09 Logging failures — audit log without secrets

## Design notes

- Validation belongs at the edge so untrusted input never reaches service or data layers.
- Production follow-ons: WAF, secrets vault, centralized observability, stronger identity provider.
- Template is meant to be copied as a starting point for other services.

## Build order

1. Bare FastAPI app and health check
2. Pydantic models and validation
3. Auth (OAuth2 password bearer)
4. Rate limiting
5. Logging
6. One protected resource endpoint
7. Security README and short threat model
8. Docker and local run instructions
9. Optional: hosted deploy

## Do not commit

- Real passwords
- JWT signing keys
- `.env` files with secrets
