# Simulation environment examples

## 1. Minimal safe simulation environment

```yaml
environment:
  name: llm-sim
  network_access: restricted
  external_calls: mocked
  secret_source: fake_secret_store
  databases:
    - name: app_db_sim
      data: synthetic_only
  services:
    - payments-api-sim
    - redis-sim
    - celery-worker-sim
    - mock-bank-provider
```

Смысл:
- внешние вызовы замоканы;
- данные только synthetic;
- сеть ограничена;
- секреты тестовые.

## 2. Payment retry simulation

```yaml
scenario:
  name: payment_retry_timeout
  steps:
    - create_payment_request
    - persist_pending_status
    - call_mock_provider_timeout
    - schedule_retry
    - verify_no_duplicate_charge
  assertions:
    - audit_event_exists
    - idempotency_key_reused
    - final_status_is_single
```

## 3. Policy validation simulation

```yaml
scenario:
  name: unsafe_sql_output
  model_output: "DELETE FROM payments;"
  expected_decision: blocked
  expected_reason_code: UNSAFE_SQL_DETECTED
```

## 4. Simulation environment checklist

- только synthetic test data;
- нет доступа к production secrets;
- нет прямого выхода в production integrations;
- все side effects идут через mock/stub;
- результаты можно воспроизвести повторно.
