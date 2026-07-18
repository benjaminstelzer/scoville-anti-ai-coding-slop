# Changelog

## 2026-07-18: Benchmark results in the README

### Added

- Benchmark section with the 45-run delivery comparison: paired median deltas
  against a native arm, the tested LOC-Bench instances, and a short protocol
  summary.
- The introduction states the measured token savings of roughly 25 to 30
  percent at identical task quality.

## 2026-07-18: Consistent and unambiguous vocabulary

### Changed

- One term per concept: the single proving check is now always the "decisive
  check" (previously also "decisive validation", "focused validation", and
  "primary decisive check"), the persisted plan artifact is always the
  "working-plan file" (previously also "working-state file"), Trivial and Tiny
  checks are both "focused checks", the owner is always the "canonical owner",
  and the current unit of work is the "active work item".
- Resolved the elliptical precedence sentence: overrides apply concern by
  concern, and they never override higher-priority instructions, safety,
  integrity, or truthful evidence.
- Removed an ambiguous pronoun chain from the subagent planning clause and
  spelled out the work-in-progress limit.
- README trigger-test wording follows the Trivial check rename.

### Note

- `SKILL.md` and `AGENTS-SECTION.md` hashes change again; pinned benchmark arms
  must re-pin. Re-run the small-model comprehension gate before relying on the
  README's validation claim for this wording.

## 2026-07-18: Runtime and user precedence at decision points

### Changed

- Planning resolves in order: user instructions, the planning mechanism the
  runtime provides in the current context, the project's designated mechanism,
  and only then the ephemeral fallback. The fallback never runs beside another
  active planning mechanism, and the working file exists only when the plan
  must survive compaction or handoff and no available mechanism already
  preserves it.
- Subagents that cannot reach their caller's planning mechanism plan
  ephemerally and return plan-relevant state in their result; persistence
  belongs to the caller.
- Workflow inheritance names runtime-supplied rules and invoked skills as an
  explicit tier between user instructions and repository conventions.
- Rereading an unchanged file is allowed when the runtime's editing tool
  requires its own read before an edit.
- Directive files the runtime expects at standard locations for touched
  directories, such as a nested `AGENTS.md`, count as identified rather than
  discovery.
- Tiny work skips a written plan unless the user or runtime requires one.
- Creating `docs/engineering-decisions.md` defers to user or runtime approval
  requirements for new files.

### Note

- `SKILL.md` and `AGENTS-SECTION.md` hashes change with this release; pinned
  benchmark arms must re-pin their commit and hashes.

## 2026-07-18: Embeddable AGENTS.md delivery

### Added

- `AGENTS-SECTION.md`: the complete `SKILL.md` instruction body adapted for
  direct embedding in a project `AGENTS.md` or, via import, `CLAUDE.md`. The
  frontmatter is replaced by a scope sentence and the skill self-references are
  reworded; the rules themselves are unchanged.
- README section explaining when to embed the rules instead of installing the
  skill and how to share one instruction file between Codex and Claude Code.

## 2026-07-16: Validation-loop termination

### Changed

- Require a specifically named Structural or High flag before adding broader
  validation that is not already required by the repository or user.
- Make one passing decisive check terminal for its work item and proceed
  directly to one final diff and version-control status inspection.
- Make that final Git inspection operationally atomic: one command bundles
  `git diff --check`, the scoped diff, and `git status --short`; separate
  pre/post inspection commands are forbidden.
- Prohibit unchanged failed-command reruns, repeated confirmation checks, and
  additional similar tests after decisive evidence.
- Classify failed checks from their output. Infrastructure failures permit at
  most one different, narrower substitute check and remain explicitly
  unverified.
- Prevent missing dependencies or import failures from automatically escalating
  into builds, installations, code generation, or renewed repository
  exploration.

### Validation intent

- Preserve Scoville's owner, structure, safety, and evidence requirements while
  removing redundant validation and post-proof exploration.
- Treat token and runtime reductions as directional goals; correctness,
  required repository tests, and truthful residual-risk reporting remain hard
  gates.

## 2026-07-16: Bounded executable repository discovery

### Changed

- Treat runtime-supplied repository directives as already loaded and avoid
  rediscovering directive or conventional workflow files without concrete
  evidence that another exact directive applies.
- Use exact task paths directly, resolve logical owners with one targeted
  filename or symbol search, and expand discovery only when inspected evidence
  leaves a material owner, boundary, or validation question unresolved.
- Stop localization after source and its directly relevant test confirm the
  canonical owner. Do not verify an opened path with another filename search or
  reread it unchanged before editing.

### Validated

- Optimized the standalone skill with SkillOpt against executable Terra/medium
  engineering tasks. The selected frozen candidate passed development,
  validation, and held-out splits at 3/3 each.
- The original control passed the held-out behavior, canonical-owner,
  changed-file, and focused-test checks in all three cases, but reached 0/3 on
  the complete hard gate because it still performed unnecessary broad or
  post-owner exploration. The selected wording removed those failures without
  relaxing behavior, ownership, or validation requirements.
- Limited the claim to the fixed nine-case executable suite and one model/run
  configuration; it does not establish general latency, token, or product-value
  improvements.

## 2026-07-15: GPT-5.6 Luna / Low optimization and validation

### Validated

- Optimization-gated the standalone skill against GPT-5.6 Luna at low reasoning
  in an isolated Codex environment. The unchanged skill identified all required
  Scoville concerns in 10/10 single-concern cases and 10/10 compound cases with
  two or three interacting concerns.
- Kept the production-proven skill rules unchanged because the complete Luna
  test suites passed without requiring model-specific wording or branches.
- Documented the evidence boundary: these suites test pre-edit instruction
  comprehension, not executable patch quality on real repositories.

## 2026-07-13: Adaptive, risk-proportionate workflow

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
- Simplified the skill with an agent-neutral trigger, direct wording, concrete
  SC1-SC5 examples, clearer gate timing, and project-owned decision records
  while retaining the full safety and risk gates.
- Added a user-overridable working-plan fallback for likely compaction or
  handoff and one shared decision-and-rationale record when projects provide no
  mechanism.
- Defined a distinct fallback file when `PLAN.md` belongs to unrelated work and
  restored append-only supersession for semantic decision history.
- Reworked the README with concrete failure examples, installation verification,
  context-cost guidance, an accurate repository inventory, and the MIT license
  link.
- Refined the README prose, replaced em-dash punctuation, and corrected the
  classification, context-cost, and fallback-record details.

**Commits:** [`596b76b`](https://github.com/benjaminstelzer/scoville-anti-ai-coding-slop/commit/596b76bfa3856dfe226b5b8d5bb61e0f84c86ca4),
[`7706e9d`](https://github.com/benjaminstelzer/scoville-anti-ai-coding-slop/commit/7706e9d6d854dbd59c3ed11a4f59015db4ddd6eb),
[`01b4269`](https://github.com/benjaminstelzer/scoville-anti-ai-coding-slop/commit/01b42691c7e743ea685b00af293d2f0970d472e0),
[`551f790`](https://github.com/benjaminstelzer/scoville-anti-ai-coding-slop/commit/551f7900577644422dcb65e9ef038d3426769113),
[`c4a96ad`](https://github.com/benjaminstelzer/scoville-anti-ai-coding-slop/commit/c4a96adcfea83c949ba71b9a7c8f18894cc279d2),
[`8818ce8`](https://github.com/benjaminstelzer/scoville-anti-ai-coding-slop/commit/8818ce806caed79bb84a723ea3c0b901ecbbe727),
[`53c1c26`](https://github.com/benjaminstelzer/scoville-anti-ai-coding-slop/commit/53c1c265c49c2d5bbdd28cb8a43603129e969fe9)

## 2026-07-10: Structural execution and review gate

### Changed

- Renamed the Codex-facing UI entry to **Scoville Engineering Gate** and updated
  its prompt to emphasize canonical ownership, structural checks, and real
  validation evidence.
- Expanded the skill from a code-change loop into explicit Change, Review,
  Advisory, and Non-engineering modes for engineering artifacts as well as code.
- Established the `SC1`-`SC10` structural failure model, covering misleading
  wrappers, silent fallbacks, lossy boundaries, state-before-durable ordering,
  duplicate pathways, responsibility growth, speculative abstraction, mode
  creep, implementation-mirroring tests, and incomplete scaffolding.
- Added explicit owner, boundary, atomicity, dependency, failure-proof,
  completion, and residual-risk gates.

**Commits:** [`98251ac`](https://github.com/benjaminstelzer/scoville-anti-ai-coding-slop/commit/98251ac576ef7a7da3c49e7342ec641bcade0f4c),
[`2c465cf`](https://github.com/benjaminstelzer/scoville-anti-ai-coding-slop/commit/2c465cf06f3926c7406bd2cee71e4dd61487421c)

## 2026-07-08: Leaner structural workflow

### Changed

- Condensed the expanded quality gate into a smaller eight-step workflow while
  preserving owner-first changes, structural review, real validation output,
  anti-oscillation behavior, and reportable risk.
- Clarified that engineering artifacts with behavioral or contract impact use
  the same gate, while pure questions apply only the relevant safety rules.

**Commit:** [`fc0730f`](https://github.com/benjaminstelzer/scoville-anti-ai-coding-slop/commit/fc0730f6d26cefab2d514d6ef652e991545bfd86)

## 2026-07-07: Structural quality beyond green tests

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

## 2026-07-03: Execution-focused quality gate

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

## 2026-07-01: Repository metadata correction

### Fixed

- Corrected the copyright holder name in the MIT license.

**Commit:** [`702ede7`](https://github.com/benjaminstelzer/scoville-anti-ai-coding-slop/commit/702ede704e0fe7b899fe007d43680968c85332b0)

## 2026-06-29: Initial skill

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
