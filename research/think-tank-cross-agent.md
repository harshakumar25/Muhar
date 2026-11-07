> **Provenance:** Think Tank `cross-agent --target codex` output from the pinned local repository. This was one read-only Codex consultation, not a Claude debate. File-line links below refer to the pre-revision design snapshot and may have shifted after the README and architecture edits.

# Cross-Agent Consultation

- **Date**: 2026-11-08-005906
- **Target**: codex
- **Arbiter**: none
- **Topic**: "Read README.md, PLAN.md, DIGITAL_ARCHITECTURE.md, and THREAT_MODEL.md in the current directory. For Muhar, identify the deepest India-specific exam-integrity problem and the strongest counterarguments against using Ethereum. Give 3 competing architectures (institutional controls only; witnessed transparency log; witnessed log plus Ethereum anchor), concrete failure scenarios, discriminating pilot tests, and a recommendation. Separate observed facts from assumptions. Do not edit files."

---

## Codex Response

## Assessment

**The deepest India-specific problem is accountable custody under a tight release clock.** The paper must be selected close enough to the exam to limit exposure, yet a public draw reveals the selected items to anyone who can read the full bank. Late entry, multiple centres, later shifts, language variants, and accommodations make “release after the gates close” an unreliable rule. A valid commitment can coexist with an insider leak, a poor or biased bank, or a centre showing candidates different content. That is the central gap between *a verifiable draw* and *an integral exam*. [PLAN.md](/Users/harshkumar/Desktop/projects/Muhar/PLAN.md:7), [PLAN.md](/Users/harshkumar/Desktop/projects/Muhar/PLAN.md:70), [DIGITAL_ARCHITECTURE.md](/Users/harshkumar/Desktop/projects/Muhar/DIGITAL_ARCHITECTURE.md:95)

This tension is grounded in the Indian context: the October 2026 parliamentary committee recommends setting papers close to exam time **and** developing a late-entry mechanism; it calls for independently audited normalisation if a major exam moves to multiple CBT sessions. It also identifies a gap in the public record of leak investigations. These are committee findings and recommendations, not evidence that Muhar has solved them. [Parliamentary committee release](https://www.pib.gov.in/PressReleaseIframePage.aspx?PRID=2321420&lang=2&reg=3)

### What is observed; what remains assumed

**Observed:** The four files describe a proposal, not deployed software or a measured pilot. The proposed first test is a synthetic, one-centre digital mock. Its intended proof concerns the frozen inventory and rules, reproduced draw, paper package, and recorded history. The documents explicitly exclude proof of bank quality, human secrecy, physical gate closure, and the truth of a centre’s signed statement. [README.md](/Users/harshkumar/Desktop/projects/Muhar/README.md:15), [README.md](/Users/harshkumar/Desktop/projects/Muhar/README.md:23), [THREAT_MODEL.md](/Users/harshkumar/Desktop/projects/Muhar/THREAT_MODEL.md:16)

**Assumptions to test:** The institution authenticates the official session and signing root; auditors and witnesses are genuinely independent; access to the full bank is constrained; the CBT system enforces the signed package; candidate challenges can supply evidence of what appeared on screen; and later disclosure does not expose reusable items. None follows from a hash or an Ethereum transaction. [PLAN.md](/Users/harshkumar/Desktop/projects/Muhar/PLAN.md:41), [DIGITAL_ARCHITECTURE.md](/Users/harshkumar/Desktop/projects/Muhar/DIGITAL_ARCHITECTURE.md:70)

### Strongest arguments against Ethereum

1. **It addresses a narrower failure than the principal leak paths.** An anchor can expose a changed commitment. It cannot stop an author leaking an item, a full-bank insider learning the selected form after the beacon, a curator stuffing the bank, or a centre misdisplaying a translation or option. [THREAT_MODEL.md](/Users/harshkumar/Desktop/projects/Muhar/THREAT_MODEL.md:22)

2. **Independent witnesses may already provide enough history.** If even one independent party retains and publishes the pre-seed checkpoint and proof bundle, a later log rewrite is detectable. Ethereum’s distinctive benefit appears when those records and witnesses are all compromised, coerced, or lost. Whether that extra protection is worth operating a chain anchor is an empirical question. [PLAN.md](/Users/harshkumar/Desktop/projects/Muhar/PLAN.md:20)

3. **An anchor preserves a commitment, not its evidence or authority.** Missing log data still make verification `INCOMPLETE`; a self-signed charter or an alternate advertised session is not made official by appearing on-chain. The institution must authenticate the canonical session, signer, network, and registry. [THREAT_MODEL.md](/Users/harshkumar/Desktop/projects/Muhar/THREAT_MODEL.md:24), [THREAT_MODEL.md](/Users/harshkumar/Desktop/projects/Muhar/THREAT_MODEL.md:44)

4. **It adds an operational deadline and permanent public metadata.** The proposed anchor must be finalized before the chosen beacon round; a late anchor must fail. Registry governance, chain pinning, finality checks, and careful field redaction become additional work. Their cost and reliability have not been measured in this project. [PLAN.md](/Users/harshkumar/Desktop/projects/Muhar/PLAN.md:62), [DIGITAL_ARCHITECTURE.md](/Users/harshkumar/Desktop/projects/Muhar/DIGITAL_ARCHITECTURE.md:99)

### Three competing architectures

Hold the **same** bank review, official charter, future-beacon draw, cancellation rules, signed CBT package, centre checks, candidate receipt, and grievance process constant. Change only how the pre-seed and subsequent evidence is preserved.

| Architecture | Evidence model | Concrete failure scenario |
| --- | --- | --- |
| **A. Institutional controls only** | Signed internal manifest and audit records; independent bank review, controlled release, dual centre sign-off, retained incident files. | Operator and record custodians replace the recorded freeze after seeing the seed. An auditor’s independently retained copy might expose this, but public proof depends on that institution and auditor producing it. |
| **B. Witnessed transparency log** | A publicly published pre-seed manifest and auditor attestation; append-only proofs; two independent witnesses retaining checkpoints and mirrored proof bundles. | The log shows a split to different parties: one honest witness catches it. If every independent copy disappears or its holder colludes, outsiders may lose the original history. |
| **C. Witnessed log plus Ethereum** | B, plus a finalized pre-seed checkpoint in an institutionally pinned, one-time registry. | After the operator and witness archives rewrite their accounts, a verifier can still reject a replacement root against the chain. If the underlying log vanished, it can detect the conflict but cannot reconstruct the paper: the result is `INCOMPLETE`. A validly anchored poisoned bank remains possible. |

These boundaries follow the proposal’s separation of draw, paper match, bank-auditor attestation, and delivery attestation; there should be no single “exam secure” verdict. [DIGITAL_ARCHITECTURE.md](/Users/harshkumar/Desktop/projects/Muhar/DIGITAL_ARCHITECTURE.md:68)

### Discriminating pilot tests

Run the same synthetic mock and fault injections through A, B, and C, with independent verifiers given only the evidence each architecture promises.

| Injection | Result that would distinguish the designs |
| --- | --- |
| Replace the frozen root after the seed; delete or reorder a release event; serve two log histories. | Record what A’s auditor can establish. B and C must reject the altered history using an independently retained checkpoint. |
| Erase or corrupt the operator’s and *all designated witnesses’* archives after a genuinely pre-seed freeze, assuming no other public copy survives. | This is C’s decisive test: an outside verifier must find the original finalized root and reject its replacement. If log data are gone, it must report `INCOMPLETE`, never a complete proof. |
| Submit a late or unfinalized anchor, a parallel manifest, then cancel after seeing an unfavourable draw. | C must reject the late anchor; every design must show the cancelled attempt, independent approval, reason, and linked replacement. No silent new beacon round. |
| Insert duplicate or falsely tagged bank items; alter a displayed language variant or option; simulate a full-bank insider leak. | Auditor, CBT, and candidate evidence must be tested on their own terms. Neither B nor C may turn a valid hash into a claim of academic quality, secrecy, or correct screen display. |
| Drop a beacon relay, centre link, or Ethereum RPC at exam start. | Use only the committed authenticated beacon round; pause where delivery fails. C should work from cached finalized-anchor witness attestations when the start-time RPC fails. Measure postponements and draw-to-release time. |

Pre-register the injected cases and require **zero incorrect `VERIFIED` results for each precisely stated claim**, two independent implementations reproducing the selected IDs and exact package, and a complete visible cancellation history. Measure detection time, proof availability, release latency, and candidate challenge usability. A small mock cannot establish a “zero leaks” rate. [PLAN.md](/Users/harshkumar/Desktop/projects/Muhar/PLAN.md:117), [THREAT_MODEL.md](/Users/harshkumar/Desktop/projects/Muhar/THREAT_MODEL.md:50)

**Recommendation:** Use **B, witnessed transparency, as the pilot’s evidence baseline**, with institutional controls as mandatory foundations. Test **C as an additional arm**, retaining Ethereum for live use only if the all-witness-compromise test demonstrates a valuable protection under a credible threat model and the finality and operating burden are acceptable. Do not advance from the synthetic mock to live questions until bank custody, release governance, centre devices, privacy, and incident handling receive the separate review the plan requires. [PLAN.md](/Users/harshkumar/Desktop/projects/Muhar/PLAN.md:122) No files were edited.
