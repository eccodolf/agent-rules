# Module end-to-end examples

## 1. FastAPI + PostgreSQL

Задача:
- добавить безопасный endpoint создания клиента.

Какие файлы подключать:
- `.ai/system/security-rules.md`
- `.ai/project/coding-rules.md`
- `.ai/project/testing-rules.md`
- `.ai/modules/fastapi.md`
- `.ai/modules/postgres.md`

Что должно получиться:
- валидация входа;
- service layer;
- параметризованный доступ к БД;
- тесты;
- безопасное логирование без персональных данных.

## 2. Django approval flow

Задача:
- реализовать согласование заявки.

Какие файлы подключать:
- `.ai/system/context-rules.md`
- `.ai/project/review-checklist.md`
- `.ai/modules/django.md`
- `.ai/modules/banking.md`

Что должно получиться:
- object-level permission checks;
- audit trail;
- controlled status transitions;
- отсутствие скрытых side effects в signals.

## 3. Celery + Redis retry-safe pipeline

Задача:
- асинхронно обработать заявку без дублей.

Какие файлы подключать:
- `.ai/project/testing-rules.md`
- `.ai/modules/celery.md`
- `.ai/modules/redis.md`
- `.ai/modules/banking.md`

Что должно получиться:
- idempotent task;
- retry with bounded attempts;
- duplicate protection;
- correlation id between API request and worker logs.

## 4. Kubernetes rollout

Задача:
- обновить образ сервиса в production-like среде.

Какие файлы подключать:
- `.ai/project/infra-rules.md`
- `.ai/project/logging-rules.md`
- `.ai/modules/kubernetes.md`
- `.ai/modules/devops.md`

Что должно получиться:
- fixed image tag;
- readiness/liveness;
- rollback steps;
- audit-friendly deploy logging.

## 5. Vault-backed secret flow

Задача:
- подключить сервис к Vault без утечки значений.

Какие файлы подключать:
- `.ai/project/secrets-rules.md`
- `.ai/modules/vault.md`
- `.ai/modules/devops.md`

Что должно получиться:
- machine-to-machine auth;
- no secret values in logs;
- observable secret retrieval failures;
- no insecure fallback.
