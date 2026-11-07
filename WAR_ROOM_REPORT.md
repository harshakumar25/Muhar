# Muhar war room: what would make this worth building?

**Date:** 8 November 2026  
**Mode used:** design + adversarial review, following the user-provided `100-dev-war-room` method and the [Think Tank critic/defender/synthesizer prompts](https://github.com/cerodb/think-tank/tree/470669957d2fe98ccb94e649cf6c913a5d670142/plugins/think-tank/prompts/debate).

## Executive verdict

Build Muhar first as **a public evidence layer for one exam form**, with an accountable operator, a reviewed private question bank, a deterministic late draw, an independently witnessed log, and a candidate challenge process. Treat Ethereum as an experimental extra witness to the frozen record; require a measured advantage over the witnessed-log baseline before making it mandatory. Confidence is **medium** that the narrow protocol can be built and tested, and **low** that it reduces live leaks or improves national exam trust without institutional adoption and operational evidence.

## Ground truth / unknowns

### Problem definition

The [Devcon 8 workshop](https://cfp.devcon.org/devcon8/talk/QB3PET/) asks what guarantees students need and where Ethereum helps. The [October 2026 Rajya Sabha committee release](https://www.pib.gov.in/PressReleseDetailm.aspx?PRID=2321420&lang=1&reg=1) recommends large reviewed banks, papers assembled close to exam time, independent audit, secure grievances, and attention to late entry, rural CBT access, and multiple-shift normalisation. These are public recommendations, **not validation of Muhar**.

The design files [PLAN.md](PLAN.md), [DIGITAL_ARCHITECTURE.md](DIGITAL_ARCHITECTURE.md), and [THREAT_MODEL.md](THREAT_MODEL.md) specify a one-centre synthetic mock. There is no implementation, partner, verified threat prevalence, measured release latency, candidate study, or live-secret pilot. A verified beacon and transparent log are plausible components because the [drand specification](https://docs.drand.love/docs/specification/) defines verifiable beacon rounds and [witnessed logs](https://blog.transparency.dev/can-i-get-a-witness-network) can preserve consistent checkpoints. The adoption case remains unproven.

**Precise success question:** For a publicly announced session, can an independent verifier establish that one authorised inventory and rule set was frozen before a future seed, reproduce the selected form after permitted disclosure, detect a changed history, and separate those facts from unproved claims about secrecy, fairness, and actual screen display? Can a candidate use a failed or incomplete result to obtain a timely, reviewable institutional response?

**Unknowns that determine viability:** who authenticates the official session and keys; whether auditors and witnesses are independent in funding and operation; who can read the full bank; whether CBT software enforces the signed package; what evidence a candidate can retain; how reused items are disclosed; what legal and operational remedy the adopter will offer. The committee's concerns about centre operations and grievances make these first-class requirements.

### Review method and evidence limits

The pasted war-room skill asks for a 10-discipline × 10-lens scan. I used that as **100 virtual perspectives**, merged repeated concerns, and carried material objections into the table below. Four actual read-only subagents examined the Think Tank repository, Muhar's architecture, README design, and Indian primary sources. The [Think Tank cross-agent orchestrator's Codex target](research/think-tank-cross-agent.md) supplied one additional read-only critique. These are not 100 independent reviewers. The full Claude-backed Think Tank debate was **not run** because the local Claude CLI reported `Not logged in`; its prompt structure was applied in this report instead.

## Council debate

### Round 0 — the two causal claims

1. **Before the exam:** a future, authenticated draw can delay knowledge of the selected form for people who cannot read the whole eligible bank. It does not protect against an author leaking an item or a full-bank insider deriving the form once the seed appears.
2. **After the exam:** signed commitments, a replayable draw, retained checkpoints, and delivery attestations can expose certain substitutions or story changes. Their value depends on independent monitors retaining evidence and an operator obliged to answer challenges.

“Fewer leaks” and “more trusted exams” are possible downstream outcomes, not properties proved by a hash or chain transaction. The first mock tests protocol behaviour and human comprehension; it cannot measure national leak reduction.

### Round 1 — three genuinely different architectures

Hold the same bank review, official charter, beacon draw, signed CBT package, centre checks, and grievance path constant. Vary the evidence record.

| Option | Mechanism | Strongest case | Failure boundary | Disproof test |
| --- | --- | --- | --- | --- |
| **A. Institutional records** | Operator signs an internal freeze and retains audit files; independent auditors and centre officials hold copies. | Lowest added complexity; fits existing responsibility. | If the operator and custodians replace or withhold the pre-seed record, outsiders may not reconstruct what happened. | Have an independent challenger detect a substituted freeze using only promised records. |
| **B. Witnessed public log** | Publish the signed manifest and auditor attestation in an append-only log; independent witnesses retain and cosign checkpoints and proof bundles. | An honest witness can expose a rewrite or split view without a chain. | All retained copies or witnesses could be lost, captured, or coerced; the log operator can make data unavailable. | Inject divergent histories and archive loss; measure what an outsider can still prove. |
| **C. B + Ethereum anchor** | Before the seed, finalize the canonical session commitment and log checkpoint in a pinned registry on Ethereum. | A neutral public record may remain when an operator and its witnesses later change their story. | The anchor proves inclusion/order of bytes, not official authority, data availability, bank quality, or delivery truth; finality and metadata add operational cost. | Erase all designated archives, then test whether the chain lets an outsider reject a replacement root and whether the remaining result is correctly marked `INCOMPLETE`. |

The [Think Tank consultation](research/think-tank-cross-agent.md) independently recommended B as the baseline and C as an additional experimental arm. A is still a necessary operational foundation, not a sufficient public evidence design.

### Round 2 — adversarial cross-examination

**Advocate:** A public replay constrains silent substitution: the operator cannot change the committed eligible inventory, rules, or selected paper without a failed verification, provided the canonical manifest is authenticated and at least one checkpoint survives. A neutral anchor may protect against a later jointly rewritten institutional account.

**Skeptic:** A bank curator can commit a biased inventory or falsely tag difficulty before the seed. A full-bank insider learns every selected item as soon as the public seed appears. A centre can show different pixels while signing a valid package receipt. An operator can cancel an unfavourable draw and start again unless every attempt and its reason stays visible. Students receive no practical benefit if no one must respond to a challenge. The Advocate **concedes** these are likely failure paths in a real deployment and that Muhar cannot certify a leak-free or fair exam.

**Operations / candidate reality checker:** The committee recommends late entry and warns about rural CBT and multiple shifts. A synchronized paper release can conflict with late candidates, accessibility accommodations, link outages, and a common form across centres. Failing closed protects integrity but may postpone an exam and harm candidates. The Advocate **concedes** that a signed policy for admissions, postponement, evidence preservation, response deadlines, and remedies must precede a live pilot. The first digital mock must measure candidate comprehension as well as software checks.

**Unresolved disagreement:** Whether Ethereum's extra neutral checkpoint is worth its finality, registry, privacy, and operating burden. The decision needs a counterfactual test of B against C, especially under credible witness failure. Neither a chain transaction nor a majority of simulated reviewers resolves that question.

### Round 3 — synthesis and decision

| Criterion | A: institutional records | B: witnessed log | C: B + Ethereum |
| --- | --- | --- | --- |
| Draw correctness | Same deterministic algorithm | Same | Same |
| Resistance to silent record rewrite | Depends on retained institutional copies | Strong if an independent witness and data survive | May survive later witness compromise; still needs data |
| Security scope | Does not prevent insider or centre leaks | Same | Same |
| Maintenance and time to implement | Lowest | Moderate | Highest; registry, finality, chain monitoring |
| Operational risk | Familiar but opaque | Witness and log availability | B risks plus chain deadline and permanent metadata |
| Current evidence of incremental benefit | Baseline procedures only | Established witness pattern; Muhar pilot untested | Hypothesis; no Muhar measurement yet |

**Decision:** prototype **B** with the mandatory human controls from A. Build **C** on a test network as an A/B experiment and retain its anchor in a live design only if it changes a meaningful failure outcome under a credible threat model. The decision does not rely on a weighted score: B tests the core evidence proposition with fewer new failure paths, while C's marginal value remains unmeasured.

## Top findings from the 100-perspective scan

Severity and likelihood are design judgments for a future high-stakes deployment, not measured incident rates. `Observed` means a limitation follows from the stated protocol or cited source; `Hypothesis` needs a pilot, partner, or adversarial test.

| Rank / lens | Finding and concrete failure | Severity / likelihood / evidence | Validation and owner |
| --- | --- | --- | --- |
| **1 · Security-H, Architect-A** | A full-bank insider derives the selected form at the public seed. With a simple uniform draw of `m` from `N`, an insider knowing `q` eligible items expects `m×q/N` of them to be selected; for `q=N`, the entire form is exposed. Stratified draws need a per-stratum calculation. | Critical / likely if full-bank access exists / observed design property. | Map real bank access and earliest selected-form exposure; bank security lead and assessment operator. |
| **2 · Product-J, Security-D** | A valid proof can be ignored. If no authority must preserve evidence, answer a candidate, or publish a remedy, verification changes no outcome. | High / plausible / committee recommendation plus adoption hypothesis. | Write a public challenge and response charter; test candidate comprehension and response drills; operator and candidate representatives. |
| **3 · Product-B, QA-I** | Correct selection can produce an unfair paper through bad difficulty labels, duplicates, translation errors, or unequal forms. | High / plausible / observed scope limit. | Independent academic and psychometric review, translation checks, and form-equating plan; assessment specialists. |
| **4 · Architect-J, SRE-G** | Ethereum may add no material protection over independently witnessed checkpoints while adding finality delay and registry work. | High / plausible / counterfactual untested. | Run B/C fault injections with predeclared metrics; protocol lead and independent witnesses. |
| **5 · Security-A, Data-H** | A bank auditor needs enough access to detect poor or duplicate items, but broad access creates a leak-capable insider. | High / plausible / unresolved tradeoff. | Compare compartmentalized review with full-bank review; record who can reconstruct a form; bank governance lead. |
| **6 · SRE-F, Frontend-F** | A fail-closed beacon or centre outage postpones candidates, while a permissive fallback can let an operator choose a favourable seed. | High / plausible / observed failure tradeoff. | Drill fixed-round outage, signed postponement, late entry, and accessible communication; exam operations lead. |
| **7 · Backend-E, Security-C** | Post-seed cancellation can grind for a favoured paper unless all attempts are linked and independently approved. | High / plausible / observed protocol attack. | Adversarial cancellation test; verifier must show the whole attempt chain; protocol and governance leads. |
| **8 · Frontend-D, Security-I** | A signed package and centre receipt can match while a compromised CBT screen displays different options or language. | High / plausible / observed trust boundary. | Controlled device mismatch drill and restricted candidate evidence; CBT vendor and centre auditor. |
| **9 · Data-F, Security-B** | A chain root survives but its log leaves or proof bundle vanish; a verifier cannot reconstruct the paper. | High / plausible / observed evidence-availability gap. | Delete or corrupt archives; expect `INCOMPLETE`, with independent mirrors; log operator and witnesses. |
| **10 · DX-H, Security-J** | Open code can still ship a compromised binary, dependency, or configuration to a centre. | High / plausible / known software supply-chain class, untested here. | Reviewed dependencies, reproducible signed releases, external artifact verification; maintainers and deployment owner. |

National-scale load, state-specific legal obligations, score normalisation, real centre hardware, and available bank sizes **cannot yet be assessed** from this repository. They should not be converted into fictitious benchmarks or universal policy claims.

## Chosen solution

```text
Accountable exam operator + independent academic audit + candidate challenge charter
              │
Private, compartmentalised bank ──► one signed canonical session manifest
              │                                  │
              └── future verified beacon ──► witnessed log ──► optional ETH trial anchor
                         │                        │
                 deterministic paper        mirrored proof bundle
                         │                        │
                  signed CBT package ──► post-exam verifier and human remedy
```

The public contract is **claim by claim**, never a universal green result. The verifier should distinguish `FROZEN_BEFORE_SEED`, `DRAW_REPRODUCED`, `SELECTED_CONTENT_OPENED`, `PAPER_MATCHES_DRAW`, `LOG_CONSISTENT`, `DELIVERY_ATTESTED`, and `BANK_AUDITOR_ATTESTED`. When reusable-bank secrecy blocks inventory disclosure, call the draw **auditor-attested**. A centre receipt means someone signed for a digest, not that a candidate saw identical pixels. Privacy requires salted commitments, redaction, delayed disclosure across affected shifts, and a restricted evidence vault for personal records.

## Implementation plan

1. **Governance and candidate need:** with a willing low-stakes partner and candidate representatives, define the official session ID, signing root, auditor/witness appointment and conflicts, late entry, cancellation, public challenge window, response owner, evidence retention, and remedy path. Publish the charter before the mock.
2. **Protocol and tests:** specify canonical manifest and item formats, salts, signer binding, fixed beacon network/round, draw byte derivation, impossible-quota behaviour, and exact paper-package bytes. Publish positive and negative vectors; require an independent implementation to replay them. Reject wrong session, late freeze, wrong language asset, reordered option, and missing proof.
3. **Witnessed evidence baseline:** run an append-only log, at least two separately operated checkpoint witnesses, and mirrored proof bundles. Inject split views, deletion, and false receipts; return precise `FAILED` or `INCOMPLETE` claims.
4. **Ethereum experiment:** add one small finalized checkpoint on a pinned network and canonical registry. Compare B and C on detection of a replaced root after designated archives disappear, proof availability, cost, finality delay, and operational burden. Do not silently swap to a new round or network when a deadline fails.
5. **One-centre CBT mock:** use synthetic or retired items, disable vendor reshuffling, require a verified package before start, rehearse centre power/link loss and candidate challenges, and publish the permitted proof bundle after the session. Measure candidate understanding, draw-to-release time, failure handling, and how many independent verifiers reproduce the result.
6. **Live-secret gate:** require an external cryptography and centre-device review, bank-access and audit design, privacy assessment, assessment-quality review, incident drills, and an institution that accepts accountability. A synthetic mock alone cannot pass this gate.

**Mock stop criteria:** Pre-register tampered-root, wrong-round, swapped-content, log-split, missing-data, and post-seed cancellation cases. Any incorrect `VERIFIED` result stops progression. Two independently written verifiers must reproduce the complete synthetic draw and released package; every failed or missing check must remain visible. The operator must meet its announced release and candidate-response deadlines or record a signed postponement and remedy. Add Ethereum to the required path only if it exposes a credible failure missed by the witnessed baseline with acceptable delay and operating burden.

**Rollback and exception policy:** During the mock, a missed beacon or package mismatch pauses the session and creates a signed incident; a replacement session links to the original. In later use, anchor failure follows the prepublished charter. Do not hide a failed integrity check behind an administrator override. A future decision to remove Ethereum should be a versioned governance change after the comparison, not an unlogged runtime fallback.

## Validation ledger

| Result | Check and evidence |
| --- | --- |
| **PASS** | Inspected the four project design documents and the pasted war-room instructions; no implementation or test suite exists. |
| **PASS** | Checked the primary [parliamentary release](https://www.pib.gov.in/PressReleseDetailm.aspx?PRID=2321420&lang=1&reg=1), [drand specification](https://docs.drand.love/docs/specification/), and [witnessed-log description](https://blog.transparency.dev/can-i-get-a-witness-network/). |
| **PASS** | Installed Think Tank's pinned `ask-claude` Codex skill and ran its **Codex-only, read-only cross-agent mode**; the [raw consultation](research/think-tank-cross-agent.md) records the result. |
| **PASS** | Validated the local `think-tank` and `ask-claude` skill folders with `quick_validate.py`; rendered and visually inspected the 1280×360 SVG hero; parsed it as XML; checked project-local Markdown links and `git diff --check`. |
| **FAIL** | Local `claude -p` test returned `Not logged in · Please run /login`; the full Claude-backed Think Tank debate mode could not run. |
| **NOT RUN** | Protocol vectors, security tests, independent verifier replay, CBT mock, candidate study, and B/C comparison; no code or partner exists yet. |

## One-line next action

Write the official-session manifest and challenge-charter draft, then test them with a synthetic one-centre scenario and a candidate representative before implementing the draw.
