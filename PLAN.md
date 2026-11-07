# Muhar: governance-first build plan

Status: design proposal, 7 November 2026. The initial scope is a low-stakes, single-session computer-based mock exam. This document does not authorize use in a public examination.

## 1. The idea and the honest promise

India's exam-leak problem is a chain of custody and coordination problem. Question authors, bank curators, exam operators, software vendors, centre staff, printers, and investigators all hold different pieces of power. Muhar makes the *rules, draw, release decision, and later corrections* checkable across these boundaries. The legally responsible exam operator still runs the exam and makes incident decisions.

**Promise for v1:** after a mock exam, anyone can check that the operator fixed an eligible question inventory and draw rules before a chosen future randomness round, that the published paper was selected by those rules, and that the recorded history was not silently rewritten. **Limits:** this does not prove the bank was academically sound, that a human did not leak an item, that a centre was physically secure, or that a signed statement about a real-world event was truthful.

This answers the Devcon theme through four lenses:

| Lens | Muhar's concrete contribution |
| --- | --- |
| Governance | A published charter defines who may freeze, approve, release, cancel, audit, and investigate an exam. Every exceptional action has an accountable signer and reason. |
| Real world | Start with a digital mock because printing and transport add separate custody risks. Record centre checks and incidents as evidence, subject to human investigation. |
| Coordination | Operator, bank auditor, independent witnesses, and later release custodians agree on one version of the rules and one visible event history. |
| Decentralisation | Distribute only powers that benefit from it: the key shares, monitoring, and independent verification. Keep legal responsibility with the exam operator. |

Ethereum's distinctive contribution is an independent public anchor for the signed manifest and log checkpoints. A conventional transparency log already supplies the detailed audit trail; the chain helps outsiders detect a later rewrite or different histories shown to different parties. A chain only stores the commitment. It does **not** verify an off-chain incident or keep the underlying log available. The log therefore needs independent monitors and mirrors. [Ethereum's public-sector design guidance](https://publicsector.ethereum.foundation/why-ethereum/) supports keeping confidential data in existing systems while independently verifying selected claims; [transparency logs](https://transparency.dev/articles/logs-a-verifiable-transport-layer/) require inclusion, consistency, and monitoring.

## 2. Why now, and what institutions actually need

The [2024 national exam reform report](https://www.education.gov.in/sites/upload_files/mhrd/files/HLCE_Report.pdf) mentions blockchain audit trails, question-bank controls, encrypted delivery, independent security assessment, and phased pilots. The [October 2026 parliamentary committee release](https://www.pib.gov.in/PressReleseDetailm.aspx?PRID=2321420&lang=1&reg=1) calls for larger question banks, papers set close to the exam, independent security auditing, secure grievances, and attention to the new risks of computer-based testing. These are reasons to test a narrow evidence protocol, not endorsements of Muhar or of a particular blockchain deployment.

The [Public Examinations (Prevention of Unfair Means) Act, 2024](https://www.indiacode.nic.in/bitstream/123456789/20100/1/a2024-01.pdf) expressly covers leaks, unauthorized access, and tampering for the public examinations within its scope; a [2026 amendment received presidential assent](https://www.pib.gov.in/PressReleasePage.aspx?PRID=2298901&lang=2&reg=48). [DoPT's summary of the 2024 Rules](https://persmin.gov.in/DOPT_achievements_2014-2025/InnerFiles/Current_Year_PDF/2025.pdf) describes the official incident-reporting and monitoring mechanisms. Muhar must export evidence into those workflows; it cannot decide legal guilt or replace reporting. A state, university, or private adopter must map its own obligations separately.

## 3. Actors and decision rights

| Actor | What they control | What checks them |
| --- | --- | --- |
| Exam operator | Exam scope, schedule, syllabus, final go/no-go, centre operations, incident response | Signed charter and manifest, external audit, public record, applicable law |
| Bank authors and reviewers | Question content and academic metadata | Compartmentalized access, conflict declarations, duplicate review, audit trail |
| Independent bank auditor | Confidential review of eligibility, blueprint, and duplicate/quality controls | Signed scope and report; cannot alter the bank alone |
| Witnesses/monitors | Copies of log checkpoints and Ethereum anchors; alerts for missing or conflicting records | Public proof and multiple independent observers |
| Release custodians (later phase) | Separate shares or approvals for releasing a selected paper | Different organizations, hardware-protected keys, quorum policy, signed ceremony |
| Centre officials | Device and local custody checks, receipt of release, incident reports | Dual sign-off, external checks, official reporting chain |
| Candidates and public | Verify post-exam evidence and submit concerns | No candidate wallet or public personal-data trail required |
| Muhar maintainers | Public code, protocol, releases | They hold no exam secrets and cannot override an exam decision |

Before a real pilot, the operator and independent participants must sign a short charter specifying the quorum, conflicts of interest, substitution, emergency authority, evidence-retention period, publication schedule, and who can cancel or postpone an exam. A lost keyholder or missed beacon round must have a pre-agreed response; it must not create an invisible override. **After the seed is known, cancellation could be used to retry until a preferred paper appears.** Require an independent quorum, logged incident evidence, a published reason and after-action review; link every replacement to the cancelled session and prohibit silent reuse of the same bank under a new round. The verifier must show the full chain of attempts.

## 4. End-to-end design

```text
private bank + reviewed metadata       signed frozen manifest
                |                               |
         salted commitments  ------> public transparency log
                |                               |
                |                      Ethereum anchor of checkpoint
                |                               |
          future drand round  ------------------+
                |                               |
       deterministic paper draw          monitors copy/check history
                |                               |
         exam-time release                      |
                +------> post-exam proof bundle + independent verifier
```

### 4.1 Prepare and freeze

The operator approves a blueprint with explicit quotas (for example, subject and difficulty) and a reviewed eligible inventory. A canonical, versioned manifest binds the exam/session identifier, **two commitments** (the ordered list of opaque item IDs and eligibility tags; the separately salted question/answer content for each ID), blueprint commitment, selection algorithm version, beacon network identity and **specific future round**, release policy, correction/cancellation policy, and authorized signer keys. The content commitment for each item must bind its ID, canonical question, answer, and random salt to this protocol/session; selected-item proofs must open against the frozen content root. A bare hash of a guessable question can reveal it by dictionary search, so content commitments need independent random salts. The independent bank auditor signs an attestation to this **exact manifest before the beacon round**. The manifest and attestation are published in the log and anchored on Ethereum **with finality and a conservative time buffer before the beacon round**. A late, unfinalized, or altered freeze fails verification. For the mock, publish a 24-hour freeze buffer; tune production timings only after operational tests. [Ethereum's proof-of-stake documentation](https://ethereum.org/developers/docs/consensus-mechanisms/pos/) distinguishes transaction inclusion from finality.

The operator can append a signed amendment before freeze. After freeze, the only permitted path is an explicit signed cancellation/reschedule and a new session identifier, subject to the charter's stricter post-seed quorum. A replacement must never silently inherit the old evidence. A simple immutable registry may enforce one commitment per session, but the verifier must still check finality and the complete off-chain bundle. No question text, answer key, candidate identifier, leaked image, secret, or grievance narrative goes on-chain. [Ethereum's privacy guidance](https://ethereum.org/privacy/ethereum) explains why public-chain data should be treated as visible and persistent.

### 4.2 Draw

After the committed future round, `muhar-draw` verifies the beacon signature and derives a deterministic selection from the committed, ordered eligibility metadata. The algorithm must specify canonical serialization, domain separation, random-byte derivation, unbiased integer sampling, quotas, tie-breaking, and failure behavior when a quota is impossible. Use established cryptographic libraries; do not invent a beacon or cryptographic primitive. The protocol and test vectors must let an independent implementation reproduce identical IDs. [drand's specification](https://docs.drand.love/docs/specification/) describes verifiable randomness rounds.

**Important secrecy limit:** anyone who can read the full bank can learn the selected paper as soon as the public seed arrives. For a live digital exam, schedule the round only after the relevant session's admission gates close and shortly before controlled release. This still leaves insider and in-room communication risks. For multiple shifts or accommodations, design separate session/release policies and protect reusable items. A paper requiring off-site printing days beforehand cannot gain this just-in-time property without redesigning the print process.

### 4.3 Release and record

The first milestone records a simulated release only. At release, the operator signs the hash of the exact paper artifact, and the centre signs what it received; the mock interface also gives participants the full hash in a receipt or QR code for a post-exam challenge. These records bind the selected IDs to what was distributed, though a dishonest centre can still lie unless participants or inspectors compare their copy. A later `muhar-seal` phase needs a reviewed release protocol, separate custodians, authenticated centre devices, tested offline/retry procedures, and an incident drill. Admission-gate closure is an attested human/centre fact, not something a contract can observe. A time-lock based on a public beacon is **not** a substitute for release governance: at its scheduled round, anyone holding the ciphertext can decrypt it; an outage can delay it. For a live exam, evaluate threshold-controlled release and encrypted per-centre delivery with independent cryptographic review. This changes the trust model only if the authoring pipeline never gives one operator a readable copy of the entire bank; otherwise that operator can reconstruct the selected paper after the seed and bypass the release custodians. The centre program cannot establish its own integrity by checking its own hash; signed builds need an external trust root such as a controlled boot/install process plus independent inspection.

`muhar-log` stores signed public events and encrypted/restricted private evidence separately. Public events include commitments, approvals, cancellations, beacon references, release attestations, and later audit outcomes. A verifiable append-only log provides inclusion and consistency proofs; independent monitors save checkpoints and alert on splits or missing entries. Periodic checkpoint hashes are anchored on Ethereum. An anchor alone does not provide durable access to the full log, so at least two independent mirrors must preserve proof bundles.

### 4.4 Verify and disclose

For the synthetic mock, publish the full bank, ordered metadata, salts, paper, signed release/centre receipts, beacon signature, manifest, signatures, log proofs, and chain reference after the exam. `muhar verify` must recompute the roots and exact selection, compare the distributed artifact hash, and report each check separately. Its top-level result is `PASS` only if all required checks pass; `INCOMPLETE` is never shown as success.

For a reusable confidential bank, the public can replay the draw if the ordered eligibility metadata and selected item content/salt openings are disclosed after that session. Unselected content and salts stay private. An independent auditor must privately review whether the undisclosed items and tags were valid; the Merkle root cannot prove that. If even the eligibility metadata cannot be disclosed, the claim must be narrower: **auditor-verifiable selection**, with a public audit attestation. Zero-knowledge proofs are a research option only after a simpler audited protocol works. The validity and fairness of the bank remain human/psychometric questions.

## 5. Minimum technical modules

| Module | First release | Later |
| --- | --- | --- |
| `muhar-draw` | Go CLI, versioned manifest format, deterministic draw, known-answer vectors | Multiple forms, reviewed psychometric constraints |
| `muhar-log` | Reuse a reviewed transparency-log implementation; signed checkpoints, witness/monitor, Ethereum anchor | Higher-volume operation, retention controls |
| `muhar verify` | Separate Go verifier plus one independent reference implementation and a readable proof report | Accessible web verifier with English/Hindi explanations |
| `muhar-bank` | Synthetic canonical bank and metadata format only | Restricted authoring, review, duplicate and conflict controls |
| `muhar-seal` | Simulation and written release protocol | Audited threshold/key ceremony and centre distribution |
| `muhar-trace` / `muhar-radar` | Defer | Investigative canaries and leak monitoring with human review; never automatic guilt decisions |

An initial repository layout after the spec review could be `cmd/muhar/`, `internal/draw/`, `internal/verify/`, `protocol/`, `testvectors/`, `demo/`, and `docs/`. Keep the number of dependencies small. A single public Ethereum anchor per session plus checkpoint anchors is sufficient to test the chain's value; do not deploy a token, candidate wallet flow, or custom chain.

## 6. Open-source security and privacy

- License code under **Apache-2.0** after a contributor/IP review; publish the protocol specification, threat model, test vectors, and independent verifier. Keep only genuine exam secrets and operational credentials private. The source being public is compatible with security when the secret is in the keys and controlled processes.
- Protect `draw`, `verify`, log integration, crypto, build scripts, and release workflow with at least two independent reviewers, mandatory checks, and protected branches. A `CODEOWNERS` entry alone can be satisfied by one owner, so configure the required review count separately. [GitHub's branch-protection documentation](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches) describes these controls.
- Pin dependencies and publish a software bill of materials, build provenance, signed release artifacts, and an independently checkable build path. Verify provenance and signature **outside** the program being checked. [SLSA](https://slsa.dev/spec/v1.0/levels) and [Sigstore](https://docs.sigstore.dev/cosign/verifying/verify/) provide existing models.
- Use synthetic data in the public repository and CI. Add secret scanning, parser fuzzing, deterministic protocol vectors, dependency review, and a private vulnerability-reporting channel before public deployment. Do not publish exploitable live-exam details in issues.
- Keep candidate identities, responses, biometrics, and raw grievances out of the public log and chain. Separate purpose-limited private evidence with encryption, access records, deletion/retention rules, and incident response. Design for the phased [DPDP Act commencement](https://www.meity.gov.in/static/uploads/2025/11/c56ceae6c383460ca69577428d36828b.pdf) and [DPDP Rules](https://www.meity.gov.in/static/uploads/2025/11/53450e6e5dc0bfa85ebd78686cadad39.pdf); a covered operator must map the applicable duties. [CERT-In's directions](https://cert-in.org.in/PDF/CERT-In_Directions_70B_28.04.2022.pdf) are relevant to incident and log processes for covered entities.
- A public verification page should meet applicable [GIGW 3.0 accessibility guidance](https://guidelines.india.gov.in/new-features-of-gigw-3-0/) and work on low-bandwidth/mobile connections. A paper or offline receipt can carry an exam reference without exposing a candidate.

## 7. Milestones and proof of success

| Gate | Deliverable | Exit test |
| --- | --- | --- |
| 0. Governance and spec | Signed pilot charter; frozen threat model; exact canonical formats and draw algorithm | Independent reviewer can explain every trust assumption and cancellation path |
| 1. Reproducible draw | Synthetic bank, CLI, reference verifier, vectors | Two independent implementations select identical IDs; changed root/rules/seed fail |
| 2. Public evidence | Signed log, external monitor, mirrored proofs, testnet Ethereum anchor | Observer detects a deleted/reordered event, alternate root, late anchor, and missing data |
| 3. Mock exam | College/coaching partner; one digital session; public post-exam bundle | All participants can replay selection; no actual question/PII secret enters public systems |
| 4. Adversarial review | External review of protocol, code, key process and centre design; outage/compromise drill | Findings are fixed and retested; written go/no-go for any live-secret pilot |
| 5. Limited live-secret pilot | Institution-approved low-stakes exam with reviewed release controls | Documented release, incident, accessibility and rollback results; no high-stakes claim |

Measure the percent of independent verifiers that reproduce the paper, time from exam end to proof availability, missing/mismatched log events, release lateness, outage recovery, and whether an auditor can reconstruct every exception. “Zero leaks” alone is not a meaningful pilot metric because it cannot be proved from a small test.

## 8. Decisions to settle before implementation

1. Pick the first partner and exact format: one digital mock session is the default. Multi-shift and printed exams need different release/custody designs.
2. Decide when a real operator may disclose the eligibility metadata and selected item openings. If it cannot, state the narrower auditor-verifiable claim.
3. Choose independent witnesses and bank auditor, and define how they are appointed, replaced, and funded without losing independence.
4. Specify a lawful retention and evidence-export schedule with the adopting institution; do not put sensitive evidence on an immutable public network.
5. Choose the exact beacon network/round and Ethereum network at pilot time, then pin them in the signed manifest. The demo testnet anchor is not a production security guarantee.

## Key design references

- [Devcon 8 workshop listing](https://cfp.devcon.org/devcon8/talk/QB3PET/)
- [2024 NTA reform report](https://www.education.gov.in/sites/upload_files/mhrd/files/HLCE_Report.pdf) and [2026 parliamentary committee release](https://www.pib.gov.in/PressReleseDetailm.aspx?PRID=2321420&lang=1&reg=1). The Ministry's report PDF URL returned HTTP 404 on 7 November 2026; its indexed text was available for review.
- [drand specification](https://docs.drand.love/docs/specification/) and [timelock documentation](https://docs.drand.love/docs/timelock-encryption/)
- [Transparency log verification](https://transparency.dev/articles/logs-a-verifiable-transport-layer/) and [Ethereum data-availability limits](https://ethereum.org/developers/docs/data-availability)
