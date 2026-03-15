# Delegation Model

Delegation (also called *liquid democracy* or *proxy voting*) is the core differentiator of d3. This document describes the delegation rules, data representation, and computation.

## Concepts

| Term | Definition |
|---|---|
| **Delegator** | A citizen who assigns their voting power to another user |
| **Delegate** | A user who receives voting power from one or more delegators |
| **Delegation weight** | The number of votes a user controls (their own + all transitively delegated votes) |
| **Direct vote** | A ballot cast personally by a voter, which always overrides any active delegation |
| **Transitive delegation** | A delegates to B, B delegates to C — C holds the voting weight of A (unless B votes) |

## Scope Hierarchy

Delegations are evaluated from most specific to least specific:

```
proposal (most specific)
  └── topic
        └── global (least specific)
```

When computing the delegate who will cast a vote on behalf of a delegator, the system uses the most specific active delegation in scope for that proposal. If the delegator has cast a direct vote, that always takes precedence regardless of scope.

### Example

Alice has:
- A **global** delegation to Bob
- A **topic** delegation (topic: Environment) to Carol

For an Environment proposal:
- Carol will cast the vote on Alice's behalf (topic delegation is more specific).

For a Finance proposal:
- Bob will cast the vote on Alice's behalf (global delegation applies).

---

## Delegation Graph

Delegations form a directed graph: `delegator → delegate`. The graph must remain a **directed acyclic graph (DAG)** — cycles are strictly forbidden.

### Cycle Detection

Before accepting a new delegation `A → B`, the system checks whether B is already (transitively) delegating to A. If so, the delegation is rejected with a `422 Unprocessable Entity` error.

The cycle check is performed using a depth-first traversal of the outbound delegation graph starting from B.

---

## Weight Computation

The voting weight of a delegate for a specific proposal is computed at vote-tally time (not when ballots are cast) to correctly handle late delegations, direct overrides, and revocations.

### Algorithm (pseudocode)

```
function effective_weight(user, proposal):
    weight = 1  # user's own vote

    for each delegator of user in scope of proposal:
        if delegator has cast a direct ballot for proposal:
            continue  # direct vote overrides delegation
        else:
            weight += effective_weight(delegator, proposal)

    return weight
```

This recursion bottoms out because the delegation graph is a DAG (no cycles).

---

## Direct Vote Override

If a delegator casts a direct vote on a proposal, their vote is recorded independently and their delegated weight is **not** added to their delegate's weight for that proposal.

This override can occur:
- **Before** the delegate votes — the weight is simply not available to the delegate.
- **After** the delegate votes — the delegator's direct ballot is recorded; the tally is recalculated at close time to exclude their weight from the delegate's total.

---

## Revocation

A delegator may revoke a delegation at any time. Revocation is immediate:

- Active sessions of the delegate will see their displayed weight decrease.
- If the delegate has already voted on an open proposal using the delegated weight, the revocation has no effect on that proposal (the ballot is already cast). The delegator may still cast their own direct vote to override.

---

## Transitive Delegation

Chains of delegation are supported to unlimited depth (subject to the DAG constraint):

```
Alice → Bob → Carol
```

If neither Alice nor Bob has voted directly, Carol's ballot on a proposal carries weight 3 (Alice + Bob + Carol).

If Bob casts a direct vote, Bob's weight is 2 (Bob + Alice) and Carol's weight is 1 (only herself).

---

## Delegation Display

Users should be shown a clear summary of their delegation status:

- **Outbound:** Who I have delegated to, in what scope.
- **Inbound:** Who has delegated to me, and the total weight I hold per topic/globally.
- **Chain:** The transitive path through which my vote will be counted (if I do not vote directly).
