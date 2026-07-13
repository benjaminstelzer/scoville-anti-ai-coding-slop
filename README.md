# Scoville Anti-AI-Coding-Slop

Sharpens the output. Turns down the slop.

Adaptive anti-AI-slop quality gate for AI/agent-assisted engineering. It inherits the user's and repository's workflow concern by concern, then supplies compact, risk-proportionate defaults only where the project is silent.

## Install

This repository contains one Agent Skill. Its root is the skill directory:

```text
scoville-anti-ai-coding-slop/
├── SKILL.md
├── LICENSE
├── README.md
└── agents/
    └── openai.yaml
```

The skill name listed in `SKILL.md` matches the directory and repository name. The file follows the standard `SKILL.md` shape: YAML frontmatter with `name` and `description`, followed by Markdown instructions. `agents/openai.yaml` is optional Codex UI metadata.

Codex project install:

```bash
mkdir -p .agents/skills
git clone https://github.com/benjaminstelzer/scoville-anti-ai-coding-slop .agents/skills/scoville-anti-ai-coding-slop
```

Codex personal install:

```bash
mkdir -p ~/.agents/skills
git clone https://github.com/benjaminstelzer/scoville-anti-ai-coding-slop ~/.agents/skills/scoville-anti-ai-coding-slop
```

GitHub Copilot project install:

```bash
mkdir -p .github/skills
git clone https://github.com/benjaminstelzer/scoville-anti-ai-coding-slop .github/skills/scoville-anti-ai-coding-slop
```

GitHub Copilot personal install:

```bash
mkdir -p ~/.copilot/skills
git clone https://github.com/benjaminstelzer/scoville-anti-ai-coding-slop ~/.copilot/skills/scoville-anti-ai-coding-slop
```

Claude Code project install:

```bash
mkdir -p .claude/skills
git clone https://github.com/benjaminstelzer/scoville-anti-ai-coding-slop .claude/skills/scoville-anti-ai-coding-slop
```

Claude Code personal install:

```bash
mkdir -p ~/.claude/skills
git clone https://github.com/benjaminstelzer/scoville-anti-ai-coding-slop ~/.claude/skills/scoville-anti-ai-coding-slop
```

For compatible agents that use a different skills directory, clone or copy the repository folder so the final path is:

```text
<skills-dir>/scoville-anti-ai-coding-slop/SKILL.md
```

Then restart or refresh the agent and confirm `scoville-anti-ai-coding-slop` is available.

## What it enforces

- user and project workflow before skill defaults
- continuous execution across planned work items until a real stop condition
- one canonical owner and one source of truth
- the fewest behavior-complete work items
- no parallel pathways or speculative abstractions
- structural quality beyond green tests
- file size as a review signal rather than an automatic split
- local simplification only when it supports the requested result
- no misleading wrappers or semantic pass-through layers
- no lossy boundaries where already-computed semantics disappear
- atomic state, cursor, checkpoint, cache, and progress publication
- fail-first regression proof for defects and invariant hardening
- focused validation without manufacturing tests for trivial or exploratory work
- optional, on-demand decision and implementation-rationale history
- separate fallback paths for decisions and rationale when the project has none
- least privilege and prompt-injection resistance
- validation evidence before completion
- version-control hygiene only when version control is present or explicitly requested

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
