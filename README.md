# Scoville Anti-AI-Coding-Slop

Sharpens the output. Turns down the slop.

You know the pattern:

- Your agent reports "✅ All tests pass" — but never ran them.
- You asked for a bugfix and got 400 lines of test scaffolding around a
  one-line change.
- A second helper appears that duplicates one that already existed, three
  files away.
- The diff is green, the PR merges, and the system is a little harder to
  understand than before.

That's AI slop: motion without progress. Scoville is an Agent Skill that makes
your coding agent prove its work, stay in scope, and keep structure honest —
without turning every one-line edit into a process.

It targets both failure directions: unvalidated work (success claims without
evidence) and structural debt that hides behind green tests (duplicate
ownership, lost boundary semantics, progress published before the work is
durable). It inherits your own rules and your repository's conventions concern
by concern, and supplies compact risk-proportionate defaults only where they
are silent.

## Why "Scoville"?

The Scoville scale measures how far you can dilute a chili before the heat
becomes undetectable. AI slop works the same way in reverse: real engineering,
diluted with scaffolding, filler tests, and unproven claims, until no actual
progress is detectable. This skill measures — and limits — the dilution.

The ten structural failure modes carry SC numbers (SC1–SC10). Officially that
stands for "structural concern". Unofficially, yes: the higher your diff
scores, the more it burns on review.

## Install

Works with any coding agent that supports the Agent Skills format (`SKILL.md`
with name/description frontmatter), e.g. Claude Code and Codex.

Usually, let your coding agent install the skill. Send it this prompt:

```text
Install this Agent Skill from GitHub and make it available for my coding work:
https://github.com/benjaminstelzer/scoville-anti-ai-coding-slop
```

Add "for all my projects" or "only for this project" when the installation
scope matters. The agent should choose its current supported skills directory,
install the repository under the unchanged name
`scoville-anti-ai-coding-slop`, and refresh its skill list.

If your agent cannot install skills itself, clone or copy the repository so
the final path is:

```text
<skills-dir>/scoville-anti-ai-coding-slop/SKILL.md
```

For Claude Code, `<skills-dir>` is `~/.claude/skills/` (all projects) or
`.claude/skills/` inside a repository (that project only). For other agents,
consult their current documentation — paths differ and change over time.

**Verify it works.** Skills load on demand, so test the trigger. Ask your
agent: *"Classify this change per Scoville: rename one local variable in one
file."* In a repository without a stricter planning rule, you should get
**Trivial** — no plan, no new test, one narrow check. If instead it proposes a
work plan, first confirm that no user or repository rule requires one.

**What it costs.** The skill puts roughly 2,100 words into context whenever it
triggers — which, by design, is most engineering tasks. That is the price of
the gate. If your context budget is tight, install it per-project rather than
globally.

## What it enforces

- **Evidence over claims.** Every validation claim needs the actual check,
  outcome, and proof — commands include their exit code. `NOT RUN` is a valid
  report; invented output never is. Green tests alone don't approve structure.
- **Scope discipline.** One behavior-complete work item at a time, the fewest
  items the outcome needs, no unrelated cleanup, and a full final-diff
  inspection before completion. Stopping requires a real stop condition — not
  just a finished sub-step.
- **Structural honesty.** Ten named failure modes (SC1–SC10) cover misleading
  wrappers, silent fallbacks, lossy boundaries, state published before durable
  work, duplicate pathways, speculative abstraction, implementation-mirroring
  tests, and scaffolding presented as completion. Introduced findings block
  completion.
- **Proportionate process.** Changes are classified by size (Trivial / Tiny /
  Standard) and risk (Structural / High) independently. Trivial edits get one
  narrow check, not a plan. Tests target defects, invariants, and risky
  contracts — not decorating a diff. Plans stay ephemeral by default; explicit
  user or project rules and long work that must survive context compaction can
  make them persistent.

The full rules live in [SKILL.md](SKILL.md).

## Design

Scoville is deliberately small. Agent skills use progressive disclosure: the
agent first sees only the name and description, then loads `SKILL.md` when
relevant. This repo has no scripts or assets because the useful behavior fits
in the main file.

The skill does not replace your instructions, architecture docs, CI, security
policy, release workflow, or human review. It resolves every workflow concern
in a fixed order — explicit user instruction first, then repository
convention, then its own default — so it fills gaps instead of fighting your
`AGENTS.md`. A project convention can replace any Scoville default; it can
never justify fabricated evidence or weakened guards.

Two mechanisms handle long-running work. When a multi-item plan must survive
context compaction or handoff and the project provides no mechanism, Scoville
maintains one uncommitted working plan file, re-reads canonical sources before
the plan after resuming, and removes the file at completion only when Scoville
created it and neither the user nor repository requires retention. Material
decisions are recorded in the project's own mechanism (ADRs, PR descriptions,
commit messages) when one exists; otherwise a single
`docs/engineering-decisions.md` is the only fallback log it will ever create.

## Sources and inspirations

The skill synthesizes the following sources:

- [OpenAI coding-agent best practices](https://developers.openai.com/codex/learn/best-practices): goal/context/constraints/done-when prompts, planning before complex work, tight permissions, focused checks, and diff review.
- [Cursor Thermo-Nuclear Code Quality Review Skill](https://github.com/cursor/plugins/blob/main/cursor-team-kit/skills/thermo-nuclear-code-quality-review/SKILL.md): strict maintainability review, code-judo simplification, 1k-line guard, anti-spaghetti review, canonical ownership, boundary cleanliness, wrapper skepticism, atomicity concerns, and branch-wide structural approval.
- [OWASP Top 10 for LLM Applications 2025](https://genai.owasp.org/llm-top-10/): prompt injection, sensitive-information disclosure, supply-chain risk, improper output handling, and excessive agency.
- [OWASP LLM01 Prompt Injection](https://genai.owasp.org/llmrisk/llm01-prompt-injection/) and [LLM06 Excessive Agency](https://genai.owasp.org/llmrisk/llm062025-excessive-agency/): least privilege, human approval for high-risk actions, untrusted external content, and deterministic safeguards.
- [Andrej Karpathy on vibe coding](https://x.com/karpathy/status/1886192184808149383): natural-language software construction is powerful, but production engineering still needs scope, review, testing, taste, and ownership.
- Simon Willison's distinction between vibe coding and reviewed, tested, understood AI-assisted coding: Scoville is for the latter.
- Martin Fowler on [internal quality](https://martinfowler.com/articles/is-quality-worth-cost.html) and [technical debt](https://martinfowler.com/bliki/TechnicalDebt.html): maintainability is a delivery property, not polish.
- Recent research on AI/vibe-coding quality: [Vibe Coding in Practice](https://arxiv.org/abs/2510.00328), [VibeContract](https://arxiv.org/abs/2603.15691), and [Is Vibe Coding Safe?](https://arxiv.org/abs/2512.03262).

## Status

Minimal single-skill repo: `SKILL.md` plus agent metadata (`agents/openai.yaml`),
changelog, and license. No bundled scripts, references, assets, runtime
dependencies, or stack-specific rules.

## License

MIT — see [LICENSE](LICENSE).
