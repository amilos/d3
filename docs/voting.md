# Voting Mechanisms

## Overview

d3 supports multiple voting methods per proposal. The method is chosen by the proposal author when creating a proposal and cannot be changed once the proposal moves out of *draft* status.

---

## Voting Methods

### Single Choice

The simplest method. Each voter (or delegate) selects exactly one option. The winner is the option with the highest total weight.

**Tally formula:**  
`option_weight = Σ weight of all ballots selecting that option`

**Tie-breaking:** If two or more options share the highest weight, the result is a tie. The proposal author may specify a tie-breaking rule (e.g., the option listed first wins, or the proposal is re-opened for a run-off).

---

### Approval Voting

Each voter may select any number of options (including all or none). The option(s) with the highest approval weight win.

**Use case:** Selecting multiple acceptable candidates or policies simultaneously.

---

### Ranked Choice (Instant Run-off)

Each voter ranks some or all options in order of preference. The winner is determined through successive elimination:

1. Count first-preference votes.
2. If no option has > 50% of the total weight, eliminate the option with the fewest votes.
3. Redistribute eliminated option's ballots to each voter's next-ranked remaining option.
4. Repeat until one option exceeds 50% or all remaining options are tied.

**Delegation note:** When a delegate votes with ranked-choice, their full weight applies uniformly to the ranking they submit.

---

## Ballot Lifecycle

```
[Proposal Opens]
      │
      ▼
Voter casts ballot ──► Ballot recorded (status: active)
      │
      ▼ (optional)
Voter changes vote ──► Previous ballot superseded, new ballot recorded
      │
      ▼
[Proposal Closes]
      │
      ▼
Tally computed (including delegation weight resolution)
      │
      ▼
Result locked and published
```

---

## Tally Computation

Tallies are computed **lazily** in near-real time for display purposes during voting, and **definitively** at proposal close.

### Definitive Tally (at close)

1. Load all active (non-superseded) ballots for the proposal.
2. For each ballot, resolve delegation weight using the delegation graph (see [Delegation Model](delegation.md)).
3. Subtract any delegated weight for delegators who cast a direct ballot.
4. Sum weights by option.
5. Apply the voting method's winner-determination rules.
6. Write the final result to the `ProposalResult` record.
7. Emit a `proposal.closed` audit event with the full tally.

### Live Tally (during voting)

The live tally is an approximation served from a Redis cache, updated within 1 second of each ballot change. It uses pre-aggregated option weights without full delegation resolution (for performance), so may differ slightly from the final definitive tally.

---

## Anonymous Proposals

When `anonymous_votes = true` on a proposal:

- Individual ballot choices are not exposed via the API to any user (including admins).
- The voter ID is still stored internally for audit and deduplication purposes.
- The public audit log records the event type and timestamp but omits the option chosen.
- The final tally is still published.

---

## Vote Integrity

- **One ballot per voter per proposal** — enforced by a database unique constraint on `(proposal_id, voter_id)`.
- **Immutable closed proposals** — once a proposal closes, its result is locked; no further ballot changes or new ballots are accepted.
- **Audit trail** — every ballot cast or changed produces an append-only audit event (see [Data Model](data-model.md)).
- **Weight integrity** — delegation weight is computed server-side; clients supply only their option choice, never their weight.
