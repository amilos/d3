# PRD: Delegated Direct Democracy Platform (D3) v0.1

## 1. Purpose

This document defines the product requirements for a constitutional-grade civic platform that supports direct participation, bounded proxy delegation, public deliberation, and legally meaningful civic action across multiple contest classes.

This PRD is a lean companion document.

- It owns product scope, system architecture, cross-cutting platform policy, rollout, and readiness.
- It aligns explicitly with the Constitutional Governance and Threat Model for democratic invariants, harms, red lines, viability conditions, and governance rationale.
- It aligns explicitly with the Technical Protocol for protocol entities, state objects, protected-action semantics, evidence objects, verifier behavior, and failure semantics.

The platform is not merely a voting application. It is civic infrastructure combining identity, eligibility, contest management, deliberation, delegation, protected participation, verification, public evidence, challenge handling, and constitutional review.

## 2. Objectives

Any deployment must satisfy product and governance goals consistent with high-assurance civic systems.

The platform must be:

- secure against insider abuse, outside interference, and infrastructure compromise
- anonymous for citizens where secret ballot is required
- coercion-resistant to the maximum extent compatible with the contest class and channel posture
- manipulation-resistant in information presentation and civic workflow
- cognitively humane for ordinary citizens
- socially legitimate through transparency, audits, public evidence, and citizen oversight
- quantum-safe by architectural mandate for platform-controlled cryptographic control surfaces
- crypto-agile so stronger suites can be introduced without redesigning the institution

## 3. Non-goals

The platform does not aim to:

- replace constitutional review
- replace ordinary administration and public-service delivery
- permit organizations to act as delegates in place of natural persons
- make every contest fully remote from day one
- optimize for engagement, virality, or time spent in product
- rely on opaque personalization to drive civic behavior
- redefine contest legality, rights posture, or protocol semantics inside the product layer

## 4. Product principles

### 4.1 Equal civic standing

Every eligible citizen has equal formal civic standing.

### 4.2 Direct participation always remains available where allowed

Proxy delegation never removes the right to act directly in a contest class that permits direct participation.

### 4.3 Public delegates and private delegators

Delegates are public constitutional actors. Delegating citizens remain private unless a contest class explicitly requires otherwise.

### 4.4 No single point of constitutional trust

Identity, eligibility, privacy-preserving participation, delegation, ballot intake, tally, certification, and oversight are institutionally and technically separated.

### 4.5 Security before convenience

High-stakes binding contests may require supervised or higher-assurance channels even when lower-stakes civic acts are remote-eligible.

### 4.6 Structured deliberation over algorithmic persuasion

The platform presents signed dossiers, adversarial briefs, citizen-assembly outputs, and transparent summaries rather than engagement-ranked feeds.

### 4.7 Crypto agility

Every platform-owned cryptographic dependency is versioned, replaceable, and governed through visible change control.

### 4.8 Public verifiability without public exposure of voters

Citizens can verify that their protected participation was correctly handled where policy allows. Independent parties can verify that public evidence supports the declared result.

### 4.9 Public evidence over institutional opacity

Critical ceremonies, releases, logs, proofs, incidents, and certification states must be publicly inspectable or publicly reconstructable.

### 4.10 Cognitive mercy

Most citizens are not full-time legislators. The platform must reduce overload, preserve clarity, and avoid manipulative interface patterns.

## 5. Contest classes and assurance tiers

This PRD uses the same contest-class taxonomy as the Constitutional Governance and Threat Model.

### 5.1 Contest classes

| Class | Coverage | Binding force | Default channel posture | Secrecy posture | Delegation posture |
|---|---|---|---|---|---|
| A | Protected civic initiation acts | Threshold-bearing or agenda-triggering | Remote-eligible | Private but attributable | Generally not applicable |
| B | Consultative civic contests | Advisory | Remote-eligible | Usually secret ballot | Allowed where policy permits |
| C | Participatory budgeting contests | Binding within a bounded budget domain | Hybrid | Usually secret ballot | Allowed under bounded rules |
| D | Local or community binding contests | Binding within local jurisdiction | Hybrid or supervised-default | Usually secret ballot | Allowed under stronger constraints |
| E | Selected national binding contests | Binding subject to constitutional pathway | Supervised-default unless elevated | Secret ballot | Allowed only under strict limits |
| F | Delegation and proxy-state acts | Structural, not substantive | Remote-eligible | Protected civic act | This class defines delegation state |
| G | Public delegate acts | Public constitutional effect | Remote-eligible | Public | Not applicable |

### 5.2 Assurance tiers

| Tier | Typical use | Default channel posture | Secrecy posture | Notes |
|---|---|---|---|---|
| 0 | Qualified protected civic acts | Remote-eligible | Private but attributable | Used for threshold support and comparable protected civic acts |
| 1 | Consultative civic contests | Remote-eligible | Secret ballot by default | Proxy delegation may be enabled |
| 2 | Local binding contests | Hybrid | Secret ballot by default | Revoting and supervised override may apply |
| 3 | High-stakes binding contests | Supervised-default | Secret ballot | Remote high-assurance extension requires separate authorization |

### 5.3 Assignment rule

Every contest must declare, before opening:

- contest class
- binding-force category
- assurance tier
- channel posture
- secrecy posture
- delegation posture
- certification path
- protocol profile reference

## 6. Institutional actors and governance

### 6.1 Core institutional actors

The platform depends on at least the following institutional actors:

- Identity Authority
- Eligibility Authority
- Privacy Credential Authority
- Delegation Registry Authority
- Contest Registry Authority
- Ballot Intake Authority
- Public Evidence Operator
- Tally Authority
- Certification Authority
- Constitutional Review Gate
- Independent Auditors
- Sortition Oversight Council
- Accredited Domestic and International Observers

No actor may both identify the citizen and control the final result path end to end.

### 6.2 Governance model

The product operates within a layered governance model:

- constitutional governance defines what the system is allowed to be
- operational governance runs contests within declared rules
- oversight governance audits, challenges, and reviews public evidence
- incident governance classifies anomalies and routes fail-safe action
- implementation governance tracks whether valid outcomes become real public acts

### 6.3 Actor map

| Actor | Role | Legitimate interest | Primary distortion risk | Primary constraint |
|---|---|---|---|---|
| Citizens | Hold civic standing | Meaningful, safe participation | Disengagement, coercion, over-delegation | One effective path, accessibility, challengeability |
| Public delegates | Receive revocable civic trust | Aggregating judgment, publishing reasons | Concentration, hidden financing, cartelization | Registration, disclosures, caps, override |
| Contest administration | Runs lifecycle operations | Orderly conduct, timely certification | Delay, discretionary asymmetry, procedural capture | Published rules, evidence duties, reviewability |
| Identity authority | Authenticates persons | Integrity of identity, recovery | Selective recovery, unequal access | Auditability, separation from ballot knowledge |
| Eligibility authority | Determines contest-specific eligibility | Accuracy and lawful inclusion | Selective exclusion, discriminatory edge cases | Reviewability, published metrics |
| Tally and certification authorities | Produce and certify results | Correctness, evidence completeness | Over-centralization, opacity, certification pressure | Threshold control, public evidence, multi-body review |
| Technical operators | Build and distribute software | Reliability, secure deployment | Trust-chain compromise, hidden dependencies | Reproducible builds, release attestations, audits |
| Constitutional review gate | Reviews legality and rights | Rights protection, lawful scope | Strategic delay, selective blockage | Narrow grounds, reason-giving, deadlines |
| Executive branch | Executes law and influences agenda | Governability, continuity | Agenda capture, implementation sabotage | Rights floor, review, public traceability |
| Legislature | Sets framework and may coexist with direct civic action | Coherence, budget discipline | Agenda monopoly, dilution of outcomes | Constitutional supremacy of valid civic acts |
| Local authorities and supervised sites | Provide local support and access | Service delivery, lawful local administration | Patronage, under-service, local coercion | Neutral access obligations, auditability |
| Public broadcasters and official information bodies | Disseminate official civic information | Public education, procedural clarity | Framing bias, selective amplification | Provenance, neutrality duties, challengeability |

## 7. Trust boundaries

This section defines what each trust boundary is for and what it must not do. Exact protocol semantics remain in the Technical Protocol.

### 7.1 Identity domain

Role:

- authenticate the person using a state-backed digital identity
- establish secure access and recovery posture

Must not:

- interpret ballots
- handle tally logic
- expose participation choices publicly

### 7.2 Eligibility domain

Role:

- determine whether the authenticated person may participate in a given contest
- enforce one participation right per person per contest

Must not:

- learn vote choice
- influence substantive civic choice

### 7.3 Contest and policy domain

Role:

- define the authoritative contest manifest
- bind contest class, assurance tier, secrecy posture, channel posture, delegation posture, certification path, and protocol profile reference

Must not:

- authenticate citizens
- handle direct ballot content
- silently mutate contest policy during an active contest

### 7.4 Privacy domain

Role:

- transform eligibility into privacy-preserving participation
- preserve separation between personhood and ballot-side activity

Must not:

- become a hidden identity-to-ballot map

### 7.5 Delegation domain

Role:

- maintain delegation state
- enforce caps and policy limits
- support direct override and auditable proxy resolution

Must not:

- expose private delegators publicly
- control ballot secrecy

### 7.6 Ballot-processing domain

Role:

- validate and accept protected direct-ballot submissions under contest policy

Must not:

- know legal identity
- certify results

### 7.7 Information and deliberation domain

Role:

- maintain official issue presentation, source provenance, moderated deliberation, and logged AI-assisted summarization

Must not:

- silently alter legal meaning
- rank or target political content with hidden engagement logic
- alter contest rules, accepted ballots, tally inputs, or certification state

### 7.8 Public evidence domain

Role:

- publish append-only public evidence, challenge states, incident markers, and certification records

Must not:

- contain undisclosed private identity data
- suppress or reorder public evidence silently

### 7.9 Tally domain

Role:

- execute the approved tally path under threshold or quorum control
- produce public evidence needed for certification and independent review

Must not:

- operate as a unilateral authority
- bypass challenge and certification processes

### 7.10 Certification domain

Role:

- turn a technically completed contest into a legally valid result when preconditions are satisfied

Must not:

- alter contest history
- recalculate hidden results outside the approved evidence path

### 7.11 Oversight domain

Role:

- inspect, verify, challenge, observe, and reproduce the public record

Must not:

- mutate operational state

## 8. Functional architecture

The platform is composed of bounded subsystems. No single subsystem should be able to authenticate the citizen, learn the vote choice, and determine the official result.

### 8.1 Core subsystems

- enrollment and identity service
- eligibility service
- privacy credential service
- delegation registry
- contest registry
- canonical issue dossier service
- deliberation service
- delegate workspace
- ballot client
- ballot intake service
- public evidence service
- tally service
- certification service
- observer and verifier APIs
- incident and challenge service

### 8.2 Contest registry

Owns:

- authoritative contest records and signed contest policy
- legal and technical identifiers
- lifecycle state from proposal through archival

Consumes:

- submissions, review decisions, and legal formatting outputs

Emits:

- contest manifests for all downstream services and observers

Must not:

- mutate contest policy invisibly after voting begins

### 8.3 Delegate workspace

Owns:

- product-facing tools for delegate rationale, disclosures, issue queues, and public profiles

Consumes:

- delegation-state views, dossier materials, and disclosure data

Emits:

- public rationales, disclosure records, and structured delegate Q&A artefacts

Must not:

- expose private delegators
- access secret-ballot content

### 8.4 Enrollment and identity service

Owns:

- platform enrollment, authentication, session establishment, and high-assurance recovery orchestration

Consumes:

- state eID assertions and supervised recovery checks

Emits:

- signed identity-side events and secure session outputs for eligibility checking

Must not:

- handle ballot content or delegation semantics

### 8.5 Eligibility service

Owns:

- contest-specific eligibility decisions and duplicate-prevention state

Consumes:

- authenticated identity state, contest policy, electorate data, and lawful overrides

Emits:

- contest-scoped authorization outcomes and auditable eligibility records

Must not:

- handle vote choice or tally logic

### 8.6 Privacy credential service

Owns:

- issuance of privacy-preserving participation credentials or equivalent authorization artefacts

Consumes:

- signed eligibility outputs and contest policy

Emits:

- privacy-preserving participation state and auditable issuance records

Must not:

- learn vote choice
- become a shadow identity ledger

### 8.7 Delegation registry

Owns:

- authoritative issue-level and domain-level delegation state
- cap enforcement and public delegate directory

Consumes:

- citizen delegation updates, delegate status, and contest policy

Emits:

- authoritative delegation-state outputs for downstream resolution and verification
- public delegate profiles and aggregate concentration signals

Must not:

- expose private delegators publicly
- access direct-ballot plaintext

### 8.8 Canonical issue dossier service

Owns:

- official issue presentation and provenance
- standardized dossier structure

Consumes:

- legal text, explanatory memoranda, expert briefs, citizen-assembly outputs, and signed source corpus entries

Emits:

- citizen-facing issue dossiers and machine-readable dossier packages

Must not:

- silently rewrite summaries
- redefine legal validity or tally semantics

### 8.9 Deliberation service

Owns:

- moderated public reasoning spaces, adversarial briefs, expert Q&A, and logged AI-assisted summary outputs

Consumes:

- citizen submissions, delegate rationales, source materials, and moderation rules

Emits:

- moderated argument sets, minority notes, and archived deliberation artefacts

Must not:

- influence contest validity or result determination
- use hidden engagement ranking or psychographic targeting

### 8.10 Ballot client

Owns:

- the protected citizen-facing experience for reading, deciding, delegating, voting directly, abstaining, and verifying where policy permits

Consumes:

- contest manifests, dossier content, delegation status, privacy-preserving participation state, and accessibility preferences

Emits:

- protected delegation actions and protected direct-ballot submissions

Must not:

- create durable proof of vote choice
- embed hidden persuasive logic

### 8.11 Ballot intake service

Owns:

- protected intake of direct-ballot submissions and enforcement of contest-specific submission policy

Consumes:

- protected ballot packages, contest policy, credential status, and lawful override signals

Emits:

- accept or reject decisions, accepted ballot artefacts, and intake audit records

Must not:

- store identity records
- decrypt ballots
- compute results

### 8.12 Public evidence service

Owns:

- append-only publication of accepted public artefacts, incident markers, challenge records, and certification records

Consumes:

- accepted artefacts, result packages, incident records, and certification artefacts

Emits:

- public evidence log, export bundles, and replication artefacts

Must not:

- suppress, reorder, or delete public evidence silently

### 8.13 Tally service

Owns:

- execution of the approved tally procedure for the contest’s protocol profile
- generation of result artefacts and corresponding public evidence

Consumes:

- authorised contest inputs, contest policy, and threshold authorizations

Emits:

- result package, proof or evidence bundle, and certification input package

Must not:

- access voter identity
- change contest policy or admissible input set during tally

### 8.14 Certification service

Owns:

- validation of evidence-package completeness and issuance of certification or refusal

Consumes:

- result and evidence package, incident state, challenge resolutions, and required review statements

Emits:

- certification record or refusal record and publication package

Must not:

- modify tally artefacts
- silently change certification conditions

### 8.15 Observer and verifier APIs

Owns:

- read-only access paths for public evidence, verifier tooling inputs, and mirror synchronization

Consumes:

- contest manifests, public evidence, result packages, and challenge state

Emits:

- machine-readable data for observers and verifiers

Must not:

- provide privileged write access into operational systems

### 8.16 Incident and challenge service

Owns:

- incident intake, challenge intake, severity classification, escalation, disposition, and archival tracking

Consumes:

- citizen reports, observer reports, anomaly alerts, auditor findings, operator incidents, and lawful review orders

Emits:

- incident records, challenge records, public status outputs, and escalation signals

Must not:

- suppress material incidents silently
- close serious challenges without attributable reasoning

### 8.17 High-level flow

At a high level, the platform operates in the following sequence:

- a contest is defined and published through the contest registry
- official issue materials are prepared through the dossier and deliberation services
- a participant authenticates and is checked for contest-specific eligibility
- the participant enters a privacy-preserving participation path appropriate to the contest class
- the participant either configures delegation or casts a direct vote through the ballot client
- protected participation artefacts are accepted or rejected by the relevant intake services
- accepted public artefacts are published to the public evidence service
- the approved tally procedure is executed for the contest’s protocol profile
- the evidence package is reviewed for certification
- observers, auditors, and participants may inspect, verify, and challenge the published record within the applicable review window

Exact protocol sequence, object semantics, timing rules, and failure behavior belong to the Technical Protocol.

### 8.18 Cross-cutting requirements for every block

Every subsystem must support:

- signed and timestamped state changes
- minimum necessary data retention
- public or auditor-visible schema documentation
- separation of duties for operators
- full audit logging
- reproducible deployment and release integrity
- emergency downgrade and continuity procedures where applicable
- localization and accessibility for user-facing surfaces
- versioned interfaces and migration discipline

## 9. Identity and participation policy

This section defines platform-wide policy for identity, eligibility, recovery, and participation rights. Service responsibilities and exact semantics are defined elsewhere.

### 9.1 State-backed identity requirement

Protected civic acts require a state-backed digital identity recognized by the platform’s identity and eligibility framework.

### 9.2 Recovery policy

Recovery posture is proportional to assurance tier.

- Lower-assurance civic acts may use lower-friction recovery mechanisms permitted by policy.
- Higher-assurance and constitutionally significant contest classes require supervised or equivalently high-assurance recovery.
- No recovery path may silently weaken contest integrity or secret-ballot guarantees.

### 9.3 One effective participation right per person per contest

The platform must ensure that each eligible person has only the participation rights permitted for a given contest and produces only one effective outcome under contest policy.

### 9.4 Contest-specific eligibility

Eligibility is determined separately for each contest according to jurisdiction, legal status, and contest class. The platform must support auditable inclusion and exclusion decisions and clear handling of edge cases.

### 9.5 Diaspora participation

Diaspora participation must be supported without collapsing assurance requirements.

- Lower-assurance classes may permit remote participation.
- Higher-assurance classes may require supervised or consular channels.
- Contest-specific restrictions must remain explicit.

### 9.6 Identity minimization

Identity information is used only to establish who the person is, determine whether they are eligible, support lawful recovery, and support legally required audit and dispute handling.

## 10. Ballot guarantees

This section defines platform-wide guarantees for direct participation and secret-ballot classes. Exact mechanics belong to the Technical Protocol.

### 10.1 Secrecy where required

Where a contest requires secret ballot, the platform must preserve secrecy across authorization, preparation, submission, storage, tally, publication, and audit.

### 10.2 Public verifiability

The platform must provide a verifiability model sufficient for independent parties to determine whether the declared result is consistent with the approved process and accepted contest inputs.

### 10.3 Revoting and supervised override capability

The platform may support revoting and supervised override for contest classes where law and assurance policy permit. These are capabilities, not assumptions that apply everywhere.

### 10.4 No durable proof of vote choice

The platform must not provide participants with durable, third-party-usable proof of vote choice in secret-ballot contests.

### 10.5 Small-electorate secrecy safeguards

Where the effective electorate is too small for meaningful secrecy, the platform must apply safeguards such as delayed publication, pooled reporting, reduced granularity, alternate contest treatment, or alternate voting method.

### 10.6 Contest-sensitive guarantees

Secrecy, verifiability, revoting, override, and publication posture are bound to contest class, assurance tier, jurisdiction, and law.

## 11. Delegation governance policy

This section defines platform-wide governance rules for proxy delegation. Exact resolution and tally semantics belong to the Technical Protocol.

### 11.1 Delegation as an optional civic mechanism

Proxy delegation is an optional aid to participation, not a replacement for direct voting.

### 11.2 Delegate eligibility

A delegate must be:

- a natural person
- eligible under applicable rules
- registered under the public delegate framework
- bound by disclosure and accountability requirements

Organizations, parties, firms, or informal collectives may advocate, but they must not act as delegates in place of natural persons.

### 11.3 Delegate obligations

Registered delegates must maintain current public disclosures covering:

- identity
- relevant affiliations
- relevant funding relationships where required
- conflicts of interest
- rationale history
- any additional legally required declarations

### 11.4 Transparency model

The platform follows this transparency rule:

- public delegates are public
- private delegators remain private
- aggregate delegation visibility is permitted only within anonymity-preserving limits

### 11.5 Direct override principle

Delegation must remain reversible by the citizen within the contest policy framework.

### 11.6 Bounded accumulation of delegated influence

Delegated influence must be bounded through policy controls such as:

- per-contest caps
- domain-specific caps
- transitivity limits
- review thresholds
- anti-concentration monitoring

### 11.7 Transitivity posture

If transitive delegation is permitted, it must be explicit, limited in depth, reviewable, and governed by contest class.

### 11.8 Anti-cartel safeguards

The platform must support:

- anomaly monitoring
- disclosure of organized advocacy and funding where relevant
- concentration-triggered review
- contest-class-specific restrictions
- governance rules that discourage durable proxy capture

## 12. Contest initiation and lifecycle

This section defines the governance lifecycle by which issues become votable and move from proposal to legally recognized outcome.

### 12.1 Authorized initiation channels

A contest may enter the platform through one or more declared channels:

- government or parliamentary submission
- citizen initiative or threshold-triggered civic mechanism
- constitutionally or legally mandated trigger
- local or community process where law permits

### 12.2 Admissibility and legal preparation

Before a contest opens, it must pass the required intake and preparation stages, including:

- admissibility review
- legal formatting and canonical-text preparation
- jurisdiction and electorate confirmation
- constitutional or legal pre-review where required
- assignment of contest class and assurance tier

### 12.3 Mandatory publication before voting

Before voting opens, the platform must publish enough information for meaningful civic inspection, including:

- authoritative contest metadata
- official issue materials
- required legal and explanatory documents
- applicable disclosure information
- deliberation and voting dates

### 12.4 Deliberation minimums

Binding and high-impact contests must not move directly from intake to vote without a minimum deliberation and inspection period.

### 12.5 Voting phase

Once opened, the contest proceeds under the assigned participation mode, secrecy posture, delegation posture, assurance tier, and incident/fallback posture.

### 12.6 Review, challenge, and certification phase

After the voting window closes, the contest enters a formal post-vote phase including:

- publication of the relevant public evidence
- challenge and incident handling
- required audit and observer review
- certification or refusal to certify

### 12.7 Lifecycle traceability

Every contest must have a visible lifecycle state from proposal through archival. The lifecycle must be traceable, versioned where necessary, and resistant to silent procedural mutation.

## 13. Information integrity and deliberation policy

This section defines platform-wide rules for official issue presentation, civic deliberation, AI usage, and information ordering.

### 13.1 Canonical issue presentation

Every contest must use a canonical issue format. The detailed dossier schema lives elsewhere; this section defines the policy intent:

- consistency across issues
- comparable presentation
- source traceability
- protection against manipulative presentation differences

### 13.2 No algorithmic persuasion feed

The platform must not use engagement-ranked political feeds, paid amplification, hidden emotional optimization, or opaque recommendation logic inside the civic decision workflow.

### 13.3 Signed source corpus and provenance

Official summaries, explanatory materials, and issue dossiers must be grounded in a signed, versioned source corpus with visible provenance.

### 13.4 AI usage policy

AI may be used only in bounded, reviewable, provenance-aware ways such as:

- summarization
- translation
- readability adaptation
- accessibility support
- clustering of arguments
- contradiction detection

AI must not be used for:

- personalized persuasion
- psychographic targeting
- hidden ranking of political content
- silent rewriting of official materials
- covert steering of civic choice

### 13.5 Moderation accountability

Public reasoning spaces may be moderated, but moderation must be policy-bound, logged, reviewable, and visibly separate from contest validity and result determination.

### 13.6 Citizen assemblies and adversarial briefing

For complex or high-impact issues, the platform should support:

- citizen assemblies
- adversarial pro and con briefs
- expert notes
- minority reports
- implementation-oriented summaries

### 13.7 Decision pacing

The platform must manage decision volume and timing so that citizens are not overwhelmed by simultaneous high-stakes choices.

### 13.8 Information integrity as a security property

Provenance, transparency of summaries, moderation accountability, AI usage constraints, and non-manipulative ordering are core civic-control requirements.

## 14. User experience principles

User experience is a constitutional-quality requirement, not a decorative layer. The platform must be understandable, neutral, safe, and legible under real-world conditions.

### 14.1 UX objectives

The user experience must:

- make protected civic participation understandable without technical expertise
- reduce cognitive overload in high-stakes decisions
- support safe participation in coercion-sensitive environments
- preserve neutrality in presentation and interaction design
- make delegation comprehensible and reversible
- support trust through clear verification and evidence access

### 14.2 Core UX principles

The platform must follow these principles:

- neutrality of presentation
- progressive disclosure from plain-language summary to full legal detail
- comprehension before protected action for high-stakes issues
- visible reversibility where policy allows
- stable system behavior across contest classes and assurance tiers

### 14.3 Decision experience

Every contest should expose, in a stable layout:

- contest type and binding status
- key dates and deadlines
- plain-language summary
- what changes and what stays the same
- strongest case for and strongest case against
- constitutional, fiscal, and implementation notes
- current delegate status where relevant
- full text and source materials
- protected action entry point

### 14.4 Delegation experience

Users must always be able to tell:

- whether delegation is active
- whether it is issue-level or domain-level
- who the public delegate is
- whether the delegate has published a rationale
- whether direct override remains available

### 14.5 Coercion-aware and privacy-safe UX

The platform must support:

- safe-exit behavior
- verification without coercion artefacts
- privacy-preserving notifications
- neutral environment-sensitive guidance

### 14.6 Evidence and trust UX

The platform should make trust legible in human terms by explaining:

- what kind of contest the user is in
- who checked eligibility
- who cannot see the vote
- who can audit the result
- whether results are preliminary or certified
- whether challenges are open

### 14.7 Failure and degraded-mode UX

When material issues occur, the platform must present:

- plain-language incident status
- effect on the user’s next steps
- whether participation continues, pauses, or is restricted
- whether supervised fallback is available
- where official incident records are published

## 15. Accessibility and assisted participation requirements

Accessibility must be first-class and validated through user testing, not treated as a post-build compliance exercise.

### 15.1 Supported user groups

The platform must explicitly design for:

- citizens with low digital literacy
- elderly users
- blind and low-vision users
- deaf and hard-of-hearing users
- users with motor impairments
- users with cognitive disabilities or reduced reading stamina
- diaspora users
- users on low-end devices
- users with intermittent connectivity
- users in coercive households or workplaces
- public delegates performing repeated issue review
- auditors, observers, and journalists inspecting evidence

### 15.2 Baseline accessibility capabilities

The platform must support:

- screen readers
- keyboard-only navigation where relevant
- high-contrast mode
- scalable text
- audio guidance
- captions and transcripts where relevant
- reduced-motion mode
- touch targets suitable for motor impairments
- plain-language mode
- multilingual support
- low-bandwidth-friendly rendering

### 15.3 Cognitive accessibility

The platform must support:

- simplified summaries
- short sentences and clear labels
- consistent navigation
- progress indicators
- minimal context switching
- glossary support for legal and civic terms
- staged review flows

### 15.4 Language accessibility

The platform must clearly distinguish:

- authoritative legal text
- plain-language explanation
- translated explanation
- AI-assisted summary where used

Users must not confuse convenience summaries with the legally operative text.

### 15.5 Trusted helper mode

If helper-assisted participation is allowed, it must include:

- visible indication that helper mode is active
- strict helper permissions
- prevention of silent takeover
- strong auditability
- clear privacy warnings

### 15.6 Supervised access points

Supervised municipal, consular, or civic access points must support:

- queue-safe privacy
- rapid user handoff
- assisted accessibility setup
- controlled session reset
- neutral terminal state between users
- clear distinction between staff assistance and political guidance

### 15.7 Cross-channel continuity

A user who begins reading remotely and later uses a supervised channel should be able to resume without losing context, while still respecting the security posture of the supervised flow.

### 15.8 UX and accessibility acceptance criteria

The UX and accessibility layer is acceptable only if testing shows that representative users can reliably:

- understand what kind of contest they are in
- distinguish reading, delegating, voting directly, abstaining, and verifying
- find the strongest case for and against
- understand whether delegation is active and reversible
- complete protected participation without accidental disclosure
- use accessibility modes successfully
- navigate supervised or helper-assisted flows safely
- interpret result state and challenge state correctly
- recover from non-critical interruption without confusion

## 16. Security architecture

This section defines how the platform is secured as a system of institutions, services, trust boundaries, and operational controls. It stays at a high level by design.

### 16.1 Architectural stance

The platform uses a split-trust architecture.

Security is derived from:

- separation of powers across system domains
- constrained interfaces between domains
- public evidence and auditability
- threshold control over sensitive actions
- open verifiability
- gradual rollout by assurance tier

### 16.2 Security objectives

At the architectural level, the platform must satisfy these objectives:

- identity and ballot separation
- secrecy where required
- publicly checkable correctness
- controlled delegation
- no silent failure paths
- cryptographic continuity
- constitutional resilience

### 16.3 Architectural layers

The platform is organized into four security layers:

- civic governance layer
- identity and authorization layer
- participation and privacy layer
- public evidence and certification layer

### 16.4 Security domains

The platform is separated into the following security domains:

- identity domain
- eligibility domain
- contest and policy domain
- privacy domain
- delegation domain
- ballot-processing domain
- information and deliberation domain
- public evidence domain
- tally domain
- certification domain
- oversight domain

### 16.5 Trust-boundary rules

The architecture relies on:

- functional separation
- institutional separation
- cryptographic separation
- data separation
- legal separation where required

### 16.6 Assurance model

The platform uses assurance-tiered security rather than one uniform model for every decision:

- lower-assurance civic acts prioritize broad access and public evidence
- mixed-assurance local binding contests combine remote and supervised channels
- high-assurance binding contests prioritize integrity, coercion mitigation, and public legitimacy over convenience

### 16.7 Control families

The architecture is organized around these control families:

- identity and access controls
- authorization and uniqueness controls
- privacy and unlinkability controls
- delegation integrity controls
- ballot integrity controls
- transparency and public-evidence controls
- tally and certification controls
- cryptographic lifecycle controls
- operational resilience controls
- oversight and challenge controls

### 16.8 Cryptographic posture

The platform requires:

- a post-quantum-safe control plane from day one for platform-owned control surfaces
- a crypto-agile privacy core behind stable interfaces
- contest-pinned cryptographic profiles
- public cryptographic governance for transitions and deprecations

### 16.9 Client and endpoint posture

The architecture assumes that personal devices are not fully trustworthy.

Therefore:

- remote participation is allowed only where assurance policy permits
- public verifiability must compensate for endpoint uncertainty
- revoting and supervised override remain core mitigations where policy allows
- the highest-assurance contest classes should not depend solely on arbitrary personal devices
- verification must avoid becoming a coercion artefact

### 16.10 Evidence, audit, and retention posture

The platform must produce sufficient public evidence for independent review, while minimizing retained data that could later increase de-anonymization or coercion risk. Destruction must itself be auditable.

### 16.11 Incident and failure posture

The platform must fail visibly, not silently.

Defined states include:

- degraded operation
- contest pause
- extension
- supervised-only downgrade
- unresolved contest
- refusal to certify
- recovery after compromise

### 16.12 Architectural acceptance criteria

The security architecture is acceptable only if:

- no single domain can authenticate the person, interpret the ballot, and certify the result
- secret-ballot contest classes remain protected across domain boundaries
- delegation remains bounded, reversible, and publicly accountable
- public evidence is sufficient for independent verification
- critical failures produce visible governance states rather than hidden operator workarounds
- cryptographic transitions are governed and auditable
- retention and destruction policies preserve both auditability and privacy
- higher-stakes uses can be restricted to higher-assurance channels without redesigning the platform
- the architecture remains understandable enough to be governed by institutions and reviewed by independent experts

## 17. Cross-document alignment and public assurance

This section defines the relationship between this PRD, the Constitutional Governance and Threat Model, and the Technical Protocol. It also retains the public-assurance requirements that belong in the product layer.

### 17.1 Ownership boundaries across the document set

| Topic | PRD owns | Threat Model owns | Technical Protocol owns |
|---|---|---|---|
| Product scope and feature boundaries | Yes | No | No |
| Contest classes and assurance tiers | Yes, aligned to shared taxonomy | Yes, as constitutional scope | Referenced only |
| Democratic invariants | Referenced | Yes | Operationalized |
| Threat families, harms, red lines, viability | Referenced | Yes | Evidence support only |
| Subsystem responsibilities and trust boundaries | Yes | Referenced at governance level | Realized precisely |
| Cross-cutting product policy | Yes | Referenced where constitutionally relevant | No |
| Protocol entities and state objects | No | No | Yes |
| Override, revote, freeze, tally, proof semantics | No | No | Yes |
| Public evidence structure and verifier behavior | Referenced | Referenced | Yes |
| Rollout, readiness, and feasibility | Yes | Referenced for legitimacy conditions | Referenced for maturity constraints |

### 17.2 Public assurance requirements

The product posture requires:

- open source for critical components and verifier tooling where policy permits
- independent domestic audit
- external scrutiny
- public evidence and reproducibility materials
- public ceremonies for critical trust events
- sortition-based citizen oversight
- structured challenge rights
- stable public records of incidents and resolutions

### 17.3 Consistency rule

If there is tension between a high-level statement in this PRD and a precise technical rule in the Technical Protocol, the protocol governs the operational semantics. If there is tension between this PRD and the Constitutional Governance and Threat Model on democratic invariants, rights posture, red lines, or viability conditions, the Threat Model governs.

## 18. Rollout roadmap

### 18.1 Phase 0: Constitutional and technical foundation

Deliver:

- legal and constitutional charter alignment
- institutional split
- contest taxonomy aligned with the Threat Model
- protocol registry
- audit framework
- challenge framework
- observer tooling
- public mock environment

Exit gate:

- no critical unresolved architectural findings
- public scrutiny period completed
- baseline audit and reproducibility proven

### 18.2 Phase 1: Lower-assurance protected civic acts and consultative contests

Deploy:

- protected civic initiation acts
- petitions and threshold sponsorship
- consultative issue voting
- non-binding delegation in permitted classes

Exit gate:

- strong uptake
- no major trust failures
- independent verification tooling used in the wild

### 18.3 Phase 2: Local binding contests

Deploy:

- participatory budgeting
- bounded local governance questions
- supervised municipal access points
- delegate disclosures and concentration controls

Exit gate:

- repeated successful audits
- coercion and access analysis completed
- local legitimacy accepted by relevant authorities and observers

### 18.4 Phase 3: National consultative shadow chamber

Deploy:

- national consultative issue voting
- proxy ecosystem at scale within bounded rules
- constitutional review rehearsal
- large-scale observer and verifier use

Exit gate:

- sustained public scrutiny
- mature challenge handling
- stable operational evidence

### 18.5 Phase 4: Limited high-stakes binding deployment

Deploy:

- selected national binding contest classes that are constitutionally authorized
- supervised-default channels
- full evidence publication
- formal certification and public challenge cycles

Exit gate:

- repeated successful audits
- legal confidence
- no severe unresolved protocol or legitimacy risks

### 18.6 Phase 5: Advanced cryptographic migration

Introduce:

- upgraded suites
- mature hybrid or post-quantum components where justified
- stronger identity and credential modules as standards and public review justify

Exit gate:

- public approval for relevant privacy-core upgrades
- successful migration drills
- no loss of public verifiability

## 19. Acceptance criteria

A contest class is production-ready only if all of the following are true:

- no single institution can both identify voters and alter the result without detection
- direct participation overrides proxy reliably where policy requires it
- public verifiers can independently validate the public evidence package
- revoting and supervised override behave as declared for the contest class
- small-electorate secrecy safeguards are enforced
- accessibility testing passes for representative users
- red-team findings above threshold are resolved
- challenge workflows are live and exercised
- supply-chain reproducibility is demonstrated
- incident response drills have been performed
- implementation ownership is clearly assigned for binding outcomes

## 20. Feasibility and unresolved risks

### 20.1 Feasible now

- protected civic initiation acts
- consultative civic contests
- participatory budgeting
- local decisions with mixed remote and supervised channels
- proxy delegation with direct override under bounded rules
- public delegate ecosystems with disclosure and caps
- open-source verifier tooling and public evidence publication
- strong audits, challenge workflows, and crypto-agile architecture

### 20.2 Feasible with discipline

- binding local contests at meaningful scale
- national consultative shadow-chamber behavior
- private delegators and public delegates at scale
- high-legitimacy public evidence bundles
- supervised high-stakes channels for selected binding acts
- protocol-governed privacy cores with public approval

### 20.3 Not honestly solved today

- fully remote, personal-device, national binding legislation with strong coercion resistance, strong client integrity, and broad social legitimacy
- large-scale proxy democracy without continuing pressure toward cartelization
- a mature, drop-in post-quantum privacy-preserving voting stack for the full anonymous ballot and proof path

### 20.4 Major unresolved risks

- post-quantum anonymous credentials for national-scale unlinkable participation
- post-quantum-ready tally and proof systems with mature public review
- migration of the state eID ecosystem itself
- preserving meaningful secrecy in very small electorates
- preventing delegate ecosystems from becoming shadow parties
- maintaining legitimacy when cryptographic complexity exceeds ordinary public understanding
- keeping deliberation structured without drifting into censorship or paternalism

## 21. Product conclusion

This platform is realistic as a staged civic operating system. It is not realistic as a one-shot national direct democracy application.

The credible path forward is:

- build the institutional split first
- launch lower-risk civic acts first
- keep proxy delegation accountable, reversible, and bounded
- treat public auditability as mandatory
- keep the highest-stakes contest classes on the highest-assurance channels
- move the privacy core toward stronger post-quantum assurance only as standards, audits, and public legitimacy justify it

That is the right merge between ambition and honesty.
