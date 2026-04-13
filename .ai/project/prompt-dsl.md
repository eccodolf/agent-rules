# Prompt DSL (стандартизированный формат промптов)

## Назначение

Этот документ вводит стандартизированный формат для prompt-ов, используемых агентом.

Цель:
- снизить вариативность и шум в запросах;
- повысить предсказуемость ответов;
- ускорить работу на повторяющихся задачах;
- встроить безопасность и production-ограничения в структуру запроса.

## Базовая структура

```text
ROLE:

CONTEXT:

TASK:

CONSTRAINTS:

SECURITY:

OUTPUT:
```

## Описание блоков

### ROLE

Кто модель в рамках задачи:
- senior backend developer;
- Django/FastAPI engineer;
- DevOps engineer;
- reviewer;
- architect.

Роль должна помогать сузить решение, а не расширять его бесконтрольно.

### CONTEXT

Минимально необходимый контекст:
- relevant files;
- стэк;
- важные контракты и ограничения;
- известные runtime details.

Контекст не должен содержать лишние файлы, дампы, секреты и нерелевантные материалы.

### TASK

Четкое и измеримое описание задачи:
- что нужно сделать;
- что не нужно делать;
- что считается результатом.

### CONSTRAINTS

Технические и архитектурные ограничения:
- без сторонних библиотек;
- не менять публичный контракт;
- сохранить backward compatibility;
- не трогать инфраструктуру;
- diff должен быть минимальным.

### SECURITY

Требования ИБ и secure development:
- no secrets;
- mask PII;
- parameterized SQL only;
- audit logging required;
- no destructive commands.

### OUTPUT

Формат результата:
- только код;
- структура файлов и код;
- код + тесты;
- архитектура + риски;
- findings only для review.

## Production-safe расширения

Если задача влияет на production behavior, в `CONSTRAINTS` или `SECURITY` стоит явно указывать:
- rollback expectations;
- idempotency;
- retry safety;
- observability/logging;
- health checks;
- migration safety;
- backward compatibility.

## Пример (простой)

```text
ROLE: Python developer

CONTEXT: FastAPI service

TASK: Add health endpoint

CONSTRAINTS:
- no external libs
- keep diff minimal

SECURITY:
- no sensitive data

OUTPUT:
- code only
```

## Пример (средний)

```text
ROLE: Backend developer

CONTEXT:
- Django service
- existing service layer
- object-level permissions already used

TASK:
Add endpoint for changing request status

CONSTRAINTS:
- keep public API stable
- use existing patterns
- add tests

SECURITY:
- validate input
- audit logging required
- no secret values in code or logs

OUTPUT:
- short plan
- code by files
- tests
```

## Пример (сложный, банковский)

```text
ROLE: Backend architect

CONTEXT:
- Banking system with FastAPI + Celery + Postgres
- payment processing flow

TASK:
Design payment processing endpoint and async handling

CONSTRAINTS:
- idempotency
- retry safe
- audit logging
- backward compatible rollout

SECURITY:
- no secrets
- mask PII
- parameterized SQL only

OUTPUT:
- architecture
- code
- risks
- checks before deploy
```

## Рекомендации

- Всегда использовать DSL для сложных задач.
- Не смешивать блоки между собой.
- Минимизировать `CONTEXT`.
- Явно задавать `OUTPUT`.
- Если задача risky, явно фиксировать `rollback` и `checks`.

## Антипаттерны

- отсутствие `SECURITY` блока;
- смешивание `CONTEXT` и `TASK`;
- слишком длинный `CONTEXT`;
- расплывчатый `TASK` без критерия готовности;
- `OUTPUT`, не пригодный для review и применения.

## Вывод

Prompt DSL — это базовый способ сделать взаимодействие с агентом управляемым, безопасным и пригодным для быстрой работы без роста числа ошибок.
