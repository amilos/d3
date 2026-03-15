# Constitutional Governance and Threat Model

## Part I — Constitutional frame

### 0. Document charter

#### 0.1 Purpose

This document defines the constitutional governance and threat model for a civic participation platform that supports direct participation, bounded proxy delegation, protected civic initiation, consultative contests, participatory budgeting, local binding contests, and selected national binding contests under differentiated constitutional conditions.

Its purpose is to specify the democratic invariants, harms, threat families, control families, governance structures, red lines, escalation logic, and protocol-facing requirements needed for such a system to remain a constitutionally serious instrument of citizen agency rather than a digital facade of participation.

This is a governance document for a high-risk civic system. It is not a product brochure, software specification, campaign manifesto, or general theory of democracy.

#### 0.2 Document type and status

This is a normative constitutional governance document.

It defines:

- what the system is constitutionally allowed to be
- what it must protect
- what kinds of failure it must recognize
- what controls must exist
- who owns risk
- when fail-safe action is required
- what the companion technical document must make operational and evidentiary

It does not define the full protocol, message flows, cryptographic constructions, or implementation semantics. Those belong to the protocol appendix or companion technical specification.

Unless explicitly stated otherwise, this document is binding on system design, deployment, review, and contest-class authorization.

#### 0.3 Companion documents

This document is designed to be read together with the following materials.

##### 0.3.1 Product and system-design materials

These define product scope, contest classes, user roles, deployment posture, and architectural intent.

##### 0.3.2 Protocol appendix or technical specification

This defines the technical actors, trust boundaries, state objects, protected-action flows, evidence artifacts, cryptographic suite binding, verifier posture, retention behavior, and protocol-level acceptance tests required by Section 13.

##### 0.3.3 Operational annexes

These include at minimum:

- Annex A — Operational Threat Register Template

Additional annexes may later cover scenario templates, audit reporting formats, or certification profiles, but they remain subordinate to this document.

#### 0.4 Audience

This document is addressed to:

- constitutional and administrative designers
- electoral and civic administrators
- product and system architects
- security and cryptography reviewers
- oversight and audit bodies
- courts or review authorities
- policy designers
- public-interest evaluators

It is written for a mixed audience because neither a purely legal nor a purely technical document is sufficient for a system of this kind.

#### 0.5 Normative hierarchy

The following hierarchy governs interpretation across the document set:

- constitutional rights and higher-order law prevail over every lower rule in this document
- this document prevails over operational convenience, administrative custom, product preference, and undeclared technical behavior
- the protocol appendix may specify technical detail only in ways that do not weaken this document’s democratic invariants, scope limits, control requirements, red lines, or governance rules
- annexes implement and operationalize this document; they do not override it

Where technical convenience conflicts with constitutional requirement, constitutional requirement prevails.

#### 0.6 Change discipline

Changes to this document are themselves governed.

No amendment may be treated as trivial if it affects:

- contest-class scope
- rights posture
- secrecy rules
- delegation posture
- channel posture
- evidence obligations
- fail-safe conditions
- governance authority
- viability conditions

Any material change must be:

- recorded
- justified
- versioned
- reviewable
- accompanied, where relevant, by conforming changes to the protocol appendix, annexes, and contest-class rules

### 1. Executive summary

This document governs a civic system that supports multiple forms of citizen participation under differentiated constitutional conditions. It covers protected civic initiation and threshold acts, consultative issue voting, participatory budgeting, local or community binding contests, selected national binding contests, and bounded proxy delegation with direct override.

The system is not treated as one uniform voting mechanism. It is treated as a family of contest classes with different legal force, secrecy posture, channel posture, coercion sensitivity, and governance burden.

#### 1.1 What the system is

The platform is a constitutional system whose legitimacy depends on the full chain from rulemaking to archival memory. It is designed to restore citizen agency without recreating hidden intermediation monopolies.

#### 1.2 What the system is not

It is not:

- a generic voting app
- a digital shortcut around constitutional rights
- a platform where proxy delegation may silently become oligarchic intermediation
- a product that can be legitimized by cryptography alone
- a substitute for judicial review, implementation discipline, or public accountability

#### 1.3 Core constitutional posture

The system is built around six commitments:

- equal civic standing remains the non-negotiable baseline
- direct citizen participation remains supreme wherever direct participation is permitted
- secrecy where required is treated as a practical constitutional condition, not merely a mathematical claim
- public delegates and private delegators are distinct constitutional roles
- implementation fidelity matters as much as result production
- constitutional validity prevails over operational continuity

#### 1.4 Highest-order threats

The system is designed under the assumption that democratic distortion rarely appears only as crude ballot tampering. Highest-order threats include:

- charter capture and rule design bias
- agenda capture and docket flooding
- admissibility choke-point control
- manipulation of official issue understanding
- coercion in homes, workplaces, and local dependency networks
- practical loss of secrecy in small or socially dense electorates
- proxy cartelization and shadow-party formation through delegates
- software trust-chain compromise
- availability sabotage and timing attacks
- certification delay or evidence failure
- implementation sabotage after valid outcomes
- sustained legitimacy warfare aimed at making valid civic outcomes socially non-binding

The threat model is therefore constitutional, institutional, social, informational, and technical at once.

#### 1.5 Viability floor

The system is viable only if, at minimum:

- no single trust domain dominates protected acts end-to-end
- at least one independent oversight and review path remains live
- open verification remains lawful and practical
- supervised access remains realistically available where required
- implementation review is not monopolized by the executive
- public evidence publication remains possible

If these conditions no longer hold for a contest class, that class is no longer constitutionally ready, regardless of whether the software still technically runs.

#### 1.6 Deployment posture

The framework adopts a consultative-first and class-sensitive deployment posture:

- lower-stakes and consultative uses can mature earlier
- local binding uses require stronger secrecy and coercion discipline
- selected national binding uses require the strictest review, evidence, and channel posture

Operational success in one contest class does not automatically justify deployment in another.

#### 1.7 Success criteria

Success does not mean frictionless digital participation. It means:

- citizens retain equal civic standing
- direct participation remains real even where delegation exists
- secrecy where required remains credible in practice
- issues are understandable
- delegates remain bounded and accountable
- outcomes are evidence-backed and challengeable
- implementation is visible and enforceable
- the system remains capable of saying stop when legitimacy conditions no longer hold

### 2. Scope, contest classes, and constitutional posture

This section defines what the system governs, what it does not govern, how much force different contest classes carry, what secrecy and channel posture they require, and under what distrust assumptions they are judged.

#### 2.1 Interpretation principles

##### 2.1.1 The system is class-based, not monolithic

No part of this document shall be read as though all civic acts are governed by the same secrecy rule, channel rule, delegation rule, or evidentiary burden.

##### 2.1.2 Higher constitutional force requires higher constitutional assurance

As the legal force of a contest increases, the burden of admissibility, intelligibility, secrecy protection, anti-coercion protection, review, and public evidence also increases.

##### 2.1.3 Scope is a constitutional decision

What the system is allowed to govern is itself part of constitutional design. A system may be technically capable of supporting a decision type and still be constitutionally unfit to govern it.

##### 2.1.4 Channel posture is constitutionally relevant

The choice between remote, supervised, hybrid, or supervised-default participation affects coercion risk, access parity, secrecy, and legitimacy. Channel decisions must therefore be tied to contest class, not merely to convenience.

##### 2.1.5 Delegation is conditional and bounded

Delegation is a constitutionally permitted aid to civic participation, not a transfer of sovereignty, not a substitute for equal civic standing, and not a license for proxy oligarchy.

#### 2.2 Contest-class summary table

| Class | What it covers | Binding force | Channel posture | Secrecy posture | Delegation posture |
|---|---|---|---|---|---|
| A | Protected civic initiation acts such as citizen initiatives, threshold sponsorship, agenda qualification, recall or veto triggers | Triggering or threshold-bearing only | Remote-eligible | Private but attributable | Not applicable or limited by law |
| B | Consultative civic contests such as non-binding issue votes and civic prioritization | Advisory | Remote-eligible | Usually secret ballot | Allowed where policy permits |
| C | Participatory budgeting contests within a bounded budget envelope | Binding within local law with implementation duty | Hybrid | Secret ballot by default with small-electorate safeguards | Allowed with stronger local controls |
| D | Local or community binding contests within a defined jurisdiction | Binding subject to review and implementation duty | Hybrid or supervised-default depending on risk | Secret ballot by default | Allowed only under explicit class rules |
| E | Selected national binding contests lawfully assigned to direct civic competence | Binding subject to constitutional review | Supervised-default unless formally elevated | Secret ballot with highest assurance | Strongly bounded and class-specific |
| F | Delegation and proxy-state acts such as delegate registration, delegation, revocation, override | Not substantive contests | Class-dependent | Usually private-but-attributable or public depending on act | Core class itself |
| G | Public delegate acts such as instructions, rationales, disclosures | Public constitutional effect | Public or regulated channel | Public | Not applicable |

#### 2.3 Classes in scope

##### 2.3.1 Class A — Protected civic initiation acts

These are protected civic acts through which citizens initiate, support, or trigger constitutional or statutory civic processes. They include citizen initiatives, support for petition thresholds, agenda qualification thresholds, recall or veto triggers where constitutionally allowed, and other threshold-bearing civic acts.

##### 2.3.2 Class B — Consultative civic contests

These are non-binding issue votes or ranking exercises intended to inform public institutions, delegates, or the broader public sphere. They may shape legitimacy and agenda-setting even without direct legal force.

##### 2.3.3 Class C — Participatory budgeting contests

These are contests in which citizens directly decide or rank the allocation of a defined budgetary portion within a legally bounded domain.

##### 2.3.4 Class D — Local or community binding contests

These are legally binding contests within a defined local or community jurisdiction.

##### 2.3.5 Class E — Selected national binding contests

These are high-stakes contests with national legal force, but only within subject-matter classes lawfully admitted to direct civic resolution.

##### 2.3.6 Class F — Delegation and proxy-state acts

These are protected civic acts by which citizens structure representation within the system. Because proxy relationships can accumulate into real constitutional power, these acts are treated as a distinct class for governance purposes.

##### 2.3.7 Class G — Public delegate acts

These are public acts performed by registered delegates in their role as visible civic intermediaries.

#### 2.4 Contest classes out of scope

The following categories are out of scope for ordinary operation unless a higher constitutional instrument explicitly provides otherwise:

- individual adjudications
- rights-restricting acts outside enhanced constitutional procedure
- measures targeting named persons or narrow identifiable groups
- ultra-small-electorate secret-ballot contests
- contest classes requiring coercive individualized enforcement without lawful mediation
- any matter not assigned to direct civic competence by law

Scope expansion is a constitutional act, not a product update.

#### 2.5 Binding-force taxonomy

Every contest in scope must belong to one of the following constitutional-effect categories:

- advisory
- binding subject to constitutional review
- binding with implementation duty
- self-executing
- constitutionally escalated

#### 2.6 Channel posture by assurance tier

The system uses differentiated channel posture according to contest class and constitutional risk:

- remote-eligible posture for protected civic initiation acts, consultative contests, and selected lower-risk participation flows
- hybrid posture for participatory budgeting, selected local binding contests, and classes where access flexibility is desirable but coercion and secrecy conditions require additional safeguards
- supervised-default posture for selected national binding contests and any class for which coercion, secrecy, and legitimacy concerns make ordinary remote participation too risky

No contest may open without an explicitly declared channel posture.

#### 2.7 Secrecy posture by civic-act class

Every contest and protected civic act must be assigned a secrecy posture in advance:

- secret-ballot contests
- private-but-attributable civic acts
- public constitutional acts

No secrecy rule may be improvised midstream.

#### 2.8 Delegation posture

Delegation is constitutionally allowed only under the following baseline conditions:

- delegation is optional
- direct participation remains supreme
- delegation must be bounded
- delegation posture is contest-class dependent

At minimum, the legal and operational framework must explicitly define, per contest class:

- whether delegation is allowed
- whether domain delegation is allowed
- whether issue delegation is allowed
- whether transitivity is allowed
- whether one-hop only is required
- when delegation freezes

#### 2.9 Deployment posture

The document assumes a staged constitutional deployment posture:

- consultative-first
- no class inherits readiness from another class
- expansion requires renewed constitutional justification

#### 2.10 Threat posture

This document is written under an explicit distrust posture. It assumes partial institutional capture, strategic use of lawful powers, political attempts to reconstitute monopolies through delegates or agenda channels, adversarial information conditions, untrusted client devices, coercive households or employers, possible foreign interference, and implementation sabotage after valid civic action.

#### 2.11 Scope integrity rule

No later section of this document, and no protocol choice made under it, may silently expand the subject-matter scope, binding force, secrecy class, delegation posture, or channel posture of any contest class beyond what is declared here or lawfully amended under the system’s own constitutional review rules.

### 3. Democratic invariants

The following democratic invariants define the minimum conditions under which the system remains constitutionally legitimate. They are binding design constraints on law, governance, operations, and protocol.

#### 3.1 Core democratic invariants

##### I1. Equal civic standing

Every eligible citizen possesses equal formal civic standing in the system.

##### I2. One effective civic path per citizen per contest

For every contest, each eligible citizen shall have exactly one effective civic outcome path: direct vote, delegated vote, or abstention.

##### I3. Supremacy of direct participation

A valid direct act by a citizen overrides any proxy, delegation, or derived delegated position affecting that same contest up to the legally defined close of the contest.

##### I4. Revocability of delegation

All delegation must be revocable by the delegating citizen until the legally defined close of the contest or until a stricter statutory freeze point that is itself publicly known, narrowly tailored, and uniformly applied.

##### I5. Secret ballot where constitutionally required

For every contest classified as secret, no institution, officer, delegate, employer, family member, political actor, or colluding set of actors below the legally defined threshold may both identify the citizen and determine that citizen’s final choice.

##### I6. No durable proof of vote choice

The system shall not furnish citizens with durable, transferable proof of their final choice in any secret-ballot contest.

##### I7. Public delegates and private delegators

Any person acting as a public delegate must be publicly identifiable, must disclose required conflicts and affiliations, and must be subject to public performance scrutiny. The identities of delegating citizens shall not be publicly disclosed, except where a different disclosure rule is constitutionally and explicitly defined for a non-secret contest class.

##### I8. Delegation concentration must remain constitutionally bounded

Delegation may not be allowed to accumulate into hidden oligarchy.

##### I9. Agenda integrity

No actor, office, faction, funding bloc, or coordinated network may monopolize, flood, invisibly filter, or strategically distort what questions reach citizens, when they reach them, or under what framing they are decided.

##### I10. Contest intelligibility

No binding contest may proceed unless an ordinary citizen, acting with reasonable effort and ordinary civic literacy, can understand what is being decided, what changes if it passes, what stays the same if it fails, the strongest argument for and against, and the principal constitutional, fiscal, and implementation consequences.

##### I11. Single-subject integrity

Every binding contest must satisfy a genuine single-subject rule unless a higher constitutional procedure explicitly allows bundled settlement.

##### I12. Rights floor and anti-majoritarian guardrail

No valid popular act may abolish, suspend, or materially hollow out fundamental constitutional rights except through a clearly defined higher-order constitutional amendment procedure with enhanced safeguards.

##### I13. Accessibility parity

The practical inability to use digital systems shall not become a hidden form of disenfranchisement.

##### I14. Neutrality of civic infrastructure

The system itself shall not manipulate, rank, nudge, shame, psychographically steer, or commercially optimize citizens toward substantive political outcomes.

##### I15. Provenance and auditability of official information

Every official summary, explanation, translation, AI-generated synthesis, and impact statement used inside the system must be attributable to a signed source corpus and preserved in versioned public records.

##### I16. Challengeability and remedy

Every meaningful civic act in the system must be challengeable through a public, time-bounded, reviewable process.

##### I17. Safe degradation, not silent exception

When security, secrecy, coercion risk, institutional neutrality, or legitimacy thresholds are materially breached, the system must degrade into a safer, more supervised, and more transparent mode.

##### I18. Symmetry of burden and benefit

No contest shall be structured so that one class of citizens bears concentrated burdens while another captures diffuse benefits without explicit constitutional disclosure and review.

##### I19. Implementation fidelity

A validly adopted outcome must enter a public implementation track with named responsible authorities, timelines, required secondary acts, and visible non-compliance signals.

##### I20. Periodic re-legitimation of the system itself

The platform, its delegation rules, its admissibility regime, and its emergency procedures must themselves be periodically reviewed under public scrutiny.

#### 3.2 Priority hierarchy among invariants

Where invariants come into tension, they shall be ordered as follows unless the constitution explicitly states otherwise:

- rights floor and anti-majoritarian guardrail
- equal civic standing
- secret ballot where required
- one effective civic path per citizen per contest
- supremacy of direct participation
- agenda integrity
- contest intelligibility
- challengeability and remedy
- accessibility parity
- implementation fidelity

#### 3.3 Invariant enforcement matrix

The main body keeps the invariant statements constitutional and readable. The structured enforcement fields are moved into the following matrix.

| Invariant | Breach condition | Detection | Adjudicator | Default remedy |
|---|---|---|---|---|
| I1 | Unequal base vote weight, eligibility standard, or access channel | Legal review, audit of eligibility and channel access, public challenge | Constitutional review gate | Suspension of affected contest class or rule |
| I2 | Citizen influences the same contest through more than one counted path | Protocol audit, tally audit, independent verification | Certification authority plus constitutional review gate for systemic breaches | Contest invalidation if material |
| I3 | Direct vote fails to supersede delegated resolution | Individual verification, public proof review, challenge procedure | Election administration first, constitutional review for systemic defects | Correction where possible; rerun if systemic |
| I4 | Delegations cannot be reasonably revoked, or revocation operates selectively or opaquely | UX audit, legal audit, incident reports, citizen complaints | Oversight council and electoral administration; constitutional review if structural | Extension of contest window or invalidation of affected delegation state |
| I5 | Voter choice can be learned, inferred with high confidence, or compelled | Technical audit, anonymity-set analysis, social-risk review, coercion complaints | Constitutional review gate with mandatory technical input | Downgrade channel, pool or suppress results, or refuse contest |
| I6 | Citizen can reliably demonstrate final vote choice using system-provided evidence | Security review, red-team exercise, field complaints | Certification authority and constitutional review gate | Immediate disablement of offending verification pathway |
| I7 | Delegates exercise public influence anonymously, or delegators become publicly exposed in secret/protected contexts | Registry audit, privacy audit, public challenge | Electoral administration and privacy authority; constitutional review if systemic | Delegate suspension, data suppression, contest remedy where material |
| I8 | Delegation concentration exceeds legal caps, or effective control concentrates through transitive or coordinated structures beyond allowed limits | Concentration metrics, graph analysis, disclosure audit, observer reports | Oversight council and electoral authority; constitutional review for repeated or structural cases | Cap enforcement, spillover rules, or contest-class redesign |
| I9 | Issue intake, scheduling, admissibility, bundling, or sequencing is materially captured or biased | Agenda-source reporting, timing audits, admissibility statistics, external review | Constitutional review gate with mandatory public reasoning | Rescheduling, re-docketing, invalidation of biased intake decisions |
| I10 | Contest wording or dossier is materially unintelligible, misleading, incomplete, or asymmetrically framed | Readability testing, adversarial review, citizen assembly feedback, public challenge | Admissibility authority, then constitutional review | Contest pause and mandatory redrafting |
| I11 | Unrelated or weakly related matters are bundled into one irreversible choice | Legal review, adversarial briefing, public challenge | Constitutional review gate | Severance or invalidation |
| I12 | Contest authorizes rights-infringing outcomes outside the required constitutional pathway | Mandatory pre-vote constitutional review and post-vote challenge | Constitutional court or equivalent review gate | Inadmissibility or nullification |
| I13 | Specific groups are materially under-served or structurally burdened | Accessibility audits, demographic participation analysis, supervised-site coverage review, complaints | Electoral administration, accessibility authority, oversight council | Channel expansion, supervised access, deadline extension, or contest suspension |
| I14 | Opaque ranking, personalized persuasion, asymmetrical exposure, paid amplification, or behavioral nudging toward vote choices inside the system | Algorithm audit, source review, adversarial testing, observer inspection | Oversight council, independent auditors, constitutional review for structural design violations | Disablement of offending module and mandatory public disclosure |
| I15 | Official explanatory material lacks provenance, version history, or challenge path | Content audit, public challenge, observer review | Electoral administration and oversight council | Contest pause if material to decision quality |
| I16 | No effective challenge path exists, or challenges are formally allowed but practically ignored, delayed, or buried | Procedural audit, challenge tracking, public reporting | Designated review body with appellate constitutional path | Stay of certification or implementation where warranted |
| I17 | Emergency or incident handling silently changes rules, visibility, secrecy, or counting logic without lawful trigger and public notice | Incident review, observer monitoring, audit trails, public reporting | Multi-body emergency review with constitutional oversight | Suspension of affected class and publication of emergency reasoning |
| I18 | Material burden asymmetries are concealed or omitted from the contest dossier | Fiscal review, impact analysis, adversarial briefing | Admissibility authority and constitutional review gate | Dossier correction or contest pause |
| I19 | Passed act is delayed, starved, diluted, or ignored without lawful review | Implementation tracker, public oversight, judicial complaints | Implementation oversight body, then constitutional/judicial path | Mandatory compliance order, sanctions, or automatic review trigger |
| I20 | Core rules become effectively unchangeable by ordinary constitutional means, or review is indefinitely postponed | Governance audit, statutory review calendar, oversight reporting | Constitutional legislature and review gate | Mandatory review session and public report |

### 4. Assumptions, distrust posture, and viability conditions

This section identifies the assumptions on which the system depends, the assumptions it refuses to make, the minimum conditions under which it remains constitutionally viable, and the distrust posture under which all later sections must be interpreted.

#### 4.1 Interpretation principles

##### 4.1.1 Assumptions are not guarantees

Any assumption stated in this section may fail in practice. The purpose of stating it is not to naturalize it as safe, but to make explicit whether the system can still function if it weakens, degrades, or is partially violated.

##### 4.1.2 Viability is conditional, not absolute

The system is not assumed to be either perfectly safe or wholly impossible. It is viable only under certain minimum political, legal, institutional, informational, and technical conditions.

##### 4.1.3 Distrust is structural

This document does not assume universal malice. It assumes that constitutional design must survive strategic behavior, selective enforcement, incentive distortion, lawful abuse, collusion, and institutional self-protection without requiring unusual virtue from powerful actors.

##### 4.1.4 Residual dependency is unavoidable

No system of this kind can eliminate all dependence on institutions, operators, legal review bodies, infrastructure, or social conditions. The relevant constitutional task is therefore not to pretend dependency does not exist, but to declare it, minimize it, distribute it, and make it reviewable.

##### 4.1.5 Hidden assumptions are constitutionally dangerous

Any condition on which legitimacy materially depends must be made explicit somewhere in this document set. No critical assumption may remain hidden inside technical practice, vendor behavior, customary procedure, or institutional culture.

#### 4.2 Assumptions that may fail

The system must assume that failures may arise in at least the following domains:

- institutional neutrality may fail
- citizens may face coercive or dependency-based social conditions
- the information environment may be adversarial or concentrated
- technical components and environments may be compromised or unevenly mature
- implementation may fail after certification through delay, reinterpretation, or sabotage

#### 4.3 Minimum viability conditions

The system is constitutionally viable only if the following minimum conditions remain true:

- no single trust domain may dominate protected acts end-to-end
- at least one independent oversight and review path remains live
- open verification must remain lawful and practically possible
- supervised access must remain realistically available where constitutionally required
- implementation review must not be wholly monopolized by the executive
- public evidence publication must remain possible
- channel equality must remain materially defensible
- the legal order must still recognize the distinction between valid result and arbitrary power

#### 4.4 Explicit distrust posture

The system is designed under an explicit distrust posture. It assumes that all of the following may act strategically under pressure, incentive, or opportunity:

- incumbent executives
- parliamentary majorities
- party machines
- administrative insiders
- public delegates
- delegate cartels
- review bodies
- technical operators
- release custodians
- local authorities
- media and platform coalitions
- organized private interests
- emergency decision-makers
- implementation authorities

The system therefore attempts, wherever possible, to respond to distrust by:

- distribution of authority
- public evidence
- challengeability
- bounded discretion
- reviewable transitions
- fail-safe degradation
- explicit residual assumptions

#### 4.5 Residual dependence rule

The system will inevitably depend, at least in part, on:

- state identity infrastructure
- legal review institutions
- operational authorities
- public evidence publication infrastructure
- software and verifier ecosystems
- supervised access environments
- the broader political and informational order in which it operates

These dependencies are constitutionally acceptable only if they are declared, minimized, distributed, reviewable, and prevented from silently redefining constitutional meaning.

#### 4.6 Assumption failure and constitutional response

When an assumption weakens or fails, the response must not be improvisational. Assumption failure shall instead be handled through one or more of the following:

- elevated review
- stronger contest-class restrictions
- channel downgrade
- supervised fallback
- enhanced evidence publication
- contest pause or rescheduling
- contest-class suspension
- refusal to proceed where viability is no longer present

#### 4.7 Viability interpretation rule

The system shall be deemed constitutionally non-viable for a contest class if the minimum viability conditions are not met and no lawful fail-safe action can restore them in time.

### 5. Actors, incentives, and collusion map

This section identifies the actors who can shape, distort, capture, defend, or restore the constitutional integrity of the system. The point is to map power, incentives, dependencies, and collusion paths, not to moralize about motives.

#### 5.1 Interpretation principles

- incentives matter more than declared intent
- lawful powers can be weaponized
- coalitions matter more than lone actors
- capacity asymmetry is constitutionally relevant
- technical roles are constitutional roles when they can affect protected acts
- distrust is structural, not personal

#### 5.2 Internal actors

| Actor | Role | Legitimate interests | Distortion incentives or vulnerabilities | Primary constraints |
|---|---|---|---|---|
| Citizens | Hold civic standing and remain the ultimate source of authority in direct-participation and proxy-enabled contest classes | Equal standing, meaningful participation, secrecy where required, understandable choices, remedy when harmed, visible implementation | Rational disengagement, overreliance on delegates, coercion, fatigue, manipulative simplification, abstention under emotional salience | One effective path per contest, identity and eligibility rules, contest intelligibility, protected-action rules, challenge procedures |
| Public delegates | Receive revocable civic trust in contest-specific or domain-specific matters | Persuading citizens, aggregating judgment, building public trust, publishing reasons and expertise | Concentration of delegated power, brand-building into shadow parties, hidden financing, brokerage for organized interests, transitivity opacity | Public registration, disclosure duties, concentration caps, revocability, direct-vote override, public rationale history, challengeability |
| Election and contest administration | Runs intake, scheduling, contest lifecycle management, operational support, certification workflow, public process handling | Orderly conduct, timely certification, operational continuity, predictable procedures, public confidence | Procedural conservatism, selective delay, overbroad incident framing, informal rulemaking, privileging incumbent or familiar actors | Published rules, reviewable deadlines, evidence publication duties, challenge workflow, multi-body certification, fail-safe limits |
| Identity authority | Authenticates legal identity for protected civic acts | Integrity of identity, fraud prevention, lawful recovery, operational reliability | Selective recovery, unequal access, biased exception handling, over-collection or misuse of identifying data | Equality of access, recovery discipline, auditability, strict separation from ballot knowledge, legal limits on data sharing |
| Eligibility authority | Determines whether a legally identified person is eligible to act in a given contest | Clean voter rolls, contest-specific accuracy, lawful exclusions, correction of errors | Selective inclusion or exclusion, delayed correction, discriminatory edge-case handling, coupling eligibility decisions to political timing | Reviewability, publication of metrics, separation from ballot content, correction deadlines, challenge rights |
| Privacy-credential, ballot, tally, and certification authorities | Issue unlinkable participation rights or equivalent credentials, receive and process protected ballot artifacts, generate result bundles, certify outcomes according to law | Correctness, secrecy where required, verifiability, evidence completeness, certifiable outcomes | Over-centralization of trust, excessive secrecy justified in technical language, under-disclosure of anomalies, resistance to external verification, pressure to certify under uncertainty | Threshold control, public evidence obligations, verifier diversity, reproducibility requirements, multi-body certification, fail-safe rules |
| Technical operators, maintainers, and release custodians | Manage source control, build systems, release signing, dependency governance, verifier tooling, supervised-terminal images, software distribution | Reliability, maintainability, secure deployment, operational consistency | Quiet operational shortcuts, hidden dependency risk, centralization of release trust, resistance to independent rebuilds, under-reporting of trust-chain incidents | Reproducible builds, multi-party release signing, SBOM discipline, attestation, public manifests, incident disclosure, independent mirror and verifier ecosystem |
| Constitutional review gate | Determines admissibility, rights compatibility, legal bounds, and post-vote constitutional validity | Rights protection, competence boundaries, legality of process, prevention of invalid outcomes | Procedural overreach, selective blockage, ideological gatekeeping, strategic timing, de facto co-governance | Narrow review grounds, reason-giving, deadlines, appellate or secondary review, public hearing requirements for major exclusions |
| Executive branch | Implements law, influences agenda, controls substantial state capacity | Governability, policy coherence, lawful execution, public order, continuity | Agenda capture, emergency-law opportunism, manipulation of access conditions, politicized use of administration, implementation sabotage | Rights floor, public evidence, judicial review, implementation tracking, multi-body emergency authorization, legislative and public scrutiny |
| Parliament and formal legislative bodies | Set legal framework, may originate issues, may ratify or implement results, may coexist with direct-participation structures | Legislative coherence, constitutional ordering, budget discipline, preservation of parliamentary role | Preserving monopoly over agenda, diluting direct-participation outcomes, procedural delay, selective incorporation, defensive redesign to protect party power | Constitutional supremacy of valid direct outcomes where applicable, public schedule and review rules, implementation duties, public accountability |
| Local government and supervised-site operators | Provide local administrative support, supervised access, local implementation, local communication, contest logistics | Service delivery, lawful local administration, stable execution, conflict reduction | Localized patronage, under-service of unfriendly populations, informal pressure networks, manipulation of access conditions, selective support | Accessibility parity, service standards, auditability, neutral supervised access obligations, local challenge rights |
| Public broadcasters, regulators, and official information bodies | Shape how official civic information, contest notices, public education, and procedural explanations reach the public | Public education, accurate procedural information, broad reach, neutrality | Selective amplification, procedural framing bias, narrative harmonization with incumbents | Neutrality duties, signed source corpus, provenance rules, external scrutiny, public complaint paths |
| Sortition oversight council | Citizen body selected by lot with formal oversight, inspection, escalation, and publication rights | Democratic legitimacy, non-partisan scrutiny, public confidence | Capture through asymmetrical expertise, overload, symbolic oversight, dependence on filtered disclosure | Guaranteed access rights, training, publication rights, protection from retaliation, transparent procedures |

#### 5.3 External actors

| Actor | Legitimate interests | Distortion incentives or vulnerabilities |
|---|---|---|
| Political parties | Representing preferences, contesting policy, mobilizing citizens, winning support | Using delegates as shadow-party vehicles, capturing agenda pathways, delegitimizing adverse results, coordinated influence operations |
| Oligarchic networks and concentrated private capital | Protecting economic position, influencing policy, preserving favorable regulation | Financing delegates or agenda campaigns, shaping media narratives, exploiting implementation choke points, capturing intermediaries |
| Employers and workplace hierarchies | Organizational stability, public policy advocacy, employee communication | Coercion, turnout monitoring, delegation pressure, retaliation threats, bloc mobilization |
| Trade unions and organized membership bodies | Representing members, mobilizing collective action, policy advocacy | Bloc delegation, pressure to conform, exchange of support for institutional favors, cartelization around public delegates |
| Religious organizations and moral authority networks | Moral advocacy, community guidance, public voice | Directive bloc voting, community pressure, hierarchy-based compliance expectations, local social retaliation |
| Foreign states and proxy actors | Strategic advantage outside the polity | Information warfare, delegitimization, covert funding, cyber disruption, polarization amplification |
| Platform companies and infrastructure intermediaries | Traffic, engagement, infrastructure stability, compliance, reputation | Opaque ranking, asymmetrical amplification, inconsistent moderation, dependency leverage, procedural influence via design defaults |
| Media groups | Reporting, commentary, investigation, audience reach | Narrative distortion, selective salience, synchronized legitimacy attacks, suppression of implementation failures |
| Organized crime and coercive patronage networks | No legitimate constitutional role | Intimidation, vote buying, local enforcement, financing dark influence channels |
| Activist swarms, influence entrepreneurs, and informal political networks | Issue mobilization, rapid organization, public pressure | Flooding, harassment, synthetic consensus, manipulative simplification, capture of low-friction agenda channels |
| Bot operators and disinformation contractors | No independent democratic legitimacy in protected civic acts | Synthetic participation, pressure simulation, brigading, spam challenges, intimidation, confusion |

#### 5.4 Incentive vectors

Across actors, constitutional distortion usually travels through a limited number of recurring vectors:

- agenda power
- access power
- information power
- dependency power
- delegation power
- review power
- certification power
- implementation power
- trust-chain power

#### 5.5 Collusion matrix

The following collusions are of special constitutional concern:

| Collusion pattern | Main risk | Constitutional impact |
|---|---|---|
| Executive + identity authority | Selective recovery, access manipulation, silent exclusion pressure | Political equality, access parity, protected-action integrity |
| Executive + constitutional review gate | Selective admissibility, timed injunctions, post-vote nullification | Agenda integrity, rights legitimacy, challengeability |
| Executive + election administration | Timing manipulation, incident framing abuse, asymmetrical operational handling, certification pressure | Fairness, legitimacy, safe degradation |
| Party machine + delegate cartel | Shadow-party reconstruction through proxy networks, manufactured grassroots legitimacy | Equal standing, revocability, anti-oligarchic purpose of delegation |
| Employer networks + local officials | Local coercion, turnout surveillance, supervised-site pressure, bloc delegation | Ballot freedom, access parity, secrecy |
| Oligarchic media + platform intermediaries + disinformation contractors | Narrative flooding, synthetic salience, trust destruction, asymmetric visibility | Intelligibility, neutrality of civic infrastructure, legitimacy |
| Technical maintainers + release-signing authority | Software trust-chain compromise hidden behind official authenticity signals | Challengeability, trust, secrecy, certification integrity |
| Identity authority + ballot-facing authority beyond tolerated threshold | Loss of secrecy through person-to-ballot linkage | Secret ballot where required, freedom from retaliation |
| Budget authority + implementing authority | Valid outcomes starved, delayed, or symbolically implemented only | Implementation fidelity, legitimacy of direct participation |
| Local strongman networks + supervised-site operators | Formal access exists, but real participation occurs under visible social control | Coercion resistance, secrecy, access parity |
| Foreign proxies + domestic partisan or media actors | Amplification of domestic polarization through apparently local channels | Legitimacy, intelligibility, continuity of governance |

## Part II — Power and risk

### 6. Asset and harm model

This section defines what the system is trying to protect and what kinds of damage it must recognize as constitutionally relevant.

#### 6.1 Interpretation principles

- constitutional assets are not limited to ballots
- harm may exist without visible software compromise
- some assets are ends in themselves, while others are enabling assets
- harm may be local, class-specific, systemic, or regime-level
- correctness is necessary but not sufficient

#### 6.2 Constitutional assets

The primary constitutional assets protected by the system are:

- political equality
- ballot freedom and secrecy where required
- freedom from retaliation and dependency-based pressure
- protected-action integrity
- agenda integrity
- contest clarity and intelligibility
- delegation accountability
- legitimacy of outcomes
- implementation fidelity
- continuity of governance under constitutional conditions
- public trust

#### 6.3 Supporting system assets

The main supporting assets are:

- public evidence integrity
- software trust-chain integrity
- availability fairness
- accessibility parity
- information integrity

#### 6.4 Harm categories

The system must recognize at least the following harm categories:

- forced or manipulated outcomes
- selective disenfranchisement
- fake participation
- shadow-party formation through delegates
- rights-violating majoritarian outcomes
- de facto loss of secrecy in small or socially dense electorates
- coercive participation conditions
- paralysis, overload, or constant destabilization
- post-vote nullification or implementation sabotage
- durable trust collapse
- silent re-concentration of power

#### 6.5 Harm severity dimensions

Every recognized harm instance should be assessed across the following dimensions:

- constitutional depth
- scope
- detectability
- reversibility
- cascading potential

### 7. System lifecycle and attack surface

Constitutional failure can occur long before a ballot is cast and long after a result is computed. The attack surface includes drafting, admissibility, information preparation, delegation formation, participation timing, incident handling, implementation, archival, and institutional memory.

#### 7.1 Lifecycle overview

The system lifecycle comprises the following major stages:

- charter and rulemaking
- identity and enrollment
- agenda setting and issue initiation
- admissibility and constitutional review
- dossier creation and deliberation
- delegation formation and proxy-state evolution
- voting window and protected participation
- tally, certification, and challenge
- implementation and execution review
- retention, archival, and historical memory

#### 7.2 Stage-specific attack surface

##### 7.2.1 Charter and rulemaking

Main risks include charter capture, vague emergency powers, weak challenge rights, permissive delegation concentration rules, under-specified rights protections, and amendment pathways that allow incumbents to domesticate the system.

##### 7.2.2 Identity and enrollment

Main risks include selective exclusion, biased recovery, soft disenfranchisement through access burden, overcollection of identity-linked data, and unequal service access.

##### 7.2.3 Agenda setting and issue initiation

Main risks include monopoly over issue entry, threshold gaming through money or organization, docket flooding, strategic timing, and fake grassroots initiation through organized intermediaries.

##### 7.2.4 Admissibility and constitutional review

Main risks include selective inadmissibility, political timing of rulings, procedural delay, ideologically biased wording changes, and judicial choke-point capture.

##### 7.2.5 Dossier creation and deliberation

Main risks include misleading summaries, hidden editorial bias, silent revision, provenance loss, manipulation through content ordering, synthetic consensus, and covert persuasive AI use.

##### 7.2.6 Delegation formation and proxy-state evolution

Main risks include delegate concentration, hidden coordination, stale delegations, cap enforcement failure, and proxy networks that harden into shadow parties.

##### 7.2.7 Voting window and protected participation

Main risks include endpoint compromise, coercion, vote buying, timing attacks, last-window outages, malformed or replayed submissions, and confusion around override or revote state.

##### 7.2.8 Tally, certification, and challenge

Main risks include opaque tally behavior, certification pressure, incomplete evidence publication, verifier mismatch, bad-faith challenge flooding, and public confusion about which result is authoritative.

##### 7.2.9 Implementation and execution review

Main risks include budget starvation, delay, hostile reinterpretation, procedural burial, and partial implementation masked as compliance.

##### 7.2.10 Retention, archival, and historical memory

Main risks include excessive retention, premature destruction, silent archive gaps, verifier irreproducibility over time, and archival opacity used to prevent later scrutiny.

#### 7.3 Cross-stage attack patterns

The most serious distortions often span multiple stages:

- front-loaded distortion through agenda manipulation, biased admissibility, misleading dossiers, or delegation concentration before the ballot phase
- midstream procedural mutation through late dossier edits, visibility changes, emergency rule drift, or altered delegation policy
- back-end domestication through challenge abuse, certification blockage, implementation sabotage, or archival opacity
- compound capture where two or more stages are captured in sequence

### 8. Threat families

This section identifies the principal constitutional threats to the system. It includes not only technical compromise, but also lawful abuse, procedural manipulation, institutional capture, social coercion, delegated oligarchy, information warfare, and post-vote sabotage.

#### 8.1 Threat family A — Charter capture

- **Description**: The founding charter, statute, or constitutional amendment is drafted to preserve durable control by incumbents, dominant parties, administrative elites, or concentrated private power.
- **Typical attacker set**: incumbent executive, dominant parliamentary coalition, constitution-writing faction, captured judicial actors, oligarchic networks.
- **Assets at risk**: equal civic standing, rights floor, agenda integrity, challengeability, safe degradation, implementation fidelity.
- **Early warning indicators**: vague emergency clauses, non-transparent drafting, weak review language, overreliance on future regulation, no meaningful remedies.
- **Required controls**: hard rights floor, explicit separation of institutional powers, public drafting process, mandatory constitutional review before activation, periodic re-legitimation of core rules.
- **Residual risk**: high.

#### 8.2 Threat family B — Agenda capture and docket flooding

- **Description**: Actors distort democracy by controlling what enters the system, what never enters it, when issues are presented, and how many issues are forced onto citizens at once.
- **Typical attacker set**: government, parliamentary majority, petition machines, oligarchic donors, activist swarms, foreign influence actors, administrative gatekeepers.
- **Assets at risk**: agenda integrity, contest intelligibility, equal civic standing, legitimacy of participation, implementation fidelity.
- **Early warning indicators**: issue-source concentration, extreme clustering of high-stakes issues, omnibus questions, repeated last-minute docket changes, civic fatigue spikes.
- **Required controls**: mixed agenda pathways, single-subject rule, public scheduling calendar, vote pacing limits, docket diversity reporting, challenge rights for intake and timing decisions.
- **Residual risk**: medium to high.

#### 8.3 Threat family C — Contest wording and option design manipulation

- **Description**: Citizens are steered through biased language, misleading summaries, asymmetrical framing, or structurally distorted option design.
- **Typical attacker set**: drafting authority, partisan legal teams, captured admissibility bodies, strategic expert panels, lobbying networks.
- **Assets at risk**: contest intelligibility, single-subject integrity, rights floor, symmetry of burden and benefit, public trust.
- **Early warning indicators**: high discrepancy between legal text and summary, late edits, repeated clarity objections, comprehension failures.
- **Required controls**: mandatory plain-language dossier, adversarial pro and con briefs, legal redline publication, comprehension testing, constitutional and fiscal notes, public version history.
- **Residual risk**: medium.

#### 8.4 Threat family D — Review-gate and judicial choke-point capture

- **Description**: The formal legal gatekeeping layer becomes the real sovereign by selectively blocking, delaying, narrowing, or neutralizing issues and outcomes.
- **Typical attacker set**: captured constitutional court, politicized admissibility authority, executive-aligned prosecutors, partisan electoral commissions, legal elites using proceduralism strategically.
- **Assets at risk**: agenda integrity, challengeability, implementation fidelity, equal civic standing, legitimacy of review.
- **Early warning indicators**: partisan asymmetry in admissibility rates, persistent review delays for certain sponsor types, repeated unexplained emergency interventions.
- **Required controls**: narrow review grounds, mandatory written reasons, strict review deadlines, publication of review metrics, appeal rights, public hearing requirements for major exclusions.
- **Residual risk**: high.

#### 8.5 Threat family E — Information and deliberation manipulation

- **Description**: Citizens are overwhelmed, misled, emotionally flooded, or strategically segmented through media operations, platform logic, AI-generated persuasion, synthetic consensus, or asymmetric visibility.
- **Typical attacker set**: political parties, oligarchic media, foreign information operators, platform-aligned networks, influence contractors, activist swarms, synthetic content farms.
- **Assets at risk**: contest intelligibility, neutrality of civic infrastructure, provenance of official information, legitimacy of outcomes, equal civic standing.
- **Early warning indicators**: synthetic submission spikes, unusual coordination patterns, late disinformation surges, repeated attacks on trust in the official dossier.
- **Required controls**: no engagement-ranked feed, signed source corpus, mandatory provenance for official summaries, adversarial briefing structure, AI usage restrictions, rate limits and identity binding for formal submissions.
- **Residual risk**: high.

#### 8.6 Threat family F — Delegation capture and cartelization

- **Description**: Delegation networks become concentrated, opaque, brokered, or effectively permanent, recreating shadow parties, patronage pyramids, or influencer oligarchies.
- **Typical attacker set**: charismatic delegates, parties operating through proxies, unions or employer blocs, ideological organizations, wealthy civic entrepreneurs, platform personalities.
- **Assets at risk**: equal civic standing, revocability of delegation, public delegates/private delegators principle, agenda integrity, anti-oligarchic purpose.
- **Early warning indicators**: steep concentration curves, low revocation rates, large transitive chains, identical voting patterns across nominally independent delegates, opaque funding.
- **Required controls**: hard concentration caps, public delegate registration, funding and conflict disclosures, delegation expiry, transitivity depth limits, direct-vote override, graph analytics.
- **Residual risk**: high.

#### 8.7 Threat family G — Selective disenfranchisement and participation asymmetry

- **Description**: Citizens are not formally excluded, but practical access is distributed unevenly by identity processes, language, disability, technology, geography, diaspora status, or social pressure.
- **Typical attacker set**: negligent or biased administrators, executive actors under-serving certain groups, identity and recovery gatekeepers, local officials, infrastructural monopolies.
- **Assets at risk**: equal civic standing, accessibility parity, legitimacy of outcomes, one effective civic path per citizen.
- **Early warning indicators**: demographic participation anomalies, recovery-denial disparities, regional supervised-site scarcity, accessibility complaints, diaspora turnout collapse.
- **Required controls**: accessibility parity as a constitutional requirement, supervised fallback channels, in-person recovery for high-stakes contests, multilingual and disability-first design, demographic participation audits.
- **Residual risk**: medium.

#### 8.8 Threat family H — Coercion, retaliation, and vote buying

- **Description**: Citizens are pressured, induced, monitored, or socially constrained by employers, family members, party brokers, neighborhood actors, or benefit-controlling authorities.
- **Typical attacker set**: employers, public-sector managers, local party networks, family heads, landlords, clientelist intermediaries, welfare gatekeepers, organized vote brokers.
- **Assets at risk**: secret ballot, no durable proof of vote choice, revocability of delegation, freedom from retaliation, equal civic standing.
- **Early warning indicators**: complaints clustered by employer or municipality, abnormal synchronized voting windows, unusual delegation surges linked to workplaces, rumors of required screenshots or proofs.
- **Required controls**: revoting, in-person override, no durable receipts, short-lived verification, neutral supervised access points, coercion complaint pathway, statutory penalties external to the platform.
- **Residual risk**: high.

#### 8.9 Threat family I — Secrecy erosion and practical deanonymization

- **Description**: Ballot secrecy is formally preserved but practically collapses through small electorates, timing correlation, social inference, delegation traces, or result granularity.
- **Typical attacker set**: local power brokers, employers, neighbors, delegates, administrative insiders, coordinated observers, family members.
- **Assets at risk**: secret ballot where required, freedom from retaliation, legitimacy of local/community decisions.
- **Early warning indicators**: low turnout in highly visible communities, complaints that everyone already knows how people voted, repeated demands for detailed result slices.
- **Required controls**: minimum anonymity-set rules, pooled or delayed reporting, secrecy-class review by contest size, bans on overly granular publication, mandatory social-risk review for small-electorate contests.
- **Residual risk**: high for small communities, moderate elsewhere.

#### 8.10 Threat family J — Tally, certification, and challenge sabotage

- **Description**: Actors manipulate outcome legitimacy by attacking tally, certification, publication, or the challenge process, not necessarily by changing votes directly.
- **Typical attacker set**: insiders, captured certifiers, partisan challengers, administrative bottlenecks, executives seeking delay, hostile observers acting strategically.
- **Assets at risk**: challengeability, implementation fidelity, public trust, one effective path per citizen, legitimacy of certification.
- **Early warning indicators**: repeated procedural disputes at certification stage, frivolous challenge floods, mismatch between official and observer result channels, selective publication delays.
- **Required controls**: public certification timeline, challenge triage rules, signed result packages, public bulletin board, independent verifier ecosystem, sanctions for bad-faith procedural obstruction.
- **Residual risk**: medium to high.

#### 8.11 Threat family K — Emergency powers abuse

- **Description**: A real or alleged crisis is used to suspend protections, alter channels, delay contests, or expand administrative discretion beyond constitutional limits.
- **Typical attacker set**: executive, security apparatus, emergency commissions, captured administration, courts deferring too broadly.
- **Assets at risk**: safe degradation, equal civic standing, secret ballot, agenda integrity, public trust.
- **Early warning indicators**: vague incident notices, repeated use of emergency channels, rule changes without public review, long emergency durations, asymmetric impact on certain contests or regions.
- **Required controls**: narrow emergency triggers, multi-body authorization, public declaration requirement, hard expiry, automatic post-incident review, no silent procedural change.
- **Residual risk**: high.

#### 8.12 Threat family L — Post-vote sabotage and non-implementation

- **Description**: Citizens successfully decide, but the result is diluted, delayed, administratively buried, underfunded, or procedurally ignored.
- **Typical attacker set**: executive, ministries, implementing agencies, budget authorities, hostile local administrations, captured courts, parliamentary committees.
- **Assets at risk**: implementation fidelity, challengeability, public trust, legitimacy of direct participation.
- **Early warning indicators**: repeated delay beyond statutory implementation clock, divergence between adopted text and implementing acts, budget non-alignment, administrative silence.
- **Required controls**: public implementation tracker, named implementing authority, statutory deadlines, mandatory explanation of deviation, sanctions or automatic review triggers, judicial fast path for non-execution.
- **Residual risk**: high.

#### 8.13 Threat family M — Legitimacy warfare

- **Description**: Actors seek not necessarily to change outcomes, but to destroy confidence in the system, selectively recognize favorable results, and reject unfavorable ones.
- **Typical attacker set**: incumbent losers, foreign influence actors, partisan media, oligarchic networks, ideological maximalists, hostile delegates, conspiratorial ecosystems.
- **Assets at risk**: public trust, implementation fidelity, continuity of governance, challengeability, safe degradation.
- **Early warning indicators**: rapid coordinated fraud narratives after major outcomes, selective acceptance by major actors, repeated attacks on oversight bodies, high divergence between verifier evidence and public belief.
- **Required controls**: public evidence packages, independent verifier ecosystem, permanent observer access, disciplined incident communication, strong challenge channels, public education and mock exercises.
- **Residual risk**: high and permanent.

#### 8.14 Threat family N — Software supply chain and distribution compromise

- **Description**: The software, firmware, verifier tools, or distribution pathways used by the system are compromised before they reach voters, supervised operators, auditors, or observers.
- **Typical attacker set**: hostile insiders, compromised maintainers, state intelligence or proxy actors, supply-chain attackers, malicious dependency publishers, hostile infrastructure providers.
- **Assets at risk**: secret ballot, one effective civic path per contest, challengeability, public trust, implementation fidelity, safe degradation, certification legitimacy.
- **Early warning indicators**: mismatch between source and released binaries, unexplained dependency drift, unsigned or inconsistently signed artifacts, verifier discrepancies, anomalous update paths, attestation failures.
- **Required controls**: reproducible builds, multi-party release signing, software bills of materials and dependency pinning, independent build and mirror network, public hashes and manifests, hardware and firmware attestation for supervised devices.
- **Residual risk**: high.

#### 8.15 Threat family O — Availability sabotage and timing attacks

- **Description**: Actors attempt to make the system unavailable, selectively degraded, or unevenly reachable during critical windows.
- **Typical attacker set**: foreign cyber operators, domestic incumbents acting through infrastructure leverage, compromised providers, botnets, malicious insiders, local officials under-serving supervised channels.
- **Assets at risk**: equal civic standing, accessibility parity, one effective civic path, safe degradation, public trust, legitimacy of outcomes.
- **Early warning indicators**: regional spikes in errors or latency, queue divergence, late-window failures, identity or recovery outages, anomalous supervised-site demand.
- **Required controls**: elastic multi-region infrastructure, queues and graceful degradation, legally predefined window extension rules, supervised fallback, signed incident notices, public service-status transparency.
- **Residual risk**: medium to high.

#### 8.16 Cross-cutting threat interactions

The threats above must not be assessed in isolation. The most dangerous failures are compound failures, especially:

- agenda capture plus information manipulation
- delegation cartelization plus secrecy erosion
- review-gate capture plus non-implementation
- emergency abuse plus legitimacy warfare
- selective disenfranchisement plus coercion

#### 8.17 Threat severity model

Each threat instance shall be rated on five dimensions:

- severity of constitutional harm
- scope of impact
- detectability
- reversibility
- capture leverage

### 9. Constitutional controls library

This section defines the control families used to mitigate the constitutional threats identified in Section 8. A constitutional control may be legal, institutional, procedural, informational, social, or technical.

#### 9.1 Interpretation rule for controls

Every control listed below shall eventually be mapped, in an operational matrix, to:

- the threats it mitigates
- the contest classes in which it is mandatory
- the authority responsible for maintaining it
- the evidence or audit artifact it must produce
- the fail-safe action triggered when it fails

#### 9.2 Institutional anti-capture controls

Key controls include:

- institutional split across identity, eligibility, privacy credentialing, ballot intake, tally, certification, and oversight
- threshold key custody for high-value secrets and critical operations
- multi-body certification for results, incident escalation, and major emergency actions
- sortition oversight and challenge rights
- external audits and observers

#### 9.3 Agenda and review controls

Key controls include:

- mixed agenda pathways
- single-subject rule
- public scheduling calendar
- vote pacing limits
- narrow review grounds
- review deadlines and public reasons
- review metrics and asymmetry reporting

#### 9.4 Contest intelligibility and information integrity controls

Key controls include:

- fixed dossier structure
- adversarial briefs and minority notes
- signed canonical source corpus
- public version history
- no paid ranking or engagement boosts
- no opaque persuasive ranking
- constrained AI use
- comprehension testing

#### 9.5 Delegation integrity controls

Key controls include:

- public delegate registration
- concentration caps
- transitive depth caps
- delegation expiry and periodic re-authorization
- easy revocation and direct override
- public rationale histories
- delegation graph analytics

#### 9.6 Ballot-freedom and anti-coercion controls

Key controls include:

- revoting
- supervised override
- no durable proof of vote choice
- short-lived verification
- long voting windows
- neutral supervised access points
- coercion complaint pathway

#### 9.7 Secrecy and privacy controls

Key controls include:

- secrecy classification by contest type
- public delegates and private delegators
- minimum anonymity-set rules
- pooled or delayed reporting
- minimal local persistence

#### 9.8 Access, participation parity, and protected-action integrity controls

Key controls include:

- state eID for protected acts
- in-person recovery for high-stakes use
- separation of public discourse from protected civic acts
- signed submissions and rate limits
- accessibility-first design
- diaspora service standards
- participation disparity audits

#### 9.9 Client integrity and software trust-chain controls

Key controls include:

- hardened distribution and signed software
- dedicated audited client
- reproducible builds
- multi-party release signing
- SBOMs and dependency pinning
- independent build and mirror network
- hardware and firmware attestation for supervised devices

#### 9.10 Verification, evidence, certification, and challenge controls

Key controls include:

- public bulletin board and evidence packages
- independent verifier ecosystem
- structured challenge workflow
- public certification timeline
- challenge triage rules
- mandatory public reasons for delay or exception

#### 9.11 Availability and continuity controls

Key controls include:

- elastic multi-region infrastructure
- queues and graceful degradation
- voting-window extension rules
- supervised fallback
- signed incident notices and recovery instructions
- public service-status transparency

#### 9.12 Implementation fidelity controls

Key controls include:

- public implementation tracker
- named responsible authority
- statutory implementation deadlines
- deviation and non-execution reporting
- automatic review triggers

#### 9.13 Emergency and safe-degradation controls

Key controls include:

- narrow emergency triggers
- multi-body authorization
- hard expiry and renewal rules
- public declaration and review
- no silent derogation from core invariants
- safe degradation pathways

#### 9.14 Control layering rule

No high-severity threat may rely on a single control family. At minimum, every high-stakes contest class must combine:

- one institutional control
- one public-evidence control
- one operational continuity control
- one remedy or challenge control
- one coercion or secrecy control where relevant

### 10. Red lines and fail-safe modes

This section defines the conditions under which a contest, contest class, channel, delegation regime, or operational state must be paused, downgraded, rerun, refused, or otherwise prevented from producing a constitutionally authoritative outcome.

#### 10.1 General principles

- constitutional validity prevails over operational continuity
- safe degradation prevails over opaque improvisation
- a fail-safe response must protect all affected citizens symmetrically
- predefined remedies only
- the chosen remedy must be the least-distortive adequate remedy
- every invocation of a red line or fail-safe mode requires public reason-giving

#### 10.2 Red-line categories

The following categories define constitutionally relevant red lines:

- rights red line
- political equality red line
- secrecy red line
- coercion red line
- agenda integrity red line
- contest intelligibility red line
- protected-action integrity red line
- availability and timing red line
- software trust-chain red line
- delegation concentration red line
- review-gate integrity red line
- certification integrity red line
- implementation fidelity red line
- legitimacy red line

#### 10.3 Fail-safe action menu

The following fail-safe actions are constitutionally authorized:

- pause
- window extension
- channel downgrade
- contest severance
- result pooling or delayed reporting
- delegation freeze or reset
- hold certification
- nullification and rerun
- contest-class suspension
- refusal to run
- automatic implementation review

#### 10.4 Red-line trigger thresholds

A fail-safe action must be invoked immediately where:

- the rights red line is crossed
- the secrecy red line is crossed in a way that cannot be reversed
- the software trust-chain red line is credibly crossed
- protected-action integrity is materially compromised
- emergency powers are used outside lawful trigger conditions
- a contest or channel can no longer credibly produce a constitutionally valid result

Material-risk, prospective-remedy, and structural triggers are also defined and must be governed through the escalation model.

#### 10.5 Non-negotiable refusal conditions

The system shall refuse to open or continue a contest where any of the following holds and cannot be remedied in time:

- the applicable secrecy class cannot be credibly maintained
- the official dossier is materially misleading or unintelligible
- legality or admissibility remains unresolved past the latest lawful decision point
- the identity and protected-action layer is not functioning at required assurance
- the official software line or supervised terminal image cannot be authenticated
- neutral supervised access is not realistically available where constitutionally required
- emergency powers are used without valid trigger, publication, and review
- required public evidence packages cannot be produced for certification
- the result cannot be challenged through a meaningful review path
- implementation authority is undefined for a self-executing or binding outcome

#### 10.6 Decision rights and authority chain

No single operational authority may unilaterally convert a red-line event into a final constitutional disposition. Major fail-safe decisions require multi-body confirmation, public reasoning, and oversight notification.

#### 10.7 Public notice and evidence obligations

Every red-line invocation must produce a public notice containing:

- contest identifier
- red-line category
- time of detection
- authorities involved
- factual summary
- immediate legal consequence
- citizen-facing instructions
- rights to challenge
- expected review timeline
- publication status of relevant evidence

#### 10.8 Contest recovery and restart rules

Recovery must be defined separately for three phases:

- before close
- after close but before certification
- after certification

Prospective remedies are preferred where they preserve equality and trust. Certification does not immunize a contest from later constitutional invalidity.

### 11. Metrics, early warning indicators, and escalation triggers

This section defines how constitutional deterioration is made observable before it becomes irreversible. It links indicators to escalation levels and potential fail-safe actions.

#### 11.1 Indicator classes

The minimum monitoring architecture includes:

- equality and access indicators
- agenda and review indicators
- intelligibility and information indicators
- delegation concentration indicators
- secrecy and coercion indicators
- protected-action integrity indicators
- availability and continuity indicators
- certification and challenge indicators
- implementation fidelity indicators
- legitimacy and trust indicators

Each indicator family must be linked to one or more contest classes, one or more constitutional assets, one or more threat families, and one or more escalation paths.

#### 11.2 Leading and lagging indicators

Indicators shall be classified as:

- leading indicators that show deterioration while corrective action is still realistic
- lagging indicators that confirm damage after it has already occurred
- mixed indicators whose meaning depends on contest class, lifecycle stage, detectability, and reversibility

#### 11.3 Escalation trigger model

The system shall use the following escalation levels:

- Level 0 — observation only
- Level 1 — enhanced review
- Level 2 — public notice
- Level 3 — pre-red-line escalation
- Level 4 — fail-safe consideration
- Level 5 — mandatory red-line determination

#### 11.4 Threshold-to-red-line linkage

Each indicator family must be explicitly linked to one or more possible red-line categories and one or more escalation levels.

#### 11.5 Publication and transparency rules

Indicators must be published in a manner consistent with transparency and the protection of secrecy, privacy, and anti-coercion conditions. Publication classes are:

- public
- delayed-public
- restricted to oversight
- restricted but challengeable
- sealed for lawful reason

#### 11.6 Indicator integrity and anti-gaming rule

No authority may selectively publish only favorable slices, redefine indicator meaning midstream without declared review, suppress material anomaly reporting because an incident is politically inconvenient, or treat metric improvement as sufficient if the underlying constitutional harm remains unresolved.

### 12. Governance, risk ownership, accountability, and review cadence

This section defines who owns constitutional risk, who has decision rights when risk materializes, who must answer for failures of control, and how the system is periodically reviewed for constitutional health.

#### 12.1 Interpretation principles

- functional operation and constitutional accountability are not the same thing
- risk ownership must be explicit
- governance must be layered
- review without remedy is not governance
- accountability must survive conflict

#### 12.2 Governance layers

The system shall be governed through distinct but connected layers:

- constitutional governance
- operational governance
- oversight governance
- incident governance
- implementation governance

#### 12.3 Core governance roles

The following roles must exist in law, charter, or binding operational structure:

- constitutional rule authority
- contest administration authority
- identity and eligibility authorities
- privacy, ballot, tally, and certification authorities
- incident response authority
- constitutional review authority
- oversight and audit authorities
- implementation authority
- sortition oversight body

#### 12.4 Risk ownership matrix

The following risk domains require explicit ownership:

- access parity
- secrecy where required
- delegation concentration and proxy integrity
- software trust-chain integrity
- incident handling and safe degradation
- certification integrity
- implementation fidelity

Each domain requires a primary owner, an oversight owner, and an escalation owner.

#### 12.5 Escalation authority

The document distinguishes among:

- first-instance incident declaration
- recommendation of fail-safe action
- invocation of red-line review
- hold of certification
- suspension of a contest or contest class
- order of post-vote implementation review

No actor may block the logging of a red-line review request.

#### 12.6 Review cadence

The system must be reviewed at multiple cadences:

- per-contest review
- periodic operational review
- annual constitutional review
- post-incident review
- post-cycle or post-election review
- mandatory redesign review after repeated structural failure

#### 12.7 Public accountability outputs

Governance must generate visible public outputs. At minimum, the following outputs must exist:

- public incident reports
- annual constitutional health report
- delegation concentration reports
- implementation fidelity reports
- review-gate asymmetry reports
- trust-chain integrity reports

#### 12.8 Sortition oversight role

The sortition oversight body must have:

- access rights
- publication rights
- escalation rights
- hearing rights
- review participation rights

#### 12.9 Governance traceability rule

Every major constitutional decision must be traceable. The record must show:

- who decided
- under what authority
- using what evidence
- at what time
- with what review path
- with what published rationale

#### 12.10 Governance failure rule

A governance structure shall be deemed constitutionally inadequate if:

- major risk domains lack explicit owners
- escalation authority is ambiguous
- review occurs without remedy powers
- public accountability outputs are missing or performative
- the same structural failures recur without redesign review

### 13. Interface to the protocol appendix

This section defines the mandatory interface between the constitutional document and the protocol appendix.

#### 13.1 Normative relationship

The constitutional document defines what must be true for legitimate operation. The protocol appendix defines how the system claims to make it true. If a constitutional claim lacks a corresponding protocol mechanism, evidence model, and failure behavior in the appendix, that claim shall be treated as unimplemented for deployment purposes.

#### 13.2 Claims the protocol appendix must operationalize

The appendix must provide explicit, reviewable mechanisms for the following claims:

- equal civic standing in protected acts
- one effective civic path per contest
- direct-vote override
- revocation and revoting
- secret ballot where required
- public delegates and private delegators
- public verifiability and result reproducibility
- threshold control and trustee behavior
- cryptographic agility and quantum-safe baseline
- retention, destruction, and post-challenge minimization
- fault and incident behavior

#### 13.3 Mandatory trust-boundary model

The appendix must define all protocol actors and trust boundaries in a way consistent with the constitutional anti-capture model. At minimum, it must identify:

- which actors know legal identity
- which actors know eligibility state
- which actors can issue or validate participation rights
- which actors see anonymous contest handles
- which actors can receive or publish ballots
- which actors can influence delegated expansion
- which actors can certify results
- which actors can verify evidence without privileged access

#### 13.4 Mandatory object and state model

The appendix must define the full state model for constitutionally relevant objects. At minimum, the following objects must have formal schemas, lifecycle rules, and transition rules:

- contest identifier
- entitlement token or equivalent
- unlinkable participation credential or equivalent
- anonymous contest handle
- delegation edge
- direct ballot envelope
- delegate instruction
- supersession or recovery record
- delegation snapshot
- bulletin-board checkpoint
- result bundle
- proof bundle
- destruction event
- incident event

#### 13.5 Evidence obligations

The appendix must define evidence required to support constitutional decisions, including evidence for:

- secrecy
- direct-vote override
- one-time participation
- delegation concentration enforcement
- tally correctness
- software trust-chain integrity
- outage and incident fairness
- destruction and minimization

#### 13.6 Mandatory interface to red lines and fail-safe modes

For every red-line category in Section 10 that depends on technical evidence, the appendix must specify:

- the relevant state variable or evidence object
- who can observe it
- how it is authenticated
- how quickly it becomes available
- whether it is public, restricted, or delayed
- what ambiguity remains
- what fail-safe transitions are technically supported

#### 13.7 Contest-class protocol binding

The appendix must bind the following per contest class:

- secrecy class
- remote versus supervised eligibility
- whether revoting is allowed
- whether supervised override is allowed
- whether transitive delegation is allowed
- delegation freeze timing
- result-publication granularity
- verification affordances
- required cryptographic profile
- fail-safe downgrade path

#### 13.8 Mandatory protocol acceptance tests

The appendix must define acceptance tests sufficient to validate the constitutional claims above. These tests must include, at minimum:

- duplicate entitlement attempt
- stale or replayed ballot submission
- direct vote after prior delegation
- multiple direct ballots with ordered supersession
- delegation cycle handling
- delegation-cap violation attempt
- supervised recovery and supersession
- independent tally reproduction from public artifacts
- suite rotation across contests
- trustee quorum loss
- verifier disagreement handling
- trust-chain compromise response

#### 13.9 No hidden-assumption rule

The appendix shall include a dedicated section listing all residual assumptions that remain true only if certain institutional, operational, or social conditions hold. No constitutional review body shall be asked to infer hidden assumptions from protocol prose.

#### 13.10 Change-management rule

The appendix must define how protocol changes are introduced without silently changing constitutional meaning. It must specify versioning discipline, contest pinning to protocol versions, what may change between contests, what may never change mid-window, what requires public review, what requires re-certification, and what requires legislative or constitutional reauthorization.

## Part III — Governance and operationalization

### 14. Scenario exercises, tabletop drills, and constitutional stress tests

Scenario exercises, tabletop drills, and constitutional stress tests are not training theater. They are the disciplined practice through which the system learns whether its constitutional promises still hold when pressure stops being hypothetical.

#### 14.1 Purpose

This section defines the scenario-based validation regime through which the system is tested under constitutional stress. It ensures that the framework described in this document is not treated as sufficient merely because it is well written.

#### 14.2 Interpretation principles

- stress testing is part of constitutional governance
- scenarios test relationships, not just components
- a successful scenario is not one without friction
- scenario failure is valuable only if it drives redesign
- contest class matters

#### 14.3 Scenario template

Every scenario, tabletop drill, or constitutional stress test must be documented using a common template. At minimum, each scenario must specify:

- scenario identifier and title
- scenario class
- lifecycle stage or stages affected
- threat family or families involved
- contest-class applicability
- assets at risk
- potential harms
- indicators and escalation triggers
- red lines potentially crossed
- expected protocol evidence
- decision authorities
- fail-safe options
- communication obligations
- success criteria
- post-incident review questions

#### 14.4 Scenario classes

The minimum scenario regime must cover:

- capture scenarios
- coercion scenarios
- secrecy-failure scenarios
- delegation-cartel scenarios
- trust-chain compromise scenarios
- availability and timing scenarios
- implementation sabotage scenarios
- legitimacy-war scenarios

#### 14.5 Contest-class sensitivity rule

Every scenario must be evaluated through contest-class sensitivity, not in the abstract.

#### 14.6 Scenario execution requirements

Every scenario exercise must identify:

- the initiating event
- the data and evidence stream available at each step
- the authorities expected to act
- the deadlines within which they must act
- the communication sequence
- the branch points where different fail-safe responses become available

#### 14.7 Scenario outputs

Every completed exercise must produce:

- a scenario record
- an evidence sufficiency finding
- an authority-path finding
- a fail-safe adequacy finding
- a control adequacy finding
- a redesign recommendation

#### 14.8 Minimum scenario set

The system shall not be considered constitutionally mature unless it has been stress-tested, at minimum, through one or more scenarios in each scenario class named above.

#### 14.9 Scenario frequency and review linkage

Scenario exercises must occur:

- before activation of a new contest class
- before material change to delegation posture
- before expansion of subject-matter scope
- after any major trust-chain or incident event
- after any repeated structural failure
- periodically as part of annual constitutional review

#### 14.10 No ceremonial exercise rule

A scenario exercise is constitutionally insufficient if it is designed or conducted in a way that avoids realistic friction.

### 15. Operational threat register

The system shall maintain an operational threat register through which constitutionally material threat instances, anomalies, structural weaknesses, and recurring failure patterns are recorded, tracked, reviewed, escalated, and closed.

#### 15.1 Purpose

The purpose of the register is to ensure that threats described abstractly in Section 8 are governed concretely over time, rather than handled as isolated incidents without institutional memory.

#### 15.2 Traceability requirement

Every constitutionally material threat instance must be traceable across the document set. At minimum, each register entry must map to:

- one or more lifecycle stages from Section 7
- one or more threat families from Section 8
- one or more constitutional assets or harms from Section 6
- one or more controls from Section 9
- one or more red-line categories or fail-safe actions from Section 10 where relevant
- one or more indicators or escalation levels from Section 11
- one or more accountable authorities from Section 12
- protocol evidence obligations defined in Section 13 where relevant

#### 15.3 Governance requirement

The operational threat register must be:

- continuously maintained
- reviewable by the designated oversight authority
- protected against informal deletion or silent closure
- used as an input to periodic operational review, annual constitutional review, post-incident review, and redesign review after repeated structural failure

No single authority may both exclusively control the register and exclusively determine what is constitutionally material enough to enter it.

## Annexes

### Annex A — Operational Threat Register Template

Without a traceable operational register, the document risks becoming conceptually strong but institutionally forgetful. The register exists so that recurring risk becomes visible, governance decisions become attributable, and structural weakness becomes harder to normalize through repetition.

#### A.1 Purpose

This annex defines the minimum schema for the operational threat register referenced in Section 15.

#### A.2 Register schema

| Field | Req. | Type / Format | Description | Example / Allowed values |
|---|---|---|---|---|
| threat_id | Yes | String / UUID | Unique persistent identifier | TR-2026-0042 |
| title | Yes | Short text | Concise descriptive title | Regional outage near close in Tier 2 contest |
| threat_family | Yes | Enum / multi-value | Section 8 mapping | Availability sabotage; Delegation cartelization |
| lifecycle_stage | Yes | Enum / multi-value | Section 7 mapping | Voting window; Implementation |
| contest_class | Yes | Enum | Section 2 mapping | Class B; Class D; Class E; Class F |
| contest_id | No | String | Specific contest affected, if any | CID-2026-BG-LOCAL-17 |
| jurisdiction | No | Text / code | Territory or institutional scope | Novi Beograd; National; Diaspora |
| assets_at_risk | Yes | Enum / multi-value | Section 6.3 mapping | Political equality; Secrecy; Implementation fidelity |
| harm_category | Yes | Enum / multi-value | Section 6.5 mapping | Selective disenfranchisement; Post-vote sabotage |
| description | Yes | Short narrative | What happened in operational terms | Free text |
| detection_source | Yes | Enum / multi-value | How issue was detected | Indicator; Complaint; Audit; Observer; Verifier mismatch; Court finding |
| date_detected | Yes | Timestamp | First formal detection | ISO 8601 |
| indicator_class | No | Enum / multi-value | Section 11 mapping | Equality and access; Certification and challenge |
| escalation_level | No | Enum | Section 11 level | L0; L1; L2; L3; L4; L5 |
| controls_active | Yes | Text / refs | Section 9 controls in force at time of issue | Revoting; Cap enforcement; Public bulletin board |
| control_adequacy | Yes | Enum + note | Whether controls worked | Worked; Partial; Failed; Missing |
| red_line_status | Yes | Enum | Section 10 relationship | None; Pre-red-line; Fail-safe considered; Mandatory determination; Confirmed |
| red_line_category | No | Enum / multi-value | Specific Section 10 category | Secrecy; Availability and timing; Implementation fidelity |
| fail_safe_action | No | Enum / multi-value | Section 10 response taken or considered | Pause; Extension; Certification hold; Rerun; Contest-class suspension |
| decision_owner | Yes | Role / authority | Primary accountable authority under Section 12 | Incident governance authority; Certification authority |
| oversight_owner | Yes | Role / body | Independent scrutiny owner | Sortition oversight body; Independent audit office |
| evidence_objects | Yes | Refs / list | Relevant Section 13 evidence artifacts | Proof bundle PB-17; DSC-44; Incident log IL-09 |
| publication_posture | Yes | Enum | Section 11.7 class | Public; Delayed-public; Restricted to oversight; Restricted but challengeable; Sealed |
| current_status | Yes | Enum | Operational state of the case | Detected; Triaged; Under review; Escalated; Mitigation in progress; Monitoring; Closed |
| residual_risk | Yes | Enum + note | Remaining constitutional risk after action | Low; Medium; High; Structural |
| next_review_date | Yes | Date | Mandatory next review point | 2026-05-30 |
| closure_rationale | No | Short narrative | Required on closure | Free text |
| linked_entries | No | List of IDs | Related threat records | TR-2026-0031; TR-2026-0037 |
| linked_incident_id | No | String | Incident-management reference | INC-2026-019 |
| linked_challenge_id | No | String / list | Challenge-case reference | CH-2026-088 |
| linked_public_report | No | String / URL ref | Published report reference | AR-2026-Q2-04 |
| redesign_required | Yes | Boolean | Whether structural redesign is required | true / false |
| redesign_status | No | Enum | Progress of redesign response | Not started; In progress; Adopted; Rejected with reasons |

#### A.3 Field rules

##### A.3.1 Multi-value fields

The following fields may contain multiple values where one incident spans several dimensions:

- threat_family
- lifecycle_stage
- assets_at_risk
- harm_category
- indicator_class
- red_line_category
- fail_safe_action
- evidence_objects
- linked_entries

##### A.3.2 Required narrative fields

The following fields may not be left as bare codes only:

- description
- control_adequacy
- residual_risk
- closure_rationale when closed

##### A.3.3 Closure rule

An entry may move to Closed only if all of the following are true:

- a decision owner is recorded
- the control_adequacy field is completed
- residual_risk is assessed
- next review is either not required or explicitly waived with reasons
- closure_rationale is recorded

##### A.3.4 Structural-pattern rule

If three or more entries within a review period map to the same threat family, lifecycle stage, control failure type, or red-line category, the maintaining authority must flag the pattern for structural review.

#### A.4 Minimal state machine

Every entry must move through this state model:

- Detected
- Triaged
- Under review
- Escalated (optional)
- Mitigation in progress / Monitoring
- Closed

Additional states allowed:

- Fail-safe considered
- Certification hold active
- Redesign required

No constitutionally material entry may be deleted after detection.

#### A.5 Minimal example row

| Field | Example |
|---|---|
| threat_id | TR-2026-0042 |
| title | Delegate concentration exceeded cap pressure in Tier 1 health-policy contest |
| threat_family | Delegation cartelization |
| lifecycle_stage | Delegation formation |
| contest_class | Class B |
| assets_at_risk | Political equality; Delegation accountability |
| harm_category | Shadow-party formation through delegates |
| detection_source | Indicator |
| indicator_class | Delegation concentration indicators |
| escalation_level | L3 |
| controls_active | Concentration caps; Public delegate registration; Revocation |
| control_adequacy | Partial — cap warning fired, but citizen re-routing flow was unclear |
| red_line_status | Pre-red-line |
| decision_owner | Contest administration authority |
| oversight_owner | Sortition oversight body |
| evidence_objects | DSC-44; concentration report CR-12; delegate manifest DM-8 |
| current_status | Monitoring |
| residual_risk | Medium — concentration trend persists across domain contests |
| next_review_date | 2026-06-15 |
| redesign_required | true |

#### A.6 Governance note

The register should be maintained by the designated operational authority, but must be reviewable by the oversight authority named in Section 12. No single authority may both exclusively curate the record and exclusively determine what is constitutionally material enough to enter it.
