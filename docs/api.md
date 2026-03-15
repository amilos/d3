# API Specification

All endpoints are served over HTTPS. The base URL for the v1 API is:

```
https://<host>/api/v1
```

## Authentication

Most endpoints require a valid **JWT Bearer token** in the `Authorization` header:

```
Authorization: Bearer <access_token>
```

Access tokens expire after **15 minutes**. Use the refresh token endpoint to obtain a new access token.

---

## Endpoints

### Authentication

#### `POST /auth/register`

Register a new user account.

**Request body**

```json
{
  "email": "alice@example.com",
  "password": "S3cur3P@ss!",
  "display_name": "Alice"
}
```

**Response `201 Created`**

```json
{
  "id": "uuid",
  "email": "alice@example.com",
  "display_name": "Alice",
  "created_at": "2026-01-01T12:00:00Z"
}
```

---

#### `POST /auth/login`

Obtain access and refresh tokens.

**Request body**

```json
{
  "email": "alice@example.com",
  "password": "S3cur3P@ss!"
}
```

**Response `200 OK`**

```json
{
  "access_token": "eyJ...",
  "refresh_token": "eyJ...",
  "expires_in": 900
}
```

---

#### `POST /auth/refresh`

Exchange a refresh token for a new access token.

**Request body**

```json
{
  "refresh_token": "eyJ..."
}
```

**Response `200 OK`** — same shape as `/auth/login`.

---

#### `POST /auth/logout`

Revoke the current refresh token.

**Response `204 No Content`**

---

### Users

#### `GET /users/me`

Return the authenticated user's profile.

**Response `200 OK`**

```json
{
  "id": "uuid",
  "email": "alice@example.com",
  "display_name": "Alice",
  "role": "citizen",
  "created_at": "2026-01-01T12:00:00Z"
}
```

---

#### `PATCH /users/me`

Update the authenticated user's profile.

**Request body** (all fields optional)

```json
{
  "display_name": "Alice B.",
  "avatar_url": "https://example.com/avatar.png"
}
```

**Response `200 OK`** — updated user object.

---

### Topics

#### `GET /topics`

List all topics.

**Response `200 OK`**

```json
[
  { "id": "uuid", "name": "Environment", "description": "..." },
  { "id": "uuid", "name": "Finance", "description": "..." }
]
```

---

### Proposals

#### `GET /proposals`

List proposals. Supports query parameters:

| Parameter | Type | Description |
|---|---|---|
| `status` | string | Filter by status (`draft`, `open`, `closed`, `archived`) |
| `topic_id` | UUID | Filter by topic |
| `page` | integer | Page number (default: 1) |
| `per_page` | integer | Results per page (default: 20, max: 100) |

**Response `200 OK`**

```json
{
  "data": [ { "id": "uuid", "title": "...", "status": "open", ... } ],
  "pagination": { "page": 1, "per_page": 20, "total": 42 }
}
```

---

#### `POST /proposals`

Create a new proposal (authenticated users only).

**Request body**

```json
{
  "title": "Should we plant more trees in the park?",
  "description": "Full description in **Markdown**.",
  "topic_id": "uuid",
  "voting_method": "single_choice",
  "anonymous_votes": false,
  "opens_at": "2026-02-01T08:00:00Z",
  "closes_at": "2026-02-08T20:00:00Z",
  "options": [
    { "label": "Yes", "position": 1 },
    { "label": "No", "position": 2 },
    { "label": "Abstain", "position": 3 }
  ]
}
```

**Response `201 Created`** — full proposal object.

---

#### `GET /proposals/:id`

Get a single proposal with its options and current tally.

**Response `200 OK`**

```json
{
  "id": "uuid",
  "title": "...",
  "status": "open",
  "options": [
    { "id": "uuid", "label": "Yes", "vote_count": 120, "vote_weight": 145.5 }
  ],
  "total_voters": 200,
  "total_weight": 230.0
}
```

---

#### `PATCH /proposals/:id`

Update a proposal (author or admin only; draft status required for most fields).

---

#### `DELETE /proposals/:id`

Archive a proposal (admin only).

---

### Voting

#### `POST /proposals/:id/ballots`

Cast or update a vote on a proposal.

**Request body**

```json
{
  "option_id": "uuid"
}
```

**Response `200 OK`**

```json
{
  "ballot_id": "uuid",
  "proposal_id": "uuid",
  "option_id": "uuid",
  "weight": 3.0,
  "cast_at": "2026-02-03T10:15:00Z"
}
```

---

#### `GET /proposals/:id/ballots/me`

Get the authenticated user's ballot for a proposal.

---

### Delegations

#### `GET /delegations`

List the authenticated user's active delegations (outbound).

---

#### `POST /delegations`

Create a new delegation.

**Request body**

```json
{
  "delegate_id": "uuid",
  "scope": "topic",
  "topic_id": "uuid"
}
```

**Response `201 Created`** — delegation object.

---

#### `DELETE /delegations/:id`

Revoke a delegation.

**Response `204 No Content`**

---

### Audit Log

#### `GET /audit`

List audit events. Supports `page` and `per_page` query parameters.

**Response `200 OK`**

```json
{
  "data": [
    {
      "sequence": 1,
      "event_type": "ballot.cast",
      "actor_id": "uuid",
      "payload": { "proposal_id": "uuid", "option_id": "uuid" },
      "hash": "sha256hex",
      "previous_hash": "sha256hex",
      "created_at": "2026-02-03T10:15:00Z"
    }
  ],
  "pagination": { "page": 1, "per_page": 50, "total": 9999 }
}
```

---

## Error Responses

All error responses share this structure:

```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Human-readable description.",
    "details": [ { "field": "email", "message": "Invalid email address." } ]
  }
}
```

Common HTTP status codes:

| Code | Meaning |
|---|---|
| 400 | Bad Request — invalid input |
| 401 | Unauthorized — missing or invalid token |
| 403 | Forbidden — insufficient permissions |
| 404 | Not Found |
| 409 | Conflict — e.g. duplicate vote |
| 422 | Unprocessable Entity — business rule violation |
| 429 | Too Many Requests — rate limit exceeded |
| 500 | Internal Server Error |
