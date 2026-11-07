# Muhar threat model (design draft)

Scope: a low-stakes, one-centre, one-session digital mock using synthetic questions. This model is a prerequisite for, not a certification of, a live exam. The public evidence protocol is distinct from the private question-bank and centre systems.

## Assets and boundaries

| Asset | Must remain private until policy allows | Publicly checkable claim |
| --- | --- | --- |
| Question packages and separate answer keys | Yes | Selected questions match prior salted commitments after opening; answer keys follow a later policy |
| Eligibility metadata and draw rules | May remain committed until exam ends | The disclosed inventory/rules match the pre-round manifest |
| Beacon round and seed | Round fixed in advance; seed public after round | Authenticated future randomness was used |
| Exam manifest and public events | No | Signatures, inclusion, consistency, and anchor agree |
| Release keys and centre secrets | Yes | Authorized release attestations, not the secrets themselves |
| Candidate records and grievances | Yes | No personal data is needed for a public proof |

Trust boundaries: author/reviewer to bank; bank/auditor to signed manifest; operator to public log; log to independent witness; witness to Ethereum; beacon to draw; operator/keyholders to centre; centre to candidate; private incident evidence to official investigator. A signature proves which key signed a statement, not that the physical statement is true.

## Attacks, defenses, and remaining limits

| Attacker goal | Required control or evidence | Residual limit |
| --- | --- | --- |
| Leak a question during authoring/review | Least-privilege bank access, per-item compartments, conflict declarations, access logs, controlled review rooms | An authorized author can remember or disclose their own item |
| Stuff the bank with favoured/duplicate items or false tags | Independent confidential bank/blueprint review, duplicate checks, signed inventory, post-exam audit | A root proves commitment, not academic quality or impartiality |
| Present a counterfeit self-signed exam as official | Publish the institution's signing root and canonical registry through an independently authenticated schedule; verify the key chain and registry code hash | A fake site or compromised institutional root can still mislead users |
| Cancel after seeing an unfavourable seed and draw again | Independent post-seed cancellation quorum, public linked attempt history, incident evidence and review | Colluding decision makers can still abuse emergency authority |
| Choose the seed after seeing the bank | Freeze exact future beacon round and rules in a finalized public anchor well before the round; verify signature and timing | Beacon committee assumptions and outages still matter |
| Swap the bank, algorithm, paper, or render after freeze | Canonical/versioned commitments, exact replay, selected-item proofs, signed output artifact hash | Public replay needs enough metadata disclosure; otherwise an auditor must check |
| Deliver a different paper than the verified draw | Verifier compares the actual package's complete ordered content with selected item openings; CBT import/start rejects digest mismatch; operator and centre sign private digest receipts; participants retain signed exit receipts | A dishonest centre can still misstate display unless a participant or inspector retains evidence |
| Let a CBT platform reshuffle or change a language/asset after Muhar signs | Disable hidden reshuffling in the first mock; verify imported package and candidate variant, bind digest/variant in private session records | A compromised frontend can still render different pixels |
| Identify a selected form from its public digest before later shifts | Log a random-salted commitment to the package digest, reveal bare digest and centre receipts only after affected sessions | Candidates or insiders who have seen the form can still disclose it |
| Show different logs to different people | Append-only inclusion/consistency proofs, independent monitors/mirrors, Ethereum checkpoint anchor | Without active monitoring and retained data, detection can be delayed |
| Obtain the selected paper between seed and start | Draw near admission closure; restrict bank access; later threshold-controlled release and centre custody | Any full-bank insider can derive selected items once seed is public; in-room communication persists |
| Compromise a centre computer or replace a binary | External signed-release verification, controlled boot/install, device checks, network isolation, two-person custody, drills | A compromised endpoint or dishonest officials can still copy content; self-hashing is ineffective |
| Force an outage to trigger an easy fallback | Precommitted retry/cancel policy, multiple beacon relays, mirrored log, rehearsed postpone process | Continuity may require postponement; no silent operator-selected seed |
| Abuse emergency authority | Named signers, quorum, signed reasons, append-only cancellation/reschedule, after-action review | Governance can be captured or colluding signers can lie |
| Identify a candidate or expose evidence | No candidate data or raw reports on chain; encrypted restricted evidence; retention and access policy | Small-group metadata and timing can still reveal information; review every public field |
| Poison open-source code or release | Protected branches, two independent reviewers for sensitive paths, dependency pinning, signed provenance, external artifact verification | A maintainer or build-platform compromise is still possible |
| Misattribute a leak via canary or AI | Treat canaries/alerts as leads, preserve chain of custody, require human investigation and appeal | A canary can be removed or copied; correlation alone is not proof of guilt |

## Security invariants for the verifier

1. Bind every proof to one protocol version, institutionally authenticated session identifier and signer root, canonical manifest, beacon chain identity, exact round, and the charter's named Ethereum registry/network. The auditor's pre-round attestation and every selected-item content opening must bind to that same manifest and item ID. Reject replay across sessions or networks.
2. Reject missing signatures, invalid beacon proof, unknown algorithm version, changed input root, impossible blueprint, parallel frozen manifests for the official session, or non-finalized/late anchor. Report which check failed.
3. Require inclusion and consistency proofs from a checkpoint independently retained by a witness. A chain hash without retrievable log data is `INCOMPLETE`.
4. Recompute the draw from the *committed ordered inventory*. Canonicalize the actual paper package, verify its complete content and order against the selected openings, then compare its digest with private release receipts and the later public commitment opening. Report draw reproduction, paper match, bank-auditor attestation, and delivery attestation as separate claims. If the inventory is undisclosed, report `AUDITOR_ATTESTED`, never `PUBLICLY_REPRODUCED`.
5. Record cancellation and emergency release as explicit terminal/exception states. Show every cancelled attempt and its replacement link, including any attempt after the seed was known. Never turn a failed verification into a green pass through a manual override.

## Review before live use

An independent security reviewer must inspect the formal protocol and implementation, bank-access design, beacon assumptions, key custody, centre hardware/software, backup paths, privacy handling, and incident process. A mock must deliberately simulate a malicious bank curator, late anchor, equivocal log, compromised centre, lost custodian, and beacon outage. The review findings and residual risks must be accepted by the accountable exam operator before any live-secret trial.
