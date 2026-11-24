# Secure FastAPI Template

A small FastAPI baseline with OWASP-oriented controls: validation, auth, rate limiting, security headers, and structured logging.

**Status:** planned. See [PROJECT.md](PROJECT.md) for architecture, OWASP mappings, and build order.

## What it includes

- Register / login with hashed passwords and bearer tokens
- Pydantic request validation
- Rate limiting
- CORS allowlist and security headers
- Structured logs with no sensitive fields
- Optional Bandit / Semgrep in CI

## Stack

Python, FastAPI, Pydantic v2, SlowAPI, OAuth2, SQLite, Docker.

## Security constraints

Do not commit real passwords, JWT signing keys, or `.env` files that contain secrets.
