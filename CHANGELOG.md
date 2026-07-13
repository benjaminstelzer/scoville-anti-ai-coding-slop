# Changelog

## 2026-07-13 — Adaptive, risk-proportionate workflow

### Changed

- Made Scoville inherit user and repository workflows concern by concern, with
  compact fallback rules only where the project is silent.
- Separated change size from structural and high-risk classification so small
  edits stay lightweight without weakening safety, ownership, boundary,
  atomicity, or validation requirements.
- Reframed execution around behavior-complete work items, real stop conditions,
  focused evidence, final-diff review, and explicit residual risk.
- Aligned the README with the current engineering gate and replaced the
  agent-specific manual installation matrix with one agent-install prompt plus
  a short manual fallback.

**Commits:** [`596b76b`](https://github.com/benjaminstelzer/scoville-anti-ai-coding-slop/commit/596b76bfa3856dfe226b5b8d5bb61e0f84c86ca4),
[`7706e9d`](https://github.com/benjaminstelzer/scoville-anti-ai-coding-slop/commit/7706e9d6d854dbd59c3ed11a4f59015db4ddd6eb)

## 2026-07-10 — Structural execution and review gate

### Changed

- Renamed the Codex-facing UI entry to **Scoville Engineering Gate** and updated
  its prompt to emphasize canonical ownership, structural checks, and real
  validation evidence.
- Expanded the skill from a code-change loop into explicit Change, Review,
  Advisory, and Non-engineering modes for engineering artifacts as well as code.
- Established the `SC1`–`SC10` structural failure model, covering misleading
  wrappers, silent fallbacks, lossy boundaries, state-before-durable ordering,
  duplicate pathways, responsibility growth, speculative abstraction, mode
  creep, implementation-mirroring tests, and incomplete scaffolding.
- Added explicit owner, boundary, atomicity, dependency, failure-proof,
  completion, and residual-risk gates.

**Commits:** [`98251ac`](https://github.com/benjaminstelzer/scoville-anti-ai-coding-slop/commit/98251ac576ef7a7da3c49e7342ec641bcade0f4c),
[`2c465cf`](https://github.com/benjaminstelzer/scoville-anti-ai-coding-slop/commit/2c465cf06f3926c7406bd2cee71e4dd61487421c)

## 2026-07-08 — Leaner structural workflow

### Changed

- Condensed the expanded quality gate into a smaller eight-step workflow while
  preserving owner-first changes, structural review, real validation output,
  anti-oscillation behavior, and reportable risk.
- Clarified that engineering artifacts with behavioral or contract impact use
  the same gate, while pure questions apply only the relevant safety rules.

**Commit:** [`fc0730f`](https://github.com/benjaminstelzer/scoville-anti-ai-coding-slop/commit/fc0730f6d26cefab2d514d6ef652e991545bfd86)

## 2026-07-07 — Structural quality beyond green tests

### Added

- Introduced explicit structural failure modes and pre- and post-edit structure
  review for code-judo opportunities, file-size signals, atomicity, lossy
  boundaries, misleading wrappers, and failure-mode tests.
- Added holistic branch-diff review and stronger completion checks so passing
  tests alone could not approve structurally harmful changes.

### Documentation

- Expanded the README to explain Scoville's structural-quality focus.

**Commits:** [`703f97b`](https://github.com/benjaminstelzer/scoville-anti-ai-coding-slop/commit/703f97bfdce236d5e96c8066d5df0d3ca8b43608),
[`f71d38d`](https://github.com/benjaminstelzer/scoville-anti-ai-coding-slop/commit/f71d38d28c75a87ff919745cf9e723f2f09f482c)

## 2026-07-03 — Execution-focused quality gate

### Changed

- Reworked the original checklist into an execution-first workflow with task
  classification, planning, source-of-truth discovery, milestone progress,
  evidence-backed validation, handoff context, and anti-oscillation rules.
- Iterated that workflow into a fixed classify, plan, locate owner, edit,
  validate, self-check, and report loop with concrete banned patterns.
- Strengthened edit and validation rules with read-before-edit, conflict
  detection, surgical changes, dependency approval, fail-first defect proof,
  narrow-to-broad checks, and repository-owned version-control policy.

**Commits:** [`4f2028e`](https://github.com/benjaminstelzer/scoville-anti-ai-coding-slop/commit/4f2028ec5fc4759d7cb6644e301992aa3aed5dc9),
[`24148db`](https://github.com/benjaminstelzer/scoville-anti-ai-coding-slop/commit/24148dbdf2e4bc8e311436d256853427fc7f7478),
[`ddb8d91`](https://github.com/benjaminstelzer/scoville-anti-ai-coding-slop/commit/ddb8d91d2b645ea784a1346e89df56be95bfccbf)

## 2026-07-01 — Repository metadata correction

### Fixed

- Corrected the copyright holder name in the MIT license.

**Commit:** [`702ede7`](https://github.com/benjaminstelzer/scoville-anti-ai-coding-slop/commit/702ede704e0fe7b899fe007d43680968c85332b0)

## 2026-06-29 — Initial skill

### Added

- Published the first README and anti-AI-slop quality-gate definition.
- Added the MIT license and Codex UI metadata.
- Added the Scoville tagline, installation guidance for compatible agents, and
  a curated source and inspiration list.

**Commits:** [`d8d9a1c`](https://github.com/benjaminstelzer/scoville-anti-ai-coding-slop/commit/d8d9a1cd6e85ca8cd9b484061125cf193052744c),
[`2915ef7`](https://github.com/benjaminstelzer/scoville-anti-ai-coding-slop/commit/2915ef7eb0418041d856820ab4ef3cfc523223f6),
[`1583888`](https://github.com/benjaminstelzer/scoville-anti-ai-coding-slop/commit/1583888119028d58e78e233bef68c198a6148748),
[`2045e8c`](https://github.com/benjaminstelzer/scoville-anti-ai-coding-slop/commit/2045e8c7700768ad82ca1ace08598c2b713965da),
[`b1614b6`](https://github.com/benjaminstelzer/scoville-anti-ai-coding-slop/commit/b1614b65076186e107ea571c1fc713aa67310a28),
[`750630b`](https://github.com/benjaminstelzer/scoville-anti-ai-coding-slop/commit/750630b5abc05278590910f8a1ec98e281d78c2a),
[`c133db9`](https://github.com/benjaminstelzer/scoville-anti-ai-coding-slop/commit/c133db9f8d9b5dcfbfb6fb53b79bff02fea15a54)
