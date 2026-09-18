# Tested Status

## Focused local workflow tests

The focused suite is:

```sh
python3 -m unittest discover -s tests -p 'test_square_dispute_workflow.py' -v
```

It covers bounded queueing and prioritization, separate currency aggregation, evidence-gap and incomplete-inventory routing, explicit accept/contest paths, exact current deletion-inventory binding, reconciliation routing limits, processing/terminal/missing-state fail-closed behavior, module command/schema mapping, and absence of direct provider bypass.

Latest local verification (2026-09-19): all 9 focused workflow tests passed, and `jq -e . workflow/square-dispute-operations-control.json` validated the JSON. The local source copy and the Station workflow file had the same SHA-256 at verification time. This does not imply that the Track 1 module suite was run.

## Real workflow / Station / Square Sandbox E2E

Not established. No real workflow run through Station against Square Sandbox has been completed for this workflow. Therefore discovery behavior against live Sandbox data, workflow-level text-evidence creation, contest, acceptance, reconciliation, and native Airlock execution remain unverified.

## Native Airlock

The workflow routes consequential operations only through the module's governed commands. Native Airlock approval and execution for these workflow paths have not yet been demonstrated by a real workflow E2E.

## Limits

The workflow is bounded to 100 scanned items and 10 selected cases, is text-evidence-only, and does not claim outcome prediction or causal attribution. A successful focused local test does not establish live provider behavior or Station integration.
