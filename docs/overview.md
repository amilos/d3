# Overview

## Purpose

d3 (Delegated Direct Democracy) is a platform that enables groups — from neighbourhoods to nation-states — to make collective decisions transparently and inclusively. It combines the simplicity of direct democracy with the practicality of representative systems through a fluid delegation mechanism.

## Core Idea

Every participant holds one vote. They may:

- **Vote directly** on any proposal at any time.
- **Delegate** their vote to a trusted person for all proposals, a specific topic, or a single proposal.
- **Revoke** a delegation at any time, including after the delegate has already voted (within the allowed revocation window).

This model — often called *liquid democracy* — gives each person maximum control while allowing specialists and trusted community members to represent those who prefer not to engage with every decision.

## Goals

1. **Inclusivity** — anyone with a verified identity can participate.
2. **Transparency** — the full delegation graph and vote tallies are publicly auditable.
3. **Privacy** — a voter's individual choice can optionally remain secret while the aggregate result remains verifiable.
4. **Resilience** — no single party controls the outcome; the system resists capture and manipulation.
5. **Accessibility** — the interface is usable on low-bandwidth mobile devices as well as desktop browsers.

## Non-Goals

- d3 is not a blockchain-based voting system (though a blockchain-backed audit log is a stretch goal).
- d3 does not manage voter registration or legal identity verification itself; it integrates with external identity providers.
- d3 does not replace legal election infrastructure; it is intended for organisational and civic deliberation.

## Stakeholders

| Role | Description |
|---|---|
| **Citizen / Member** | Any verified participant who holds voting rights |
| **Delegate** | A citizen who has received delegated voting power from others |
| **Proposal Author** | A citizen who submits a proposal for a vote |
| **Administrator** | Manages the platform instance, configures topics, and resolves disputes |
| **Auditor** | Reads-only access to the full vote log for transparency purposes |

## Milestones

| Milestone | Description |
|---|---|
| M1 — Specification | Architecture, data model, API, and UX specification complete |
| M2 — MVP | Single-topic direct voting with web UI |
| M3 — Delegation | Full liquid-democracy delegation graph |
| M4 — Audit | Public audit log and verifiability tools |
| M5 — Scale | Multi-tenant, multi-topic, federation support |
