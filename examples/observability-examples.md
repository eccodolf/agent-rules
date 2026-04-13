# Observability examples

## 1. Metric set for LLM gateway

```yaml
metrics:
  - name: llm_request_latency_ms
    type: histogram
  - name: llm_request_total
    type: counter
  - name: llm_blocked_total
    type: counter
  - name: llm_human_review_total
    type: counter
  - name: llm_tool_call_total
    type: counter
  - name: llm_output_violation_total
    type: counter
```

## 2. Trace example

```json
{
  "trace_id": "trace_9001",
  "spans": [
    { "name": "request_received", "duration_ms": 4 },
    { "name": "context_build", "duration_ms": 20 },
    { "name": "policy_check", "duration_ms": 7 },
    { "name": "model_inference", "duration_ms": 840 },
    { "name": "output_validation", "duration_ms": 15 }
  ]
}
```

## 3. Alerting example

```yaml
alerts:
  - name: llm_block_rate_spike
    condition: blocked_rate_5m > 0.15
    severity: high
  - name: llm_policy_engine_errors
    condition: policy_engine_errors_5m > 0
    severity: critical
  - name: llm_tool_mutation_attempts
    condition: mutating_tool_attempts_5m > 3
    severity: high
```

## 4. Good correlation model

- `request_id` for user request;
- `trace_id` for end-to-end processing;
- `job_id` for async task;
- `entity_id` for business object;
- `decision_id` for policy or guardrail decision.
