# Decision logging examples

## 1. Allow

```json
{
  "timestamp": "2026-04-13T12:00:00Z",
  "trace_id": "trace_1200",
  "request_id": "req_1200",
  "decision": "allow",
  "reason_code": "SAFE_READ_ONLY_TASK",
  "context_summary": [
    "README.md",
    ".ai/system/security-rules.md",
    ".ai/modules/fastapi.md"
  ],
  "tools_used": [],
  "notes": "Read-only documentation request"
}
```

## 2. Block

```json
{
  "timestamp": "2026-04-13T12:10:00Z",
  "trace_id": "trace_1210",
  "request_id": "req_1210",
  "decision": "block",
  "reason_code": "SECRET_IN_OUTPUT",
  "context_summary": [
    "service/config.py",
    ".ai/system/output-rules.md"
  ],
  "tools_used": [],
  "notes": "Secret-like value detected in model output"
}
```

## 3. Approval required

```json
{
  "timestamp": "2026-04-13T12:20:00Z",
  "trace_id": "trace_1220",
  "request_id": "req_1220",
  "decision": "require_human_review",
  "reason_code": "PROD_DB_WRITE",
  "context_summary": [
    "migration.sql",
    ".ai/project/database-rules.md"
  ],
  "tools_used": ["sql-client"],
  "notes": "Schema-changing SQL proposed for production"
}
```

## 4. What a good decision log must contain

- timestamp;
- trace_id and request_id;
- decision;
- reason_code;
- summary of context;
- tools used or explicitly no tools;
- short explanation suitable for audit.
