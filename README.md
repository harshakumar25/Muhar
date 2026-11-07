# Muhar (मुहर)

**Sealed until the gates close.**

Muhar is a proposed open-source exam-integrity protocol inspired by Devcon 8 India's [“What Can Ethereum Do for India? The Exam Leak Challenge”](https://cfp.devcon.org/devcon8/talk/QB3PET/) workshop. Its purpose is to make the choice and release of an exam paper harder to manipulate and easier to investigate. It does not claim that a blockchain can stop a human who already knows a question from leaking it.

The operating model is **one accountable exam operator, independent checks on the critical steps, and public verification of recorded evidence**. Ethereum has a narrow job: anchor a frozen, signed exam commitment and transparency-log checkpoints before the future random draw. Question text, answer keys, candidate data, and release keys stay off-chain. No token, wallet for candidates, DAO, or new chain is required.

## First build

1. `muhar-draw`: a deterministic, independently verifiable draw from a synthetic question bank and published blueprint, using a future, signature-verified randomness-beacon round.
2. `muhar-log`: a signed append-only record with inclusion and consistency proofs, independent monitors, and a minimal Ethereum anchor.
3. `muhar verify`: one command that checks the bank/metadata commitment, frozen rules, beacon proof, exact selected IDs, log proofs, and anchor. The first pilot reveals its entire synthetic bank after the mock exam.

The first real-world pilot should be a **low-stakes, single-session digital mock exam** run with a willing college or coaching partner. Live question-paper custody, threshold release, centre devices, and printing require a separate security review and institutional agreement.

## Read the design

- [PLAN.md](PLAN.md): purpose, governance, architecture, protocol, milestones, and pilot gates.
- [THREAT_MODEL.md](THREAT_MODEL.md): attacker goals, mitigations, evidence, and residual risks.

This directory currently contains a design, not deployable exam software. The project is not affiliated with any exam authority.
