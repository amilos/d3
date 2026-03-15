# PRD: Delegated Direct Democracy Platform (D3) v0.1
  
## 1. Purpose  
  
Create a constitutional-grade civic platform that enables direct participation, proxy voting, public deliberation, and legally meaningful civic action across several use cases:  
- Citizen initiatives and agenda-setting  
- Participatory budgeting  
- Local and community decisions  
- National consultative voting  
- Selected classes of binding votes after phased rollout  
- Structured proxy delegation with direct override  
  
The platform is not merely a voting application. It is a civic operating system combining identity, eligibility, deliberation, delegation, voting, verification, public audit, challenge handling, and constitutional review.  
  
## 2. Objectives  
  
Any real deployment must satisfy governance and trust goals consistent with high-assurance public e-voting standards and practices: secret ballot where required, end-to-end verifiability where feasible, public certification and auditability, crypto agility, institutional separation of powers, and public legitimacy through transparency and challengeability.  
  
The platform must be:  
- Secure against insider abuse, outside interference, and infrastructure compromise.  
- Anonymous for citizens where secret ballot is required.  
- Coercion-resistant to the maximum extent compatible with remote participation.  
- Manipulation-resistant in its information architecture.  
- Cognitively humane for ordinary citizens.  
- Socially legitimate through transparency, audits, public proofs, and citizen oversight.  
- Quantum-safe by architectural mandate.  
- Crypto-agile so stronger suites can be introduced without redesigning the institution.  
  
## 3. Non-goals  
  
The platform does not aim to:  
- Replace constitutional review.  
- Replace ordinary administrative processes.  
- Permit organizations to act as delegates in place of natural persons.  
- Make every decision fully remote on day one.  
- Optimize for engagement, virality, or time spent in app.  
- Rely on opaque personalization to drive civic behavior.  
  
## 4. Product principles  
  
**4.1 Equal civic weight**  
  
Every eligible citizen has equal formal voting weight.  
  
**4.2 Direct vote always available**  
  
Proxy delegation never removes the right to vote directly on a specific issue.  
  
**4.3 Public delegates, private delegators**  
  
Delegate identities, disclosures, rationale, and effective public role are visible. Individual delegators remain private.  
  
**4.4 No single point of constitutional trust**  
  
Identity, eligibility, privacy credentialing, delegation, ballot intake, tally, certification, and oversight are institutionally separated.  
  
**4.5 Security before convenience**  
  
High-stakes binding acts can require supervised or higher-assurance channels even when lower-stakes civic acts are remote.  
  
**4.6 Structured deliberation over algorithmic persuasion**  
  
The system presents signed dossiers, adversarial briefs, citizen-assembly outputs, and transparent summaries, not a social feed.  
  
**4.7 Crypto agility**  
  
Every cryptographic dependency is versioned, replaceable, and governed by change control.  
  
**4.8 Public verifiability without public exposure of voters**  
  
Citizens can verify inclusion of their ballot, and the public can verify tally integrity, without disclosing vote choice.  
  
**4.9 Direct evidence over institutional opacity**  
  
Critical ceremonies, releases, logs, proofs, and incident handling must be publicly inspectable or publicly reconstructable.  
  
**4.10 Cognitive mercy**  
  
The platform assumes most citizens are not full-time legislators and must not overload them with decision volume, language complexity, or manipulative interfaces.  
  
## 5. Scope by decision class and assurance tier  
  
**5.1 Decision classes**  
  
**Class I: Initiatives and agenda-setting - **Citizen sponsorship of proposals, petitions, and threshold-triggered civic acts.  
**Class C: Consultative voting **- Non-binding issue polling, prioritization, and shadow-chamber decision-making.  
**Class L: Local binding decisions - **Participatory budgeting, neighborhood or municipal questions, and other bounded local matters.  
**Class N: National binding decisions - **Selected classes of legislation, vetoes, ratifications, recalls, or other constitutionally authorized national decisions.  
  
**5.2 Assurance tiers**  
  
**Tier 0: Qualified civic acts**  
  
For petition signatures, initiative support, and threshold sponsorship.  
- Remote work is allowed.  
- A state eID is required.  
- Proxy is not allowed by default.  
- The act is private but attributable.  
  
**Tier 1: Consultative civic voting**  
  
For non-binding votes.  
- Remote allowed  
- Secret ballot by default  
- Proxy enabled  
- Revoting enabled  
  
**Tier 2: Binding local decisions**  
  
For local or community-level binding decisions.  
- Remote plus supervised access points  
- Secret ballot by default  
- Proxy enabled  
- Revoting plus in-person override where lawful  
  
**Tier 3: High-stakes binding decisions**  
  
For national or other constitutionally critical acts.  
- Supervised by default  
- Remote high-assurance extension only after later certification and public legitimacy thresholds are met  
- Secret ballot  
- Proxy enabled under strict caps and controls  
- Revoting and supervised override where legally defined  
  
## 6. Actors and governance  
  
The platform depends on these institutional actors:  
- Identity Authority  
- Eligibility Authority  
- Privacy Credential Authority  
- Delegation Registry Authority  
- Contest Registry Authority  
- Ballot Intake Authority  
- Public Bulletin Board Operator  
- Tally Authority  
- Certification Authority  
- Constitutional Review Gate  
- Independent Auditors  
- Sortition Oversight Council  
- Accredited Domestic and International Observers  
  
No actor may both identify the citizen and control the final tally path.  
  
## 7. Trust boundaries  
  
**7.1 Identity domain**  
  
This domain authenticates the person using state-backed eID, verifies possession of the credential, handles step-up authentication where needed, and records that an authentication event occurred.  
  
It must never handle ballot content, candidate or issue choice, tally logic, or public reporting of how a person participated.  
  
This boundary exists because identity is the strongest de-anonymization surface.  
  
**7.2 Eligibility domain**  
  
This domain decides whether the authenticated person is eligible for the specific contest: age, residence, citizenship, jurisdiction, contest-specific inclusion or exclusion, and duplicate-prevention status.  
  
It must never handle ballot choice or tally logic. It outputs only a contest-scoped authorization result.  
  
This boundary keeps legal eligibility enforcement separate from political expression.  
  
**7.3 Privacy credential domain**  
  
This domain converts a valid eligibility signal into a one-time, contest-scoped participation credential designed to be unlinkable from the person by the ballot system. It handles uniqueness, revocation lists, and credential lifetime.  
  
It must never learn vote choice and must not be able, on its own, to map a cast ballot back to a person.  
  
This is the core bridge between identity and anonymity.  
  
**7.4 Delegation domain**  
  
This domain stores domain-level and issue-level delegations, revocations, caps, transitive-resolution data, delegate disclosures, and public delegate profiles. It computes the effective delegate path at close if the citizen does not vote directly.  
  
It must never know plaintext ballot content and must not expose delegator identities publicly.  
  
This boundary exists because delegation creates its own privacy, influence, and accountability problems distinct from secret ballot voting.  
  
**7.5 Ballot preparation domain**  
  
Primarily client-side. It renders the canonical issue dossier, lets the citizen select direct vote, proxy, or abstention, produces the encrypted ballot package, and runs local verification steps.  
  
It must never create durable third-party-usable proof of vote choice and must never embed hidden persuasion logic.  
  
This is where usability, manipulation resistance, and client security meet.  
  
**7.6 Ballot intake domain**  
  
This domain receives encrypted ballot packages, validates format and one-time participation credentials, enforces revoting rules, rejects malformed submissions, and posts accepted artifacts to the bulletin board.  
  
It must never hold identity records, decrypt votes, or certify results.  
  
This is the main protocol-abuse and denial-of-service boundary.  
  
**7.7 Public bulletin board domain**  
  
This domain publishes accepted ballot artifacts, signed checkpoints, proof references, challenge records, incident markers, and certification packages in an append-only public log.  
  
It must contain no private identity data and no hidden edits.  
  
This is the shared public evidence surface.  
  
**7.8 Tally domain**  
  
This domain manages tally keys under threshold control, performs the approved tally procedure, produces public evidence that the tally is correct, and prepares result artifacts.  
  
It must never know voter identities and must never operate under unilateral institutional control.  
  
This is where result integrity could be destroyed if power accumulates.  
  
**7.9 Certification domain**  
  
This domain validates the full contest evidence package: procedure compliance, published artifacts, tally evidence, challenge resolution, incident logs, and required approvals.  
  
It must not perform tally operations or modify historical artifacts.  
  
Certification is a legal act, not just a technical computation.  
  
**7.10 Deliberation and content domain**  
  
This domain stores the canonical source corpus, plain-language summaries, pro and con briefs, constitutional and fiscal notes, delegate rationales, citizen-assembly outputs, and moderated public submissions.  
  
It must contain no hidden engagement optimization, no individualized persuasion ranking, and no unlogged AI rewriting of official materials.  
  
Manipulation often enters through information ordering, not ballot tampering.  
  
**7.11 Oversight and audit domain**  
  
This domain includes read-only mirrors, verifier tooling, challenge interfaces, incident dashboards, observer exports, and audit evidence bundles.  
  
It must never have operational control over identity, ballots, tally, or certification.  
  
Oversight must be powerful enough to detect abuse, but not become the abuse path.  
  
## 8. Functional architecture  
  
Core subsystems:  
	•	enrollment and identity service,  
	•	eligibility service,  
	•	privacy credential service,  
	•	delegation registry,  
	•	contest registry,  
	•	canonical issue dossier service,  
	•	deliberation service,  
	•	delegate workspace,  
	•	ballot client,  
	•	ballot intake service,  
	•	bulletin board,  
	•	tally service,  
	•	certification service,  
	•	observer and verifier APIs,  
	•	incident and challenge service.  
  
The functional architecture follows one core rule: **no single subsystem should be able to authenticate the citizen, learn the vote choice, and determine the official result**. Each block has a bounded role, explicit interfaces, and auditable outputs.  
  
**8.1 Contest registry**  
  
The contest registry is the authoritative catalog of all civic acts, votes, and legally relevant procedural milestones. It is also the **authoritative source of signed contest policy** consumed by identity, eligibility, delegation, ballot, tally, certification, and verifier-facing services.  
  
**Responsibilities**  
	•	create and maintain the canonical contest record,  
	•	assign legal and technical identifiers,  
	•	define jurisdiction, electorate, decision class, and assurance tier,  
	•	bind each contest to its secrecy class, proxy policy, and voting rules,  
	•	track lifecycle state from proposal through certification and archival,  
	•	bind result and proof packages to the contest record.  
  
**Required fields**  
	•	contest ID,  
	•	legal title,  
	•	plain-language title,  
	•	machine-readable legal text,  
	•	redline against prior text where applicable,  
	•	jurisdiction and electorate definition,  
	•	decision class,  
	•	assurance tier,  
	•	secrecy class,  
	•	proxy policy,  
	•	revoting policy,  
	•	supervised override policy,  
	•	constitutional review state,  
	•	dossier publication state,  
	•	deliberation window,  
	•	voting window,  
	•	challenge window,  
	•	certification state,  
	•	result package reference,  
	•	proof package reference,  
	•	incident markers.  
  
**Inputs**  
	•	government or parliamentary submissions,  
	•	citizen initiative records,  
	•	constitutionally triggered contests,  
	•	legal formatting output,  
	•	constitutional review decisions.  
  
**Outputs**  
	•	canonical contest metadata for all downstream services,  
	•	immutable references used by ballot client, bulletin board, tally, and certification,  
	•	machine-readable contest manifests for observer tooling.  
  
**Critical constraints**  
	•	no hidden contest mutation after voting begins,  
	•	all state transitions must be signed and timestamped,  
	•	any post-publication change must create a new version with a visible diff,  
	•	all downstream services must resolve contest policy from the same signed registry state.  
  
  
**8.2 Delegate workspace**  
  
The delegate workspace is the public operating environment for natural-person delegates who accept issue-level or domain-level delegation. It is a **product-facing interface**; authoritative delegation state is maintained by the **delegation registry**, and authoritative delegate-instruction records are maintained by the **delegate instruction service**.  
  
**Responsibilities**  
	•	provide delegates with issue queues and domain worklists,  
	•	support publication of rationale, intended stance, and policy notes,  
	•	manage disclosure obligations and conflict declarations,  
	•	show current delegation cap utilization,  
	•	support structured responses to citizen questions,  
	•	expose the delegate’s public performance history.  
  
**Core features**  
	•	domain dashboard,  
	•	issue dashboard,  
	•	rationale editor,  
	•	disclosure manager,  
	•	conflict alerting,  
	•	delegation cap monitor,  
	•	public profile preview,  
	•	audit trail of edits and publications.  
  
**Inputs**  
	•	delegation registry data,  
	•	contest registry state,  
	•	dossier materials,  
	•	disclosure filings,  
	•	citizen questions routed through moderation.  
  
**Outputs**  
	•	public delegate profiles,  
	•	signed rationales,  
	•	declared intended stances,  
	•	disclosure records,  
	•	structured Q&A artifacts.  
  
**Critical constraints**  
	•	no access to secret ballot content,  
	•	no ability to target or message individual delegators privately inside the voting workflow,  
	•	no suppression of historical rationale or disclosure records after publication except through visible amendment flows.  
  
  
**8.3 Enrollment and identity service**  
  
The enrollment and identity service establishes who the person is and whether they can securely access the platform.  
  
**Responsibilities**  
	•	register platform participation against state-backed eID,  
	•	authenticate users,  
	•	perform step-up authentication for sensitive actions,  
	•	manage account lifecycle and credential binding,  
	•	maintain minimal identity event logs,  
	•	coordinate high-assurance recovery for eligible classes.  
  
**Core features**  
	•	one-time enrollment,  
	•	login/authentication,  
	•	device registration where allowed,  
	•	high-assurance session establishment,  
	•	in-person recovery workflow for high-stakes use,  
	•	diaspora access path integration.  
  
**Inputs**  
	•	state eID assertions,  
	•	in-person identity checks where required,  
	•	legal eligibility references for enrollment scope.  
  
**Outputs**  
	•	authentication event token,  
	•	session token for downstream eligibility check,  
	•	signed identity event logs.  
  
**Critical constraints**  
	•	no ballot content or proxy choice handling,  
	•	no public participation disclosure,  
	•	identity logs must be minimized and retained only as legally necessary,  
	•	high-stakes recovery must never be remote-only.  
  
  
**8.4 Eligibility service**  
  
The eligibility service determines whether an authenticated person may participate in a specific contest.  
  
**Responsibilities**  
	•	evaluate contest-specific eligibility,  
	•	apply jurisdiction, residence, citizenship, age, and exclusion rules,  
	•	prevent duplicate effective participation,  
	•	return contest-scoped authorization results,  
	•	maintain legally auditable eligibility decisions.  
  
**Core features**  
	•	contest-specific rules engine,  
	•	jurisdiction mapping,  
	•	duplicate-prevention check,  
	•	supervised-override eligibility check,  
	•	revote validity resolution support,  
	•	diaspora routing rules.  
  
**Inputs**  
	•	identity-authentication result,  
	•	contest registry policy,  
	•	authoritative electorate data,  
	•	legal challenge or court orders where applicable.  
  
**Outputs**  
	•	eligible / not eligible decision,  
	•	contest-scoped authorization signal,  
	•	duplicate-prevention state,  
	•	audit record of the decision basis.  
  
**Critical constraints**  
	•	no vote-choice handling,  
	•	no tally logic,  
	•	no public exposure of individual eligibility status beyond authorized channels,  
	•	any legal override must be logged and reviewable.  
  
  
**8.5 Privacy credential service**  
  
The privacy credential service is the functional bridge from “this person may participate” to “this ballot is valid without revealing who cast it.”  
  
**Responsibilities**  
	•	transform an eligibility result into a one-time contest-scoped participation credential,  
	•	enforce uniqueness and lifetime of the credential,  
	•	support revocation or invalidation where policy allows,  
	•	keep identity-side authorization separate from ballot-side validation,  
	•	support future migration of anonymous credential schemes.  
  
**Core features**  
	•	issuance of one-time participation credentials,  
	•	contest scoping,  
	•	revocation handling,  
	•	replay resistance,  
	•	credential-expiry handling,  
	•	audit log of issuance events without vote linkage.  
  
**Inputs**  
	•	signed eligibility result,  
	•	contest policy,  
	•	revote and override rules.  
  
**Outputs**  
	•	privacy-preserving participation credential,  
	•	revocation signals,  
	•	issuance audit artifacts.  
  
**Critical constraints**  
	•	must not learn vote choice,  
	•	must not on its own be able to map a ballot to a person,  
	•	must not become a shadow identity ledger,  
	•	issuance, revocation, and expiry rules must be publicly specifiable and testable.  
  
**8.6 Delegation registry**  
  
The delegation registry is the authoritative service for issue-level and domain-level proxy delegation.  
  
**Responsibilities**  
	•	store active delegations and revocations,  
	•	support issue-level, domain-level, and capped transitive delegation,  
	•	enforce delegate eligibility and registration status,  
	•	enforce concentration caps and transitive-depth limits,  
	•	resolve effective proxy path at close when no direct vote exists,  
	•	expose public delegate data while protecting delegator privacy.  
  
**Core features**  
	•	create / revoke delegation,  
	•	issue-level override,  
	•	domain-level default delegation,  
	•	cap enforcement,  
	•	transitive path computation,  
	•	public delegate directory,  
	•	aggregate delegation-flow reporting above anonymity thresholds.  
  
**Inputs**  
	•	citizen delegation instructions,  
	•	delegate registration status,  
	•	contest registry policy,  
	•	legal limits on delegation structure.  
  
**Outputs**  
	•	effective delegation map for close-of-contest resolution,  
	•	public delegate profiles,  
	•	aggregate delegation metrics,  
	•	cap and anomaly alerts.  
  
**Critical constraints**  
	•	no plaintext ballot access,  
	•	delegator identities are private,  
	•	effective delegation path must be reproducible for audit,  
	•	contest close must freeze relevant delegation state for that contest.  
  
  
**8.7 Canonical issue dossier service**  
  
The dossier service is the structured knowledge layer for each contest. It is authoritative for **official issue presentation and provenance**, but not for **legal validity**, **vote semantics**, or **tally semantics**.  
  
**Responsibilities**  
	•	assemble the canonical issue packet for each contest,  
	•	bind legal text, plain-language summaries, and structured analysis,  
	•	ensure every issue is presented in the same fixed format,  
	•	maintain signed, versioned source materials,  
	•	provide source-linked summaries for citizens and observers.  
  
**Core features**  
	•	issue summary generation,  
	•	source corpus management,  
	•	plain-language rendering,  
	•	fiscal and constitutional notes,  
	•	implementation notes,  
	•	supporter/opponent disclosures,  
	•	redline visualization.  
  
**Required dossier sections**  
	•	what changes,  
	•	what stays the same,  
	•	strongest argument for,  
	•	strongest argument against,  
	•	constitutional impact,  
	•	fiscal impact,  
	•	implementation impact,  
	•	backers and opponents,  
	•	delegate stance if applicable,  
	•	citizen assembly summary,  
	•	full text and redline.  
  
**Inputs**  
	•	contest registry,  
	•	legal text,  
	•	official explanatory memoranda,  
	•	expert briefs,  
	•	citizen assembly outputs,  
	•	signed source corpus.  
  
**Outputs**  
	•	citizen-facing issue dossier,  
	•	machine-readable dossier package,  
	•	source-linked explanation artifacts.  
  
**Critical constraints**  
	•	no hidden editorial ranking,  
	•	no silent content rewrites,  
	•	every public summary must be traceable to signed sources,  
	•	any update must be versioned and visible.  
  
  
**8.8 Deliberation service**  
  
The deliberation service hosts structured public reasoning around each issue. It is **outside the protocol-critical vote path** and must not be able to alter contest rules, accepted ballots, tally inputs, or certification state.  
  
**Responsibilities**  
	•	support moderated public submissions,  
	•	collect pro and con arguments in structured form,  
	•	host expert and institutional briefs,  
	•	support citizen-assembly outputs,  
	•	enable transparent, logged AI-assisted summarization,  
	•	maintain moderation without turning into a social feed.  
  
**Core features**  
	•	structured submission templates,  
	•	moderated discussion threads,  
	•	pro/con brief publication,  
	•	expert Q&A,  
	•	citizen assembly module,  
	•	summary and translation services,  
	•	contradiction-detection assistance.  
  
**Inputs**  
	•	citizen submissions,  
	•	expert briefs,  
	•	delegate rationales,  
	•	official source materials,  
	•	moderation and policy rules.  
  
**Outputs**  
	•	moderated public argument sets,  
	•	issue summaries,  
	•	minority notes,  
	•	deliberation transcripts and archives.  
  
**Critical constraints**  
	•	no engagement ranking,  
	•	no algorithmic virality boosting,  
	•	no psychographic targeting,  
	•	all moderation actions must be logged and appealable where policy requires.  
  
  
**8.9 Ballot client**  
  
The ballot client is the protected user-facing application through which citizens read, decide, verify, and act. It routes participation through two distinct protected paths: **delegation actions** to the delegation registry and **direct ballot submissions** to the ballot intake service, under contest policy defined elsewhere.  
  
**Responsibilities**  
	•	render the canonical issue dossier and contest-specific options,  
	•	let the citizen vote directly, rely on proxy, override proxy, or abstain,  
	•	prepare protected participation artifacts locally,  
	•	perform allowed verification steps,  
	•	support revoting where policy permits,  
	•	protect the user from manipulative interface patterns.  
  
**Core features**  
	•	authenticated session handling,  
	•	issue-view and summary modes,  
	•	direct vote / proxy / abstain flow,  
	•	local preparation of participation artifacts,  
	•	short-lived verification flow,  
	•	progress saving,  
	•	accessibility modes,  
	•	safe-exit behavior.  
  
**Inputs**  
	•	contest registry,  
	•	dossier service,  
	•	delegation registry status,  
	•	privacy-preserving participation state,  
	•	accessibility and language preferences.  
  
**Outputs**  
	•	protected delegation updates,  
	•	protected direct ballot submissions,  
	•	local confirmation state,  
	•	non-durable verification artifacts,  
	•	client-side audit events.  
  
**Critical constraints**  
	•	no durable receipt of vote choice,  
	•	no hidden persuasive ranking,  
	•	no uncontrolled local storage of sensitive voting state,  
	•	high-stakes protected actions must use a dedicated audited application rather than a generic web flow by default.  
  
  
**8.10 Ballot intake service**  
  
The ballot intake service is the hardened ingestion layer for cast ballots.  
  
**Responsibilities**  
	•	receive protected ballot packages,  
	•	validate contest-scoped participation credentials,  
	•	enforce format and well-formedness rules,  
	•	apply revoting rules,  
	•	reject malformed, duplicated, or unauthorized submissions,  
	•	post accepted ballot artifacts to the bulletin board.  
  
**Core features**  
	•	submission validation,  
	•	one-time credential enforcement,  
	•	revote replacement logic,  
	•	malformed payload rejection,  
	•	replay protection,  
	•	intake audit logging,  
	•	throughput protection against floods and abuse.  
  
**Inputs**  
	•	ballot packages from clients or supervised terminals,  
	•	contest policy from registry,  
	•	credential status from privacy credential service,  
	•	override or revocation signals where applicable.  
  
**Outputs**  
	•	accept / reject decision,  
	•	accepted ballot artifact,  
	•	updated effective-ballot state,  
	•	intake audit logs,  
	•	bulletin board publication request.  
  
**Critical constraints**  
	•	no identity storage,  
	•	no ballot decryption,  
	•	no result computation,  
	•	no silent discard path.  
  
  
**8.11 Bulletin board**  
  
The bulletin board is the public append-only evidence surface of the platform.  
  
**Responsibilities**  
	•	publish accepted ballot artifacts,  
	•	publish signed checkpoints and sequence commitments,  
	•	publish proof references, incident markers, and certification packages,  
	•	provide immutable contest evidence access,  
	•	support public mirroring and independent replay.  
  
**Core features**  
	•	append-only log,  
	•	signed checkpoints,  
	•	versioned artifact retrieval,  
	•	public replication endpoints,  
	•	contest evidence packaging,  
	•	observer export formats.  
  
**Inputs**  
	•	accepted ballot artifacts,  
	•	tally proofs,  
	•	incident records,  
	•	certification packages,  
	•	challenge outcomes.  
  
**Outputs**  
	•	public evidence log,  
	•	mirrorable exports,  
	•	verification bundles.  
  
**Critical constraints**  
	•	no hidden deletion or reordering,  
	•	no private identity information,  
	•	any correction must be additive and visible,  
	•	availability and integrity must survive partial infrastructure compromise.  
  
  
**8.12 Tally service**  
  
The tally service is the controlled environment in which accepted contest inputs are converted into an official result package. It executes the **approved tally procedure for the contest’s protocol profile** and publishes the resulting evidence bundle. The detailed tally semantics are defined in the **Protocol Appendix**, not here.  
  
**Responsibilities**  
	•	execute the approved tally procedure for the contest’s protocol profile,  
	•	operate under threshold or quorum control,  
	•	consume the authorized contest inputs from the evidence chain,  
	•	produce result artifacts and the corresponding evidence bundle,  
	•	prepare certification inputs.  
  
**Core features**  
	•	key-ceremony integration,  
	•	threshold key custody,  
	•	tally execution,  
	•	proof and evidence generation,  
	•	result packaging,  
	•	contest closure workflow,  
	•	audit transcript generation.  
  
**Inputs**  
	•	accepted contest artifacts from the bulletin board,  
	•	contest policy and protocol profile from the contest registry,  
	•	authorized override or supersession state where applicable,  
	•	threshold authorization from trustees.  
  
**Outputs**  
	•	result package,  
	•	proof or evidence bundle,  
	•	tally transcript,  
	•	certification input package.  
  
**Critical constraints**  
	•	no voter identity access,  
	•	no unilateral institutional control,  
	•	no off-record tally execution,  
	•	no hidden change to contest policy or admissible input set during tally.  
  
  
**8.13 Certification service**  
  
The certification service converts a technically completed contest into a legally recognized result. It validates the completeness and admissibility of the contest evidence package but does **not** define the underlying protocol semantics of that package.  
  
**Responsibilities**  
	•	validate that all procedural prerequisites are satisfied,  
	•	validate evidence package completeness,  
	•	ensure challenge and incident workflows have been resolved or classified,  
	•	issue certification or refusal,  
	•	publish legal certification artifacts.  
  
**Core features**  
	•	procedural checklist engine,  
	•	evidence package validator,  
	•	certification decision workflow,  
	•	legal sign-off chain,  
	•	certification publication,  
	•	refusal and remediation path.  
  
**Inputs**  
	•	result and evidence package from the tally service,  
	•	contest registry state,  
	•	incident logs,  
	•	challenge resolutions,  
	•	auditor statements where required.  
  
**Outputs**  
	•	certified result,  
	•	certification refusal,  
	•	certification record,  
	•	publication package for public archive.  
  
**Critical constraints**  
	•	no modification of tally artifacts,  
	•	no hidden certification condition changes,  
	•	certification must be legally attributable and publicly inspectable,  
	•	certification and tally must remain institutionally separate.  
  
  
**8.14 Observer and verifier APIs**  
  
These interfaces exist so outsiders can independently inspect, verify, replay, and challenge the system.  
  
**Responsibilities**  
	•	expose contest data, public artifacts, proofs, and logs in machine-readable form,  
	•	provide verifier-friendly export formats,  
	•	support public mirrors and replay tools,  
	•	expose audit hooks without operational privilege.  
  
**Core features**  
	•	public contest manifest API,  
	•	bulletin board export API,  
	•	proof and result package API,  
	•	challenge status API,  
	•	integrity-check endpoints,  
	•	mirror synchronization.  
  
**Inputs**  
	•	contest registry,  
	•	bulletin board data,  
	•	tally proof bundles,  
	•	certification records,  
	•	incident and challenge records.  
  
**Outputs**  
	•	public machine-readable data,  
	•	verifier tool inputs,  
	•	observer evidence bundles.  
  
**Critical constraints**  
	•	read-only by design,  
	•	no privileged write path into operational systems,  
	•	stable schemas for independent tooling,  
	•	no hidden filtering of politically sensitive artifacts.  
  
  
**8.15 Incident and challenge service**  
  
This service handles operational failures, legal objections, protocol disputes, and public challenges.  
  
**Responsibilities**  
	•	register incidents and challenges,  
	•	classify severity and assign workflow,  
	•	track remediation, escalation, and disposition,  
	•	pause or flag contests where rules require,  
	•	expose public challenge status and final resolution,  
	•	preserve incident evidence for audit and review.  
  
**Core features**  
	•	incident intake,  
	•	challenge filing,  
	•	severity taxonomy,  
	•	escalation workflow,  
	•	pause / downgrade triggers,  
	•	public disposition publishing,  
	•	immutable incident archive.  
  
**Inputs**  
	•	citizen reports,  
	•	observer reports,  
	•	automated anomaly alerts,  
	•	auditor findings,  
	•	operator incident reports,  
	•	constitutional or judicial orders.  
  
**Outputs**  
	•	incident records,  
	•	challenge records,  
	•	public status page,  
	•	resolution or remediation artifacts,  
	•	escalation signals to certification or contest operators.  
  
**Critical constraints**  
	•	no silent incident suppression,  
	•	no hidden closure of material challenges,  
	•	every disposition must be attributable and timestamped,  
	•	high-severity incidents must automatically surface to oversight and certification domains.  
  
  
  
  
**8.16 Inter-block flow**  
  
The normal flow across blocks is:  
	1.	the citizen authenticates through the enrollment and identity service,  
	2.	the eligibility service evaluates contest-specific participation rights,  
	3.	the privacy credential service issues a contest-scoped participation credential,  
	4.	the citizen reviews the issue through the dossier and deliberation services,  
	5.	the delegation registry resolves any applicable proxy state,  
	6.	the ballot client prepares and submits the protected ballot,  
	7.	the ballot intake service validates and accepts or rejects the submission,  
	8.	accepted artifacts are posted to the bulletin board,  
	9.	the tally service computes the result and proof package,  
	10.	the certification service validates the full evidence chain and certifies or refuses,  
	11.	observer and verifier APIs expose the evidence,  
	12.	incident and challenge service remains open through the challenge window and archive phase.  
  
  
**8.17 Cross-cutting requirements for every block**  
  
Every subsystem in Section 8 must support:  
	•	signed and timestamped state changes,  
	•	minimum necessary data retention,  
	•	public or auditor-visible schema documentation,  
	•	separation of duties for operators,  
	•	full audit logging,  
	•	reproducible deployment and release integrity,  
	•	emergency downgrade and continuity procedures where applicable,  
	•	localization and accessibility for user-facing surfaces,  
	•	versioned interfaces and backward-compatible migration plans.  
  
  
  
  
## 9. Identity and participation policy 
  
This section defines the platform-wide policy for identity, eligibility, recovery, and participation rights. Service responsibilities and trust boundaries are defined elsewhere.  
  
**9.1 State-backed identity requirement**  
  
Participation in protected civic acts requires a state-backed digital identity recognized by the platform’s identity and eligibility framework.  
  
This requirement exists to:  
	•	prevent Sybil participation,  
	•	support legally meaningful eligibility decisions,  
	•	enable strong recovery and audit processes,  
	•	preserve a clean distinction between authentic participation and anonymous public discussion.  
  
**9.2 Participation recovery policy**  
  
Recovery policy must be proportional to contest assurance tier.  
	•	lower-assurance civic acts may use lower-friction recovery mechanisms permitted by platform policy,  
	•	higher-assurance and constitutionally significant contest classes require in-person or equivalently supervised recovery,  
	•	no recovery path may silently weaken contest integrity or ballot secrecy requirements.  
  
**9.3 One effective participation right per person per contest**  
  
The platform must enforce the rule that each eligible person has only the participation rights permitted for a given contest and may produce only one effective outcome under contest policy.  
  
This is a platform-wide guarantee.  
The exact technical and protocol semantics are defined elsewhere.  
  
**9.4 Eligibility is contest-specific**  
  
Eligibility is determined separately for each contest according to jurisdiction, legal status, and contest class.  
  
The platform must support:  
	•	contest-specific electorate definitions,  
	•	legally auditable inclusion and exclusion decisions,  
	•	clear handling of cross-jurisdiction and diaspora cases,  
	•	visible treatment of overrides, exceptions, and dispute paths.  
  
**9.5 Diaspora participation policy**  
  
Diaspora participation must be supported, but not by collapsing assurance requirements.  
  
The platform may support:  
	•	remote participation for lower-assurance classes,  
	•	supervised or consular participation for higher-assurance classes,  
	•	contest-specific channel restrictions where required by law or risk posture.  
  
**9.6 Identity minimization principle**  
  
Identity information must be used only to:  
	•	establish who the person is,  
	•	determine whether they are eligible,  
	•	support lawful recovery,  
	•	support legally required audit and dispute handling.  
  
Identity must not be reused as a shortcut for exposing political participation or weakening ballot secrecy.  
  
⸻  
  
**10. Ballot guarantees**  
  
This section defines the platform-wide guarantees that apply to direct voting and secret-ballot participation. Exact protocol mechanics are defined in the Protocol Appendix.  
  
**10.1 Secrecy where required**  
  
Where a contest requires secret ballot, the platform must preserve that property across:  
	•	participation authorization,  
	•	ballot preparation,  
	•	submission,  
	•	storage,  
	•	tally,  
	•	publication,  
	•	and audit.  
  
No convenience feature, operational fallback, or dispute process may silently negate this requirement.  
  
**10.2 Public verifiability**  
  
The platform must provide a verifiability model sufficient for independent parties to determine whether the declared result is consistent with the approved process and the accepted contest inputs.  
  
Where contest policy allows, the platform should support:  
	•	participant-facing verification that their participation was correctly recorded,  
	•	public verification that published evidence supports the declared result.  
  
**10.3 Revoting and override capability**  
  
The platform may support revoting and supervised override for contest classes where law and assurance policy permit.  
  
These capabilities exist to:  
	•	mitigate endpoint uncertainty,  
	•	reduce coercion value,  
	•	support correction of mistakes,  
	•	preserve higher-assurance fallback paths.  
  
The exact semantics of these capabilities are not defined in this section.  
  
**10.4 No durable proof of vote choice**  
  
The platform must not provide participants with a durable artifact that can serve as third-party-usable proof of vote choice in secret-ballot contests.  
  
Verification mechanisms must be designed so that they improve confidence without turning into coercion or vote-buying tools.  
  
**10.5 Small-electorate secrecy safeguards**  
  
Where the effective electorate is too small for meaningful secrecy, the platform must apply additional safeguards such as:  
	•	delayed publication,  
	•	pooled reporting,  
	•	reduced result granularity,  
	•	alternate contest treatment,  
	•	or alternate voting method.  
  
The goal is to avoid pretending secrecy exists where it is not credible.  
  
**10.6 Ballot guarantees are contest-sensitive**  
  
Not all contests require the same secrecy model, verification model, or override policy.  
  
The platform must bind these guarantees explicitly to:  
	•	contest class,  
	•	assurance tier,  
	•	jurisdiction,  
	•	and legal requirements.  
  
⸻  
  
**11. Delegation governance policy**  
  
This section defines the platform-wide governance rules for proxy delegation. It does not define the exact protocol semantics of delegation resolution, revocation ordering, or tally treatment.  
  
**11.1 Delegation as an optional civic mechanism**  
  
The platform supports proxy delegation as an optional participation mechanism, not as a replacement for direct voting.  
  
Any citizen entitled to participate in a proxy-enabled contest must retain the ability to act directly, subject to contest policy and timing rules.  
  
**11.2 Delegate eligibility**  
  
A delegate must be:  
	•	a natural person,  
	•	eligible under applicable platform and jurisdiction rules,  
	•	registered under the platform’s public delegate framework,  
	•	bound by disclosure and accountability requirements.  
  
Organizations, parties, firms, or informal collectives may advocate, but they must not act as delegates in place of natural persons.  
  
**11.3 Delegate obligations**  
  
Registered delegates must maintain current public disclosures covering:  
	•	identity,  
	•	relevant affiliations,  
	•	relevant funding relationships,  
	•	conflicts of interest,  
	•	rationale history,  
	•	and any additional legally required declarations.  
  
Delegates act in a public civic role and must be treated accordingly.  
  
**11.4 Transparency model**  
  
The platform follows this transparency rule:  
	•	delegates are public,  
	•	delegators are private,  
	•	aggregate delegation visibility is permitted only within anonymity-preserving limits.  
  
This model is meant to support public accountability without turning delegators into visible political subjects.  
  
**11.5 Direct override principle**  
  
Delegation must remain reversible by the citizen within the contest policy framework.  
  
The platform must be designed so that delegation does not become an irreversible transfer of civic agency.  
  
**11.6 Bounded accumulation of delegated influence**  
  
Delegated influence must be bounded through policy controls such as:  
	•	per-contest caps,  
	•	domain-specific caps,  
	•	transitivity limits,  
	•	review thresholds,  
	•	and anti-concentration monitoring.  
  
The purpose is to prevent proxy participation from mutating into hidden party structures or delegate monopolies.  
  
**11.7 Transitivity posture**  
  
If transitive delegation is permitted, it must be:  
	•	explicitly policy-bound,  
	•	limited in depth,  
	•	reviewable,  
	•	and publicly governable.  
  
Transitivity is not a default democratic good; it is a controlled design option.  
  
**11.8 Anti-cartel safeguards**  
  
The platform must support anti-cartel measures including:  
	•	anomaly monitoring,  
	•	disclosure of relevant organized advocacy and funding,  
	•	concentration-triggered review,  
	•	contest-class-specific restrictions,  
	•	and governance rules that discourage durable capture of proxy power.  
  
**11.9 Delegation is contest-policy-governed**  
  
The availability, scope, and limits of delegation must be explicitly tied to contest policy rather than assumed to be globally identical across all use cases.  
  
⸻  
  
**12. Contest initiation and decision lifecycle**  
  
This section defines the governance lifecycle by which issues become votable and move from proposal to legally recognized outcome.  
  
**12.1 Authorized initiation channels**  
  
A contest may enter the platform through one or more of the following channels:  
	•	government or parliamentary submission,  
	•	citizen initiative or threshold-triggered civic mechanism,  
	•	constitutionally or legally mandated trigger,  
	•	local or community process where authorized.  
  
The platform must not allow undeclared or ad hoc routes into binding decision-making.  
  
**12.2 Admissibility and legal preparation**  
  
Before a contest is opened for participation, it must pass the required intake and preparation stages, including as applicable:  
	•	admissibility review,  
	•	legal formatting and canonical-text preparation,  
	•	jurisdiction and electorate confirmation,  
	•	constitutional or legal pre-review,  
	•	classification into contest class and assurance tier.  
  
**12.3 Mandatory publication before voting**  
  
Before voting opens, the platform must publish the contest in a form sufficient for meaningful civic inspection, including:  
	•	authoritative contest metadata,  
	•	official issue materials,  
	•	required legal and explanatory documents,  
	•	applicable disclosure and accountability information,  
	•	and the timing of the deliberation and voting phases.  
  
**12.4 Deliberation minimums**  
  
Binding and high-impact contests must not move directly from intake to vote without a minimum deliberation and inspection period.  
  
That period should be long enough to support:  
	•	public review,  
	•	expert challenge,  
	•	citizen understanding,  
	•	delegate accountability,  
	•	and procedural correction where needed.  
  
**12.5 Voting phase**  
  
Once opened, the contest proceeds under the policy and assurance conditions assigned to it.  
  
This includes:  
	•	the applicable participation mode,  
	•	the secrecy model,  
	•	the delegation policy,  
	•	the assurance tier,  
	•	and the permitted incident and fallback posture.  
  
**12.6 Review, challenge, and certification phase**  
  
After the voting window closes, the contest must enter a formal post-vote review phase that includes:  
	•	publication of the relevant evidence package,  
	•	challenge and incident handling,  
	•	any required audit and observer review,  
	•	and certification or refusal to certify.  
  
No contest should become legally final without completing this governance path.  
  
**12.7 Lifecycle integrity**  
  
Every contest must have a visible lifecycle state from proposal through archival.  
  
The lifecycle must be:  
	•	publicly traceable,  
	•	versioned where changes occur,  
	•	and resistant to silent procedural mutation.  
  
⸻  
  
**13. Information integrity and deliberation policy**  
  
This section defines the platform-wide rules for official issue presentation, civic deliberation, AI use, and information ordering.  
  
**13.1 Canonical issue presentation**  
  
Every contest must be presented through a canonical issue format defined by the platform.  
  
The detailed dossier schema is specified elsewhere.  
This section governs the policy intent:  
	•	consistency across issues,  
	•	comparable presentation,  
	•	source traceability,  
	•	and protection against manipulative presentation differences.  
  
**13.2 No algorithmic persuasion feed**  
  
The platform must not use an engagement-ranked political feed, paid amplification, hidden emotional optimization, or opaque political recommendation logic inside the civic decision workflow.  
  
The platform is a deliberative and decision-making system, not a social-media persuasion engine.  
  
**13.3 Signed source corpus and provenance**  
  
Official summaries, explanatory materials, and issue dossiers must be grounded in a signed, versioned source corpus with visible provenance.  
  
Citizens and observers must be able to determine:  
	•	where official summaries came from,  
	•	what source materials were used,  
	•	and whether those materials changed over time.  
  
**13.4 AI usage policy**  
  
AI may be used only in bounded, reviewable, provenance-aware ways such as:  
	•	summarization,  
	•	translation,  
	•	readability adaptation,  
	•	accessibility support,  
	•	clustering of arguments,  
	•	contradiction detection.  
  
AI must not be used for:  
	•	personalized persuasion,  
	•	psychographic targeting,  
	•	hidden ranking of political content,  
	•	silent rewriting of official materials,  
	•	or covertly steering civic choice.  
  
**13.5 Moderation accountability**  
  
Public reasoning spaces may be moderated, but moderation must be:  
	•	policy-bound,  
	•	logged,  
	•	reviewable,  
	•	and visibly separated from contest validity and result determination.  
  
Moderation must not become a hidden mechanism for shaping the legal meaning of the contest.  
  
**13.6 Citizen assemblies and adversarial briefing**  
  
For complex or high-impact issues, the platform should support structured deliberative mechanisms such as:  
	•	citizen assemblies,  
	•	adversarial pro and con briefs,  
	•	expert notes,  
	•	minority reports,  
	•	and implementation-oriented summaries.  
  
The purpose is to improve comprehension and legitimacy, not to create another elite veto point.  
  
**13.7 Decision pacing and cognitive load**  
  
The platform must actively manage decision volume and timing so that citizens are not overwhelmed by simultaneous high-stakes choices.  
  
This includes policy mechanisms such as:  
	•	issue calendars,  
	•	spacing rules,  
	•	contest grouping constraints,  
	•	and escalation thresholds for particularly complex matters.  
  
**13.8 Information integrity as a security property**  
  
Manipulation resistance in official issue presentation is a security and legitimacy requirement, not just a content-design preference.  
  
The platform must therefore treat:  
	•	provenance,  
	•	transparency of summaries,  
	•	moderation accountability,  
	•	AI usage constraints,  
	•	and non-manipulative ordering  
  
as core civic-control requirements.  
  
  
  
## 14. User experience and accessibility  
  
The platform must be usable, understandable, and safe for ordinary citizens under real-world conditions, including low digital literacy, disability, remote access constraints, political sensitivity, and coercive environments.  
  
User experience is treated as a **constitutional-quality requirement**, not a presentation layer. A platform that is cryptographically strong but confusing, manipulative, or socially exclusionary does not meet the goals of this PRD.  
  
**14.1 UX objectives**  
  
The user experience must achieve all of the following:  
	•	make protected civic participation understandable without requiring technical expertise,  
	•	reduce cognitive overload in high-stakes decisions,  
	•	support safe participation under coercion-sensitive conditions,  
	•	preserve neutrality in presentation and interaction design,  
	•	make delegation comprehensible and reversible,  
	•	provide strong accessibility across ability, age, language, and literacy differences,  
	•	support public confidence through transparent verification and evidence access,  
	•	enable secure supervised and assisted participation without undermining privacy.  
  
**14.2 Supported user groups**  
  
The platform must explicitly design for:  
	•	citizens with low digital literacy,  
	•	elderly users,  
	•	blind and low-vision users,  
	•	deaf and hard-of-hearing users,  
	•	users with motor impairments,  
	•	users with cognitive disabilities or reduced reading stamina,  
	•	diaspora users,  
	•	users on low-end devices,  
	•	users with intermittent connectivity,  
	•	users participating from coercive households or workplaces,  
	•	registered delegates performing repeated issue review,  
	•	auditors, observers, and journalists inspecting evidence.  
  
The default experience must not assume high political literacy, high reading endurance, or constant broadband access.  
  
**14.3 Core UX principles**  
  
**14.3.1 Neutrality of presentation**  
  
The interface must not steer users through visual emphasis, ranking tricks, emotional framing, or asymmetric friction.  
  
This includes:  
	•	neutral ordering of options,  
	•	neutral typography and color use for vote choices,  
	•	no gamification,  
	•	no urgency styling that pressures vote choice,  
	•	no popularity or bandwagon cues in the protected decision workflow.  
  
**14.3.2 Progressive disclosure**  
  
The platform must present information in layers:  
	•	short plain-language summary,  
	•	medium-detail explanation,  
	•	full legal and evidentiary detail.  
  
Citizens should be able to stop at the level they need without being blocked by expert-level complexity.  
  
**14.3.3 Comprehension before action**  
  
For high-stakes or complex issues, the UX should encourage understanding before protected action by exposing:  
	•	what changes,  
	•	what does not change,  
	•	strongest case for,  
	•	strongest case against,  
	•	implementation consequences,  
	•	fiscal consequences,  
	•	constitutional consequences.  
  
**14.3.4 Reversible participation where policy allows**  
  
Where contest policy permits revoting, override, or delegation changes, the experience must make reversibility explicit without creating false confidence or coercion artifacts.  
  
**14.3.5 One system, many confidence levels**  
  
The UX must support different decision classes and assurance tiers without making the platform feel like a different product each time.  
  
The user should understand:  
	•	what kind of contest this is,  
	•	how binding it is,  
	•	what participation method applies,  
	•	whether delegation is available,  
	•	whether supervised access is required or recommended.  
  
**14.4 Decision experience**  
  
**14.4.1 Canonical issue page**  
  
Every contest must have a standard decision page structure with stable placement of:  
	•	title and contest type,  
	•	binding status,  
	•	decision deadline and key dates,  
	•	plain-language summary,  
	•	“what changes / what stays the same,”  
	•	strongest case for,  
	•	strongest case against,  
	•	constitutional and fiscal notes,  
	•	implementation note,  
	•	current delegate status if relevant,  
	•	full text and source materials,  
	•	protected action entry point.  
  
The location and naming of these elements should remain stable across contests.  
  
**14.4.2 Choice architecture**  
  
The platform must distinguish clearly between:  
	•	reading about an issue,  
	•	delegating,  
	•	voting directly,  
	•	abstaining,  
	•	verifying a prior action,  
	•	reviewing delegate rationale.  
  
The system must not blur these actions together.  
  
**14.4.3 Cognitive pacing**  
  
The platform must reduce overload through:  
	•	issue calendars,  
	•	saved progress,  
	•	reading-time estimates,  
	•	“review later” queues,  
	•	grouped low-stakes contests,  
	•	spacing rules for complex or binding decisions.  
  
High-stakes contests should never be experienced as just another notification in a stream.  
  
**14.5 Delegation UX**  
  
Proxy voting is one of the hardest UX challenges in the system. The platform must make delegation legible and auditable to ordinary users.  
  
**14.5.1 Delegation clarity**  
  
The user must always be able to see:  
	•	whether they are currently delegating on this issue,  
	•	to whom they are delegating,  
	•	whether the delegation comes from issue-level or domain-level policy,  
	•	whether the delegate has published a rationale,  
	•	whether the user can still override directly.  
  
**14.5.2 Domain and issue separation**  
  
The UX must clearly distinguish:  
	•	domain-level delegation,  
	•	issue-level delegation,  
	•	temporary override,  
	•	direct vote.  
  
Users should not need to understand graph semantics to know what will happen if they do nothing.  
  
**14.5.3 Public delegate profile**  
  
Every delegate profile should expose, in a readable form:  
	•	identity,  
	•	relevant disclosures,  
	•	rationale history,  
	•	prior positions,  
	•	current intended stance where published,  
	•	cap or concentration status where policy allows publication.  
  
**14.5.4 Revocation simplicity**  
  
Where contest policy allows it, revoking delegation must be simple, visible, and reversible until the applicable deadline.  
  
A citizen must never feel “trapped” by having delegated earlier.  
  
**14.6 Coercion-aware and privacy-safe UX**  
  
The system must assume that some users participate under observation or pressure.  
  
**14.6.1 Safe-exit behavior**  
  
The platform must support:  
	•	immediate neutral exit,  
	•	suppression of vote-choice remnants in local UI state,  
	•	non-revealing return screens,  
	•	no visible confirmation pages that expose sensitive choice to a shoulder-surfer.  
  
**14.6.2 Verification without coercion artifacts**  
  
Verification flows must be:  
	•	short-lived,  
	•	difficult to repurpose as proof of vote choice,  
	•	understandable to ordinary users,  
	•	visually distinct from durable receipts.  
  
**14.6.3 Privacy-preserving notifications**  
  
Reminders and status messages must never reveal:  
	•	issue choice,  
	•	delegate choice,  
	•	prior vote direction,  
	•	protected participation state on a lock screen or casual glance surface.  
  
**14.6.4 Environment-sensitive guidance**  
  
The platform should provide safety guidance such as:  
	•	use a private space when possible,  
	•	supervised access is available,  
	•	you may be able to revise your participation under contest policy,  
	•	helper mode should only be used when you trust the helper.  
  
This guidance must remain neutral and non-alarmist.  
  
**14.7 Assisted and supervised participation UX**  
  
Accessibility is not only digital; it also includes safe assisted access.  
  
**14.7.1 Trusted helper mode**  
  
The platform may provide a helper-assisted flow for citizens who need support, but it must include:  
	•	strict role boundaries,  
	•	visible indication when helper mode is active,  
	•	prevention of silent helper takeover,  
	•	limited helper permissions,  
	•	strong auditability,  
	•	clear privacy warnings.  
  
Helper mode must not become an unlogged avenue for coercion or fraud.  
  
**14.7.2 Supervised access points**  
  
For supervised municipal, consular, or civic access points, the UX must support:  
	•	queue-safe privacy,  
	•	rapid user handoff,  
	•	assisted accessibility setup,  
	•	controlled session reset,  
	•	neutral terminal state between users,  
	•	clear distinction between staff assistance and political guidance.  
  
**14.7.3 Cross-channel continuity**  
  
A user who begins reading remotely and later uses a supervised channel should be able to resume without losing context, while still respecting the security posture of the supervised flow.  
  
**14.8 Accessibility requirements**  
  
Accessibility must be designed as a first-class product requirement and validated through user testing, not treated as a post-build compliance pass.  
  
**14.8.1 Baseline capabilities**  
  
The platform must support:  
	•	screen readers,  
	•	keyboard-only navigation,  
	•	high contrast mode,  
	•	scalable text,  
	•	audio guidance,  
	•	captions and transcripts where relevant,  
	•	reduced motion mode,  
	•	touch-target sizing suitable for motor impairments,  
	•	plain-language mode,  
	•	multilingual support,  
	•	low-bandwidth-friendly rendering.  
  
**14.8.2 Cognitive accessibility**  
  
The platform must support:  
	•	simplified summaries,  
	•	short sentences and clear labels,  
	•	consistent navigation,  
	•	progress indicators,  
	•	minimal context switching,  
	•	glossary support for legal and civic terms,  
	•	“read this later” and staged review flows.  
  
**14.8.3 Language accessibility**  
  
For multilingual contexts, the platform must clearly distinguish:  
	•	authoritative legal text,  
	•	plain-language explanation,  
	•	translated explanation,  
	•	AI-assisted summary if used.  
  
Users must not confuse a convenience summary with the legally operative text.  
  
**14.9 Verification and evidence UX**  
  
Not every citizen will inspect proofs, but the platform should not hide evidence behind expert-only doors.  
  
**14.9.1 Layered verification experience**  
  
Verification should be presented in layers:  
	•	citizen-level confirmation,  
	•	observer-level artifact inspection,  
	•	expert-level verifier and reproducibility package.  
  
**14.9.2 Evidence discoverability**  
  
Every contest should expose:  
	•	current lifecycle state,  
	•	whether results are preliminary or certified,  
	•	whether challenges are open,  
	•	where official evidence can be inspected,  
	•	what independent verifiers are available.  
  
**14.9.3 Explainable trust**  
  
The UX should explain system trust in human terms, for example:  
	•	who checked eligibility,  
	•	who cannot see the vote,  
	•	who can audit the result,  
	•	why certification is separate from counting.  
  
The goal is not to teach cryptography, but to make institutional security legible.  
  
**14.10 Notification and communication policy**  
  
Platform communication must be civic, neutral, and non-manipulative.  
  
Notifications may be used for:  
	•	deadlines,  
	•	contest publication,  
	•	challenge windows,  
	•	delegate disclosure updates,  
	•	system incidents,  
	•	availability of supervised access,  
	•	publication of certified results.  
  
Notifications must not:  
	•	optimize for engagement,  
	•	rank political urgency opaquely,  
	•	nudge users toward a side,  
	•	expose sensitive participation state on insecure surfaces.  
  
**14.11 Failure and degraded-mode UX**  
  
Users must not experience failures as silent disappearance.  
  
When material issues occur, the platform must present:  
	•	plain-language incident status,  
	•	effect on the user’s next steps,  
	•	whether voting continues, pauses, or is restricted,  
	•	whether supervised fallback is available,  
	•	where official incident records are published.  
  
This is critical for legitimacy. Confusing failure UX is politically toxic.  
  
**14.12 UX acceptance criteria**  
  
The UX and accessibility layer is acceptable only if testing shows that representative users can reliably:  
	•	understand what kind of contest they are in,  
	•	distinguish reading, delegating, voting, abstaining, and verifying,  
	•	find the strongest case for and against,  
	•	understand whether delegation is active and reversible,  
	•	complete protected participation without accidental disclosure,  
	•	use accessibility modes successfully,  
	•	navigate supervised or helper-assisted flows safely,  
	•	interpret result state and challenge state correctly,  
	•	recover from non-critical interruption without confusion.  
  
Testing must include:  
	•	low-literacy users,  
	•	elderly users,  
	•	disability users,  
	•	diaspora users,  
	•	proxy-heavy users,  
	•	first-time participants,  
	•	and users operating under time pressure.  
  
**14.13 UX as a legitimacy requirement**  
  
A civic platform of this kind does not earn trust only through cryptography, auditability, and law. It also earns trust through:  
	•	clarity,  
	•	neutrality,  
	•	predictability,  
	•	accessibility,  
	•	and the felt experience that the system is not trying to trick, rush, shame, or overwhelm the citizen.  
  
For this reason, UX and accessibility are part of the platform’s democratic legitimacy, not merely part of its interface design.  
  
  
  
## 15. Security architecture  
  
**15.1 Purpose**  
  
The security architecture defines how the platform is secured as a **system of institutions, services, trust boundaries, and operational controls**.  
  
It exists to ensure that the platform can meet the PRD goals for:  
	•	secure participation,  
	•	citizen anonymity where required,  
	•	public verifiability,  
	•	coercion mitigation,  
	•	manipulation resistance,  
	•	operational resilience,  
	•	institutional non-capture,  
	•	crypto agility,  
	•	and staged deployment of higher-assurance use cases.  
  
The security architecture does **not** define low-level protocol mechanics.  
Those are specified in the **Cryptographic Protocol Appendix**.  
  
**15.2 Architectural stance**  
  
The platform uses a **split-trust architecture**.  
  
Security is not derived from one trusted application, one ministry, one operator, or one cryptographic trick. It is derived from:  
	•	separation of powers across system domains,  
	•	constrained interfaces between domains,  
	•	public evidence and auditability,  
	•	threshold control over sensitive actions,  
	•	open verifiability,  
	•	and gradual rollout by assurance tier.  
  
The architecture assumes that some components may fail, some actors may become malicious, some endpoints may be compromised, and some channels may be unavailable. The system must remain inspectable and governable under those conditions.  
  
**15.3 Security objectives**  
  
At the architectural level, the platform must satisfy these objectives.  
  
**15.3.1 Identity and ballot separation**  
  
No single domain should both know who the citizen is and control or interpret the citizen’s effective ballot.  
  
**15.3.2 Secrecy where required**  
  
Where a contest requires secret ballot, the architecture must preserve that property across identity, casting, storage, tally, publication, and audit.  
  
**15.3.3 Publicly checkable correctness**  
  
The system must produce sufficient public evidence for independent parties to check that the declared result matches the accepted inputs and the approved process.  
  
**15.3.4 Controlled delegation**  
  
Proxy voting must be secure, bounded, auditable, and reversible by the citizen, without exposing delegators publicly.  
  
**15.3.5 No silent failure paths**  
  
Critical failures must surface through declared incident, pause, downgrade, extension, or refusal-to-certify states. The architecture must not contain hidden emergency backdoors.  
  
**15.3.6 Cryptographic continuity**  
  
The platform must be secure under current standards, upgradeable under future standards, and governable during cryptographic transitions.  
  
**15.3.7 Constitutional resilience**  
  
No single operator, vendor, authority, or technical subsystem should be able to subvert a contest without leaving detectable evidence or requiring collusion across trust boundaries.  
  
**15.4 Architectural layers**  
  
The platform is organized into four security layers.  
  
**15.4.1 Civic governance layer**  
  
This layer defines who is authorized to do what, who oversees whom, how certification works, who can challenge outcomes, and how incidents are escalated.  
  
This layer is about institutional trust, not cryptography.  
  
**15.4.2 Identity and authorization layer**  
  
This layer determines whether a person may participate in a given contest, while minimizing what downstream domains learn about that person.  
  
This layer is responsible for access legitimacy, not ballot interpretation.  
  
**15.4.3 Participation and privacy layer**  
  
This layer protects the citizen-facing act of delegation or direct voting and preserves anonymity or confidentiality according to contest policy.  
  
This is where the privacy core lives, but the protocol details are delegated to the appendix.  
  
**15.4.4 Evidence and certification layer**  
  
This layer turns system activity into verifiable public evidence, supports observer replay, manages challenges, and determines whether the contest can be legally certified.  
  
This is the layer that converts technical process into public legitimacy.  
  
**15.5 Security domains**  
  
The architecture separates the platform into distinct security domains. Each domain has a narrow security role and constrained knowledge.  
  
**15.5.1 Identity domain**  
  
Responsible for authenticating the person and establishing secure access.  
  
**Security role**  
	•	confirm that the participant is the person they claim to be,  
	•	support recovery under controlled policy,  
	•	establish high-assurance sessions.  
  
**Security constraint**  
	•	must not participate in ballot interpretation or tally decisions.  
  
**15.5.2 Eligibility domain**  
  
Responsible for contest-specific eligibility decisions.  
  
**Security role**  
	•	determine whether the authenticated person may participate in the contest,  
	•	enforce one participation right per eligible person,  
	•	support legally auditable inclusion and exclusion decisions.  
  
**Security constraint**  
	•	must not learn or influence the citizen’s political choice.  
  
**15.5.3 Contest and policy domain**  
  
Responsible for the authoritative contest manifest and all security-relevant contest parameters.  
  
**Security role**  
	•	define the authoritative contest policy consumed by all operational domains,  
	•	bind jurisdiction, electorate, secrecy class, delegation policy, assurance tier, certification path, and cryptographic suite selection,  
	•	ensure that all services resolve contest rules from one signed source of truth,  
	•	provide traceability for contest-rule changes.  
  
**Security constraint**  
	•	must not authenticate citizens,  
	•	must not handle direct ballot content,  
	•	must not certify results,  
	•	must not permit silent policy mutation during an active contest.  
  
**15.5.4 Privacy domain**  
  
Responsible for transforming eligibility into privacy-preserving participation.  
  
**Security role**  
	•	support anonymous or unlinkable participation,  
	•	prevent unauthorized duplication,  
	•	preserve separation between personhood and ballot-side activity.  
  
**Security constraint**  
	•	must not become a hidden identity-to-ballot map.  
  
**15.5.5 Delegation domain**  
  
Responsible for secure handling of proxy relationships.  
  
**Security role**  
	•	maintain valid delegation state,  
	•	enforce caps and policy rules,  
	•	support direct override,  
	•	support auditable and reproducible proxy resolution.  
  
**Security constraint**  
	•	must not expose delegator identities publicly,  
	•	must not control ballot secrecy.  
  
**15.5.6 Ballot-processing domain**  
  
Responsible for protected intake of direct votes and related participation artifacts.  
  
**Security role**  
	•	validate submissions,  
	•	enforce timing and replay rules,  
	•	ensure only valid inputs are admitted into the public evidence trail.  
  
**Security constraint**  
	•	must not know legal identity,  
	•	must not certify results.  
  
**15.5.7 Information and deliberation domain**  
  
Responsible for official issue presentation, source provenance, structured public reasoning, moderation, and logged AI-assisted summarization.  
  
**Security role**  
	•	protect informational integrity,  
	•	ensure provenance of official summaries and dossier materials,  
	•	maintain visible versioning of issue explanations,  
	•	prevent hidden persuasion logic from entering the civic workflow,  
	•	ensure moderation and AI usage remain reviewable and policy-bound.  
  
**Security constraint**  
	•	must not silently alter legal meaning,  
	•	must not rank or target political content using hidden engagement logic,  
	•	must not modify contest rules, accepted ballots, tally inputs, or certification state,  
	•	must not become an alternate certification path.  
  
**15.5.8 Public evidence domain**  
  
Responsible for append-only publication of contest artifacts, checkpoints, proofs, challenge states, and certification records.  
  
**Security role**  
	•	provide durable public evidence,  
	•	support mirroring and independent inspection,  
	•	make tampering or suppression visible.  
  
**Security constraint**  
	•	must not contain undisclosed private identity data.  
  
**15.5.9 Tally domain**  
  
Responsible for protected result computation under multi-party control.  
  
**Security role**  
	•	execute the approved tally path,  
	•	operate only under threshold or quorum conditions,  
	•	produce evidence needed for independent checking.  
  
**Security constraint**  
	•	must not operate as a unilateral authority,  
	•	must not be allowed to bypass certification and challenge handling.  
  
**15.5.10 Certification domain**  
  
Responsible for turning a technically completed contest into a legally valid result.  
  
**Security role**  
	•	validate completeness of evidence,  
	•	verify that procedural prerequisites are satisfied,  
	•	refuse certification if critical conditions fail.  
  
**Security constraint**  
	•	must not alter contest history or recalculate hidden results.  
  
**15.5.11 Oversight domain**  
  
Responsible for public-interest oversight, audit, challenge, and review.  
  
**Security role**  
	•	inspect,  
	•	verify,  
	•	challenge,  
	•	observe,  
	•	reproduce.  
  
**Security constraint**  
	•	must be powerful enough to detect abuse, but not able to mutate operational state.  
  
**15.6 Trust-boundary design**  
  
The platform is built on explicit trust boundaries.  
  
**15.6.1 Functional separation**  
  
Identity, eligibility, privacy, delegation, ballot intake, tally, and certification are separate functional domains.  
  
**15.6.2 Institutional separation**  
  
Sensitive domains should be operated by different institutional actors or governance bodies wherever possible.  
  
**15.6.3 Cryptographic separation**  
  
Different key hierarchies are used for different security purposes. Long-lived roots, contest operations, publication integrity, recovery, and certification must not collapse into one signing authority.  
  
**15.6.4 Data separation**  
  
Logs, credentials, delegation data, accepted ballot artifacts, proofs, and certification records should not be co-resident in a way that creates an unnecessary correlation surface.  
  
**15.6.5 Legal separation**  
  
The architecture assumes that some separations are enforced not only technically but also legally and procedurally.  
  
**15.7 Assurance model**  
  
The platform uses **assurance-tiered security**, not one uniform model for every decision.  
  
**15.7.1 Lower-assurance civic acts**  
  
For petitions, initiatives, and consultative use cases, the architecture prioritizes accessibility, broad participation, and strong public evidence, while accepting more remote-channel risk.  
  
**15.7.2 Mixed-assurance local binding decisions**  
  
For local binding decisions, the architecture combines remote participation with supervised or assisted access paths and tighter operational controls.  
  
**15.7.3 High-assurance binding decisions**  
  
For the highest-stakes uses, the architecture prioritizes contest integrity, coercion mitigation, public legitimacy, and supervised fallback over pure convenience.  
  
This means the architecture can support different operational policies per tier without changing the constitutional logic of the platform.  
  
**15.8 Control families**  
  
The security architecture is organized into the following control families.  
  
**15.8.1 Identity and access controls**  
  
These protect enrollment, authentication, session establishment, step-up actions, and recovery.  
  
**15.8.2 Authorization and uniqueness controls**  
  
These ensure that only eligible people participate and that each person gets only the allowed effective participation right per contest.  
  
**15.8.3 Privacy and unlinkability controls**  
  
These minimize identity leakage into downstream participation and voting flows.  
  
**15.8.4 Delegation integrity controls**  
  
These secure proxy creation, revocation, cap enforcement, resolution reproducibility, and citizen override.  
  
**15.8.5 Ballot integrity controls**  
  
These ensure that accepted direct votes are valid, ordered, and governed by declared contest policy.  
  
**15.8.6 Transparency and evidence controls**  
  
These ensure that public artifacts are published in a durable, append-only, independently inspectable form.  
  
**15.8.7 Tally and certification controls**  
  
These ensure that results are produced only under approved conditions and never silently certified after unresolved critical failure.  
  
**15.8.8 Cryptographic lifecycle controls**  
  
These govern key generation, key custody, suite registration, algorithm rotation, deprecation, compromise response, and archival integrity.  
  
**15.8.9 Operational resilience controls**  
  
These cover outage handling, failover, downgrade paths, public incident declaration, restoration, and continuity of evidence.  
  
**15.8.10 Oversight and challenge controls**  
  
These ensure that auditors, observers, and citizens can inspect, verify, and challenge the system in a structured way.  
  
**15.9 Cryptographic architecture posture**  
  
This section stays high level by design.  
  
**15.9.1 Quantum-safe baseline**  
  
The architecture requires a **post-quantum-safe control plane from day one** for platform-owned cryptographic control surfaces.  
  
**15.9.2 Crypto-agile privacy core**  
  
The architecture treats the privacy-preserving voting core as a replaceable subsystem behind stable interfaces, because the PQ standardization and operational maturity of the full anonymous-voting stack is not yet on the same footing as KEMs and signatures.  
  
**15.9.3 Contest-pinned suites**  
  
Every contest must run under an explicitly declared cryptographic profile. Cryptographic posture may evolve between contests, but not invisibly within one.  
  
**15.9.4 Public cryptographic governance**  
  
Cryptographic transitions are governance events, not hidden engineering changes. They require public policy, observable versioning, and independent verifier support.  
  
The detailed mechanism is in the protocol appendix.  
  
**15.10 Client and endpoint posture**  
  
The architecture assumes personal devices are not fully trustworthy.  
  
Therefore:  
	•	remote participation is allowed where assurance policy permits,  
	•	public verifiability must compensate for endpoint uncertainty,  
	•	revoting and supervised override remain core mitigations,  
	•	the highest-assurance use cases should not depend solely on arbitrary personal devices,  
	•	user verification must avoid turning into a coercion artifact.  
  
This is a system posture, not a protocol detail.  
  
**15.11 Delegation security posture**  
  
Delegation is treated as a first-class security and governance concern.  
  
The architecture requires:  
	•	public delegate identity and accountability,  
	•	private delegator identity,  
	•	bounded accumulation of delegated influence,  
	•	reproducible resolution of proxy state,  
	•	direct citizen override,  
	•	policy-configurable treatment of transitivity,  
	•	anomaly monitoring for concentration and coordinated capture.  
  
Exactly how this is encoded belongs in the protocol appendix. The architecture here defines the control intent and governance stance.  
  
**15.12 Evidence architecture**  
  
The platform is built around the principle that **trust comes from inspectable evidence**.  
  
The evidence architecture must provide:  
	•	public contest manifests,  
	•	append-only publication of accepted public artifacts,  
	•	signed checkpoints,  
	•	proof bundles,  
	•	software and build provenance,  
	•	certification records,  
	•	incident markers,  
	•	challenge records,  
	•	reproducibility packages.  
  
This evidence must be sufficient for independent observers to reconstruct whether the official result is consistent with the published process.  
  
**15.13 Audit architecture**  
  
The system maintains a structured audit architecture across all critical services.  
  
At a high level, the audit system must provide:  
	•	signed event emission,  
	•	append-only chaining,  
	•	role attribution,  
	•	object scoping,  
	•	public or auditor-visible schemas,  
	•	defined retention and destruction policies,  
	•	independent reviewability.  
  
The audit architecture is not just an admin log. It is part of the public-assurance model.  
  
**15.14 Certification architecture**  
  
Certification is a separate security domain because the act of saying “this result is legally valid” is not the same as computing a result.  
  
The architecture requires:  
	•	separation between tally and certification,  
	•	visible certification preconditions,  
	•	refusal paths when conditions fail,  
	•	signed certification artifacts,  
	•	public linkage between result, evidence, incidents, and certification state.  
  
No result should become official merely because a computation ran.  
  
**15.15 Retention and destruction posture**  
  
The architecture follows a minimization principle:  
  
retain enough to verify, challenge, and legally defend the contest; retain nothing unnecessary that could later increase de-anonymization or coercion risk.  
  
Therefore:  
	•	different domains retain different categories of data,  
	•	identity-side data and participation-side data remain separated,  
	•	superseded or no-longer-needed artifacts are destroyed or cryptographically shredded according to policy,  
	•	destruction is itself auditable.  
  
Detailed lifecycle rules belong in the appendix and operational manual.  
  
**15.16 Incident and failure architecture**  
  
The platform must fail visibly, not silently.  
  
The architecture requires defined states for:  
	•	degraded operation,  
	•	contest pause,  
	•	extension,  
	•	supervised-only downgrade,  
	•	unresolved contest,  
	•	refusal to certify,  
	•	recovery after compromise.  
  
Every material incident must trigger:  
	•	signed incident recording,  
	•	public classification where appropriate,  
	•	routing to oversight,  
	•	effect on contest state,  
	•	eventual public disposition.  
  
**15.17 Threat posture**  
  
The architecture is primarily designed against:  
	•	state capture and insider manipulation,  
	•	foreign interference,  
	•	party and oligarch capture,  
	•	endpoint compromise,  
	•	coercion by employers or households,  
	•	vote buying,  
	•	misinformation and influence operations,  
	•	denial of service,  
	•	delegation cartelization,  
	•	legitimacy collapse through opacity or overload.  
  
Not every threat is solved at the same layer.  
  
Some are mitigated through cryptography.  
Some through process and institutional split.  
Some through interface design.  
Some through supervised access paths.  
Some through transparency and public challengeability.  
  
That layered treatment is intentional.  
  
**15.18 Legitimacy architecture**  
  
Security alone is not enough. The platform must also be publicly believable.  
  
The legitimacy architecture therefore requires:  
	•	open source for critical components,  
	•	independent domestic audit,  
	•	external scrutiny,  
	•	public proofs and reproducibility materials,  
	•	public ceremonies,  
	•	sortition-based citizen oversight,  
	•	structured challenge rights,  
	•	stable public records of incidents and resolutions.  
  
A system that is technically secure but socially opaque is not sufficient for this use case.  
  
**15.19 Relationship to protocol appendix**  
  
This section defines the **high-level architecture and security posture**.  
  
The **Cryptographic Protocol Appendix** defines:  
	•	protocol entities,  
	•	data objects,  
	•	issuance semantics,  
	•	delegation semantics,  
	•	direct-vote override semantics,  
	•	revote semantics,  
	•	tally semantics,  
	•	verification semantics,  
	•	retention and destruction rules,  
	•	failure handling logic,  
	•	acceptance tests.  
  
If there is ever tension between a generic high-level statement in this section and a precise technical rule in the appendix, the appendix governs the protocol behavior.  
  
**15.20 Architectural acceptance criteria**  
  
The security architecture is acceptable only if all of the following are true:  
	•	no single domain can authenticate the person, interpret the ballot, and certify the result,  
	•	secret-ballot use cases remain protected across domain boundaries,  
	•	delegation remains bounded, reversible, and publicly accountable,  
	•	public evidence is sufficient for independent verification,  
	•	critical failures produce visible governance states rather than hidden operator workarounds,  
	•	cryptographic transitions are governed and auditable,  
	•	retention and destruction policies preserve both auditability and privacy,  
	•	higher-stakes uses can be restricted to higher-assurance channels without redesigning the platform,  
	•	the architecture remains understandable enough to be governable by institutions and reviewable by independent experts.  
  
  
## 16. Threat model and controls  
  
Comprehensive threat model is described in Constitutional Governance and Threat Model document.  
  
## 17. Operations, certification, and legitimacy  
  
**17.1 Open source**  
  
Core protocols, verifier tools, and critical server-side code are public.  
  
**17.2 Independent audits**  
  
Regular code, protocol, operations, and red-team audits are mandatory.  
  
**17.3 International scrutiny**  
  
The platform supports observation and review by credible outside experts and institutions.  
  
**17.4 Public proofs**  
  
Each contest publishes a complete evidence package.  
  
**17.5 Sortition oversight**  
  
A standing citizen oversight council selected by lot has formal rights to inspect evidence, receive incident briefings, and trigger challenge review.  
  
**17.6 Challenge process**  
  
Any citizen, delegate, auditor, or observer can file a challenge. Every challenge receives a public disposition.  
  
**17.7 Public ceremonies**  
  
Key generation, release signing, archive sealing, and result certification are public or publicly reconstructable.  
  
## 18. Rollout roadmap  
  
**Phase 0: Constitutional and technical foundation**  
  
Deliver:  
- Legal charter  
- Institutional split  
- Contest taxonomy  
- Protocol registry  
- Audit framework  
- Challenge framework  
- Observer tooling  
- Public mock environment  
  
Exit gate:  
* No critical unresolved architectural findings.  
* Public scrutiny period completed.  
* Baseline audit and reproducibility proven.  
  
**Phase 1: Tier 0 and Tier 1**  
  
Deploy:  
	•	initiatives,  
	•	petitions,  
	•	threshold sponsorship,  
	•	consultative votes,  
	•	non-binding delegation.  
  
Exit gate:  
	•	strong uptake,  
	•	no major trust failures,  
	•	independent verification tooling used in the wild.  
  
**Phase 2: Tier 2 local binding**  
  
Deploy:  
	•	participatory budgeting,  
	•	local governance questions,  
	•	supervised municipal access points,  
	•	delegate disclosures and caps.  
  
Exit gate:  
	•	repeated successful audits,  
	•	coercion-complaint analysis,  
	•	local legitimacy acceptance.  
  
**Phase 3: National consultative shadow chamber**  
  
Deploy:  
	•	national consultative issue voting,  
	•	proxy ecosystem at scale,  
	•	constitutional review rehearsal,  
	•	large-scale observer and verifier use.  
  
Exit gate:  
	•	sustained public scrutiny,  
	•	mature challenge handling,  
	•	stable operational evidence.  
  
**Phase 4: Limited high-stakes binding deployment**  
  
Deploy:  
	•	selected binding national use cases,  
	•	supervised channels as default,  
	•	full evidence publication,  
	•	formal certification and public challenge cycles.  
  
Exit gate:  
	•	repeated successful audits,  
	•	legal confidence,  
	•	no severe unresolved protocol risks.  
  
**Phase 5: Advanced crypto migration**  
  
Introduce:  
	•	upgraded suites,  
	•	hybrid or post-quantum components where mature,  
	•	stronger identity and credential modules as standards and public review justify.  
  
Exit gate:  
	•	full public approval for the relevant privacy-core upgrades,  
	•	successful migration drills,  
	•	no loss of public verifiability.  
  
**19. Acceptance criteria**  
  
A contest class is production-ready only if all are true:  
	•	no single institution can both identify voters and alter the result undetectably,  
	•	direct vote overrides proxy reliably,  
	•	public verifiers can independently validate the result package,  
	•	revoting and override logic work as specified,  
	•	small-electorate secrecy rules are enforced,  
	•	accessibility testing passes,  
	•	red-team findings above threshold are resolved,  
	•	challenge workflows are live and exercised,  
	•	supply-chain reproducibility is demonstrated,  
	•	incident response drills have been performed.  
  
**20. Feasibility assessment**  
  
**Feasible now**  
	•	petitions and agenda-setting,  
	•	consultative voting,  
	•	participatory budgeting,  
	•	local decisions with mixed remote and supervised channels,  
	•	proxy voting with direct override,  
	•	public delegate ecosystems,  
	•	open-source verifier tooling,  
	•	strong audits, public logs, and challenge workflows,  
	•	crypto-agile architecture with staged PQ-hardening.  
  
**Feasible with discipline**  
	•	binding local decisions at meaningful scale,  
	•	national consultative shadow-chamber behavior,  
	•	private delegators plus public delegates,  
	•	high-legitimacy public evidence bundles,  
	•	supervised high-stakes channels for selected binding acts,  
	•	protocol-governed privacy cores with public approval.  
  
**Not honestly solved today**  
	•	fully remote, personal-device, national binding legislation with strong coercion resistance, strong client integrity, and broad social legitimacy,  
	•	large-scale proxy democracy without ongoing pressure toward cartelization,  
	•	a mature drop-in post-quantum privacy-preserving voting stack for the full ballot-anonymity and tally-proof path.  
  
**21. Major unresolved engineering and governance risks**  
	•	PQ anonymous credentials for national-scale unlinkable participation,  
	•	PQ-ready tally and proof systems with mature public review,  
	•	migration of the state eID ecosystem itself,  
	•	preserving meaningful secrecy in very small electorates,  
	•	preventing delegate ecosystems from becoming shadow parties,  
	•	maintaining legitimacy when cryptographic complexity exceeds ordinary public understanding,  
	•	keeping deliberation structured without drifting into censorship or paternalism.  
  
**22. Candid product conclusion**  
  
This system is realistic as a staged civic operating system. It is not realistic as a one-shot “national direct democracy app.”  
  
The right merge between ambition and honesty is:  
	•	build the institutional split first,  
	•	launch low-risk civic acts first,  
	•	make proxy voting accountable and reversible,  
	•	treat public auditability as mandatory,  
	•	keep the highest-stakes uses on the highest-assurance channels,  
	•	and move the ballot privacy core toward full PQ assurance only as standards, audits, and public legitimacy actually justify it.  
