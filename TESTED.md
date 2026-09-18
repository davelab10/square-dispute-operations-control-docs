# Tested Status

## Focused local workflow tests

The focused suite is:

```sh
python3 -m unittest discover -s tests -p 'test_square_dispute_workflow.py' -v
```

It covers bounded queueing and prioritization, separate currency aggregation, evidence-gap and incomplete-inventory routing, explicit accept/contest paths, exact current deletion-inventory binding, reconciliation routing limits, processing/terminal/missing-state fail-closed behavior, module command/schema mapping, and absence of direct provider bypass.

Latest local verification (2026-09-19): all 10 focused workflow tests passed. The tests cover the bounded behavior listed above, the seven-stage Marketplace DAG (six valid edges), acyclic runtime dependencies, valid engine-node references, and the absence of direct provider bypass. `jq -e . workflow/square-dispute-operations-control.json` validated the JSON. The local source copy and Station workflow file are byte-identical (SHA-256 `01eedfe1369925ae636a85c77cfd3aa65a0acb1f9a1bc1b842cc9572bde7ad1a`). This does not imply that the Track 1 module suite was run.

## Marketplace publication and local recognition

RailCall's normal `market publish` flow accepted the workflow and its publisher signature on 2026-09-19. The authoritative publish response returned listing ID `cmu7amknx0bzsjxw2c34prond`, type `workflow`, category `Ops`, and URL <https://railcall.ai/marketplace/cmu7amknx0bzsjxw2c34prond>. The workflow is version `0.1.0`.

The normal `railcall market install dave/square-dispute-operations-control` path fetched and installed the Marketplace workflow. Station's receipt identifies the Marketplace source, workflow ID `dave__square-dispute-operations-control`, and embedded spec version `0.1.0`. The receipt result is `UNVERIFIED`; this is not evidence of a separate local receipt-signature verification. The generic `railcall market get` catalog path had not indexed the listing when checked, but Marketplace publication and backend installation succeeded; the workflow was not republished for indexing lag.

## Real workflow / Station / Square Sandbox E2E

Not established. No real workflow run through Station against Square Sandbox has been completed for this workflow. Therefore discovery behavior against live Sandbox data, workflow-level text-evidence creation, contest, acceptance, reconciliation, and native Airlock execution remain unverified.

## Native Airlock

The workflow routes consequential operations only through the module's governed commands. Native Airlock approval and execution for these workflow paths have not yet been demonstrated by a real workflow E2E.

## Limits

The workflow is bounded to 100 scanned items and 10 selected cases, is text-evidence-only, and does not claim outcome prediction or causal attribution. A successful focused local test does not establish live provider behavior or Station integration.
