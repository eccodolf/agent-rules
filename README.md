# Правила работы с агентом Qwen Code и моделью Qwen Coder

Этот репозиторий содержит набор правил и рекомендаций по безопасной и эффективной работе с локальным агентом **Qwen Code** и моделью **Qwen Coder** в **закрытом контуре**.

Документация ориентирована на практическое использование в корпоративной среде с повышенными требованиями к:
- информационной безопасности;
- безопасной разработке;
- контролю контекста и качества промптов;
- эксплуатации локального агентного решения;
- проверке и валидации результатов, сгенерированных моделью.

## Содержание

- [Быстрый старт](#быстрый-старт)
- [Структура](#структура)
  - [Базовая документация](#базовая-документация)
  - [Управление агентами через файлы проекта](#управление-агентами-через-файлы-проекта)
  - [AI governance и production control plane](#ai-governance-и-production-control-plane)
  - [Директория `.ai/`](#директория-ai)
- [Цели документа](#цели-документа)
- [Базовые принципы](#базовые-принципы)
- [Рекомендуемый порядок внедрения](#рекомендуемый-порядок-внедрения)
- [Для кого этот набор правил](#для-кого-этот-набор-правил)
- [Практическое замечание](#практическое-замечание)
- [Минимальный стандарт использования](#минимальный-стандарт-использования)

## Быстрый старт

### Начать с `.ai/`

- [AI-правила и шаблон `.ai/`](.ai/README.md)
- [Системные правила безопасности](.ai/system/security-rules.md)
- [Prompt templates](.ai/project/prompt-templates.md)
- [Prompt DSL](.ai/project/prompt-dsl.md)
- [Модули `.ai/`](.ai/README.md#модульный-слой)

### Далее перейти к governance и control plane

- [Threat model для LLM](docs/llm-threat-model.md)
- [LLM Testing Framework](docs/llm-testing-framework.md)
- [Audit & Observability](docs/audit-observability.md)
- [LLM Policy Engine](docs/llm-policy-engine.md)
- [Runtime Guardrails](docs/runtime-guardrails.md)
- [Prompt Compiler](docs/prompt-compiler.md)
- [Policy-as-Code](docs/policy-as-code.md)
- [Simulation Environment](docs/simulation-environment.md)
- [Финансовые сценарии](docs/banking-scenarios.md)
- [Anti-Fraud DSL](docs/anti-fraud-dsl.md)

## Структура

### Базовая документация

- [docs/architecture.md](docs/architecture.md) — архитектура локального решения и границы доверия
- [docs/security.md](docs/security.md) — требования информационной безопасности
- [docs/secure-development.md](docs/secure-development.md) — правила безопасной разработки при использовании модели
- [docs/prompting.md](docs/prompting.md) — правила составления промптов
- [docs/context-management.md](docs/context-management.md) — управление контекстом и ограничениями модели
- [docs/operations.md](docs/operations.md) — эксплуатация, логирование, мониторинг и обновления
- [docs/validation.md](docs/validation.md) — проверка результатов модели и контроль качества
- [docs/checklists.md](docs/checklists.md) — короткие практические чек-листы для повседневной работы

### Управление агентами через файлы проекта

- [docs/agent-markdown-files.md](docs/agent-markdown-files.md) — использование Markdown-файлов для управления агентами
- [docs/agent-ignore.md](docs/agent-ignore.md) — правила для `.agentignore`, `.aiignore`, `.llmignore`

### AI governance и production control plane

- [docs/llm-threat-model.md](docs/llm-threat-model.md) — модель угроз для LLM и локального агента
- [docs/llm-testing-framework.md](docs/llm-testing-framework.md) — тестирование prompt templates, сценариев и регрессий
- [docs/audit-observability.md](docs/audit-observability.md) — аудит, трассировка и наблюдаемость
- [docs/llm-policy-engine.md](docs/llm-policy-engine.md) — policy engine для input/context/tool/output
- [docs/decision-logging.md](docs/decision-logging.md) — логирование решений агента и explainability
- [docs/runtime-guardrails.md](docs/runtime-guardrails.md) — runtime enforcement и inline guardrails
- [docs/prompt-compiler.md](docs/prompt-compiler.md) — компиляция Prompt DSL в нормализованный prompt
- [docs/policy-as-code.md](docs/policy-as-code.md) — декларативные политики как код
- [docs/simulation-environment.md](docs/simulation-environment.md) — среда симуляции для безопасной проверки сценариев
- [docs/synthetic-test-data.md](docs/synthetic-test-data.md) — генерация синтетических тестовых данных
- [docs/banking-scenarios.md](docs/banking-scenarios.md) — финансовые и платежные сценарии
- [docs/anti-fraud-dsl.md](docs/anti-fraud-dsl.md) — DSL для антифрод-логики

### Директория `.ai/`

`.ai/` — это основная точка входа для правил, которые реально используются агентом.

- [.ai/README.md](.ai/README.md) — структура и порядок использования `.ai/`
- [.ai/system/security-rules.md](.ai/system/security-rules.md) — обязательные системные правила безопасности
- [.ai/project/prompt-templates.md](.ai/project/prompt-templates.md) — production-ready шаблоны промптов
- [.ai/project/prompt-dsl.md](.ai/project/prompt-dsl.md) — стандартизированный Prompt DSL
- [.ai/modules/fastapi.md](.ai/modules/fastapi.md)
- [.ai/modules/django.md](.ai/modules/django.md)
- [.ai/modules/celery.md](.ai/modules/celery.md)
- [.ai/modules/postgres.md](.ai/modules/postgres.md)
- [.ai/modules/redis.md](.ai/modules/redis.md)
- [.ai/modules/vault.md](.ai/modules/vault.md)
- [.ai/modules/devops.md](.ai/modules/devops.md)
- [.ai/modules/banking.md](.ai/modules/banking.md)

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
5. Затем внедрить policy engine, runtime guardrails и testing framework.
6. В конце оформить чек-листы для пользователей и сопровождающих команд.

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
- [llm-policy-engine.md](docs/llm-policy-engine.md)
- [runtime-guardrails.md](docs/runtime-guardrails.md)

## Минимальный стандарт использования

Перед началом промышленной эксплуатации рекомендуется обеспечить:
- изоляцию контура;
- разграничение доступа;
- контроль журналов;
- шаблоны промптов;
- правила сокращения контекста;
- обязательную валидацию выходного результата;
- testing framework для промптов и сценариев;
- policy engine и runtime guardrails;
- процесс обновления модели и промптов через контроль изменений.
