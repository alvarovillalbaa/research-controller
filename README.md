# research-controller

Last updated: 2026-11-10

A planned reusable controller for bounded candidate-model research:
generate or select tasks, obtain verified training data, request candidate
training, evaluate a frozen holdout, and propose promotion or rollback.

**Status: planned.** This repository establishes the standalone product,
interfaces, original requirements, and first implementation backlog. It contains
no controller engine, package, CLI, provider integration, or model-quality result.

## Independent use

The intended consumer supplies data-generation, training, evaluation, artifact,
and policy adapters. It can use an existing model checkpoint, a third-party
trainer, and its own evaluator without installing Lab or this ecosystem's other
model tools. Lab will use the same public controller interface for demonstrations.

[Component specification](docs/specs/README.md) defines the input/output seam,
ownership, failure cases, and first useful acceptance case.
[Original requirement provenance](docs/sources/provenance.json) records the
bounded self-improvement design from Lab.

## Ownership

The controller owns run/candidate identity, dependency sequencing, explicit
limits, attempt state, and model promotion policy. It consumes evaluator results;
[open-evals](https://github.com/alvarovillalbaa/open-evals) owns evaluation and
system-prompt improvement. Model-data, model-tokenizers, model-distillation,
model-pretraining, and model-posttraining own their respective transformations.
Compute economics, planning, and execution remain replaceable external layers.

The controller's promotion decision does not deploy an endpoint or publish
weights. Publication and production rollout remain explicit external actions.

MIT applies to this repository's authored material. No private evaluation-lab,
decision-runtime, or research-contracts code is redistributed here.
