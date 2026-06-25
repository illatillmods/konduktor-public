# Verified Behavior Summary

This summary is based on inspection of the private repository on June 25, 2026.

## Verified

- The project is a Python CLI developer tool.
- The runtime package declares no third-party Python dependencies.
- The CLI reports version `0.2.0`.
- Python syntax and package metadata require Python >= 3.10.
- Editing tasks run in Git worktrees under a Konduktor-specific branch prefix.
- Accepted work can merge into local `main` after review.
- Push and deploy behavior is not implemented.
- The test suite covers routing, workers, review, safety, Git operations, quota, VS Code
  tasks, dispatch failure modes, and an end-to-end mocked run.
- The test suite passed with 78 tests on June 25, 2026.

## Not Claimed

- No public performance benchmark is claimed.
- No public model-quality benchmark is claimed.
- No hosted service, SaaS backend, billing system, or web app is claimed.
- No guarantee is claimed that automated scanning catches every secret or unsafe edit.
- No public source license is granted.

