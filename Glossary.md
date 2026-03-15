# Glossary  
  
  
This glossary defines terms as they are used in the proposed direct-participation and proxy-voting system.  
Where a term has a broader legal, political, or cryptographic meaning, the definition below reflects the **system-specific** meaning intended for this design.  
  
**A**  
  
**Accessibility parity**  
The principle that people with disabilities, low digital literacy, poor connectivity, or constrained physical access should have a practical ability to participate that is not materially worse than that of other citizens.  
  
**Admissibility review**  
A legal and procedural check performed before a proposal can go to vote. It verifies that the proposal is properly formed, understandable, within the allowed scope, and not clearly unconstitutional.  
  
**Agenda integrity**  
The property that no actor or coalition can secretly dominate, flood, suppress, or manipulate which questions are brought to citizens for decision.  
  
**Agenda setting**  
The process by which proposals, initiatives, or measures are introduced into the system so they can be reviewed, discussed, and possibly voted on.  
  
**Anonymity set**  
The size of the group within which an individual voter’s choice can plausibly be hidden. If the group is too small, secrecy may be weak in practice even if the cryptography is strong.  
  
**Audit trail**  
The evidence left by system actions, procedures, and decisions so that auditors can later verify what happened.  
  
⸻  
  
**B**  
  
**Ballot**  
A voter’s formal expression of choice in a given vote. In this system, a ballot may be cast directly by a citizen or resolved through delegation, depending on the rules of the vote.  
  
**Ballot certification**  
The formal process of confirming that a vote’s result package is valid, the procedures were followed, and the tally can be accepted as official.  
  
**Ballot secrecy**  
The requirement that no one should be able to determine how a specific citizen voted in vote types that are meant to be secret.  
  
**Ballot tally / tally**  
The process of counting valid ballots and producing the final outcome.  
  
**Binding vote**  
A vote whose result has direct legal or institutional effect, rather than serving only as advice or public signal.  
  
**Bulletin board (public bulletin board)**  
A public, append-only record where election artifacts are posted so observers and auditors can independently check that the process was followed and the result can be verified.  
  
⸻  
  
**C**  
  
**Cast-as-intended**  
A verification property meaning the system correctly captured the voter’s intended choice.  
  
**Certification authority**  
The institution that formally validates the result package after tally, checks that required procedures were followed, and issues the official certification.  
  
**Challenge window**  
A defined period after voting during which citizens, observers, auditors, or authorized bodies may dispute the conduct or result of the vote.  
  
**Citizen assembly**  
A structured body of ordinary citizens, often selected by lot, that studies an issue and produces a summary or recommendation to help the wider public understand it.  
  
**Civic participation platform**  
The broader system that supports initiatives, deliberation, proxy voting, direct voting, participatory budgeting, and other democratic functions. It is more than just a voting app.  
  
**Civic qualification**  
A low-stakes participation layer used for acts like petition signing, initiative support, or agenda sponsorship, where the goal is to show verified civic support rather than to conduct a full binding vote.  
  
**Coercion resistance**  
The degree to which the system makes it hard for others to force, pressure, bribe, or verify how a citizen voted.  
  
**Collusion threshold**  
The number or combination of institutions that would need to secretly cooperate in order to violate a core property such as ballot secrecy or result integrity.  
  
**Community decision**  
A vote about local matters such as neighborhood projects, municipal priorities, or other decisions affecting a defined local population.  
  
**Concentration cap**  
A hard limit on how much delegated voting power any one delegate may accumulate.  
  
**Constitutional review gate**  
The legal body or process that determines whether a proposal may go to vote and whether an adopted measure is constitutionally valid.  
  
**Consultative civic voting**  
Voting used to measure citizen opinion or priorities without directly creating binding law. It is politically meaningful, but not self-executing.  
  
**Contest**  
A single voting event or decision process on one defined question or proposal. In ordinary language, this is basically “the vote” on a particular issue.  
  
**Contest class**  
A category of vote defined by its risk and legal effect, such as consultative, local binding, or national binding.  
  
**Contest fallback**  
The predefined safer mode the system switches to if normal operation becomes insecure, illegitimate, or unavailable. Example: downgrading from remote voting to supervised voting.  
  
**Contest intelligibility**  
The requirement that a vote must be explained clearly enough that ordinary citizens can understand what is being decided and what the consequences are.  
  
**Cryptographic proof**  
Mathematical evidence published by the system to show that certain steps, such as counting or shuffling votes, were performed correctly.  
  
**Crypto agility**  
The ability to replace or upgrade cryptographic algorithms without redesigning the whole system.  
  
⸻  
  
**D**  
  
**Delegate**  
A person chosen by citizens to exercise proxy voting power on their behalf for some domain or issue.  
  
**Delegate cartelization**  
A failure mode in which a few delegates accumulate excessive power and begin functioning like an opaque shadow elite or party machine.  
  
**Delegation**  
The act of allowing another person to vote on your behalf under the system’s proxy rules.  
  
**Deliberation**  
The structured process by which citizens, experts, and delegates examine arguments, evidence, impacts, and tradeoffs before voting.  
  
**Direct override**  
The rule that a citizen’s own direct vote always takes precedence over any delegated vote for that same contest.  
  
**Direct participation**  
Citizens voting on issues themselves rather than only electing representatives who vote for them.  
  
**Domain delegation**  
Delegating your vote for a broad policy area, such as health, education, transport, or housing.  
  
⸻  
  
**E**  
  
**eID (electronic identity)**  
A state-backed digital identity system used to prove that a person is who they claim to be. In this design, eID is the main basis for voter authentication.  
  
**Eligibility**  
The legal status of being entitled to participate in a specific vote.  
  
**Eligibility authority**  
The body that determines whether a citizen is entitled to take part in a given contest.  
  
**End-to-end verifiability**  
A family of properties that allow voters and observers to verify that votes were captured correctly, included correctly, and counted correctly without relying purely on trust.  
  
⸻  
  
**F**  
  
**Fail-safe mode**  
A safer operating mode entered when normal operation cannot be trusted. The point is not to keep everything running at any cost, but to preserve legitimacy under stress.  
  
**Fallback**  
A backup path used when the preferred path cannot safely continue.  
  
**Fiscal note**  
A structured explanation of the expected financial consequences of a proposal.  
  
⸻  
  
**H**  
  
**High-assurance channel**  
A voting channel with stronger security and operational controls than ordinary remote use, typically involving audited devices, stronger supervision, or controlled environments.  
  
**Homomorphic tally**  
A way of counting encrypted votes without first decrypting every individual vote. It allows a final result to be produced while preserving secrecy of individual ballots.  
  
⸻  
  
**I**  
  
**Implementation fidelity**  
The principle that if a measure passes validly, the responsible institutions must carry it out faithfully rather than undermining it through delay, reinterpretation, or symbolic compliance.  
  
**Implementation tracker**  
A public record showing whether and how a passed measure is being put into effect.  
  
**Initiative**  
A proposal introduced by citizens or institutions to be considered for possible vote.  
  
**Issue**  
A policy question, proposal, or measure presented for review and possible vote.  
  
**Issue dossier**  
The standard package of information attached to each issue. It typically includes a plain-language explanation, legal text, impact analysis, arguments for and against, and supporting materials.  
  
**Issue-specific delegation**  
Delegation that applies only to one particular vote, not to a whole policy area.  
  
⸻  
  
**K**  
  
**K-anonymity threshold**  
A privacy rule requiring that published results or data only be released when an individual’s choice is hidden among at least a minimum number of similar participants.  
  
⸻  
  
**L**  
  
**Liquid delegation / liquid democracy**  
A model in which citizens may vote directly or delegate their vote to someone else, often by issue or domain, with the ability to reclaim that vote later.  
  
⸻  
  
**M**  
  
**Manipulation resistance**  
The degree to which the system resists distortion by propaganda, platform gaming, coercive framing, artificial amplification, hidden ranking, or organized influence operations.  
  
**Mix-and-decrypt**  
A counting approach where encrypted votes are first shuffled to break any link to voters and then decrypted for tallying.  
  
**Mixnet / mix network**  
The cryptographic machinery used to shuffle encrypted votes so they cannot be linked back to the order in which they were cast.  
  
⸻  
  
**N**  
  
**Non-binding issue sensing**  
A lightweight form of civic voting used to understand public priorities or sentiment without creating a legally binding outcome.  
  
⸻  
  
**O**  
  
**Observer**  
An independent party, domestic or international, allowed to inspect and review the process.  
  
**Outcome package / result package**  
The official bundle of published materials for a completed vote, including totals, proofs, certification, and supporting evidence.  
  
⸻  
  
**P**  
  
**Participatory budgeting**  
A process in which citizens directly decide how a defined portion of public money will be spent, usually on local projects.  
  
**Plain-language summary**  
A non-technical explanation of what a proposal does, meant for ordinary citizens rather than legal or technical specialists.  
  
**Post-quantum cryptography / quantum-safe cryptography**  
Cryptographic methods intended to remain secure even against attackers who possess large-scale quantum computers. In this project, it is a non-negotiable requirement.  
  
**Privacy authority**  
The body or subsystem responsible for helping ensure that voter identity is separated from the vote itself.  
  
**Proof package**  
The full set of cryptographic and procedural evidence published so auditors and observers can verify that the result is legitimate.  
  
**Proxy**  
A delegated voting relationship in which one person is allowed to vote on behalf of another according to the system’s rules.  
  
**Proxy voting**  
Voting through a delegate rather than casting your own direct vote.  
  
⸻  
  
**Q**  
  
**Quantum-safe baseline**  
The minimum cryptographic standard the system is required to meet in order to be considered resistant to future quantum-capable attackers.  
  
⸻  
  
**R**  
  
**Recorded-as-cast**  
A verification property meaning the vote stored by the system matches the vote the citizen actually cast.  
  
**Residual risk**  
The amount of risk that remains after all reasonable controls have been applied.  
  
**Revocation**  
Cancelling an earlier delegation or earlier vote, subject to the rules of the contest.  
  
**Revoting**  
Casting a new vote during the allowed voting period so that the newer valid vote replaces the earlier one.  
  
⸻  
  
**S**  
  
**Secret ballot**  
A vote in which the system is designed to prevent others from learning the voter’s final choice.  
  
**Secrecy class**  
A formal classification specifying whether a given contest must be secret, attributable, or public.  
  
**Small-electorate secrecy problem**  
The problem that ballot secrecy can become weak in very small groups even if the technical system itself is sound.  
  
**Software independence**  
The property that an undetected software error or software attack should not be able to change the result without the problem being detectable through independent evidence.  
  
**Sortition**  
Selection by random draw rather than election or appointment.  
  
**Sortition oversight council**  
A citizen oversight body chosen by lot and given formal rights to observe, question, and challenge aspects of the system.  
  
**Sponsorship**  
Formal support for placing a proposal on the agenda, usually by signing or endorsing it as an eligible citizen.  
  
**Structured submissions**  
Arguments or comments provided in a predefined format rather than as free-form chaotic discussion.  
  
**Supervised voting**  
Voting performed in a controlled environment, such as a municipal site, embassy, consulate, or audited kiosk, rather than entirely from a private personal device.  
  
⸻  
  
**T**  
  
**Tally authority**  
The institution or subsystem that performs the counting process and publishes the evidence needed for verification.  
  
**Threshold cryptography / threshold key custody**  
A method of splitting control of important keys across multiple parties so that no single party can act alone.  
  
**Threat model**  
A structured description of what can go wrong, who might try it, how they might do it, and what controls are needed.  
  
**Transitive delegation**  
A form of delegation in which your delegate may themselves delegate onward, creating a chain.  
  
**Trust domain**  
A part of the system governed by a particular institution or control boundary. Splitting the system into trust domains reduces the danger of any one actor controlling everything.  
  
⸻  
  
**U**  
  
**Universal verifiability**  
The property that the public, not just insiders, can independently verify that the announced result matches the accepted ballots and published evidence.  
  
**Unlinkability**  
The property that participation records and cast votes cannot be connected back to the same person, except under prohibited or highly constrained collusion.  
  
⸻  
  
**V**  
  
**Verification**  
The process of checking that a vote or result was handled correctly.  
  
**Verification token**  
A short-lived artifact that helps a voter confirm a limited property of their vote, such as inclusion or correct recording, without becoming a durable proof usable for coercion or vote buying.  
  
**Voting window**  
The period during which a vote may be cast, changed, or revoked according to the rules.  
  
⸻  
  
**W**  
  
**Well-formed ballot**  
A ballot that satisfies the technical and legal rules of the contest, such as choosing a valid option and being correctly signed or encrypted.  
  
**Workload pacing**  
A rule limiting how many major decisions citizens must handle at the same time, so that the system remains cognitively humane.  
  
⸻  
  
**Suggested short “reader’s guide”**  
  
If this glossary is attached to the main document, I would also add this one-paragraph note at the top of the appendix:  
  
In this project, “contest” means a single vote or decision event, “issue” means the proposal being decided, “ballot” means the citizen’s formal choice, “delegate” means a proxy voter chosen by citizens, “consultative” means politically meaningful but not legally binding, and “supervised” means participation through controlled and audited access points rather than fully private personal-device voting.  
  
If you want, I can now turn this into a **tighter, publication-ready glossary** with only the most essential 25–30 terms, or into a **two-level glossary** with “plain-language” and “technical” definitions side by side.  
