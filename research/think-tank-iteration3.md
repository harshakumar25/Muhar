# Cross-Agent Consultation

- **Date**: 2026-11-09-195621
- **Target**: codex
- **Arbiter**: none
- **Topic**: "Adversarial review of Muhar exam-security proposal. Read README.md, PLAN.md, DIGITAL_ARCHITECTURE.md, THREAT_MODEL.md in /Users/harshkumar/Desktop/projects/Muhar. User requires India-wide generality, scarce CBT capacity, corrupt invigilators/centre staff, NEET scale versus JEE, and first-iteration sealed paper with no unauthorized preview. Compare conventional isolated assembly with HSM controlled release, confidential-compute/TEE assembly plus independently governed key release, and MPC/threshold-only architecture. Explain exact threat-dependent meaning of no one sees the final paper, why approvals are not threshold cryptography, full-bank auditor/public-seed bypass, post-release centre collusion, accessibility/normalization and simultaneous capacity. Identify strongest fatal counterexample and smallest synthetic experiment; recommend proposal changes. Do not edit files. Do not treat claimed national CBT shortage or 2X candidate ratio as verified data."

---

## Codex Response

## Verdict

Muhar has a defensible **post-exam integrity** design, but the four documents do not yet establish a **first-iteration sealed-paper** design. The revised [README.md](/Users/harshkumar/Desktop/projects/Muhar/README.md:15) now calls for protected assembly with synthetic questions, while [PLAN.md](/Users/harshkumar/Desktop/projects/Muhar/PLAN.md:77) still simulates release and defers `muhar-seal`. The proposal should resolve that conflict before claiming it has tested unauthorized preview.

## What “no one sees the final paper” can mean

Define a time and an attacker. A useful pre-release claim is: **before the first authorized plaintext delivery, no human in the stated attacker set can reconstruct or export the complete ordered form.** Authors still see assigned items; a protected computer processes plaintext; candidates eventually see the form. If a human reviews the assembled form, that person is an explicit exception. The README’s stronger “no authorized human preview” target excludes conventional human final-form review ([README.md](/Users/harshkumar/Desktop/projects/Muhar/README.md:17)).

There is a second, different claim: **no candidate gets an advance view before their own start**. Pre-release controls cannot ensure this after the first centre displays a shared form. A corrupt official can relay it to a centre still admitting candidates. The documents recognize that receipts cannot prove displayed pixels and that multiple centres create a timing problem ([THREAT_MODEL.md](/Users/harshkumar/Desktop/projects/Muhar/THREAT_MODEL.md:28), [DIGITAL_ARCHITECTURE.md](/Users/harshkumar/Desktop/projects/Muhar/DIGITAL_ARCHITECTURE.md:108)).

| Design | Strongest plausible pre-release claim | Decisive trust boundary |
| --- | --- | --- |
| Conventional isolated assembly | Outsiders cannot preview if room, people, devices, and output custody hold. | Assemblers and any final-form reviewers see plaintext. A corrupt one defeats a claim that includes them. |
| HSM-controlled release | Key use can be gated by an enforced release policy. | An ordinary HSM safeguards keys and performs cryptography; it does not make plaintext already held by an assembler or full-bank reader secret. |
| TEE assembly plus independently governed key release | Reviewed, attested code can assemble from encrypted items and emit only encrypted, recipient-bound output until release. This is the strongest practical candidate for *no routine human final-form preview*. | It depends on bank access, measured code, attestation policy, hardware, side-channel assumptions, independent custodians, and the receiving device. The TEE itself processes plaintext. |
| MPC or threshold-only | Genuine MPC could avoid one assembly machine holding the full plaintext; threshold decryption can protect a key. | Key shares alone do not protect plaintext copied upstream or disclosed at the endpoint. Full MPC for content, assets, rendering, and release adds substantial engineering and assessment complexity. |

These distinctions follow the [NIST HSM definition](https://csrc.nist.gov/glossary/term/hardware_security_module_hsm), the [Confidential Computing Consortium’s TEE model](https://confidentialcomputing.io/wp-content/uploads/sites/10/2023/03/CCC-A-Technical-Analysis-of-Confidential-Computing-v1.3_Updated_November_2022.pdf), and [NIST’s threshold-cryptography definition](https://csrc.nist.gov/Projects/threshold-cryptography). **Multiple approvals are not threshold cryptography**: signatures document consent; a cryptographic threshold requires independently held secret shares such that fewer than the threshold cannot perform the protected operation. Even an attestation result depends on the verifier’s reference values and policy ([RFC 9334](https://www.rfc-editor.org/rfc/rfc9334.html)).

## Fatal counterexample and smallest test

Let `B` be the complete bank, `I` its ordered eligibility metadata, and `R` the public seed. The final form is a deterministic function `Draw(B, I, R)`. A corrupt auditor or administrator holding `B` and `I` computes it as soon as `R` appears, while release keys remain closed. **Every freeze, witness, draw, and delivery check can still pass.** Muhar already states this bypass ([README.md](/Users/harshkumar/Desktop/projects/Muhar/README.md:69), [PLAN.md](/Users/harshkumar/Desktop/projects/Muhar/PLAN.md:73), [DIGITAL_ARCHITECTURE.md](/Users/harshkumar/Desktop/projects/Muhar/DIGITAL_ARCHITECTURE.md:104)).

The smallest falsification needs four distinct synthetic items, two strata, and a draw of one item per stratum. Give a tester full-bank read access but no release authority; publish the committed seed while holding release closed. A timestamped correct ordered paper **before release**, alongside a passing integrity verifier, disproves the secrecy claim for that attacker model. Then run a separate two-centre drill: let centre A open a shared form while centre B still admits someone, and have colluding staff relay an item. That tests the post-release failure that key custody cannot solve.

## India-wide constraint

Use **simultaneous, usable capacity**, not annual candidate totals or nominal computer counts. If `N` candidates need one window and `S` geographically suitable, accessible seats are usable at once after outage reserves, at least `ceil(N/S)` CBT sittings are needed when `S < N`; actual scheduling may require more. A shared form across sittings creates an advance-leak path. Separate forms need independent calibration, language and accessibility equivalence, a published normalization method, and a timely challenge route. Late admission, scribes, extra time, delayed starts, and corrupt centre staff also widen the overlap window ([DIGITAL_ARCHITECTURE.md](/Users/harshkumar/Desktop/projects/Muhar/DIGITAL_ARCHITECTURE.md:45), [DIGITAL_ARCHITECTURE.md](/Users/harshkumar/Desktop/projects/Muhar/DIGITAL_ARCHITECTURE.md:108)). Treat NEET-like large common-form and JEE-like multiple-sitting cases as **workload scenarios**; this review does not verify a national CBT shortage or a 2× candidate ratio.

## Changes to make

1. **Align the first iteration across documents.** Put an actual synthetic sealed-assembly and release gate, plaintext-access inventory, and negative-preview test in PLAN and DIGITAL_ARCHITECTURE, or narrow the first-iteration claim to integrity evidence. The README currently promises the former while PLAN specifies the latter.
2. **Specify two secrecy invariants:** before first authorized plaintext release, and between that release and each candidate’s start. Name corrupt roles, permitted human viewers, collusion threshold, exact release event, and emergency bypasses.
3. **Make bank access the first gate.** No auditor, operator, administrator, backup path, or assembler may hold the complete readable bank plus draw metadata if that actor is in the attacker set. Govern input keys, attested assembly, and output keys separately; a release quorum cannot repair an upstream copy.
4. **Add exam-mode acceptance gates.** Model effective seat capacity, synchronized starts and late entry, accessible variants, outages, multi-form equating, and print/OMR custody separately. A one-centre CBT mock cannot validate India-wide readiness.

The reviewed files changed during reading. In the final checked snapshot, the README also linked to proposed architecture and capacity files that were not present, so those links cannot yet resolve the contradictions above. No files were edited.
