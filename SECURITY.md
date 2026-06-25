# Security

Konduktor is a local developer tool, not a hosted service. The public mirror does not
contain source code or live infrastructure.

## Reporting

If you believe a public document exposes sensitive implementation detail, private strategy,
or copyable product mechanics, report it privately to the maintainer before sharing it
publicly.

If a future public release includes binaries or source, vulnerability reporting instructions
will be expanded before release.

## Current Trust Posture

The private implementation is designed to:

- Avoid pushing, deploying, force-merging, or installing packages.
- Keep per-repo operational state local.
- Use isolated Git worktrees for editing tasks.
- Block merges unless deterministic review gates pass.
- Redact obvious secret-looking material in manual review packets.

Known boundary: automated scanners are pattern-based and cannot prove the absence of all
secrets, unsafe edits, or undesirable worker behavior. Human review remains part of the
workflow.

