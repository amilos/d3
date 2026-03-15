# Security

## Threat Model

The primary assets to protect are:

1. **Vote integrity** — votes must reflect the genuine intentions of eligible voters.
2. **Vote secrecy** — on anonymous proposals, individual choices must not be disclosed.
3. **User privacy** — personal data must be handled in accordance with applicable law.
4. **Audit log integrity** — the event log must be tamper-evident.
5. **Platform availability** — the system must be resilient to denial-of-service attacks.

---

## Authentication and Session Management

| Control | Implementation |
|---|---|
| Password hashing | bcrypt, cost factor ≥ 12 |
| Token format | JWT (RS256, asymmetric signing) |
| Access token lifetime | 15 minutes |
| Refresh token lifetime | 30 days (rotated on each use) |
| MFA | TOTP (RFC 6238); mandatory for administrators |
| Account lockout | Exponential backoff after 5 consecutive failed login attempts |
| Session revocation | Refresh token blocklist in Redis |

---

## Transport Security

- All traffic is encrypted with **TLS 1.2 or higher**; TLS 1.0 and 1.1 are disabled.
- HTTP Strict Transport Security (HSTS) is enforced with a `max-age` of at least 1 year.
- Certificates are obtained via Let's Encrypt and rotated automatically.

---

## Input Validation and Injection Prevention

- All API inputs are validated against strict JSON Schema definitions before reaching business logic.
- The ORM (Prisma) uses parameterised queries exclusively; raw SQL is forbidden.
- User-supplied content rendered in the UI is escaped by the frontend framework (React) and additionally sanitised server-side with a whitelist-based HTML sanitiser before storage.
- File uploads are not accepted at this time; this threat surface does not apply.

---

## Authorisation

Access control is enforced at the service layer (not only at the API Gateway):

| Role | Permissions |
|---|---|
| `citizen` | Read all proposals; vote; create proposals; manage own delegations; read public audit log |
| `admin` | All citizen permissions; manage users; manage topics; force-close proposals; read full audit log |
| `auditor` | Read-only access to proposals, tallies, and full audit log |

Ownership checks are applied in addition to role checks (e.g., only the proposal author or an admin may edit a draft proposal).

---

## Vote Secrecy

For proposals configured with `anonymous_votes = true`:

- The API never returns the `option_id` of an individual ballot to any caller, including admins.
- Database-level row security policies prevent direct reads of `Ballot.option_id` outside the voting module.
- The audit log records the event with the `option_id` **encrypted** with a proposal-specific symmetric key. The key is held in escrow and can only be released by a quorum of administrators after the proposal closes, if legally required.

---

## Audit Log Integrity

The audit log uses a **hash chain**:

1. Each event row includes a `hash` field: `SHA-256(sequence || event_type || actor_id || payload || previous_hash)`.
2. Any modification to a past event changes its hash and breaks the chain from that point onward.
3. The latest hash is published publicly (e.g., on a canary page) so external auditors can verify it matches the chain tip.

---

## Delegation Security

- A user cannot delegate to themselves.
- The system prevents circular delegation chains (see [Delegation Model](delegation.md)).
- Delegation weight is computed server-side; the client never supplies weight values.
- Delegations are scoped and cannot be widened by the delegate.

---

## Rate Limiting

| Endpoint | Limit |
|---|---|
| `POST /auth/login` | 10 requests / minute / IP |
| `POST /auth/register` | 5 requests / minute / IP |
| `POST /proposals/:id/ballots` | 20 requests / minute / user |
| All other endpoints | 200 requests / minute / user |

Exceeded limits return `429 Too Many Requests`.

---

## Dependency Management

- All third-party dependencies are pinned to exact versions in lock files.
- Automated vulnerability scanning (e.g., Dependabot, `npm audit`) runs on every pull request.
- Critical or high-severity vulnerabilities block merging.

---

## Security Testing

| Activity | Frequency |
|---|---|
| SAST (static analysis) | Every CI run |
| Dependency vulnerability scan | Every CI run + daily |
| DAST (OWASP ZAP) | Before each release |
| Manual penetration test | Annually and before M4 (first public release) |
| OWASP Top-10 review | Before first production release |

---

## Incident Response

In the event of a security incident:

1. The on-call engineer isolates the affected service(s).
2. The security lead performs an initial triage within 2 hours.
3. Affected users are notified within 72 hours in accordance with GDPR Article 33/34.
4. A post-mortem is published publicly within 30 days.
