# Scoville Anti-AI-Coding-Slop

Sharpens the output. Turns down the slop.

Anti-AI-slop quality gate for AI/agent-assisted engineering. Apply it while editing, reviewing, refactoring, testing, or planning code, so scope control, correctness, minimal diffs, source-of-truth discipline, validation, reviewability, and safe version-control hygiene stay explicit.

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

- scope before work
- one canonical owner and one source of truth
- smallest useful diff
- no parallel pathways or speculative abstractions
- least privilege and prompt-injection resistance
- validation evidence before completion
- independent final review for security, edge cases, architecture drift, and diff quality
- version-control hygiene only when version control is present or explicitly requested

## Design

Scoville is deliberately small. Agent skills use progressive disclosure: the agent first sees only the name and description, then loads `SKILL.md` when relevant, and only loads extra resources when needed. This repo has no scripts or assets because the useful behavior fits in the main file.

The skill does not replace local instructions, architecture docs, CI, security policy, release workflow, or human review. It fills gaps where local rules are silent.

## Sources and inspirations

The skill synthesizes the following sources:

- [OpenAI coding-agent best practices](https://developers.openai.com/codex/learn/best-practices): goal/context/constraints/done-when prompts, planning before complex work, tight permissions, focused checks, and diff review.
- [OWASP Top 10 for LLM Applications 2025](https://genai.owasp.org/llm-top-10/): prompt injection, sensitive-information disclosure, supply-chain risk, improper output handling, and excessive agency.
- [OWASP LLM01 Prompt Injection](https://genai.owasp.org/llmrisk/llm01-prompt-injection/) and [LLM06 Excessive Agency](https://genai.owasp.org/llmrisk/llm062025-excessive-agency/): least privilege, human approval for high-risk actions, untrusted external content, and deterministic safeguards.
- [Andrej Karpathy on vibe coding](https://x.com/karpathy/status/1886192184808149383): natural-language software construction is powerful, but production engineering still needs scope, review, testing, taste, and ownership.
- Simon Willison's distinction between vibe coding and reviewed, tested, understood AI-assisted coding: Scoville is for the latter.
- Martin Fowler on [internal quality](https://martinfowler.com/articles/is-quality-worth-cost.html) and [technical debt](https://martinfowler.com/bliki/TechnicalDebt.html): maintainability is a delivery property, not polish.
- Recent research on AI/vibe-coding quality: [Vibe Coding in Practice](https://arxiv.org/abs/2510.00328), [VibeContract](https://arxiv.org/abs/2603.15691), and [Is Vibe Coding Safe?](https://arxiv.org/abs/2512.03262).

## Status

Minimal single-skill repo. No bundled scripts, references, assets, runtime dependencies, or stack-specific rules.
