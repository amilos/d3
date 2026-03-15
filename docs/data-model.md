# Data Model

## Entity–Relationship Overview

```
User ─────< Delegation >───── User
 │                               │
 │                               │
 ├──< Proposal                   │
 │       │                       │
 │       ├──< VotingOption        │
 │       │        │               │
 │       └──< Comment            │
 │                               │
 └──< Ballot >────── VotingOption
          │
          └── (delegated_from: User?)
```

---

## Entities

### User

Represents an authenticated platform participant.

| Column | Type | Constraints | Description |
|---|---|---|---|
| `id` | UUID | PK | Unique identifier |
| `email` | VARCHAR(255) | UNIQUE, NOT NULL | Login email |
| `password_hash` | VARCHAR(255) | NULLABLE | Null when using SSO only |
| `display_name` | VARCHAR(100) | NOT NULL | Public-facing name |
| `avatar_url` | TEXT | NULLABLE | Profile image URL |
| `role` | ENUM | NOT NULL | `citizen`, `admin`, `auditor` |
| `is_active` | BOOLEAN | NOT NULL, DEFAULT true | False = deactivated account |
| `mfa_secret` | VARCHAR(255) | NULLABLE | Encrypted TOTP secret |
| `created_at` | TIMESTAMPTZ | NOT NULL | Account creation timestamp |
| `updated_at` | TIMESTAMPTZ | NOT NULL | Last modification timestamp |

---

### Proposal

A question or motion put to a vote.

| Column | Type | Constraints | Description |
|---|---|---|---|
| `id` | UUID | PK | Unique identifier |
| `author_id` | UUID | FK → User | Creator of the proposal |
| `topic_id` | UUID | FK → Topic, NULLABLE | Optional topic category |
| `title` | VARCHAR(255) | NOT NULL | Short title |
| `description` | TEXT | NOT NULL | Full proposal text (Markdown) |
| `status` | ENUM | NOT NULL | `draft`, `open`, `closed`, `archived` |
| `voting_method` | ENUM | NOT NULL | `single_choice`, `approval`, `ranked_choice` |
| `anonymous_votes` | BOOLEAN | NOT NULL, DEFAULT false | Whether individual votes are hidden |
| `opens_at` | TIMESTAMPTZ | NULLABLE | Scheduled open time |
| `closes_at` | TIMESTAMPTZ | NULLABLE | Scheduled close time |
| `created_at` | TIMESTAMPTZ | NOT NULL | |
| `updated_at` | TIMESTAMPTZ | NOT NULL | |

---

### VotingOption

One selectable option within a proposal.

| Column | Type | Constraints | Description |
|---|---|---|---|
| `id` | UUID | PK | |
| `proposal_id` | UUID | FK → Proposal | Parent proposal |
| `label` | VARCHAR(255) | NOT NULL | Display text |
| `description` | TEXT | NULLABLE | Optional additional detail |
| `position` | INTEGER | NOT NULL | Display order |

---

### Ballot

A user's vote on a proposal. One ballot per user per proposal; updated if the user changes their vote.

| Column | Type | Constraints | Description |
|---|---|---|---|
| `id` | UUID | PK | |
| `proposal_id` | UUID | FK → Proposal, NOT NULL | |
| `voter_id` | UUID | FK → User, NOT NULL | The user whose vote this is |
| `option_id` | UUID | FK → VotingOption, NOT NULL | Chosen option |
| `weight` | DECIMAL(10,4) | NOT NULL, DEFAULT 1.0 | Voting weight (≥ 1.0 when delegation included) |
| `is_delegated` | BOOLEAN | NOT NULL, DEFAULT false | True if cast via delegation |
| `delegated_from_id` | UUID | FK → User, NULLABLE | Original delegator (if delegated) |
| `cast_at` | TIMESTAMPTZ | NOT NULL | When the ballot was recorded |
| `updated_at` | TIMESTAMPTZ | NOT NULL | |

**Unique constraint:** `(proposal_id, voter_id)`

---

### Delegation

Represents a delegation of voting power from one user (delegator) to another (delegate).

| Column | Type | Constraints | Description |
|---|---|---|---|
| `id` | UUID | PK | |
| `delegator_id` | UUID | FK → User, NOT NULL | User granting voting power |
| `delegate_id` | UUID | FK → User, NOT NULL | User receiving voting power |
| `scope` | ENUM | NOT NULL | `global`, `topic`, `proposal` |
| `topic_id` | UUID | FK → Topic, NULLABLE | Required when scope = `topic` |
| `proposal_id` | UUID | FK → Proposal, NULLABLE | Required when scope = `proposal` |
| `created_at` | TIMESTAMPTZ | NOT NULL | |
| `revoked_at` | TIMESTAMPTZ | NULLABLE | Null = currently active |

**Unique constraint:** `(delegator_id, scope, topic_id, proposal_id)` where `revoked_at IS NULL`

---

### Topic

An optional category used to scope delegations.

| Column | Type | Constraints | Description |
|---|---|---|---|
| `id` | UUID | PK | |
| `name` | VARCHAR(100) | UNIQUE, NOT NULL | E.g. "Environment", "Finance" |
| `description` | TEXT | NULLABLE | |
| `created_at` | TIMESTAMPTZ | NOT NULL | |

---

### Comment

User comment on a proposal.

| Column | Type | Constraints | Description |
|---|---|---|---|
| `id` | UUID | PK | |
| `proposal_id` | UUID | FK → Proposal, NOT NULL | |
| `author_id` | UUID | FK → User, NOT NULL | |
| `parent_id` | UUID | FK → Comment, NULLABLE | For threaded replies |
| `body` | TEXT | NOT NULL | Markdown content |
| `created_at` | TIMESTAMPTZ | NOT NULL | |
| `updated_at` | TIMESTAMPTZ | NOT NULL | |
| `deleted_at` | TIMESTAMPTZ | NULLABLE | Soft-delete timestamp |

---

### AuditEvent

Append-only event log entry.

| Column | Type | Constraints | Description |
|---|---|---|---|
| `id` | UUID | PK | |
| `sequence` | BIGINT | UNIQUE, NOT NULL | Monotonically increasing sequence number |
| `event_type` | VARCHAR(100) | NOT NULL | E.g. `ballot.cast`, `delegation.created` |
| `actor_id` | UUID | FK → User, NULLABLE | User who triggered the event |
| `payload` | JSONB | NOT NULL | Event-specific data |
| `previous_hash` | VARCHAR(64) | NOT NULL | SHA-256 of the previous event row |
| `hash` | VARCHAR(64) | NOT NULL | SHA-256 of this event row |
| `created_at` | TIMESTAMPTZ | NOT NULL | |

---

## Indexes

Key indexes beyond primary keys:

| Table | Columns | Type | Purpose |
|---|---|---|---|
| `Proposal` | `(status, opens_at, closes_at)` | B-Tree | Listing open/upcoming proposals |
| `Ballot` | `(proposal_id, option_id)` | B-Tree | Fast tally queries |
| `Delegation` | `(delegator_id)` WHERE `revoked_at IS NULL` | Partial B-Tree | Finding active delegations |
| `Delegation` | `(delegate_id)` WHERE `revoked_at IS NULL` | Partial B-Tree | Computing delegate weight |
| `AuditEvent` | `(sequence)` | B-Tree | Sequential log reads |
