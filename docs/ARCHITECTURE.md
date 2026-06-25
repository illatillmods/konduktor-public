# Public Architecture Overview

Konduktor is organized as a local orchestration pipeline. This document describes the
shape of the system without exposing source code, prompts, internal heuristics, or safety
pattern lists.

## Components

### CLI Surface

The user interacts through a single local command. Commands cover initialization, status,
questions, task execution, planning, review, merge, logs, packets, quota state, inventory,
doctor checks, and VS Code task generation.

### Per-Repo State

Each target repository gets local operational state for tasks, runs, logs, reviews,
decisions, and configuration. This state is intended to stay untracked and local to the
developer machine.

### Routing Layer

Requests are classified by intent and risk before dispatch. Routing chooses a local worker
CLI based on task type, worker availability, usage state, and manual overrides.

### Worker Layer

Konduktor invokes existing local worker CLIs in non-interactive modes. Prompts are provided
through process input rather than command arguments, so stored command records do not
contain full task prompts.

### Review Layer

Review combines deterministic gates with optional model review depending on risk. Gates
cover path boundaries, secret-like additions, attribution, identity, and configured project
checks.

### Merge Layer

Accepted work can merge into local `main`. Konduktor prefers fast-forward merges, refuses
unsafe conditions, cleans up worktrees/branches after success, and does not push.

### Manual Escalation

When automated review is insufficient, Konduktor can create a redacted review packet for a
human reviewer. This is a local artifact and is not intended for publication.
