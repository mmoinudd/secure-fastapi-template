# Secure FastAPI Template

A small FastAPI baseline with OWASP-oriented controls: validation, auth, rate limiting, security headers, and structured logging.

**Status:** planned. Implementation has not started. See [PROJECT.md](PROJECT.md) for the full plan and build order.

## What it includes

- Register / login with hashed passwords and bearer tokens
- Pydantic request validation
- Rate limiting
- CORS allowlist and security headers
- Structured logs with no sensitive fields
- Optional Bandit / Semgrep in CI
- A security status page

## Stack

- Python 3.11+
- FastAPI
- Pydantic v2
- SlowAPI (rate limiting)
- OAuth2 password bearer
- SQLite (first datastore)
- Docker
- Bandit and Semgrep (optional CI)

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

Security controls live at the edge. Business logic stays in the service layer and never sees unvalidated input.

## Short threat model

Assets: user credentials, bearer tokens, and any data behind a protected route.

Trusted boundary: the FastAPI edge (validation, auth, rate limit, headers). Everything past that boundary is treated as internal.

Main risks and controls:

| Risk | Control |
|------|---------|
| Broken access control | Auth required on protected routes; no client-supplied user id for authorization |
| Weak passwords / token theft | Hashed passwords, token expiry, rate limit on login |
| Injection | Pydantic validation; no string-built SQL |
| Misconfiguration | Explicit CORS allowlist and security headers; secrets outside the repo |
| Sensitive data in logs | Structured logging with sensitive fields dropped |

Out of scope for the first version: WAF, a secrets vault, a full identity provider, and production HTTPS termination. Those are notes for a later deploy, not part of the MVP.

## Planned layout

```
app/
  main.py            # FastAPI app, middleware, headers
  models.py          # Pydantic request/response models
  auth.py            # register, login, token checks
  routes.py          # public and protected endpoints
  services.py        # business logic
  db.py              # SQLite access
  logging_config.py  # structured logs, no secrets
Dockerfile
requirements.txt
.env.example         # placeholders only, never real secrets
```

## Getting started

Not runnable yet. First implementation step is a bare FastAPI app with a health check.

Once that lands, the local path will be:

```bash
python -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install -r requirements.txt
uvicorn app.main:app --reload
```

Health check will be `GET /health`.

## Security constraints

Do not commit:

- Real passwords
- JWT signing keys
- `.env` files that contain secrets

Commit `.env.example` with empty placeholders only.

## License

No license file yet. One will be added when the first code lands.
