# Requirements

## Functional Requirements

### Identity and Access

| ID | Requirement |
|---|---|
| FR-ID-01 | A user must be able to register with an email address and password. |
| FR-ID-02 | A user must be able to authenticate via an external OAuth 2.0 / OpenID Connect provider (e.g., Google, GitHub). |
| FR-ID-03 | A user must be able to reset their password via an email link. |
| FR-ID-04 | An administrator must be able to deactivate or permanently delete a user account. |
| FR-ID-05 | The platform must support multi-factor authentication (TOTP). |

### Proposals

| ID | Requirement |
|---|---|
| FR-PR-01 | A verified user must be able to create a proposal with a title, description, and one or more voting options. |
| FR-PR-02 | A proposal must have a configurable open and close date/time. |
| FR-PR-03 | Only the proposal author or an administrator may edit a proposal while it is in *draft* state. |
| FR-PR-04 | A proposal must transition through the states: Draft → Open → Closed → Archived. |
| FR-PR-05 | A user must be able to comment on an open proposal. |

### Voting

| ID | Requirement |
|---|---|
| FR-VT-01 | A verified user must be able to cast a vote on any open proposal. |
| FR-VT-02 | A user must be able to change their vote while the proposal is still open. |
| FR-VT-03 | A user must be able to see the current tally of an open proposal in real time. |
| FR-VT-04 | Once a proposal closes, the final tally must be locked and publicly visible. |
| FR-VT-05 | A user's individual vote choice must be optionally anonymous (configurable per proposal). |

### Delegation

| ID | Requirement |
|---|---|
| FR-DL-01 | A user must be able to delegate their vote to another user globally (all topics). |
| FR-DL-02 | A user must be able to delegate their vote to another user for a specific topic. |
| FR-DL-03 | A user must be able to delegate their vote to another user for a specific proposal. |
| FR-DL-04 | A user must be able to revoke any delegation at any time. |
| FR-DL-05 | When a user who has delegated their vote also casts a direct vote, the direct vote takes precedence. |
| FR-DL-06 | The system must detect and reject circular delegation chains. |
| FR-DL-07 | A delegate must be able to see the total voting weight they currently hold. |

### Audit and Transparency

| ID | Requirement |
|---|---|
| FR-AU-01 | Every state-changing action must be recorded in the append-only audit log. |
| FR-AU-02 | Any user must be able to download the full audit log for a closed proposal. |
| FR-AU-03 | The audit log must be cryptographically verifiable (hash-chained events). |

---

## Non-Functional Requirements

### Performance

| ID | Requirement |
|---|---|
| NFR-PE-01 | The API must respond to 95% of read requests within 200 ms under a load of 1 000 concurrent users. |
| NFR-PE-02 | Real-time vote tally updates must be delivered to subscribed clients within 1 second. |
| NFR-PE-03 | The system must support at least 10 000 concurrent voters during a peak voting period. |

### Availability

| ID | Requirement |
|---|---|
| NFR-AV-01 | The platform must achieve 99.9% monthly uptime (excluding planned maintenance). |
| NFR-AV-02 | Planned maintenance windows must not exceed 30 minutes and must be announced 48 hours in advance. |

### Security

| ID | Requirement |
|---|---|
| NFR-SE-01 | All communication must be encrypted in transit using TLS 1.2 or higher. |
| NFR-SE-02 | Passwords must be hashed using bcrypt with a cost factor of at least 12. |
| NFR-SE-03 | The platform must pass an OWASP Top-10 vulnerability assessment before the first production release. |
| NFR-SE-04 | JWT access tokens must expire after 15 minutes; refresh tokens after 30 days. |

### Scalability

| ID | Requirement |
|---|---|
| NFR-SC-01 | The Core Service must scale horizontally without shared in-process state. |
| NFR-SC-02 | The database schema must support at least 1 million users and 100 000 proposals without architectural changes. |

### Usability

| ID | Requirement |
|---|---|
| NFR-US-01 | The web application must conform to WCAG 2.1 Level AA accessibility guidelines. |
| NFR-US-02 | The UI must be responsive and fully functional on screens 360 px wide and larger. |
| NFR-US-03 | Core flows (register, vote, delegate) must be completable in under 3 minutes by a first-time user. |

### Internationalisation

| ID | Requirement |
|---|---|
| NFR-I18N-01 | All user-facing strings must be externalised and translatable. |
| NFR-I18N-02 | The platform must support right-to-left (RTL) text layouts. |
