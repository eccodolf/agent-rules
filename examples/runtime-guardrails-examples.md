# Runtime guardrails examples

## 1. Blocked output with secrets

```json
{
  "status": "blocked",
  "reason_code": "OUTPUT_SECRET_DETECTED",
  "message": "Response blocked by runtime guardrail policy",
  "next_step": "Provide redacted context or request human review"
}
```

Когда использовать:
- обнаружен token;
- обнаружен private key;
- в output попал секрет из конфигурации.

## 2. Human review required for production infrastructure

```json
{
  "status": "require_human_review",
  "reason_code": "PROD_INFRA_MUTATION",
  "message": "Production infrastructure change requires approval",
  "requested_action": "kubectl apply -f deployment.yaml"
}
```

## 3. Blocked SQL output

Входной ответ модели:

```sql
DELETE FROM payments;
```

Guardrail decision:

```json
{
  "status": "blocked",
  "reason_code": "UNSAFE_SQL_DETECTED",
  "message": "Potentially destructive SQL blocked"
}
```

## 4. Warn-only case

```json
{
  "status": "warn",
  "reason_code": "LARGE_CONTEXT",
  "message": "Context is larger than the recommended limit",
  "next_step": "Reduce context and retry if output quality degrades"
}
```

## 5. Banking confidentiality block

```json
{
  "status": "blocked",
  "reason_code": "BANKING_CONFIDENTIAL_DATA",
  "message": "Output contains banking secrecy or commercial secret data",
  "next_step": "Replace confidential details with masked or abstracted equivalents"
}
```
