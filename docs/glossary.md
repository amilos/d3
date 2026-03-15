# Glossary

| Term | Definition |
|---|---|
| **Approval voting** | A voting method in which each voter may select any number of options; the option(s) with the most approvals win. |
| **Audit event** | An append-only record of a state-changing action on the platform, forming the cryptographically chained audit log. |
| **Audit log** | The complete, immutable, hash-chained sequence of audit events that enables independent verification of all platform activity. |
| **Ballot** | A voter's recorded choice for a specific proposal. A voter has at most one active ballot per proposal. |
| **bcrypt** | A password-hashing algorithm designed to be computationally expensive, making brute-force attacks impractical. |
| **Citizen** | A verified platform participant who holds one vote. |
| **DAG (Directed Acyclic Graph)** | A graph where edges have direction and there are no cycles. The delegation graph in d3 must always be a DAG. |
| **Delegate** | A citizen who receives delegated voting power from one or more other citizens (delegators). |
| **Delegated democracy** | See *liquid democracy*. |
| **Delegator** | A citizen who assigns (delegates) their voting power to a delegate. |
| **Delegation** | The act of transferring one's voting power to another user, optionally scoped to a topic or proposal. |
| **Delegation chain** | A sequence of delegations where A → B → C, meaning A's vote will be cast by C unless B or A votes directly. |
| **Delegation graph** | The directed graph formed by all active delegations. Must be a DAG to prevent circular delegation. |
| **Delegation scope** | The breadth of a delegation: *global* (all proposals), *topic* (proposals in a topic), or *proposal* (a single proposal). |
| **Delegation weight** | The total number of votes a delegate controls: their own plus all transitively delegated votes that have not been overridden by direct votes. |
| **Direct vote** | A ballot personally cast by a voter, which always overrides any active delegation for that proposal. |
| **Draft** | The initial status of a proposal; it is not yet visible to voters. |
| **Hash chain** | A sequence of records where each record contains the hash of its predecessor, making any tampering detectable. |
| **HPA (Horizontal Pod Autoscaler)** | A Kubernetes resource that automatically adjusts the number of pod replicas based on observed metrics. |
| **Identity provider (IdP)** | An external service (e.g., Google, GitHub) that authenticates users via OAuth 2.0 / OpenID Connect. |
| **Instant run-off voting** | A ranked-choice method that successively eliminates the least-popular option and redistributes those votes until one option has a majority. |
| **JWT (JSON Web Token)** | A compact, URL-safe token format used to represent claims between parties. d3 uses RS256-signed JWTs for access tokens. |
| **Liquid democracy** | A form of democracy that combines direct and representative democracy: citizens can vote directly or delegate their vote to a trusted representative, and that representative can further delegate. |
| **MFA (Multi-Factor Authentication)** | An authentication method requiring the user to provide two or more verification factors. d3 uses TOTP as the second factor. |
| **OpenID Connect (OIDC)** | An identity layer on top of OAuth 2.0 that allows clients to verify the identity of the end-user. |
| **Proposal** | A question or motion submitted to the platform for a vote. It has a lifecycle: Draft → Open → Closed → Archived. |
| **Quorum** | The minimum participation (by count or weight) required for a proposal's result to be considered valid. Quorum rules are configurable per proposal. |
| **Ranked-choice voting** | A voting method in which voters rank options in order of preference; see *instant run-off voting*. |
| **Refresh token** | A long-lived token used to obtain new access tokens without requiring the user to re-authenticate. |
| **Single-choice voting** | A voting method in which each voter selects exactly one option; the option with the highest weight wins. |
| **Tally** | The aggregated vote weights per option for a proposal. |
| **Topic** | A category used to organise proposals and scope delegations (e.g., "Environment", "Finance"). |
| **TOTP (Time-based One-Time Password)** | A time-limited one-time password algorithm (RFC 6238) used as a second factor in MFA. |
| **Transitive delegation** | When A delegates to B, and B delegates to C, C holds A's voting weight transitively (unless B or A votes directly). |
| **TLS (Transport Layer Security)** | A cryptographic protocol for secure communication over a network. d3 requires TLS 1.2 or higher. |
| **Vote weight** | The number of votes a single ballot counts for. Normally 1 for a direct voter; higher when the voter is a delegate with active delegations. |
| **Voting method** | The rule set used to determine the winner of a proposal vote. d3 supports single-choice, approval, and ranked-choice methods. |
| **Voter** | Any citizen who casts a ballot (either directly or as a delegate). |
