# Cryptographic Protocol Appendix v0.1

## 0. Implementation Status and Standards Basis

This appendix adopts the current NIST post-quantum standards for key establishment and signatures: **`ML-KEM` (FIPS 203)**, **`ML-DSA` (FIPS 204)**, and **`SLH-DSA` (FIPS 205)**. NIST finalized these standards in 2024, and BSI recommends that new products be designed for **cryptographic agility** during the PQ transition. At the same time, the public election-security standards landscape still treats cryptographic end-to-end voting protocols as artifacts that must be accompanied by a written specification, security analysis, and reference implementation for public evaluation, rather than as settled procurement commodities. Accordingly, this appendix defines a **PQ-ready control plane** from the first implementation and a **crypto-agile privacy core** whose initial implementation may use a mature classical E2E-verifiable voting construction until a PQ replacement reaches comparable assurance.

## 1. Status, Scope, and Conformance Language

This appendix is **normative** for:
- one-time eligibility without ballot linkability,
- direct-vote override,
- revote semantics,
- public verifiability,
- auditability,
- threshold control,
- result reproducibility,
- cryptographic agility,
- PQ baseline selection,
- retention/destruction behavior,
- failure handling.

“MUST”, “SHOULD”, and “MAY” are used normatively.

This appendix covers the technical substrate for the direct-democracy and proxy ideas described in the manifesto, especially the per-issue proxy mechanism and the previously deferred technical/security details.

## 2. Standards Posture and Design Constraints

This appendix is aligned with four official realities.

First, the Council of Europe’s 2017 e-voting recommendation says **all voting channels, including e-voting, must comply with democratic-election principles**, remote channels should be **additional and optional unless universally accessible**, e-voting systems must provide evidence independently verifiable from the system itself, preserve secrecy at all stages, be auditable, and be introduced **gradually and progressively**.

Second, the EAC’s public process for cryptographic end-to-end voting protocols requires a **complete written protocol specification**, design rationale, security analysis, and a **reference implementation**. This appendix is therefore written at that level of specificity rather than as product prose.

Third, NIST’s finalized PQ standards presently cover **KEMs and digital signatures**, not a settled full stack for anonymous credentials, coercion-resistant remote voting, homomorphic tallying, or mixnet proofs. Accordingly, this appendix treats the privacy core as **pluggable and crypto-agile**, while locking down the PQ control plane now. This is an inference from the official standards retrieved here and from the EAC’s still-open public protocol evaluation process.

Fourth, BSI explicitly recommends **cryptographic agility** for new products, and its online-voting work treats certification, protection profiles, and end-to-end verifiability as core disciplines rather than optional extras.

## 3. Claim-to-Mechanism Map

The PRD claims are operationalized like this.

- **One-time eligibility without ballot linkability:** split identity/eligibility from ballot acceptance; issue a contest entitlement token; transform it into an unlinkable participation credential through blind or anonymous issuance; use a contest-scoped anonymous handle for all ballot-box and delegation actions.

- **Direct-vote override semantics:** direct ballot keyed by anonymous contest handle always beats any delegation edge during resolution; delegation graph is frozen before close; direct ballots remain open until close.

- **Revote semantics:** multiple ballots per contest handle are accepted, but only the highest valid sequence number before close counts.

- **Public verifiability:** signed public bulletin board, append-only log, proof bundles, deterministic tally/replay package, and open verifier tooling.

- **Audit logs:** every critical service emits signed event records into a transparency log; each record type has a schema and retention policy.

- **Threshold control:** tally keys generated and held under t-of-n trustee control, with public ceremonies and quorum-bound operations.

- **Result reproducibility:** canonical input manifests, deterministic tally container, signed software bill of materials, and published verifier hashes.

- **Cryptographic agility:** suite registry, versioned protocol envelopes, explicit algorithm identifiers in every signed record, dual-sign and rotation support.

- **Quantum-safe baseline:** PQ control plane from day one; privacy core abstracted behind stable interfaces until a PQ replacement reaches equal assurance.

## 4. Protocol Entities and Trust Boundaries

The protocol has these actors.

### 4.1 Identity Authority (`IA`)

Authenticates the person using state eID.
Knows: legal identity.
Must not know: contest handle, ballot contents, delegation graph.

### 4.2 Eligibility Authority (`EA`)

Checks whether the authenticated person is eligible for contest `CID`.
Knows: legal identity and eligibility status.
Issues: **Contest Entitlement Token** `CET`.
Must not know: final ballot, contest handle, delegate choice.

### 4.3 Participation Credential Authority set (`PCA`[1..m])

Transforms the entitlement into an **Unlinkable Participation Credential** `UPC` using blind or anonymous issuance.
Knows: issuance transcript metadata only.
Must not know: legal identity-to-final-handle mapping.

The minimum trust goal is: **no single authority can map a cast ballot to a legal person**.

### 4.4 Delegation Registry (`DR`)

Stores contest-scoped anonymous delegation edges.
Knows: anonymous contest handles and public delegate IDs.
Must not know: legal identity.

### 4.5 Ballot Box (`BB`)

Accepts encrypted direct ballots bound to anonymous contest handles.
Knows: anonymous contest handles, sequence numbers, ciphertexts, acceptance times.
Must not know: legal identity.

### 4.6 Delegate Registry / Delegate Instruction Service (`DIS`)

Stores public delegate status and per-contest signed delegate instructions.
Knows: public delegate identities and signed instructions.

### 4.7 Tally Trustees (`TT`[1..n])

Hold shares of tally/decryption authority.
May act only under threshold quorum.

### 4.8 Public Bulletin Board / Transparency Log (`PBB/TL`)

Publishes accepted records, signed checkpoints, proofs, artifact manifests.

### 4.9 Verifiers

Anyone. Auditors, observers, civic technologists, parties, media, citizens.

## 5. Core Data Objects

All protocol claims depend on concrete objects.

### 5.1 Contest Identifier
```
CID = unique identifier of a vote, initiative, or budget contest.
```
### 5.2 Contest Entitlement Token
```
CET = Sign_EA(protocol_version, CID, rights_class, expiry, issuance_nonce, issuance_counter)
```
Purpose: proves the person is eligible exactly once for the contest at the eligibility layer.

### 5.3 Unlinkable Participation Credential
```
UPC
```
Logical properties:
- derived from `CET`,
- supports proof of validity to `DR` and `BB`,
- yields a **contest-scoped anonymous handle** `H`,
- prevents a second independent participation identity for the same `CID`,
- does not reveal legal identity to `DR` or `BB`.

Initial implementation note: in v1, `UPC` issuance MAY be implemented using a mature classical blind-signature or anonymous-credential construction, but only inside a stable interface designed for later PQ replacement. The interface is intentionally stable across cryptographic revisions.

### 5.4 Anonymous Contest Handle
```
H
```
`H` is a contest-scoped pseudonymous identifier derived from `UPC`. It is:
- Unique per eligible participant per contest.
- Public on `DR` and `BB` records.
- Not linkable across contests.
- Not attributable to a legal person by any single actor.

This construction enables both **privacy** and **public verifiability of delegation resolution**.

### 5.5 Direct Ballot Envelope
```
DBE = (CID, H, seq_b, ciphertext, proof_valid_ballot, proof_valid_UPC, timestamp, sig_BB)
```
### 5.6 Delegation Edge
```
DE = (CID, H, mode, target_delegate_id, scope, seq_d, timestamp, sig_DR)
```
Where `mode ∈ {issue, domain}`.

### 5.7 Delegate Instruction
```
DI = (CID, delegate_id, version, choice, rationale_ref, timestamp, sig_delegate)
```
A registered public delegate’s effective choice for delegated votes is derived from `DI`, not from a secret personal ballot.

This is a normative semantic rule. It removes a hidden assumption. If delegated weight follows a delegate, the delegate’s effective vote on that contest must be attributable after close.

### 5.8 Result Bundle
```
RB = (contest_manifest_hash, delegation_snapshot_hash, accepted_ballots_hash, delegate_instruction_hash, tally_output, proof_bundle, software_manifest, verifier_manifest, sig_certifier)
```
## 6. Cryptographic Profile

### 6.1 `CP-1`: current PQ control-plane profile

This profile is mandatory in v1.
- `ML-KEM` is the key establishment mechanism used.
- **`ML-DSA`** is the signature mechanism used.
- `SLH-DSA` is used for backup / root / long-lived recovery signatures.
- SHA-3 / SHAKE family is used for hashing / extendable output.
- 256-bit security level is used for symmetric protection of stored secrets and transport session keys.
- Threshold custody is implemented using secret sharing plus quorum-controlled key operations.

This part is operationally ready because the NIST standards are final and public, and the migration posture is consistent with BSI’s crypto-agility guidance.

### 6.2 `PP-1`: initial privacy-core profile

This is the privacy-core profile used by a contest unless the contest manifest names another approved profile.

The privacy core MUST provide these properties:
- ballot secrecy for contest classes marked secret,
- one-time eligibility,
- anonymous contest-handle issuance,
- well-formed-ballot proofs,
- replay and revote handling,
- public tally verifiability,
- compatibility with the public bulletin-board evidence model,
- compatibility with the contest-class fail-safe rules.

In v1, `PP-1` MAY use a mature classical E2E-verifiable voting construction, such as a mixnet or homomorphic-tally family with public proofs, because the official standards and approval processes retrieved here do not yet amount to a settled PQ standard for anonymous credentials plus verifiable tally. That is why `PP-1` is isolated behind a stable protocol interface.

#### 6.2.1 Contest binding
Every contest manifest MUST specify:
- privacy_profile_id,
- tally_family_id,
- proof_family_id,
- verifier_profile_id,
- suite_id for the control plane,
- whether the selected privacy profile is approved for that contest class.

No contest may open unless its manifest pins these values.

#### 6.2.2 Approval discipline
A privacy-core profile MAY be used only for contest classes for which it has been explicitly approved through the applicable public review and certification process.

The fact that a privacy-core profile is acceptable for a lower-stakes or consultative contest class does not imply that it is acceptable for a higher-stakes or binding contest class.

#### 6.2.3 Mid-contest stability
No contest may silently switch privacy profile, tally family, proof family, or verifier profile after the contest opens.

If a selected profile becomes unavailable or revoked mid-contest, the contest must follow the fail-safe rules for pause, downgrade, restart, or rerun, but may not silently continue under altered assumptions.

### 6.3 Crypto-agility rules

Every cryptographic record MUST carry:
- suite_id.
- algorithm_id.
- key_id.
- protocol_version.

The system MUST support:
- Dual-sign periods.
- Rolling certificate/key rotations.
- Verifier support for old and new suites.
- Public deprecation calendars.
- Algorithm revocation lists.
- Contest-level pinning of cryptographic suites.

No contest may silently switch suites mid-window.

## 7. Key Ceremonies

### 7.1 Ceremony types

There are four ceremony classes.

#### A. Root trust ceremony

For governance root keys, audit-log roots, and suite registry updates.

#### B. Contest setup ceremony

For contest-specific tally keys and trustee shares.

#### C. Verifier release ceremony

For publishing verifier binaries, manifests, and reproducible build hashes.

#### D. Recovery / compromise ceremony

For emergency rotation and contest downgrade.

### 7.2 Ceremony requirements

Every ceremony MUST be:
- Pre-announced.
- Witnessed by multiple institutions.
- Recorded.
- Hash-published.
- Dual-signed.
- Reproducible from the public artifact package.

### 7.3 Threshold control

Contest tally authority MUST use t-of-n trustees. No one actor may decrypt or finalize alone.

Minimum rule:
- n ≥ 5.
- t ≥ 3.
- Trustees must span at least three institutional domains.

The tally key is not exportable in plaintext after ceremony. Trustee actions are quorum-authorized and logged.

## 8. Credential Lifecycle

### 8.1 Enrollment

The citizen authenticates to `IA` with state eID.
```
Citizen -> IA : AuthRequest(CID)
IA -> Citizen : AuthAssertion AA
```
### 8.2 Eligibility check

Citizen submits `AA` to `EA`.
```
Citizen -> EA : EligibilityRequest(CID, AA)
EA -> Citizen : CET
```
`EA` records that one entitlement has been issued for that legal identity and contest.

### 8.3 Unlinkable issuance

Citizen transforms `CET` into `UPC` through `PCA` issuance.
```
Citizen <-> PCA quorum : BlindIssue(CET) -> UPC
```
Normative property:
- `PCA` validates that `CET` is genuine and unused for issuance.
- `PCA` cannot see the final `H`.
- `DR` and `BB` can later validate proofs derived from `UPC` without learning the legal identity.

### 8.4 Derivation

Citizen derives:
- `H` = contest-scoped anonymous handle.
- local revote state.
- local proof material for `DR` and `BB`.

### 8.5 Recovery

Lost-client recovery for high-stakes contests is supervised only.

Recovery issues a Supersession Record:
```
SR = (CID, H_old, H_new, reason_code, timestamp, sig_recovery_quorum)
```
Rules:
- any later direct ballot under `H_new` supersedes any ballot under `H_old`,
- `SR` is publicly logged,
- `SR` never reveals legal identity,
- recovery is rate-limited and audited,
- recovery must not create a second effective participation path.

#### 8.5.1 Privacy note on supersession
The supersession mechanism intentionally links two anonymous contest handles for the limited purpose of preserving contest integrity and public verifiability of supersession.

This is a controlled privacy cost and MUST be treated as such.

The publication of `SR` is permitted because:
- it does not reveal legal identity,
- it is necessary to explain why `H_old` no longer resolves,
- it allows independent verification that recovery did not create duplicate effective participation.

Recovery MUST therefore remain rare, supervised, rate-limited, and explicitly logged.

#### 8.5.2 Recovery challengeability
Every `SR` MUST be challengeable through the challenge interface defined in this appendix.

A recovery event may block certification if it is alleged to have created duplicate effective participation, invalidated a valid ballot without basis, or materially weakened secrecy beyond the declared assumptions.

## 9. Delegation Protocol

### 9.1 Delegation registration

A citizen holding `UPC` may write or update a delegation edge in `DR` without revealing legal identity.
```
Citizen -> DR : DelegationUpdate(CID, H, mode, target_delegate_id, seq_d, proof_valid_UPC)
```
`DR` verifies:
- `proof_valid_UPC` is valid.
- `H` belongs to this contest.
- `seq_d` is strictly greater than prior `seq_d` for `H`.
- target delegate is eligible and active.
- no tier-specific cap or policy violation occurs.

`DR` then publishes the accepted edge record.

### 9.2 Delegation freeze and publication discipline

To make override semantics verifiable and to reduce end-window chaos, delegation updates close at `T_freeze`, while direct ballots remain open until `T_close`.

This is a protocol rule.
```
T_freeze < T_close
```
At `T_freeze`, the Delegation Registry computes the frozen delegation snapshot `DS*`.

#### 9.2.1 Pre-close publication rule
Before `T_close`, the system MUST publish only a signed commitment to `DS*`, not the full snapshot, unless a contest-class rule explicitly authorizes stronger pre-close visibility.

The commitment object is:
```
DSC = (CID, T_freeze, hash(DS*), record_count, policy_digest, timestamp, sig_DR_quorum)
```
Purpose:
- prove that `DS*` was fixed at `T_freeze`,
- prevent later silent reconstruction,
- avoid unnecessary pre-close exposure of delegation structure.

#### 9.2.2 Post-close publication rule
After `T_close`, the full `DS*` MUST be published for universal verification unless a secrecy-class rule requires delayed or coarsened publication.

The post-close publication package MUST allow independent verifiers to confirm:
- every accepted delegation update before `T_freeze` was either included or superseded correctly,
- no post-freeze update altered `DS*`,
- direct-vote override was computed against the committed `DS*`.

#### 9.2.3 Contest-class exceptions
Any contest class that allows publication of more than `DSC` before `T_close` MUST explicitly define:
- what additional delegation information is visible,
- why that visibility is compatible with its secrecy and anti-coercion posture,
- which body authorized the exception.

No contest may rely on informal operator choice for pre-close delegation visibility.

### 9.3 Delegation cap enforcement

Delegation caps are normative, not advisory.

#### 9.3.1 Cap semantics
For each contest class, the system MUST define whether the applicable cap is:
- an incoming-edge cap,
- an effective resolved-weight cap,
- or both.

Unless the contest manifest states otherwise, the cap applies to effective resolved weight.

#### 9.3.2 Enforcement point
Cap compliance MUST be checked:
- at delegation acceptance time where feasible,
- and again at post-freeze resolution time.

This dual check exists because transitive resolution and supersession can alter effective concentration after an edge was initially accepted.

#### 9.3.3 Overflow behavior
When an attempted delegation would breach the applicable cap, the system MUST follow one of the predeclared behaviors bound to the contest class:
- reject the new delegation attempt,
- accept it only if prior delegations are re-resolved under explicit spillover rules,
- or place the attempted delegation into a pending state that has no constitutional effect until the citizen chooses an alternative.

No silent truncation is allowed.

#### 9.3.4 Citizen notice
If a delegation attempt fails or becomes non-effective due to cap enforcement, the citizen MUST receive a clear notice and a path to choose another delegate or revert to direct participation.

#### 9.3.5 Public evidence
After close, the result package MUST include artifacts sufficient for independent verification that:
- the applicable cap model was the one declared,
- cap checks were actually performed,
- overflow behavior matched policy,
- no delegate exceeded the allowed bound under the declared semantics.

### 9.4 Transitivity policy

Because the system supports both direct participation and proxy voting, transitivity must be contest-class-bound, not left to default interpretation.

#### 9.4.1 Tier 1 consultative contests
For Tier 1 consultative contests, transitivity MAY be enabled with a declared maximum depth `d_max`.

If enabled, `d_max` MUST be included in the contest manifest.

#### 9.4.2 Tier 2 binding local or community contests
For Tier 2 binding contests, transitivity SHOULD be disabled unless a specific legal rule authorizes it for that contest class.

If enabled, the contest manifest MUST state:
- the legal basis,
- the maximum depth,
- the cycle-handling rule,
- the cap model used for effective concentration.

#### 9.4.3 Tier 3 binding national contests
For Tier 3 binding national contests, transitivity MUST be disabled unless a higher constitutional act explicitly authorizes it.

Absent such authorization, binding national contests use one-hop delegation only.

#### 9.4.4 Cycle handling
If transitivity is enabled and a cycle is detected, the system MUST apply the predeclared fallback rule for that contest class.

The fallback rule MUST be one of:
- abstention,
- revert to direct vote if one exists,
- revert to issue-specific non-cyclic edge if one exists.

No cycle may be resolved through silent operator choice.

#### 9.4.5 Public verifiability
If transitivity is enabled, the result package MUST expose enough information for an independent verifier to reproduce transitive resolution under the declared depth cap without learning legal identity.

### 9.5 Delegate instructions

Delegates submit signed public instructions.

```
Delegate -> DIS : DI(CID, delegate_id, version, choice, rationale_ref, timestamp, sig_delegate)
```

Only the highest valid version before `T_close` counts.

A delegate’s effective vote on delegated weight is derived from `DI`, not from a secret personal ballot.

This is a semantic rule, not a user-interface convenience.

#### 9.5.1 Visibility policy by contest class
The visibility of `DI` before `T_close` MUST be bound to contest class.
- Tier 1 consultative contests: `DI` MAY be visible before close.
- Tier 2 binding local/community contests: pre-close visibility MUST be explicitly set by law or manifest policy.
- Tier 3 binding national contests: `DI` SHOULD NOT expose final binding choice before close unless a higher rule explicitly authorizes that visibility model.

#### 9.5.2 Minimum pre-close disclosure
Even where full `DI` is not visible before close, a delegate MAY publish:
- rationale material,
- issue commentary,
- declared principles,
- conflict disclosures,
- prior voting history.

This material does not substitute for the contest-bound `DI` that becomes effective in resolution.

#### 9.5.3 Weight opacity before close
No contest class may publish real-time or near-real-time delegated-weight totals by delegate during the open voting window.

This rule exists to reduce herding, coercive signaling, and end-window pressure.

#### 9.5.4 Post-close accountability
After close, the effective `DI` set for the contest MUST be published in the result package, subject only to lawful delay where a secrecy-class rule requires it.

---

## 10. Direct Ballot Protocol

### 10.1 Cast
```
Citizen -> BB : DBE(CID, H, seq_b, ciphertext, proof_valid_ballot, proof_valid_UPC)
```
`BB` verifies:
- credential proof is valid,
- ballot is well-formed,
- `H` belongs to this contest,
- `seq_b` is strictly greater than the previous accepted sequence number for `H`,
- contest is open,
- no supersession record invalidates `H`.

If accepted, `BB` returns an acceptance receipt and records the acceptance event.

#### 10.1.1 Bulletin-board publication during open voting
During the open voting window, the public bulletin board MUST operate in one of two declared modes:

##### Commitment mode
The system publishes signed commitments, checkpoints, and aggregate record counts sufficient to prove append-only behavior without exposing full accepted-record manifests during the open window.

##### Full-record mode
The system publishes accepted-record manifests during the open window.

The contest manifest MUST declare which mode applies.

#### 10.1.2 Default rule
For Tier 2 and Tier 3 contests, Commitment mode is the default.

Full-record mode during the open window may be used only where the contest class and secrecy posture explicitly allow it.

#### 10.1.3 Post-close disclosure
After `T_close`, the accepted direct-ballot manifest required for universal verification MUST be published, unless a secrecy-class rule requires delayed or coarsened publication.

### 10.2 Revote semantics

Revoting is defined precisely:

For each `H`, the counted direct ballot is the accepted `DBE` with the **maximum valid `seq_b`** received no later than `T_close`.

All lower-sequence accepted ballots for that same `H` remain sealed and excluded from tally. They are retained only until challenge close, then destroyed or cryptographically shredded according to retention rules.

This operationalizes the PRD claim that only the latest valid vote counts.

### 10.3 Abstention

A citizen may explicitly cast abstention as a valid ballot option. Silence is not abstention.

## 11. Resolution Semantics

At tally time, every anonymous contest handle resolves to exactly one effective outcome.

### 11.1 Resolution order

For each `H`:
1. If there exists a counted direct ballot for `H`, use it;
2. Else if there exists a valid issue-specific delegation edge in `DS*`, follow it;
3. Else if there exists a valid domain delegation edge in `DS*`, follow it;
4. Else abstain.

### 11.2 Transitive follow

If transitivity is enabled for that tier:
- Follow the chain until a delegate with valid `DI` is found.
- Stop at depth cap.
- Detect cycles.
- On cycle or unresolved target, use fallback or abstain.

### 11.3 Direct-vote override theorem

A direct ballot overrides delegation because resolution starts with the counted direct ballot before consulting `DS*`.

This is the mechanism; it is not a UI convention.

### 11.4 Public proof of override

Any verifier can inspect:
- Public `DS*`.
- Public set of accepted direct-ballot records by `H`.
- Public delegate instructions.
- Public tally software.

After inspection any verifier can confirm that every `H` with a counted direct ballot was excluded from delegated expansion.

## 12. Tally Semantics

### 12.1 Inputs

The tally inputs are:
- Contest manifest.
- Supersession records.
- Frozen delegation snapshot `DS*`.
- Accepted direct-ballot list.
- Delegate instructions.
- Trustee keys / proof materials.
- Software manifest.

### 12.2 Direct-ballot tally

Direct ballots are tallied through the privacy core:
- Mix-and-decrypt with proofs.
- Homomorphic aggregation with proofs.

depending on the selected PP profile.

The public must be able to verify:
- Only direct ballots counted per `H` were entered into the direct tally.
- All counted direct ballots were well-formed.
- The decryption or aggregate proof is valid.

The CoE standard requires sound evidence that each authentic vote is accurately included in the result, verifiable independently of the e-voting system, and that it must not be possible to reconstruct a link between the unsealed vote and the voter.

### 12.3 Delegated tally

Delegated votes are expanded deterministically from `DS*` and `DI`.

For each `H` without a counted direct ballot:
- Compute choice (`H`) from the resolution algorithm.
- Increment the corresponding option count.

### 12.4 Combined result

Final result =
```
DirectSecretTally + DelegatedDeterministicTally
```
The combined result is intentionally split as follows:
- Direct citizen ballots preserve secret-ballot treatment.
- Delegated outcomes are publicly attributable to delegate instructions.
- The merged result is still reproducible.

### 12.5 Certification

A contest cannot be certified unless:
- Quorum tally proof passes.
- Deterministic delegated expansion reproduces.
- Artifact hashes match.
- No unresolved critical challenge remains.

## 13. Verification Semantics

### 13.1 Individual verification

A voter may verify:
- The direct ballot record of `H` exists.
- The accepted sequence number is the one they expect.
- The latest accepted delegation record is present before freeze.

Verification tokens must not become durable vote receipts usable for coercion. The CoE standard explicitly forbids giving the voter proof of vote content for third parties.

### 13.2 Universal verification

Any observer may verify:
- Signatures on all accepted records.
- Hash-chain / Merkle integrity of the bulletin board.
- Direct-ballot inclusion/exclusion by sequence rule.
- Correctness of `DS*`.
- Correctness of delegated expansion.
- Correctness of direct-ballot proof bundle.
- Correctness of the final combined result.

### 13.3 Procedural verification

Auditors may verify:
- Ceremony records.
- Build reproducibility.
- Software manifest.
- Key provenance.
- Incident and challenge logs.
- Retention/destruction events.

### 13.4 Challenge object model

All constitutionally relevant artifacts MUST be challengeable through typed challenge records.

#### 13.4.1 Challenge record
```
CR = (challenge_id, CID, object_type, object_ref, challenge_type, filer_role, timestamp, status, sig_filer)
```

Where:
- object_type identifies the contested artifact class,
- object_ref identifies the specific contested object or manifest entry,
- challenge_type identifies the nature of the claim.

#### 13.4.2 Minimum challengeable object classes
At minimum, the following object classes MUST be challengeable:
- `CET` issuance state where legally reviewable,
- `UPC` issuance event class,
- supersession record,
- delegation edge,
- delegation snapshot commitment or snapshot,
- direct-ballot acceptance or rejection record,
- delegate instruction,
- tally manifest,
- proof bundle,
- certification artifact,
- destruction event,
- incident event,
- software or verifier manifest.

#### 13.4.3 Challenge lifecycle
Each challenge MUST have a public status state machine:
- filed,
- accepted for review,
- merged with related challenge,
- dismissed with reasons,
- sustained,
- resolved by remedy,
- escalated,
- closed.

No challenge may disappear into informal administrative handling.

#### 13.4.4 Certification dependency
The contest manifest or certification rules MUST specify which challenge types automatically block certification, which may proceed in parallel, and which require only post-certification review.

## 14. Audit Log Model

Every critical service MUST emit append-only signed audit records.

Mandatory record classes:
- Authentication attempt.
- Eligibility issued.
- Blind issuance transcript accepted.
- Delegation updated.
- Direct ballot accepted/rejected.
- Supersession issued.
- Tally ceremony event.
- Proof package published.
- Challenge filed/resolved.
- Retention/destruction event.
- Incident declared/resolved.
- Suite change / key rotation.

Each record has the following fields:
- event_id.
- event_type.
- timestamp.
- actor_role.
- object_id.
- prev_hash.
- event_hash.
- sig_service.

This makes the audit system “open and comprehensive” rather than a closed admin log, which is exactly what the CoE standard demands.

## 15. Result Reproducibility

Every certified contest MUST publish a reproducibility package containing all public artifacts and manifests necessary for an independent party to reproduce, from public artifacts alone and under the declared contest profile:
- the counted direct-ballot set,
- the final delegation snapshot or committed snapshot resolution state,
- the delegated expansion,
- the final tally,
- the verifier environment used for official certification.

At minimum, the reproducibility package MUST include:
- the contest manifest,
- the exact protocol version,
- cryptographic suite identifiers,
- the privacy profile identifier,
- the tally family identifier,
- the proof family identifier,
- the verifier profile identifier,
- the signed delegation snapshot commitment and, where publication is permitted, the full delegation snapshot,
- the accepted direct-ballot manifest published under the contest’s bulletin-board mode rules,
- the delegate-instruction manifest,
- the result bundle,
- the proof bundle,
- the software manifest,
- verifier source or equivalent verifier specification,
- deterministic build instructions,
- verifier container or binary hashes,
- the expected canonical outputs.

Any independent verifier MUST be able to use this package to determine whether:
- the counted direct-ballot set was derived according to the accepted sequence and supersession rules,
- delegation resolution was performed from the committed or published snapshot according to the declared contest policy,
- delegated expansion matched the declared transitivity, cap, and fallback rules,
- the final tally corresponds to the published manifests and proof bundle,
- the software and verifier artifacts used for certification match the declared manifests and hashes.

Where a contest’s secrecy class forbids immediate publication of some artifact in full, the reproducibility package MUST still publish:
- the commitment, hash, or manifest entry proving that the artifact existed in the certified state,
- the legal basis for delayed or restricted release,
- the conditions and timeline under which fuller disclosure, restricted review, or sealed audit access becomes available.

No contest may be certified unless the reproducibility package is sufficient for an independent party to reproduce the certified result under the declared contest profile, subject only to explicitly declared secrecy-class restrictions.

## 16. Retention and Destruction Requirements

The system must retain enough to verify and challenge, but no more.

Retention policy is defined per actor and per artifact class.

### 16.1 `IA`
Retains authentication logs per identity law.
Must not receive `H` or ballot data.

### 16.2 `EA`
Retains entitlement issuance ledger until challenge close, then archives under separate legal controls.
Must not receive ballots or delegation graph.

### 16.3 `PCA`
Retains issuance transcript metadata and service logs, but not final `H`.

### 16.4 `DR`
Retains accepted delegation records and the post-close delegation snapshot artifacts required for verification.

### 16.5 `BB`
Retains accepted direct-ballot envelopes and receipts until challenge close.
Superseded direct ballots for the same `H` remain sealed; after challenge close they are destroyed or cryptographically shredded according to contest policy.

### 16.6 Tally materials
Trustee ephemeral session material is destroyed immediately after certification or contest halt, except where a challenge hold lawfully preserves specific material.

### 16.7 Destruction records
Every destruction operation emits a signed destruction event into the audit log.

### 16.8 Artifact-retention matrix
Every contest class MUST publish an artifact-retention matrix with at least these columns:
- artifact class,
- visibility class: public / restricted / sealed,
- retention horizon,
- destruction method,
- destruction evidence object.

At minimum, the matrix MUST cover:
- entitlement-related ledgers,
- issuance metadata,
- delegation records,
- delegation snapshot commitment,
- delegation snapshot full artifact,
- direct-ballot acceptance records,
- superseded ballot records,
- supersession records,
- proof bundles,
- result bundles,
- verifier manifests,
- incident logs,
- challenge records,
- destruction events.

### 16.9 Permanent public artifacts
The appendix or contest manifest MUST explicitly identify which artifacts remain permanently public on the bulletin board or transparency log, and which artifacts are retained only through challenge close or by separate legal rule.

No artifact class may drift between permanent and temporary retention by informal operator choice.
## 17. Fault Resilience Behavior

### 17.1 `IA` unavailable

Already issued UPCs remain usable.
No new eligibility flows until `IA` restored or supervised contingency invoked.

### 17.2 `EA` unavailable

No new `CET` issuance.
Contests may continue if issuance window already closed.
For high-stakes contests, supervised contingency may replace remote issuance.

### 17.3 `PCA` quorum unavailable

No new `UPC` issuance.
No fallback to identity-linked ballot casting is allowed.

### 17.4 `DR` failure before `T_freeze`

Delegation window extended or contest downgraded.
No silent reconstruction from backups without published signed snapshot.

### 17.5 `DR` failure after `T_freeze`

Use last quorum-signed `DS*`.
Direct ballots continue until `T_close`.

### 17.6 `BB` outage

Voting window may be extended.
Supervised channels may buffer sealed ballot submissions.
Incident must be publicly declared.

### 17.7 Trustee quorum unavailable

No certification.
Contest enters unresolved state until quorum restored or legal fallback triggered.

### 17.8 Proof failure

If tally proof or delegated-expansion reproducibility fails, result is not certifiable.

### 17.9 Suite compromise / cryptanalytic break

If a cryptographic suite is revoked mid-contest, the contest may be:
- paused,
- downgraded to supervised-only channel,
- restarted under a new suite.

but never silently continued under a revoked assumption.

### 17.10 Irregularity affecting specific handles

Affected records are flagged, quarantined, and published for challenge. The CoE standard requires identification of votes affected by irregularity.

## 18. Hidden-Assumption Elimination

These are the constitutional controls that now have concrete mechanisms.

“Only one effective participation right per eligible person”
Mechanism: `CET` issuance ledger + `UPC` issuance control + unique `H`.

“Ballot box must not know identity”
Mechanism: blind / anonymous issuance of `UPC`; `BB` sees only `H`.

“Direct vote overrides proxy”
Mechanism: resolution order + delegation freeze + public `DS*`.

“Revoting must work”
Mechanism: strictly increasing `seq_b` per `H`.

“Proxy decisions must be auditable”
Mechanism: public delegate instructions + public `DS*` + deterministic resolution.

“Results must be independently reproducible”
Mechanism: public manifests + proofs + open verifier.

“Threshold control must be real”
Mechanism: quorum key ceremonies + trustee shares + public ceremony records.

“Crypto agility must be real”
Mechanism: suite registry + versioned records + dual-sign rotations.

“PQC must be a real baseline, not marketing”
Mechanism: `ML-KEM` / `ML-DSA` / `SLH-DSA` in the control plane from v1; privacy core isolated for later PQ replacement.

## 19. Residual Assumptions

These assumptions remain true only if the declared institutional and operational conditions actually hold. They are therefore explicit, not hidden.

### 19.1 Secrecy and collusion assumptions
The secrecy model is designed so that no single actor among `IA`, `EA`, `PCA` quorum minority, `DR`, or `BB` can, by acting alone, map a final cast ballot to a legal person.

Secrecy may fail if collusions occur beyond the declared tolerance threshold.

The appendix MUST treat the following as system-breaking collusions unless a stronger formally analyzed model is declared:
- `IA` + `EA` + effective control over `UPC` issuance,
- `IA` + `BB` with a broken or bypassed anonymous issuance layer,
- `EA` + `PCA` quorum + `DR` where issuance isolation is not preserved,
- any coalition that can both reconstruct legal identity and control or inspect final ballot acceptance state.

### 19.2 Client compromise assumptions
Client compromise remains possible, especially in remote settings.

The system therefore assumes:
- supervised channels remain necessary for the highest-stakes classes,
- revoting and override reduce but do not eliminate coercion or malware risk,
- local device secrecy cannot be treated as a constitutional guarantee.

### 19.3 PQ readiness assumptions
PQ readiness is strong for the control-plane KEM and signature layers in v1.

PQ readiness is not yet equally mature for the full anonymous-voting privacy core.

For that reason, the privacy core is abstracted behind a stable interface and pinned per contest.

### 19.4 Verifier diversity assumptions
Public verifiability depends on the existence of multiple independent verifiers and not solely on one official verifier binary.

### 19.5 Supervised-channel neutrality assumptions
The constitutional validity of supervised fallback depends on those channels being practically reachable and institutionally neutral.

Where neutrality or reachability fails, supervised fallback does not cure the red-line condition by itself.

## 20. Acceptance Tests for the Protocol

The protocol appendix is not conformant unless the following minimum acceptance tests pass for the applicable contest class and are reproducible from the declared test harness, manifests, and verifier profile.

### 20.1 Identity, eligibility, and participation-right tests
1. Attempt to duplicate entitlement issuance for the same legal person and contest and verify that a second effective participation right cannot be created.
2. Attempt to derive more than one effective anonymous contest handle for the same contest entitlement and verify that only one effective participation identity can exist for the contest.
3. Simulate high-stakes recovery and verify that supervised recovery creates a valid supersession record without creating a second effective participation path.
4. Attempt protected participation with an expired, revoked, or wrong-contest credential and verify rejection.

### 20.2 Delegation and override tests
5. Set a valid delegation, then cast a direct ballot, and verify that the direct ballot overrides delegation in final resolution.
6. Register multiple delegation updates for the same handle and verify that only the highest valid delegation sequence before `T_freeze` is effective.
7. Attempt a delegation update after `T_freeze` and verify rejection or non-effect according to contest policy.
8. Compute `DS*`, publish `DSC`, and verify that:
- before `T_close`, only the signed commitment is public in commitment mode,
- after `T_close`, the full `DS*` is published where allowed,
- the published `DS*` matches the pre-close commitment.

### 20.3 Delegation-cap and transitivity tests
9. Attempt to exceed the applicable delegation cap and verify that the declared overflow behavior is followed exactly:
- rejection,
- spillover under declared rules,
- or pending non-effective state.
10. Verify that a citizen receives explicit notice when a delegation becomes non-effective due to cap enforcement.
11. For a Tier 1 contest with transitivity enabled, create a valid chain and verify that resolution follows the declared depth cap.
12. For a Tier 2 contest, verify that transitivity is disabled unless explicitly authorized in the contest manifest.
13. For a Tier 3 contest, verify that one-hop delegation is enforced unless a higher authorization is present.
14. Create a delegation cycle and verify that the declared cycle fallback rule is applied deterministically.

### 20.4 Direct-ballot and revote tests
15. Cast multiple direct ballots for the same handle and verify that only the highest valid sequence number received no later than `T_close` is counted.
16. Replay a stale ballot with a lower sequence number and verify rejection.
17. Submit a ballot under a superseded handle and verify rejection or non-effect according to supersession rules.
18. Verify that abstention is treated as a valid explicit outcome and not inferred from silence.

### 20.5 Bulletin-board and publication-mode tests
19. Run a contest in commitment mode and verify that during open voting the bulletin board publishes only commitments, checkpoints, and counts required by policy.
20. Run a contest in full-record mode and verify that accepted-record publication matches the declared manifest policy.
21. Verify that post-close accepted direct-ballot manifests are published according to the contest’s secrecy and publication rules.
22. Verify append-only integrity of the bulletin board across checkpoints.

### 20.6 Delegate-instruction tests
23. Submit multiple delegate instructions for the same contest and verify that only the highest valid version before `T_close` is effective.
24. Verify that pre-close visibility of delegate instructions matches the contest-class policy.
25. Verify that delegated-weight totals are not published before close.
26. Verify that post-close effective delegate instructions are included in the result package where required.

### 20.7 Tally and reproducibility tests
27. Reproduce the final result from public artifacts only and verify that the reproduced result matches the certified result.
28. Verify that the counted direct-ballot set corresponds exactly to accepted sequence and supersession rules.
29. Verify that delegated expansion matches declared cap, transitivity, and fallback rules.
30. Verify that the final tally corresponds to:

- the direct-ballot tally,
- the delegated deterministic tally,
- the published proof bundle,
- and the contest manifest.

### 20.8 Challenge and certification tests
31. File typed challenges against at least the following object classes and verify lifecycle handling:

- supersession record,
- delegation edge,
- delegation snapshot commitment,
- direct-ballot acceptance record,
- delegate instruction,
- proof bundle,
- certification artifact.

32. Verify that challenge status transitions follow the declared public state machine.
33. Verify that challenge types declared as certification-blocking actually prevent certification until resolved.
34. Verify that non-blocking challenge types remain visible and reviewable without silently disappearing.

### 20.9 Retention and destruction tests
35. Verify that superseded ballots remain sealed until challenge close and are then destroyed or cryptographically shredded according to the retention policy.
36. Verify that every destruction operation emits a signed destruction event.
37. Verify that the published artifact-retention matrix covers all mandatory artifact classes and that actual retention behavior matches the matrix.
38. Verify that permanent public artifacts remain available after challenge close while temporary artifacts follow the declared destruction path.

### 20.10 Trust-chain and verifier tests
39. Rebuild the verifier from declared source and build instructions and verify that hashes match the published manifest.
40. Simulate a mismatch between published manifests and actual verifier or software artifacts and verify that certification cannot proceed.
41. Simulate a compromised or revoked software line and verify that the affected contest enters the correct fail-safe state rather than silently continuing.
42. Rotate the cryptographic suite between contests and verify that old contests remain verifiable under their pinned suite while new contests use the updated suite.

### 20.11 Fault and fail-safe tests
43. Simulate Identity Authority unavailability and verify that already issued participation credentials remain usable while no new issuance proceeds.
44. Simulate Delegation Registry failure before `T_freeze` and verify that the system follows the declared extension or downgrade path.
45. Simulate Delegation Registry failure after `T_freeze` and verify that the last quorum-signed delegation snapshot commitment remains the binding reference.
46. Simulate Ballot Box outage near close and verify that:

- incident declaration occurs,
- recovery instructions are published,
- extension or fallback behavior follows declared rules.

47. Simulate trustee quorum loss and verify that certification is impossible.
48. Simulate proof failure and verify that the result is not certifiable.
49. Simulate a cryptographic-suite revocation mid-contest and verify that the contest is paused, downgraded, or restarted according to declared fail-safe rules.

### 20.12 Cross-class conformance rule

No contest class is conformant unless all tests applicable to its:
- secrecy class,
- delegation mode,
- publication mode,
- transitivity policy,
- recovery policy,
- and certification posture.

have been executed successfully against that contest-class profile.
