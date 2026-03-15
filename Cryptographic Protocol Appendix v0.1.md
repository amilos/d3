# Cryptographic Protocol Appendix v0.1  
  
> Note: For what is standardized and operationally ready today, this appendix uses the current NIST PQ standards for KEMs and signatures: ML-KEM (FIPS 203), ML-DSA (FIPS 204), and SLH-DSA (FIPS 205). NIST finalized them in 2024, and BSI explicitly recommends designing new crypto products for **cryptographic agility** during the PQ transition. At the same time, the official election-standard landscape still treats cryptographic E2E voting protocols as something that must be submitted with a full written specification, security analysis, and reference implementation for public evaluation, rather than something settled once and for all. So this appendix uses a **PQ-ready control plane now**, and a **crypto-agile privacy core** whose first implementation can use a mature classical E2E-verifiable voting core until a PQ replacement is ready at similar assurance.    
  
## 1. Status, scope, and conformance language  
  
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
  
## 2. Standards posture and design constraints  
  
This appendix is aligned with four official realities.  
  
First, the Council of Europe’s 2017 e-voting recommendation says **all voting channels, including e-voting, must comply with democratic-election principles**, remote channels should be **additional and optional unless universally accessible**, e-voting systems must provide evidence independently verifiable from the system itself, preserve secrecy at all stages, be auditable, and be introduced **gradually and progressively**.    
  
Second, the EAC’s public process for cryptographic end-to-end voting protocols requires a **complete written protocol specification**, design rationale, security analysis, and a **reference implementation**. This appendix is therefore written at that level of specificity, not as a product brochure.    
  
Third, NIST’s finalized PQ standards presently cover **KEMs and digital signatures**, not a settled full stack for anonymous credentials, coercion-resistant remote voting, homomorphic tallying, or mixnet proofs. That is why this appendix treats the privacy core as **pluggable and crypto-agile**, while locking down the PQ control plane now. This is an inference from the official standards retrieved here and from the EAC’s still-open public protocol evaluation process.    
  
Fourth, BSI explicitly recommends **cryptographic agility** for new products, and its online-voting work treats certification, protection profiles, and end-to-end verifiability as core disciplines rather than optional extras.    
  
## 3. Claim-to-mechanism map  
  
The PRD claims are operationalized like this.  
  
**One-time eligibility without ballot linkability**  
Mechanism: split identity/eligibility from ballot acceptance; issue a contest entitlement token; transform it into an unlinkable participation credential through blind or anonymous issuance; use a contest-scoped anonymous handle for all ballot-box and delegation actions.  
  
**Direct-vote override semantics**  
Mechanism: direct ballot keyed by anonymous contest handle always beats any delegation edge during resolution; delegation graph is frozen before close; direct ballots remain open until close.  
  
**Revote semantics**  
Mechanism: multiple ballots per contest handle are accepted, but only the highest valid sequence number before close counts.  
  
**Public verifiability**  
Mechanism: signed public bulletin board, append-only log, proof bundles, deterministic tally/replay package, and open verifier tooling.  
  
**Audit logs**  
Mechanism: every critical service emits signed event records into a transparency log; each record type has a schema and retention policy.  
  
**Threshold control**  
Mechanism: tally keys generated and held under t-of-n trustee control, with public ceremonies and quorum-bound operations.  
  
**Result reproducibility**  
Mechanism: canonical input manifests, deterministic tally container, signed software bill of materials, and published verifier hashes.  
  
**Cryptographic agility**  
Mechanism: suite registry, versioned protocol envelopes, explicit algorithm identifiers in every signed record, dual-sign and rotation support.  
  
**Quantum-safe baseline**  
Mechanism: PQ control plane from day one; privacy core abstracted behind stable interfaces until a PQ replacement reaches equal assurance.  
  
## 4. Protocol entities and trust boundaries  
  
The protocol has these actors.  
  
**4.1 Identity Authority (IA)**  
  
Authenticates the person using state eID.  
Knows: legal identity.  
Must not know: contest handle, ballot contents, delegation graph.  
  
**4.2 Eligibility Authority (EA)**  
  
Checks whether the authenticated person is eligible for contest CID.  
Knows: legal identity and eligibility status.  
Issues: **Contest Entitlement Token** CET.  
Must not know: final ballot, contest handle, delegate choice.  
  
**4.3 Participation Credential Authority set (PCA[1..m])**  
  
Transforms the entitlement into an **Unlinkable Participation Credential** UPC using blind or anonymous issuance.  
Knows: issuance transcript metadata only.  
Must not know: legal identity-to-final-handle mapping.  
  
The minimum trust goal is: **no single authority can map a cast ballot to a legal person**.  
  
**4.4 Delegation Registry (DR)**  
  
Stores contest-scoped anonymous delegation edges.  
Knows: anonymous contest handles and public delegate IDs.  
Must not know: legal identity.  
  
**4.5 Ballot Box (BB)**  
  
Accepts encrypted direct ballots bound to anonymous contest handles.  
Knows: anonymous contest handles, sequence numbers, ciphertexts, acceptance times.  
Must not know: legal identity.  
  
**4.6 Delegate Registry / Delegate Instruction Service (DIS)**  
  
Stores public delegate status and per-contest signed delegate instructions.  
Knows: public delegate identities and signed instructions.  
  
**4.7 Tally Trustees (TT[1..n])**  
  
Hold shares of tally/decryption authority.  
May act only under threshold quorum.  
  
**4.8 Public Bulletin Board / Transparency Log (PBB/TL)**  
  
Publishes accepted records, signed checkpoints, proofs, artifact manifests.  
  
**4.9 Verifiers**  
  
Anyone. Auditors, observers, civic technologists, parties, media, citizens.  
  
## 5. Core data objects  
  
All protocol claims depend on concrete objects.  
  
**5.1 Contest Identifier**  
  
```
CID = unique identifier of a vote, initiative, or budget contest.

```
  
**5.2 Contest Entitlement Token**  
  
```
CET = Sign_EA(protocol_version, CID, rights_class, expiry, issuance_nonce, issuance_counter)

```
  
Purpose: proves the person is eligible exactly once for the contest at the eligibility layer.  
  
**5.3 Unlinkable Participation Credential**  
  
```
UPC

```
  
Logical properties:  
- derived from CET,  
- supports proof of validity to DR and BB,  
- yields a **contest-scoped anonymous handle** H,  
- prevents a second independent participation identity for the same CID,  
- does not reveal legal identity to DR or BB.  
  
Initial implementation note: in v1, UPC issuance MAY be implemented using a mature classical blind-signature or anonymous-credential construction, but only inside a stable interface designed for later PQ replacement. That is deliberate, not evasive.  
  
**5.4 Anonymous Contest Handle**  
  
```
H

```
  
H is a contest-scoped pseudonymous identifier derived from UPC. It is:  
- Unique per eligible participant per contest  
- Public on DR and BB records  
- Not linkable across contests  
- Not attributable to a legal person by any single actor  
  
This is the key technical compromise that makes both **privacy** and **public verifiability of delegation resolution** possible.  
  
**5.5 Direct Ballot Envelope**  
  
```
DBE = (CID, H, seq_b, ciphertext, proof_valid_ballot, proof_valid_UPC, timestamp, sig_BB)

```
  
**5.6 Delegation Edge**  
  
```
DE = (CID, H, mode, target_delegate_id, scope, seq_d, timestamp, sig_DR)

```
  
Where mode ∈ {issue, domain}.  
  
**5.7 Delegate Instruction**  
  
```
DI = (CID, delegate_id, version, choice, rationale_ref, timestamp, sig_delegate)

```
  
A registered public delegate’s effective choice for delegated votes is derived from DI, not from a secret personal ballot.  
  
That is a deliberate semantic rule. It removes a hidden assumption. If delegated weight follows a delegate, the delegate’s effective vote on that contest must be attributable after close.  
  
**5.8 Result Bundle**  
  
```
RB = (contest_manifest_hash, delegation_snapshot_hash, accepted_ballots_hash, delegate_instruction_hash, tally_output, proof_bundle, software_manifest, verifier_manifest, sig_certifier)

```
  
## 6. Cryptographic profile  
  
**6.1 CP-1: current PQ control-plane profile**  
  
This is mandatory in v1.  
- ML-KEM is the key establishment mechanism used.  
- **ML-DSA** is the signature mechanism used.  
- SLH-DSA is used for backup / root / long-lived recovery signatures.  
- SHA-3 / SHAKE family is used for hashing / extendable output.  
- 256-bit security level is used for symmetric protection of stored secrets and transport session keys.  
- Threshold custody is implemented using secret sharing plus quorum-controlled key operations.  
  
This part is operationally ready because the NIST standards are final and public, and the migration posture is consistent with BSI’s crypto-agility guidance.    
  
**6.2 PP-1: initial privacy-core profile**  
  
This is the part that is **crypto-agile by design**.  
  
The privacy core MUST provide these properties:  
- Ballot secrecy  
- One-time eligibility  
- Anonymous contest handle issuance  
- Well-formed-ballot proofs  
- Replay/revote handling  
- Public tally verifiability  
  
In v1, PP-1 MAY use a mature classical E2E-verifiable voting construction, such as a mixnet or homomorphic-tally family with public proofs, because the official standards and approval processes retrieved here do not yet amount to a settled PQ standard for anonymous credentials plus verifiable tally. That is why PP-1 is isolated behind a stable protocol interface.    
  
**6.3 Crypto-agility rules**  
  
Every cryptographic record MUST carry:  
- suite_id  
- algorithm_id  
- key_id  
- protocol_version  
  
The system MUST support:  
- Dual-sign periods  
- Rolling certificate/key rotations  
- Verifier support for old and new suites  
- Public deprecation calendars  
- Algorithm revocation lists  
- Contest-level pinning of cryptographic suites  
  
No contest may silently switch suites mid-window.  
  
## 7. Key ceremonies  
  
**7.1 Ceremony types**  
  
There are four ceremony classes.  
  
**A. Root trust ceremony**  
  
For governance root keys, audit-log roots, and suite registry updates.  
  
**B. Contest setup ceremony**  
  
For contest-specific tally keys and trustee shares.  
  
**C. Verifier release ceremony**  
  
For publishing verifier binaries, manifests, and reproducible build hashes.  
  
**D. Recovery / compromise ceremony**  
  
For emergency rotation and contest downgrade.  
  
**7.2 Ceremony requirements**  
  
Every ceremony MUST be:  
- Pre-announced  
- Witnessed by multiple institutions  
- Recorded  
- Hash-published  
- Dual-signed  
- Reproducible from the public artifact package  
  
**7.3 Threshold control**  
  
Contest tally authority MUST use t-of-n trustees. No one actor may decrypt or finalize alone.  
  
Minimum rule:  
- n ≥ 5  
- t ≥ 3  
- Trustees must span at least three institutional domains.  
  
The tally key is not exportable in plaintext after ceremony. Trustee actions are quorum-authorized and logged.  
  
## 8. Credential lifecycle  
  
**8.1 Enrollment**  
  
The citizen authenticates to IA with state eID.  
  
```
Citizen -> IA : AuthRequest(CID)
IA -> Citizen : AuthAssertion AA

```
  
**8.2 Eligibility check**  
  
Citizen submits AA to EA.  
  
```
Citizen -> EA : EligibilityRequest(CID, AA)
EA -> Citizen : CET

```
  
EA records that one entitlement has been issued for that legal identity and contest.  
  
**8.3 Unlinkable issuance**  
  
Citizen transforms CET into UPC through PCA issuance.  
  
```
Citizen <-> PCA quorum : BlindIssue(CET) -> UPC

```
  
Normative property:  
* PCA validates that CET is genuine and unused for issuance.  
* PCA cannot see the final H.  
* DR and BB can later validate proofs derived from UPC without learning the legal identity.  
  
**8.4 Derivation**  
  
Citizen derives:  
* H = contest-scoped anonymous handle  
* local revote state  
* local proof material for DR and BB  
  
**8.5 Recovery**  
  
Lost-client recovery for high-stakes contests is **supervised only**.  
  
Recovery issues a **Supersession Record**:  
```
SR = (CID, H_old, H_new, reason_code, sig_recovery_quorum)

```
  
Rules:  
* Any later direct ballot under H_new supersedes any ballot under H_old.  
* SR is public.  
* SR reveals no legal identity.  
* Recovery is rate-limited and audited.  
  
## 9. Delegation protocol  
  
**9.1 Delegation registration**  
  
A citizen holding UPC may write or update a delegation edge in DR without revealing legal identity.  
  
```
Citizen -> DR : DelegationUpdate(CID, H, mode, target_delegate_id, seq_d, proof_valid_UPC)

```
  
DR verifies:  
* proof_valid_UPC:  
* H belongs to this contest.  
* seq_d is strictly greater than prior seq_d for H.  
* target delegate is eligible and active.  
* no tier-specific cap or policy violation occurs.  
  
DR then publishes the accepted edge record.  
  
**9.2 Delegation freeze**  
  
To make override semantics verifiable and to reduce end-window chaos, delegation updates close at T_freeze, while direct ballots remain open until T_close.  
  
This is a deliberate protocol choice.  
* T_freeze < T_close  
* The frozen delegation snapshot DS* is quorum-signed and published.  
* Any later direct ballot still overrides DS*.  
  
This is the cleanest way to make “direct vote overrides proxy” a deterministic and auditable rule instead of a fuzzy UI promise.  
  
**9.3 Transitivity policy**  
  
Because you chose all proxy modes, the system supports transitivity in principle, but not uniformly.  
  
Recommended enforcement:  
* Tier 1 consultative: transitivity allowed with depth cap d_max  
* Tier 2/3 binding: one-hop only by default  
  
That is not ideological. It is a verification and cartel-risk control.  
  
**9.4 Delegate instructions**  
  
Delegates submit signed public instructions.  
  
```
Delegate -> DIS : DI(CID, delegate_id, version, choice, rationale_ref)

```
  
Rule:  
* Only the highest valid version before T_close counts.  
* Delegate instructions are public after close.  
* Pre-close visibility may be allowed, but delegated-weight totals are not.  
  
## 10. Direct ballot protocol  
  
**10.1 Cast**  
  
```
Citizen -> BB : DBE(CID, H, seq_b, ciphertext, proof_valid_ballot, proof_valid_UPC)

```
  
BB verifies:  
- Credential proof is valid.  
- Ballot is well-formed.  
- Sequence number (seq_b) is strictly greater than the previous sequence number (seq_b) for H.  
- Contest is open.  
- No supersession record invalidates H.  
  
BB returns an acceptance receipt and posts the accepted record to PBB.  
  
**10.2 Revote semantics**  
  
Revoting is defined precisely:  
  
For each H, the counted direct ballot is the accepted DBE with the **maximum valid seq_b** received no later than T_close.  
  
All lower-sequence accepted ballots for that same H remain sealed and excluded from tally. They are retained only until challenge close, then destroyed or cryptographically shredded according to retention rules.  
  
This operationalizes the PRD claim that only the latest valid vote counts.  
  
**10.3 Abstention**  
  
A citizen may explicitly cast abstention as a valid ballot option. Silence is not abstention.  
  
**11. Resolution semantics**  
  
At tally time, every anonymous contest handle resolves to exactly one effective outcome.  
  
**11.1 Resolution order**  
  
For each H:  
1. If there exists a counted direct ballot for H, use it;  
2. Else if there exists a valid issue-specific delegation edge in DS*, follow it;  
3. Else if there exists a valid domain delegation edge in DS*, follow it;  
4. Else abstain.  
  
**11.2 Transitive follow**  
  
If transitivity is enabled for that tier:  
- Follow the chain until a delegate with valid DI is found.  
- Stop at depth cap.  
- Detect cycles.  
- On cycle or unresolved target, use fallback or abstain.  
  
**11.3 Direct-vote override theorem**  
  
A direct ballot overrides delegation because resolution starts with the counted direct ballot before consulting DS*.  
  
That is the mechanism. Not a UI convention.  
  
**11.4 Public proof of override**  
  
Any verifier can inspect:  
- Public DS*  
- Public set of accepted direct-ballot records by H  
- Public delegate instructions  
- Public tally software  
  
After inspection any verifier can confirm that every H with a counted direct ballot was excluded from delegated expansion.  
  
## 12. Tally semantics  
  
**12.1 Inputs**  
  
The tally inputs are:  
- Contest manifest  
- Supersession records  
- Frozen delegation snapshot DS*  
- Accepted direct-ballot list  
- Delegate instructions  
- Trustee keys / proof materials  
- Software manifest  
  
**12.2 Direct-ballot tally**  
  
Direct ballots are tallied through the privacy core:  
- Mix-and-decrypt with proofs  
- Homomorphic aggregation with proofs  
  
depending on the selected PP profile.  
  
The public must be able to verify:  
- Only direct ballots counted per H were entered into the direct tally.  
- All counted direct ballots were well-formed.  
- The decryption or aggregate proof is valid.  
  
The CoE standard requires sound evidence that each authentic vote is accurately included in the result, verifiable independently of the e-voting system, and that it must not be possible to reconstruct a link between the unsealed vote and the voter.    
  
**12.3 Delegated tally**  
  
Delegated votes are expanded deterministically from DS* and DI.  
  
For each H without a counted direct ballot:  
- Compute choice (H) from the resolution algorithm.  
- Increment the corresponding option count.  
  
**12.4 Combined result**  
  
Final result =  
```
DirectSecretTally + DelegatedDeterministicTally

```
  
This split is intentional:  
- Direct citizen ballots preserve secret-ballot treatment.  
- Delegated outcomes are publicly attributable to delegate instructions.  
- The merged result is still reproducible.  
  
**12.5 Certification**  
  
A contest cannot be certified unless:  
- Quorum tally proof passes.  
- Deterministic delegated expansion reproduces.  
- Artifact hashes match.  
- No unresolved critical challenge remains.  
  
## 13. Verification semantics  
  
**13.1 Individual verification**  
  
A voter may verify:  
- The direct ballot record of H exists.  
- The accepted sequence number is the one they expect.  
- The latest accepted delegation record is present before freeze.  
  
Verification tokens must not become durable vote receipts usable for coercion. The CoE standard explicitly forbids giving the voter proof of vote content for third parties.    
  
**13.2 Universal verification**  
  
Any observer may verify:  
- Signatures on all accepted records  
- Hash-chain / Merkle integrity of the bulletin board  
- Direct-ballot inclusion/exclusion by sequence rule  
- Correctness of DS*  
- Correctness of delegated expansion  
- Correctness of direct-ballot proof bundle  
- Correctness of the final combined result  
  
**13.3 Procedural verification**  
  
Auditors may verify:  
- Ceremony records  
- Build reproducibility  
- Software manifest  
- Key provenance  
- Incident and challenge logs  
- Retention/destruction events  
  
**14. Audit log model**  
  
Every critical service MUST emit append-only signed audit records.  
  
Mandatory record classes:  
- Authentication attempt  
- Eligibility issued  
- Blind issuance transcript accepted  
- Delegation updated  
- Direct ballot accepted/rejected  
- Supersession issued  
- Tally ceremony event  
- Proof package published  
- Challenge filed/resolved  
- Retention/destruction event  
- Incident declared/resolved  
- Suite change / key rotation  
  
Each record has the following fields:  
- event_id  
- event_type  
- timestamp  
- actor_role  
- object_id  
- prev_hash  
- event_hash  
- sig_service  
  
This makes the audit system “open and comprehensive” rather than a closed admin log, which is exactly what the CoE standard demands.    
  
## 15. Result reproducibility  
  
Every certified contest MUST publish a reproducibility package containing:  
- The contest manifest includes:  
- The exact protocol version  
- Cryptographic suite IDs  
- A signed delegation snapshot  
- An accepted direct-ballot manifest  
- A delegate-instruction manifest  
- Proof files  
- Verifier source  
- Deterministic build instructions  
- Verifier container hash  
- Expected outputs  
  
Any independent party must be able to reproduce from public artifacts alone:  
- counted direct-ballot set  
- delegated expansion  
- final tally  
  
  
## 16. Retention and destruction requirements  
  
The system must retain enough to verify and challenge, but no more.  
  
**16.1 IA**  
  
Retains authentication logs per identity law.  
Must not receive H or ballot data.  
  
**16.2 EA**  
  
Retains entitlement issuance ledger until challenge close, then archives under separate legal controls.  
Must not receive ballots or delegation graph.  
  
**16.3 PCA**  
  
Retains blind issuance transcript metadata and service logs, but not final H.  
  
**16.4 DR**  
  
Publicly retains signed DS* and accepted delegation records by anonymous handle.  
  
**16.5 BB**  
  
Retains accepted direct-ballot envelopes and receipts until challenge close. Superseded direct ballots for the same H remain sealed; after challenge close they are destroyed or cryptographically shredded.  
  
**16.6 Tally materials**  
  
Trustee ephemeral session material is destroyed immediately after certification or contest halt.  
  
**16.7 Destruction records**  
  
Every destruction operation emits a signed destruction event into the audit log.  
  
This is required by both privacy discipline and by the CoE requirement that e-voting process and store only the personal data needed and preserve secrecy of erased prior choices.    
  
## 17. Fault resilience behavior  
  
**17.1 IA unavailable**  
  
Already issued UPCs remain usable.  
No new eligibility flows until IA restored or supervised contingency invoked.  
  
**17.2 EA unavailable**  
  
No new CET issuance.  
Contests may continue if issuance window already closed.  
For high-stakes contests, supervised contingency may replace remote issuance.  
  
**17.3 PCA quorum unavailable**  
  
No new UPC issuance.  
No fallback to identity-linked ballot casting is allowed.  
  
**17.4 DR failure before T_freeze**  
  
Delegation window extended or contest downgraded.  
No silent reconstruction from backups without published signed snapshot.  
  
**17.5 DR failure after T_freeze**  
  
Use last quorum-signed DS*.  
Direct ballots continue until T_close.  
  
**17.6 BB outage**  
  
Voting window may be extended.  
Supervised channels may buffer sealed ballot submissions.  
Incident must be publicly declared.  
  
**17.7 Trustee quorum unavailable**  
  
No certification.  
Contest enters unresolved state until quorum restored or legal fallback triggered.  
  
**17.8 Proof failure**  
  
If tally proof or delegated-expansion reproducibility fails, result is not certifiable.  
  
**17.9 Suite compromise / cryptanalytic break**  
  
If a cryptographic suite is revoked mid-contest, the contest may be:  
- paused,  
- downgraded to supervised-only channel,  
- restarted under a new suite.  
  
but never silently continued under a revoked assumption.  
  
**17.10 Irregularity affecting specific handles**  
  
Affected records are flagged, quarantined, and published for challenge. The CoE standard requires identification of votes affected by irregularity.    
  
## 18. Hidden-assumption elimination  
  
These are the constitutional controls that now have concrete mechanisms.  
  
“Only one effective participation right per eligible person”  
Mechanism: CET issuance ledger + UPC issuance control + unique H.  
  
“Ballot box must not know identity”  
Mechanism: blind / anonymous issuance of UPC; BB sees only H.  
  
“Direct vote overrides proxy”  
Mechanism: resolution order + delegation freeze + public DS*.  
  
“Revoting must work”  
Mechanism: strictly increasing seq_b per H.  
  
“Proxy decisions must be auditable”  
Mechanism: public delegate instructions + public DS* + deterministic resolution.  
  
“Results must be independently reproducible”  
Mechanism: public manifests + proofs + open verifier.  
  
“Threshold control must be real”  
Mechanism: quorum key ceremonies + trustee shares + public ceremony records.  
  
“Crypto agility must be real”  
Mechanism: suite registry + versioned records + dual-sign rotations.  
  
“PQC must be a real baseline, not marketing”  
Mechanism: ML-KEM / ML-DSA / SLH-DSA in the control plane from v1; privacy core isolated for later PQ replacement.  
  
## 19. Residual assumptions  
  
These are still assumptions, but they are no longer hidden.  
- No single actor can link person to ballot.  
- Stronger privacy against multi-actor collusion depends on the blind issuance design, batching, and institutional separation actually being enforced.  
- Client compromise is still possible, which is why supervised channels remain mandatory for the highest-stakes tiers.  
- PQ readiness is strong today for control-plane KEMs and signatures, not equally strong yet for the full anonymous-voting privacy core.  
- Public verifiability depends on open verifier diversity, not a single official verifier binary.  
  
## 20. Acceptance tests for this appendix  
  
Minimum test suite:  
1. Attempt to duplicate entitlement issuance for the same person and contest.  
2. Cast a direct ballot after setting a delegation and verify if the override is successful.  
3. Cast multiple direct ballots and verify if the highest sequence number of ballots is counted.  
4. Create a delegation cycle and verify if the deterministic fallback is working correctly.  
5. Exceed the cap or invalid target and verify if the rejection is happening as expected.  
6. Recover from a lost client in a supervised channel and verify if the supersession is happening correctly.  
7. Replay a stale ballot with a lower sequence number and verify if the rejection is happening as expected.  
8. Reproduce the final result from public artifacts only and verify if the result is accurate.  
9. Rotate the crypto suite between contests and verify if the old contests remain verifiable.  
10. Simulate a trustee quorum loss and verify if no certification is possible.  
