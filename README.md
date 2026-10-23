# Dependency Upgrade

A Camillia camflow that implements a dependency-upgrade task end to end: it reads the
upstream changelogs and migration guides, applies the migration steps to code and
configuration, updates tests, and leaves a review-ready change on the task branch.

## What it does

1. **Plans** — pins down current and target versions, inventories every manifest,
   lockfile, and API usage site, and reads the changelogs for every version in between.
2. **Migrates** — updates manifests and lockfiles, applies the code migrations step by
   step with fast per-step validation, and adjusts tests the intended upstream changes
   obsolete (never weakening a test to force a pass).
3. **Validates** — clean reinstall, build, full test suite, and lint/typecheck per
   repository, fixing stragglers the migration missed.
4. **Decides and finishes** — moves the task to review with a reviewer-facing summary
   only when validation is green; otherwise reports exactly what remains blocked.

## How it triggers

Task-type camflow. Schedule a task that names the dependency and the target version
(for example "upgrade Newtonsoft.Json to 13.x" or "move Node to the latest LTS") with
this camflow, or bind it to a task event in your workspace trigger bindings.

## Install

Install from the Camillia Community Hub. The hub imports `camflow.yaml` into your
Camillia instance; no other files are required at runtime.

## License

MIT — Copyright (c) 2026 Camillia contributors. See [LICENSE](LICENSE).
