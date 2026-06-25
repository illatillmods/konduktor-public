# Konduktor

Konduktor is a Mac-local command line control layer for AI coding work.

It is built for developers who already use Claude Code and Codex CLI, but want
the workflow to stop being a loose chat window pointed at a repo. Konduktor adds
routing, isolated worktrees, deterministic review gates, repair loops, local
merge discipline, and clean human authorship.

This repository is a public mirror for product transparency. It intentionally
does not contain source code, prompts, routing heuristics, safety pattern lists,
internal strategy, datasets, worker output, or deployment detail.

## Snapshot

Verified from the private implementation on June 25, 2026:

| Area | Public-safe status |
| --- | --- |
| Private implementation | Active internal product repository. |
| Current internal version | `0.2.0`. |
| Runtime shape | Local Python CLI; no server, daemon, hosted worker, or web app. |
| Worker surface | Claude Code and Codex CLI adapters using local non-interactive CLI modes. |
| Verification | 78 automated tests passing in the private workspace. |
| Public source release | Not planned in this mirror. |

## What It Does

Konduktor turns an AI coding request into a controlled local workflow:

1. Classify the request as a question, task, plan, review, or continuation.
2. Route read-only and editing work to the appropriate local worker CLI.
3. Create an isolated `git worktree` for editing tasks.
4. Capture worker output, metadata, logs, and review records in local per-repo
   state.
5. Run deterministic safety checks and configured project checks.
6. Use risk-aware model review where appropriate.
7. Repair small fixable failures when policy allows.
8. Merge accepted work into local `main` when all gates pass.

It never pushes, deploys, force-merges, or becomes a hosted service.

## Why It Exists

AI coding tools are powerful, but the last mile is still engineering discipline:
who touched the repo, where the diff landed, what checks ran, whether secrets
leaked, whether attribution got injected, and whether a human can inspect the
result before publication.

Konduktor treats those concerns as the product, not as cleanup after the fact.

## Verified Capability Surface

The private implementation currently includes CLI surfaces for:

- `init`, `status`, `ask`, `run`, `plan`, `continue`, `dispatch`, `review`, and
  `merge`
- `packet`, `runs`, `logs`, `show`, `quota`, `vscode`, `inventory`, `doctor`,
  and `version`
- isolated branch/worktree execution for editing tasks
- per-repo state under `.ai/konduktor/` and `.worktrees/konduktor/`
- model/effort metadata reporting with warnings when exact model selection
  cannot be verified from the local CLI/config
- deterministic review gates for forbidden paths, common secret patterns,
  attribution, identity, and configured test/lint/build commands
- redacted manual review packets for escalation to a human reviewer
- VS Code task generation that opens only a status/watch terminal on folder open

No performance benchmark is currently published for Konduktor, and this mirror
makes no latency, quality, or cost-reduction claims.

## Safety Posture

Konduktor is intentionally conservative:

- Workers are instructed not to commit, push, deploy, or touch secrets.
- Konduktor authors commits with the user's configured human git identity.
- AI/co-author/generated-by attribution is stripped or blocked before merge.
- Accepted work is merged locally only after review passes.
- High-risk, ambiguous, or exhausted-worker situations route back to the human.
- Review packets redact obvious secret-looking material before manual escalation.

This is a safety net for local development, not proof that every possible bad
edit or secret format can be detected automatically. Users still review diffs.

## Public Mirror Contents

- Product overview and verified behavior summary.
- [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md) - public architecture summary.
- [docs/VERIFIED_BEHAVIOR.md](docs/VERIFIED_BEHAVIOR.md) - verified public behavior notes.
- [ROADMAP.md](ROADMAP.md) - roadmap and limits.
- [SECURITY.md](SECURITY.md) - security and disclosure notes.
- [FAQ.md](FAQ.md) - public answers.
- [NOTICE.md](NOTICE.md) - copy-protection notice.

## Audience

Konduktor is for experienced local-first engineers who want AI coding assistance
constrained by Git hygiene, review discipline, and explicit human control over
publication.
