# Operator Inputs and Module Routes

## Workflow inputs

The default context sets `environment` to `sandbox`. Supply explicit `operator_requests` arrays; empty arrays request no operator action. Each category is capped at 10 items, and the combined number of mutation requests is capped at 10 per run.

| Category | Input | Workflow route |
| --- | --- | --- |
| `prepare_text` | `dispute_id`, `evidence_type`, `evidence_text` | Prepare text evidence locally through the module. |
| `create_text` | `expected_environment`, `dispute_id`, `evidence_type`, `evidence_text` | Governed module write; requires native approval. |
| `delete_evidence` | `expected_environment`, `dispute_id`, `evidence_id`, `expected_inventory_fingerprint` | Governed module write; current inventory must match. |
| `prepare_accept` | `dispute_id` | Produce an acceptance preview/plan; does not accept the dispute. |
| `execute_accept` | `dispute_id`, exact `plan` from the preview | Governed module write; requires native approval and module validation. |
| `prepare_contest` | `dispute_id` | Produce a contest preview/plan; does not submit evidence. |
| `execute_contest` | `dispute_id`, exact `plan` from the preview | Governed module write; requires native approval and module validation. |
| `reconcile` | `reconciliation_ref` | Ask the module to reread and reconcile the referenced operation. |
| `defer_escalate` | `dispute_id`, `action` (`defer` or `escalate`), optional `reason_code` | Record an operator disposition; no provider mutation. |

The workflow blocks missing, unsupported, terminal, processing, stale, or insufficiently observed case requests. It does not treat its own routing as a legal or outcome decision.

## Published module commands orchestrated

- Discovery and context: `square.dispute.list`, `square.dispute.deadline_queue`, `square.dispute.operational_summary`
- Case and evidence reads: `square.dispute.inspect`, `square.dispute.evidence_requirements`, `square.dispute.evidence_inventory`, `square.dispute.evidence_gap`
- Text evidence: `square.dispute.evidence_text_prepare`, `square.dispute.evidence_text_create`, `square.dispute.evidence_delete`
- Governed dispute actions: `square.dispute.accept_preview`, `square.dispute.accept_execute`, `square.dispute.contest_preview`, `square.dispute.contest_execute`
- Reconciliation: `square.dispute.reconcile`

All provider operations above go through `dave/square-dispute-operations@0.1.0`. The workflow contains no direct Square API call.
