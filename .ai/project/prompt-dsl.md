# Prompt DSL (стандартизированный формат промптов)

## Назначение

Этот документ вводит стандартизированный формат (DSL) для промптов, используемых в агенте.

Цель:
- снизить вариативность промптов
- повысить предсказуемость ответов
- упростить автоматизацию
- встроить безопасность в структуру запроса

---

## Базовая структура

```text
ROLE:

CONTEXT:

TASK:

CONSTRAINTS:

SECURITY:

OUTPUT:
```

---

## Описание блоков

### ROLE
Кто модель (senior developer, architect и т.д.)

### CONTEXT
Минимально необходимый контекст

### TASK
Четкое описание задачи

### CONSTRAINTS
Ограничения

### SECURITY
Требования ИБ

### OUTPUT
Формат ответа

---

## Пример (простой)

```text
ROLE: Python developer

CONTEXT: FastAPI service

TASK: Add health endpoint

CONSTRAINTS: no external libs

SECURITY: no sensitive data

OUTPUT: code
```

---

## Пример (сложный, банковский)

```text
ROLE: Backend architect

CONTEXT: Banking system with FastAPI + Celery + Postgres

TASK: Design payment processing endpoint

CONSTRAINTS:
- idempotency
- retry safe
- audit logging

SECURITY:
- no secrets
- mask PII

OUTPUT:
- architecture
- code
- risks
```

---

## Рекомендации

- Всегда использовать DSL для сложных задач
- Не смешивать блоки
- Минимизировать CONTEXT
- Явно задавать OUTPUT

---

## Антипаттерны

- отсутствие SECURITY блока
- смешивание CONTEXT и TASK
- слишком длинный CONTEXT

---

## Вывод

Prompt DSL — это основа для управляемых и безопасных AI-агентов.
