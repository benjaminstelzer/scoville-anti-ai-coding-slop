# Scoville Anti-AI-Coding-Slop

Sharpens the output. Turns down the slop.

We have all seen it:

- Your agent reports "✅ All tests pass" but never ran them.
- You asked for a bugfix and got 400 lines of test scaffolding around a
  one-line change.
- A second helper appears even though the same helper already exists three
  files away.
- The diff is green, the PR merges, and the system is a little harder to
  understand than before.

That is AI slop: motion without progress toward what you actually asked for.
Scoville is an Agent Skill that keeps your coding agent optimizing for the
requested observable outcome. Correctness, structure, and validation act as
delivery constraints, not as substitute deliverables, so you get the behavior
you asked for, proven honestly, without every one-line edit turning into a
process. A one-line fix should not arrive wrapped in a seven-section plan. It
has, historically.

It targets both failure directions: unvalidated work, where success is claimed
without evidence, and process theater, where the agent produces tests, plans,
refactors, and documentation instead of the requested behavior. It follows your
rules and your repository's conventions concern by concern, then supplies
compact defaults only where they are silent.

## Why "Scoville"?

The original Scoville test measured how far chili extract could be diluted
before trained tasters could no longer detect the heat. AI slop works the same
way in reverse: real engineering gets diluted with scaffolding, filler tests,
and unproven claims until no actual progress is detectable. This skill measures,
and limits, that dilution. It is the one Scoville scale where you want the
heat.

## Install

Works with any coding agent that supports the Agent Skills format (`SKILL.md`
with name/description frontmatter), including Claude Code and Codex.

Usually, let your coding agent install the skill. Send it this prompt:

```text
Install this Agent Skill from GitHub and make it available for my coding work:
https://github.com/benjaminstelzer/scoville-anti-ai-coding-slop
```

Add "for all my projects" or "only for this project" when the installation
scope matters. The agent should choose its supported skills directory,
install the repository under the unchanged name
`scoville-anti-ai-coding-slop`, and refresh its skill list.

If your agent cannot install skills itself, clone or copy the repository so the
final path is:

```text
<skills-dir>/scoville-anti-ai-coding-slop/SKILL.md
```

For Claude Code, `<skills-dir>` is `~/.claude/skills/` for all projects or
`.claude/skills/` inside a repository for that project only. For other agents,
consult their documentation; paths differ per agent.

**Verify it works.** Skills load on demand, so test the trigger. Ask your agent:
*"Per Scoville, which mode applies to renaming one purely local variable with no
behavior or contract effect, and how should it be validated?"* When neither user
nor repository rules replace Scoville's defaults, you should get **Develop**
with at most one existing focused check: no plan, no new test, no broad suite.

**What it costs.** `SKILL.md` currently contains roughly 1,700 words. A
compatible agent loads the instructions when the skill triggers, although exact
context accounting depends on the agent. Installing it per project limits where
it is available; it does not reduce the cost of an individual invocation.

## Use via AGENTS.md instead of a skill

Skills load on demand: the agent sees name and description first and reads the
full rules only when the task triggers them. If your agent does not support
skills, or you want the rules active from the very first action, embed Scoville
directly in your project instructions instead.

Append the content of [AGENTS-SECTION.md](AGENTS-SECTION.md) to your project's
instruction file: `AGENTS.md` for Codex, `CLAUDE.md` for Claude Code.

> [!WARNING]
> Do not install the skill and embed the section in the same project: one
> delivery mechanism is enough. Two copies can drift apart, and when the skill
> triggers, the same rules load into context twice and cost additional tokens.

`AGENTS-SECTION.md` contains the same rules as `SKILL.md`; only the packaging
differs, so both delivery forms enforce identical behavior. The file is
regenerated whenever `SKILL.md` changes.

## What it enforces

- **Goal-first delivery.** After safety and explicit constraints, the agent
  optimizes for the requested observable outcome. When work starts producing
  only tests, process artifacts, documentation, or internal cleanup without
  advancing the outcome or closing a named risk, that line of work stops.
- **Evidence over claims.** Validation continues exactly as long as another
  check could plausibly change the implementation or completion decision, and
  behavior that was not observed is never claimed. A failed check is presumed
  substantive and caused by the change unless specific evidence shows it is
  pre-existing or environmental. An infrastructure failure permits one
  different substitute check rather than an environment-probing loop. Decisive
  evidence ends validation for that behavior and leads to one coherent final
  Git inspection. Two consecutive failed attempts against the same substantive
  check force a change of approach instead of a third blind patch.
- **Modes instead of one ceremony.** Advisory, Review, Explore, Develop, and
  Harden separate answering, inspecting, experimenting, ordinary delivery, and
  release gating. Touching a central file, public API, or existing test suite
  alone never escalates Develop to Harden, and prototype code kept beyond an
  experiment must meet Develop validation before completion is claimed.
- **A hard integrity floor.** Misleading wrappers, silent fallbacks, lossy
  projections, progress published before the work is durable, and duplicate
  owners that bypass canonical invariants are never introduced. Maintainability
  smells are review signals resolved when the active change worsens them
  materially, not automatic blockers.
- **No artifact economy.** No automatic plan files or decision logs. Material
  decisions go into the project's existing plan, ADR, or pull-request
  mechanism; a handoff across interruption or compaction records only the
  requested outcome, current state, decisive evidence, and next concrete step.

The full rules live in [SKILL.md](SKILL.md).

## Design

Scoville is deliberately small: this repo has no scripts or assets because the
useful behavior fits in the instruction file.

The skill does not replace your instructions, architecture docs, CI, security
policy, release workflow, or human review. It resolves every workflow concern
in a fixed order: explicit instructions for the current request, current
runtime requirements, repository directives and conventions, then its own
default. This lets it fill gaps instead of fighting your `AGENTS.md`. A project
convention can replace any Scoville default, but it can never justify
fabricated evidence or weakened guards.

Earlier versions maintained their own working-plan file, decision log, and
completion templates. Practical use exposed the Goodhart failure in that
design: agents increasingly optimized for producing plans, tests, and
defensible process instead of advancing the requested outcome. The anti-slop
skill had started producing slop of its own, which was at least on topic. The
current
goal-first version therefore creates no artifacts of its own. If a repository
designates an authoritative plan, that plan is the sole planning state; a
runtime that requires its own plan tool receives only a disposable mirror of
it. Material decisions, meaning changes to outcome, scope, ownership, public
contracts, data or security posture, reversibility, or validation limits, are
recorded in the mechanisms your project already has, never in a new parallel
one.

## Sources and inspirations

The skill draws from the following sources:

- [OpenAI coding-agent best practices](https://developers.openai.com/codex/learn/best-practices): goal/context/constraints/done-when prompts, planning before complex work, tight permissions, focused checks, and diff review.
- [Cursor Thermo-Nuclear Code Quality Review Skill](https://github.com/cursor/plugins/blob/main/cursor-team-kit/skills/thermo-nuclear-code-quality-review/SKILL.md): strict maintainability review, code-judo simplification, 1k-line guard, anti-spaghetti review, canonical ownership, boundary cleanliness, wrapper skepticism, atomicity concerns, and branch-wide structural approval.
- [OWASP Top 10 for LLM Applications 2025](https://genai.owasp.org/llm-top-10/): prompt injection, sensitive-information disclosure, supply-chain risk, improper output handling, and excessive agency.
- [OWASP LLM01 Prompt Injection](https://genai.owasp.org/llmrisk/llm01-prompt-injection/) and [LLM06 Excessive Agency](https://genai.owasp.org/llmrisk/llm062025-excessive-agency/): least privilege, human approval for high-risk actions, untrusted external content, and deterministic safeguards.
- [Andrej Karpathy on vibe coding](https://x.com/karpathy/status/1886192184808149383): natural-language software construction is powerful, but production engineering still needs scope, review, testing, taste, and ownership.
- Simon Willison's distinction between vibe coding and reviewed, tested,
  understood AI-assisted coding: Scoville is for the latter.
- Martin Fowler on [internal quality](https://martinfowler.com/articles/is-quality-worth-cost.html) and [technical debt](https://martinfowler.com/bliki/TechnicalDebt.html): maintainability is a delivery property, not polish.
- Recent research on AI/vibe-coding quality: [Vibe Coding in Practice](https://arxiv.org/abs/2510.00328), [VibeContract](https://arxiv.org/abs/2603.15691), and [Is Vibe Coding Safe?](https://arxiv.org/abs/2512.03262).

## Status

Minimal single-skill repo: `SKILL.md`, the embeddable `AGENTS-SECTION.md`
variant, agent metadata (`agents/openai.yaml`), changelog, and license. No
bundled scripts, references, assets, runtime dependencies, or stack-specific
rules.

Benchmark and small-model validation results published for earlier versions
were removed from this README: they measured the previous rule set and will be
re-run against the current goal-first rules before any efficiency claim
returns. Quoting them anyway would have been exactly the kind of claim this
skill exists to stop.

## License

MIT - see [LICENSE](LICENSE).
