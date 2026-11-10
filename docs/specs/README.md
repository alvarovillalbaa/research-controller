# Bounded research controller specification

Last updated: 2026-11-10

Status: planned. The first release should provide a small usable local controller
with supplied stage adapters, independent of Lab and any managed service.

## Public capability

Accept an explicit experiment plan: baseline model/artifact identity, ordered
stages and their input/output references, frozen evaluator/holdout identity,
resource/attempt limits, and promotion criteria. Produce an inspectable run
record linking candidate artifacts, attempts, measurements, failures, and the
final promotion/rejection/rollback proposal.

The first concrete API and record format must be versioned with the first
implementation. This document specifies behavior, not an implemented wire schema.

## Component boundaries

- Generation/curation adapters produce permitted, provenance-bearing training data.
- Attempt/verification adapters retain actual student responses and objective scores before accepted traces become training inputs.
- Training adapters consume explicit model/data/tokenizer artifacts and return candidate artifacts.
- Evaluation adapters return frozen evaluator identity, coverage, metrics, uncertainty, and gate results.
- Execution adapters own actual job submission/cancellation and observed lifecycle.
- The controller sequences these stages and applies the declared model policy.
- Lab owns integrated recipes and comparisons; Open Evals owns its evaluation engine.

No mandatory dependency on a particular trainer, scheduler, service, or Lab is
needed. Artifact references should preserve URI, exact revision/format, and
content hashes rather than copy all payloads into the controller.

## Required failure behavior

Record failed/cancelled attempts and unknown external outcomes. Retry policy
must preserve execution identity and avoid silently dispatching uncertain work
again. Missing holdout coverage, contamination, changed evaluator versions, or
unknown cost coverage cannot silently become passing promotion evidence.
Bound attempts/resources before dispatch, and expose which limits the selected
backend can actually enforce.

The original gates include base capability, target-domain improvement, safety,
instruction following, contamination, data diversity, and cost per improvement.
A policy can propose promotion only from observed evidence under those frozen
gates. A synthetic fixture never establishes real-model progress.

## First implementation and acceptance

- [ ] Define the minimal local plan/run records and adapter call interface.
- [ ] Execute one authored baseline/candidate workflow with supplied local adapters.
- [ ] Preserve attempt identity, stage dependencies, input/output hashes, and failed outcomes.
- [ ] Demonstrate accepted, rejected, cancelled, and unknown-result decisions.
- [ ] Show evaluator/version drift and missing coverage prevent promotion.
- [ ] Install and run the fixture independently of Lab, providers, databases, and GPUs.
- [ ] Add a Lab recipe using exactly that public interface.

All boxes remain pending until implementation and runtime evidence exist.

## Existing projects

The existing autoresearch fork can supply a deliberately selected research
workload; it does not become an implicit controller dependency.
The separate private decision-runtime and research-contracts projects have
their own scientific contracts and no redistribution license. Their existence
does not authorize copying them into this MIT repository.
