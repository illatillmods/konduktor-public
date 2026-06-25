# Konduktor

Konduktor is a Mac-local, CLI-first orchestration layer for AI coding work. It is built for
developers who already use Claude Code and Codex CLI, but want a stricter workflow around
routing, isolated worktrees, review, repair, and local merge discipline.

This repository is a public mirror for product transparency and updates. It intentionally
does not contain source code, prompts, routing heuristics, safety pattern lists, internal
strategy, datasets, or deployment details.

## Status

- Private implementation: active internal product repository
- Current internal version: `0.2.0`
- Runtime: local Python CLI, no server or daemon
- Verification snapshot: 78 automated tests passing on June 25, 2026
- Public source release: not planned in this mirror

## What Konduktor Does

Konduktor turns an AI coding request into a controlled local workflow:

1. Classifies the request as a question, task, plan, review, or continuation.
2. Routes read-only work and editing work to the appropriate local worker CLI.
3. Creates an isolated `git worktree` for editing tasks.
4. Captures worker output, metadata, and review records in local per-repo state.
5. Runs deterministic safety checks and configured project checks.
6. Uses risk-aware model review where appropriate.
7. Repairs small fixable failures when policy allows.
8. Merges accepted work into local `main` when all gates pass.

Konduktor never pushes, deploys, force-merges, or runs as a hosted service.

## Verified Capabilities

The private implementation currently includes:

- `init`, `status`, `ask`, `run`, `plan`, `continue`, `dispatch`, `review`, `merge`,
  `packet`, `runs`, `logs`, `show`, `quota`, `vscode`, `inventory`, `doctor`, and
  `version` CLI surfaces.
- Isolated branch/worktree execution for editing tasks.
- Local state under `.ai/konduktor/` and `.worktrees/konduktor/` in the target repo.
- Claude Code and Codex CLI adapters using non-interactive local CLI modes.
- Model/effort metadata reporting, with warnings when exact model selection cannot be
  verified from the local CLI/config.
- Deterministic review gates for forbidden paths, common secret patterns, attribution,
  identity, and configured test/lint/build commands.
- A redacted manual review packet for escalation to a human reviewer.
- VS Code task generation that opens only a status/watch terminal on folder open.

No performance benchmark is currently published for Konduktor, and this mirror makes no
latency, quality, or cost-reduction claims.

## Safety Posture

Konduktor is designed around conservative local automation:

- Workers are instructed not to commit, push, deploy, or touch secrets.
- Konduktor authors commits with the user's configured human git identity.
- AI/co-author/generated-by attribution is stripped or blocked before merge.
- Accepted work is merged locally only after review passes.
- High-risk, ambiguous, or exhausted-worker situations are routed back to the human.
- Review packets redact obvious secret-looking material before manual escalation.

This is a safety net for local development, not a guarantee that every possible bad edit or
secret format can be detected automatically. Users still review diffs.

## Public Mirror Boundaries

Included here:

- Product overview
- Public architecture summary
- Verified behavior summary
- Security and disclosure notes
- FAQ
- Public roadmap
- Copy-protection notice

Excluded by design:

- Source code
- Prompt templates and system instructions
- Routing, risk, and repair heuristics
- Secret-scanning patterns
- Internal test fixtures
- Operational logs, worker outputs, review packets, and local state
- Private strategy, pricing, customer, or deployment material

## Audience

Konduktor is a developer tool for experienced local-first engineers who want AI coding
assistance constrained by Git hygiene, review discipline, and explicit human control over
publication.

