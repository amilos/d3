# Architecture

## High-Level Design

d3 follows a layered, service-oriented architecture with clear separation between the presentation, application, and data layers.

```
┌────────────────────────────────────────────────────┐
│                   Clients                          │
│   Web App (SPA)  │  Mobile PWA  │  CLI / API       │
└────────────────────────┬───────────────────────────┘
                         │ HTTPS / REST + WebSocket
┌────────────────────────▼───────────────────────────┐
│                  API Gateway                        │
│   Auth  │  Rate Limiting  │  Routing  │  TLS        │
└────────────────────────┬───────────────────────────┘
                         │
          ┌──────────────┼──────────────┐
          │              │              │
┌─────────▼──────┐ ┌─────▼──────┐ ┌────▼────────────┐
│  Identity      │ │  Core      │ │  Audit Log      │
│  Service       │ │  Service   │ │  Service        │
└─────────┬──────┘ └─────┬──────┘ └────┬────────────┘
          │              │              │
┌─────────▼──────────────▼──────────────▼────────────┐
│                  Data Layer                         │
│   PostgreSQL (primary)  │  Redis (cache/sessions)  │
└────────────────────────────────────────────────────┘
```

## Components

### API Gateway

- Entry point for all external traffic.
- Responsible for TLS termination, request routing, rate limiting, and authentication token validation.
- Emits structured access logs to the audit pipeline.

### Identity Service

- Manages user accounts, credentials, and session tokens (JWT).
- Integrates with external identity providers (OAuth 2.0 / OpenID Connect).
- Issues scoped tokens that encode the user's roles and verified attributes.

### Core Service

The main application service. Exposes the REST API (see [API Specification](api.md)) and contains:

- **Proposal module** — CRUD for proposals, lifecycle management (draft → open → closed → archived).
- **Delegation module** — manages the delegation graph; detects cycles; propagates vote weight.
- **Voting module** — records ballots, resolves delegated votes, and computes tallies.
- **Notification module** — sends emails and push notifications for relevant events.

### Audit Log Service

- Append-only store of every state-changing event (proposal created, vote cast, delegation granted/revoked, etc.).
- Events are cryptographically chained (each event includes the hash of the previous event) to detect tampering.
- Exposes a public read API so that any auditor can verify the integrity of the log.

## Data Storage

| Store | Purpose |
|---|---|
| PostgreSQL | Primary relational store for all mutable application state |
| Redis | Session cache, real-time vote-count cache, message queue back-end |

## Deployment Topology

See [Deployment](deployment.md) for detailed infrastructure diagrams.

A minimal single-node deployment runs all services as Docker containers managed by Docker Compose. A production deployment uses Kubernetes with horizontal pod autoscaling on the Core Service.

## Technology Choices

| Concern | Choice | Rationale |
|---|---|---|
| API | REST over HTTPS | Broad client compatibility |
| Real-time updates | WebSocket (via API Gateway) | Live tally updates |
| Auth tokens | JWT (RS256) | Stateless verification |
| Primary language | TypeScript (Node.js) | Strong typing, large ecosystem |
| Database ORM | Prisma | Type-safe queries, migration tooling |
| Container runtime | Docker | Reproducible environments |
| Orchestration | Kubernetes | Horizontal scaling, rolling deploys |

## Security Boundaries

- The Core Service never trusts data from the client directly; all inputs are validated and sanitised at the API boundary.
- The Audit Log Service is write-only from the Core Service's perspective; it does not accept writes from any other source.
- Secrets (database passwords, signing keys) are stored in a secrets manager (e.g., HashiCorp Vault or Kubernetes Secrets) and never in source code or environment files committed to version control.
