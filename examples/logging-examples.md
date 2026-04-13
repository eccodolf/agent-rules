# Logging examples

## 1. Good application log

```json
{
  "timestamp": "2026-04-13T10:15:00Z",
  "service": "payments-api",
  "environment": "prod",
  "request_id": "req_8f03b1",
  "operation": "payment_create",
  "entity_id": "payment_4921",
  "outcome": "rejected",
  "reason_code": "duplicate_request"
}
```

Почему это хорошо:
- есть request id;
- есть безопасный идентификатор сущности;
- нет персональных данных, реквизитов и секретов;
- outcome и reason_code пригодны для алертов и расследования.

## 2. Bad application log

```json
{
  "card_number": "4111111111111111",
  "cvv": "123",
  "customer_name": "Ivan Ivanov",
  "auth_header": "Bearer eyJ...",
  "payment_payload": {
    "amount": 12000,
    "receiver_account": "40817810000000000001"
  }
}
```

Почему это плохо:
- содержит персональные данные;
- содержит платежные реквизиты;
- содержит token-like value;
- не проходит требования по банковской тайне.

## 3. Good Celery retry log

```json
{
  "task_id": "task_2199",
  "job_type": "send_receipt",
  "attempt": 2,
  "max_attempts": 5,
  "outcome": "retry_scheduled",
  "retry_in_seconds": 30,
  "error_class": "TemporarySMTPFailure"
}
```

## 4. Good infrastructure deploy log

```json
{
  "timestamp": "2026-04-13T11:20:00Z",
  "pipeline": "payments-api-deploy",
  "environment": "stage",
  "artifact_version": "1.8.4",
  "step": "rollout",
  "outcome": "success",
  "correlation_id": "deploy_20260413_1120"
}
```

## 5. Redaction example

Исходное сообщение:

```text
Customer Ivan Ivanov transferred 12000 RUB to account 40817810000000000001
```

Безопасный вариант:

```text
Customer [REDACTED] transferred [REDACTED_AMOUNT] to account [REDACTED_ACCOUNT]
```
