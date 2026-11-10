# Research controller agent instructions

- Read README.md and docs/specs/README.md before changing scope.
- This repository owns reusable bounded model-research orchestration; Lab assembles examples.
- Evaluation/scoring is supplied through an external contract. Do not duplicate Open Evals.
- Do not import sibling checkouts or make Lab a runtime dependency.
- Current state is planned: do not imply an engine, durable ledger, or promotion implementation exists.
- Keep artifacts referenced by immutable revision/hash. Preserve failed and unknown outcomes.
- Do not launch providers, training jobs, deployments, or release promotions implicitly.
- Keep focused checks and provenance beside the owning component; preserve user work.
