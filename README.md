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

That is AI slop: motion without progress. Scoville is an Agent Skill that makes
your coding agent prove its work, stay in scope, and keep the structure honest,
without turning every one-line edit into a process.

It targets both failure directions: unvalidated work, where success is claimed
without evidence, and structural debt that hides behind green tests, such as
duplicate ownership, lost boundary semantics, or progress published before the
work is durable. It follows your rules and your repository's conventions
concern by concern, then supplies compact, risk-proportionate defaults only
where they are silent.

## Why "Scoville"?

The original Scoville test measured how far chili extract could be diluted
before trained tasters could no longer detect the heat. AI slop works the same
way in reverse: real engineering gets diluted with scaffolding, filler tests,
and unproven claims until no actual progress is detectable. This skill measures,
and limits, that dilution.

The ten structural failure modes carry SC numbers (SC1-SC10). Here, SC stands
for "structural concern." The more SC findings your diff collects, the more it
burns on review.

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
*"Classify this change per Scoville: rename one purely local variable with no
behavior or contract effect."* When neither user nor repository rules replace
Scoville's classification, you should get **Trivial**: no plan, no new test, and
one natural narrow check when one exists.

**What it costs.** `SKILL.md` currently contains roughly 2,600 words. A
compatible agent loads the instructions when the skill triggers, although exact
context accounting depends on the agent. Installing it per project limits where
it is available; it does not reduce the cost of an individual invocation.

**Small-model validation.** Scoville was tested against GPT-5.6 Luna at low
reasoning in an isolated Codex environment, to check whether small models need
extra rules. They do not: the unchanged skill identified all required Scoville
concerns in 10/10 single-concern cases and 10/10 compound cases with two or
three interacting concerns. These tests establish instruction comprehension before editing; they do
not by themselves establish the quality of executable patches on real
repositories.

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
regenerated whenever `SKILL.md` changes. A benchmark comparing the two delivery
mechanisms is in progress; results will be added here.

## What it enforces

- **Evidence over claims.** Every validation claim needs the actual check,
  outcome, and proof. Commands include their exit code. `NOT RUN` is a valid
  report for a relevant expected check; invented output never is. Green tests
  alone do not approve structure.
- **Scope discipline.** One behavior-complete work item at a time, the fewest
  items the outcome needs, no unrelated cleanup, and a full final-diff
  inspection before completion. Stopping requires a real stop condition, not
  just a finished sub-step.
- **Structural honesty.** Ten named failure modes (SC1-SC10) cover misleading
  wrappers, silent fallbacks, lossy boundaries, state published before durable
  work, duplicate pathways, responsibility growth, speculative abstraction,
  mode creep, implementation-mirroring tests, and scaffolding presented as
  completion. Introduced findings block
  completion.
- **Proportionate process.** Changes are classified by size (Trivial / Tiny /
  Standard) and risk (Structural / High) independently. Trivial edits get one
  narrow check when one exists, not a plan. Tests target defects, invariants,
  and risky contracts rather than decorating a diff. Plans stay ephemeral by
  default; explicit user or project rules and long work that must survive
  context compaction can make them persistent.

The full rules live in [SKILL.md](SKILL.md).

## Design

Scoville is deliberately small: this repo has no scripts or assets because the
useful behavior fits in the instruction file.

The skill does not replace your instructions, architecture docs, CI, security
policy, release workflow, or human review. It resolves every workflow concern
in a fixed order: explicit user instruction first, then repository convention,
then its own default. This lets it fill gaps instead of fighting your
`AGENTS.md`. A project convention can replace any Scoville default, but it can
never justify fabricated evidence or weakened guards.

Two mechanisms handle long-running work. When a multi-item plan must survive
context compaction or handoff and the project provides no mechanism, Scoville
maintains one working-plan file, re-reads canonical sources before the plan
after resuming, and removes the file at completion only when Scoville created it
and neither the user nor repository requires retention. The file stays
uncommitted unless the user or repository tracks plans. Material decisions are
recorded in the project's own mechanism when one exists. Otherwise, an already
authorized commit message or pull-request description carries the record when
available; if not, `docs/engineering-decisions.md` is the single fallback log.

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

## License

MIT - see [LICENSE](LICENSE).
