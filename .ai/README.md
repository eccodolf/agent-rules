# Шаблон директории `.ai/` для проектов в банковском секторе

Этот каталог содержит готовый шаблон правил для локальных AI-агентов, работающих с проектами на стеке:
- Python
- FastAPI / Django / Flask
- Vault
- Celery
- PostgreSQL
- Redis
- boto3
- Yandex Cloud
- VPS / DevOps
- Nginx / Apache
- Oracle Linux
- Docker / Docker Compose
- Kubernetes

Шаблон ориентирован на использование в проектах банковского сектора, где действуют повышенные требования к:
- защите данных;
- безопасной разработке;
- аудиту;
- минимизации контекста;
- воспроизводимости действий агента.

## Быстрая навигация

### Системный слой

- [system/security-rules.md](system/security-rules.md) — обязательные системные ограничения безопасности

### Проектный слой

- [project/prompt-templates.md](project/prompt-templates.md) — production-ready шаблоны промптов
- [project/prompt-dsl.md](project/prompt-dsl.md) — стандартизированный Prompt DSL

### Модульный слой

- [modules/fastapi.md](modules/fastapi.md)
- [modules/django.md](modules/django.md)
- [modules/celery.md](modules/celery.md)
- [modules/postgres.md](modules/postgres.md)
- [modules/redis.md](modules/redis.md)
- [modules/vault.md](modules/vault.md)
- [modules/devops.md](modules/devops.md)
- [modules/banking.md](modules/banking.md)

### Связанные документы из `docs/`

- [../docs/llm-policy-engine.md](../docs/llm-policy-engine.md) — policy engine для input/context/tool/output
- [../docs/runtime-guardrails.md](../docs/runtime-guardrails.md) — runtime guardrails и inline enforcement
- [../docs/llm-testing-framework.md](../docs/llm-testing-framework.md) — тестирование prompt templates и сценариев
- [../docs/decision-logging.md](../docs/decision-logging.md) — explainability и decision logging
- [../docs/audit-observability.md](../docs/audit-observability.md) — аудит, трассировка и наблюдаемость
- [../docs/prompt-compiler.md](../docs/prompt-compiler.md) — компиляция Prompt DSL в нормализованный prompt
- [../docs/policy-as-code.md](../docs/policy-as-code.md) — декларативные политики как код
- [../docs/simulation-environment.md](../docs/simulation-environment.md) — симуляция сценариев и безопасная проверка
- [../docs/banking-scenarios.md](../docs/banking-scenarios.md) — финансовые и платежные сценарии
- [../docs/anti-fraud-dsl.md](../docs/anti-fraud-dsl.md) — DSL для антифрод-логики

## Рекомендуемая структура

```text
.ai/
  README.md
  system/
    security-rules.md
  project/
    prompt-templates.md
    prompt-dsl.md
  modules/
    fastapi.md
    django.md
    celery.md
    postgres.md
    redis.md
    vault.md
    devops.md
    banking.md
```

## Как использовать

1. Начинать чтение с `AGENTS.md` в корне проекта.
2. Затем подключать `.ai/system/*`.
3. Потом `.ai/project/*`.
4. И только после этого — нужный модульный файл из `.ai/modules/*`.
5. Для сложных и критичных сценариев учитывать связанные документы из `docs/`:
   - policy engine
   - runtime guardrails
   - testing framework
   - audit & observability
   - banking scenarios
6. Не включать в контекст весь `.ai/` целиком без необходимости.

## Приоритет инструкций

1. `.ai/system/*`
2. `.ai/project/*`
3. `.ai/modules/*`
4. локальный запрос пользователя

При конфликте побеждает более высокий уровень.

## Как `.ai/` связано с control plane

Директория `.ai/` — это trusted instructions layer. Она определяет, **что агент должен делать**.

Документы в `docs/` определяют, **как контролировать и проверять поведение агента**:
- threat model
- testing framework
- policy engine
- runtime guardrails
- decision logging
- audit & observability
- simulation environment

Упрощенно:
- `.ai/` = policy/rules for agent behavior
- `docs/` = governance, control, validation, observability

## Обязательные правила

- Не передавать в модель секреты, реальные ключи, пароли, токены, сертификаты, закрытые ключи.
- Не доверять результатам модели без проверки.
- Любой сгенерированный код должен проходить review, тестирование и статический анализ.
- Любые инфраструктурные и эксплуатационные изменения должны быть обратимыми.
- Любые действия, влияющие на безопасность, должны быть явно помечены и проверены человеком.
- Для банковских и финансовых сценариев обязательны audit trail, idempotency и controlled rollback.

## Практическая рекомендация

Если агент используется в production-потоках, `.ai/` рекомендуется применять вместе с:
- `AGENTS.md`
- `.agentignore`
- LLM policy engine
- runtime guardrails
- testing framework
- audit logging

В таком режиме `.ai/` становится не просто каталогом заметок, а частью управляемого AI control plane.
