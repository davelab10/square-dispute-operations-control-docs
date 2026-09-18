# Square Dispute Operations Control Tower

`dave/square-dispute-operations-control` is a Track 2 RailCall workflow, version `0.1.0`. It orchestrates the published `dave/square-dispute-operations@0.1.0` module; it does not call Square directly or reimplement the module's provider operations.

The workflow builds a bounded operational queue from dispute observations, groups observed exposure by currency, separates processing and terminal cases, and prioritizes actionable cases by deadline and evidence readiness. It inspects selected cases, requirements, inventories, and mapped gaps, then routes explicit operator requests to prepare evidence, create or delete text evidence, preview acceptance or contest, execute an unchanged approved plan, defer/escalate, or reconcile an ambiguous result.

Consequential actions remain governed by the module and RailCall's native approval path. The workflow does not infer legal merits, predict dispute outcomes, automatically retry irreversible actions, or claim that observed provider state proves workflow causality. Reconciliation reports observations, not causal proof.

Discovery is bounded to 5 pages / 100 items and selects no more than 10 cases for detailed review. The workflow is text-evidence-only. Acceptance and contest use separate preview and execution requests; execution requires the exact unchanged plan returned by preview. `PROCESSING` is not a win, and non-actionable or unsupported states are deferred.

See [COMMANDS.md](COMMANDS.md) for operator inputs and module routes, and [TESTED.md](TESTED.md) for verified test and runtime status.
