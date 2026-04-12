# Prompt Compiler

## Назначение

Prompt compiler преобразует структурированный DSL (см. `prompt-dsl.md`) в нормализованный prompt, который передается модели.

Цель:
- стандартизировать формат промптов;
- исключить лишний шум;
- гарантировать наличие обязательных блоков;
- автоматически добавлять security и constraints;
- контролировать размер контекста.

---

## Вход

DSL формат:

```text
ROLE:
CONTEXT:
TASK:
CONSTRAINTS:
SECURITY:
OUTPUT:
```

---

## Выход

Нормализованный prompt:

```text
Ты {ROLE}.

Контекст:
{CONTEXT}

Задача:
{TASK}

Ограничения:
{CONSTRAINTS}

Требования безопасности:
{SECURITY}

Формат ответа:
{OUTPUT}
```

---

## Этапы компиляции

1. Валидация DSL
2. Нормализация текста
3. Добавление системных ограничений
4. Добавление security layer
5. Обрезка контекста
6. Финальный prompt

---

## Пример

### Вход

```text
ROLE: Backend dev
TASK: create endpoint
```

### Выход

```text
Ты Backend dev.

Контекст: не задан

Задача: create endpoint

Ограничения: соблюдать secure development

Требования безопасности: не использовать секреты

Формат ответа: код
```

---

## Интеграция

Prompt compiler должен использовать:
- `.ai/system/*`
- policy engine
- context manager

---

## Вывод

Prompt compiler превращает хаотичные промпты в управляемый интерфейс взаимодействия с LLM.
