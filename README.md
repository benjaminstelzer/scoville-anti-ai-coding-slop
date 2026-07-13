# Scoville Anti-AI-Coding-Slop

Sharpens the output. Turns down the slop.

Scoville is an adaptive structural execution and review gate for AI/agent-assisted engineering. It targets both unvalidated work and "validated structural accumulation": changes that pass tests while duplicating ownership, losing boundary semantics, or publishing progress before the represented work is durable.

The skill inherits the user's and repository's workflow concern by concern, supplies compact risk-proportionate defaults only where the project is silent, and requires focused evidence plus final-diff review before completion.

## Install

Usually, let your coding agent install the skill. Send it this prompt:

```text
Install this Agent Skill from GitHub and make it available for my coding work:
https://github.com/benjaminstelzer/scoville-anti-ai-coding-slop
```

Add "for all my projects" or "only for this project" when the installation scope matters. The agent should choose its current supported skills directory, install the repository under the unchanged name `scoville-anti-ai-coding-slop`, and refresh its skill list.

Only if your agent cannot install skills itself, clone or copy the repository manually so the final path is:

```text
<skills-dir>/scoville-anti-ai-coding-slop/SKILL.md
```

Then restart or refresh the agent and confirm that `scoville-anti-ai-coding-slop` is available. Consult the agent's current documentation for its skills directory; paths differ between agents and may change over time.

## What it enforces

- explicit user and project workflow, resolved concern by concern, before skill defaults
- independent size and risk classification instead of one heavyweight process for every change
- safety and source-of-truth correctness ahead of local convenience or a smaller diff
- one canonical owner, preserved boundary semantics, and durable work before progress or publication
- the fewest meaningful behavior-complete work items, with one active item until a real stop condition
- structural checks for misleading wrappers, silent fallbacks, duplicate pathways, responsibility growth, speculative abstractions, mode creep, implementation-mirroring tests, and scaffolding presented as completion
- focused validation without manufacturing tests; fail-first is the default for defects and invariant hardening
- actual validation evidence, complete final-diff inspection, and explicit residual risk before completion
- optional decision and implementation-rationale history, searched only when current sources leave a concrete need
- scoped version-control and external actions that follow repository rules and explicit authorization

## Design

Scoville is deliberately small. Agent skills use progressive disclosure: the agent first sees only the name and description, then loads `SKILL.md` when relevant, and only loads extra resources when needed. This repo has no scripts or assets because the useful behavior fits in the main file.

The skill does not replace local instructions, architecture docs, CI, security policy, release workflow, or human review. It fills gaps where local rules are silent.

Scoville keeps the structural bar high without turning every edit into a heavyweight test project. One active work item is a work-in-progress limit, not a reason to stop the turn. Tiny changes normally reuse one focused check, proofs of concept validate only their stated hypothesis, and fail-first remains the default for actual defects and invariant hardening. Passing tests is still not enough when a change creates duplicate ownership, lossy boundaries, or state-before-durable behavior.

When a project has no established provenance mechanism, Scoville can create compact, independent fallbacks at `docs/engineering-decisions.md` and `docs/engineering-history.md`. Neither file is routine startup context; agents search it only when current sources reveal a concrete need.

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

Minimal single-skill repo. No bundled scripts, references, assets, runtime dependencies, or stack-specific rules.
