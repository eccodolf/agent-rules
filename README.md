# Правила работы с агентом Qwen Code и моделью Qwen Coder

Этот репозиторий содержит набор правил и рекомендаций по безопасной и эффективной работе с локальным агентом **Qwen Code** и моделью **Qwen Coder** в **закрытом контуре**.

Документация ориентирована на практическое использование в корпоративной среде с повышенными требованиями к:
- информационной безопасности;
- безопасной разработке;
- контролю контекста и качества промптов;
- эксплуатации локального агентного решения;
- проверке и валидации результатов, сгенерированных моделью.

## Точка входа

Для практического использования этого репозитория рекомендуется читать материалы в таком порядке:

1. [docs/architecture.md](docs/architecture.md)
2. [docs/security.md](docs/security.md)
3. [docs/secure-development.md](docs/secure-development.md)
4. [docs/prompting.md](docs/prompting.md)
5. [docs/context-management.md](docs/context-management.md)
6. [docs/operations.md](docs/operations.md)
7. [docs/validation.md](docs/validation.md)
8. [docs/checklists.md](docs/checklists.md)
9. [`.ai/README.md`](.ai/README.md)

## Сценарии

Для типовых вариантов использования Qwen Code смотрите отдельный раздел:

- [scenarios/README.md](scenarios/README.md) — сценарии для Django, FastAPI, прокси-сервиса, десктопного приложения и DevOps-пайплайна, с целевой структурой проекта и командами для PowerShell и Linux/OEL

## Структура репозитория

### Базовые документы

- [docs/architecture.md](docs/architecture.md) — архитектура локального решения и границы доверия
- [docs/security.md](docs/security.md) — требования информационной безопасности
- [docs/secure-development.md](docs/secure-development.md) — правила безопасной разработки при использовании модели
- [docs/prompting.md](docs/prompting.md) — правила составления промптов
- [docs/context-management.md](docs/context-management.md) — управление контекстом и ограничениями модели
- [docs/operations.md](docs/operations.md) — эксплуатация, логирование, мониторинг и обновления
- [docs/validation.md](docs/validation.md) — проверка результатов модели и контроль качества
- [docs/checklists.md](docs/checklists.md) — короткие практические чек-листы для повседневной работы

### Governance и контроль выполнения

- [docs/llm-policy-engine.md](docs/llm-policy-engine.md) — слой политик для проверки input, context, tools и output
- [docs/runtime-guardrails.md](docs/runtime-guardrails.md) — runtime-ограничения и enforcement во время выполнения
- [docs/policy-as-code.md](docs/policy-as-code.md) — декларативное описание и сопровождение политик
- [docs/decision-logging.md](docs/decision-logging.md) — журналирование решений агента и policy outcomes
- [docs/audit-observability.md](docs/audit-observability.md) — аудит, метрики, трассировка и расследование

### Prompting и инженерия контекста

- [docs/prompt-compiler.md](docs/prompt-compiler.md) — компиляция структурированного DSL в нормализованный prompt
- [docs/agent-markdown-files.md](docs/agent-markdown-files.md) — правила работы агента с markdown-документами
- [docs/agent-ignore.md](docs/agent-ignore.md) — ограничения на включение файлов в агентный контекст

### Тестирование и моделирование

- [docs/llm-testing-framework.md](docs/llm-testing-framework.md) — framework для тестирования prompt- и agent-сценариев
- [docs/llm-threat-model.md](docs/llm-threat-model.md) — модель угроз для LLM-агента
- [docs/simulation-environment.md](docs/simulation-environment.md) — безопасная среда симуляции и отладки
- [docs/synthetic-test-data.md](docs/synthetic-test-data.md) — правила генерации синтетических тестовых данных

### Банковский домен

- [docs/banking-scenarios.md](docs/banking-scenarios.md) — типовые банковские сценарии
- [docs/anti-fraud-dsl.md](docs/anti-fraud-dsl.md) — DSL и подходы для антифрод-логики
- [scenarios/README.md](scenarios/README.md) — практические сценарии использования и целевые структуры проектов для Qwen Code

### Агентные правила в `.ai/`

- [`.ai/README.md`](.ai/README.md) — шаблон структуры и порядок подключения правил
- [`.ai/system/security-rules.md`](.ai/system/security-rules.md) — системные security-ограничения для агента
- [`.ai/project/prompt-dsl.md`](.ai/project/prompt-dsl.md) — проектный DSL для структурированных запросов
- [`.ai/project/prompt-templates.md`](.ai/project/prompt-templates.md) — шаблоны prompt-ов
- [`.ai/modules/fastapi.md`](.ai/modules/fastapi.md) — правила для FastAPI
- [`.ai/modules/django.md`](.ai/modules/django.md) — правила для Django
- [`.ai/modules/celery.md`](.ai/modules/celery.md) — правила для Celery
- [`.ai/modules/postgres.md`](.ai/modules/postgres.md) — правила для PostgreSQL
- [`.ai/modules/redis.md`](.ai/modules/redis.md) — правила для Redis
- [`.ai/modules/vault.md`](.ai/modules/vault.md) — правила для Vault
- [`.ai/modules/devops.md`](.ai/modules/devops.md) — правила для DevOps-процессов
- [`.ai/modules/banking.md`](.ai/modules/banking.md) — доменные ограничения для банковских сценариев

## Цели документа

Документ предназначен для того, чтобы:
1. снизить риск утечки данных и неконтролируемого использования модели;
2. формализовать подход к применению локального AI-агента в разработке;
3. предотвратить типовые ошибки при передаче контекста и постановке задач;
4. сократить число небезопасных, неточных и невалидированных результатов;
5. упростить внедрение единых правил в команде.

## Базовые принципы

1. **Модель не является источником истины.** Любой результат подлежит проверке.
2. **Локальность не отменяет риски.** Даже в закрытом контуре нужно применять меры ИБ.
3. **Минимально необходимый контекст.** В модель передается только то, что нужно для решения конкретной задачи.
4. **Безопасность по умолчанию.** Любая интеграция, автоматизация и выполнение кода должны быть ограничены и контролируемы.
5. **Проверяемость.** Все значимые действия агента и его результаты должны быть воспроизводимы и проверяемы.

## Рекомендуемый порядок внедрения

1. Сначала определить архитектурные границы и доверенные зоны.
2. Затем утвердить правила ИБ и безопасной разработки.
3. После этого подготовить шаблоны промптов и правила ограничения контекста.
4. Далее включить логирование, мониторинг и процессы валидации.
5. В конце оформить чек-листы для пользователей и сопровождающих команд.

## Для кого этот набор правил

- разработчики;
- тимлиды;
- DevOps и администраторы платформы;
- специалисты ИБ;
- архитекторы;
- владельцы внутренних AI-инструментов.

## Практическое замечание

Если агент используется для генерации кода, изменений конфигурации, SQL, shell-команд, инфраструктурных шаблонов или автоматизации, необходимо применять дополнительные ограничения из разделов:
- [security.md](docs/security.md)
- [secure-development.md](docs/secure-development.md)
- [validation.md](docs/validation.md)

## Минимальный стандарт использования

Перед началом промышленной эксплуатации рекомендуется обеспечить:
- изоляцию контура;
- разграничение доступа;
- контроль журналов;
- шаблоны промптов;
- правила сокращения контекста;
- обязательную валидацию выходного результата;
- процесс обновления модели и промптов через контроль изменений.

## Практическое назначение репозитория

Этот репозиторий полезен в трех режимах:

1. как набор корпоративных правил для внедрения локального AI-агента;
2. как шаблон `.ai/`-структуры для проектов с повышенными требованиями к безопасности;
3. как базовая governance-документация для банковских и других чувствительных сценариев.
