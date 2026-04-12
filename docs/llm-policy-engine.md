# LLM Policy Engine

## Назначение

LLM Policy Engine — это слой правил, который проверяет входные запросы, контекст, действия агента и выходные ответы до того, как они будут показаны пользователю или применены в инфраструктуре.

Цель:
- запретить опасные действия;
- ограничить доступ к чувствительным данным;
- обеспечить единообразное соблюдение политик ИБ и secure development;
- сделать поведение агента предсказуемым и проверяемым.

---

## Уровни контроля

Policy engine рекомендуется применять на четырех этапах:

1. **Input policy** — проверка пользовательского запроса
2. **Context policy** — проверка состава контекста
3. **Tool policy** — проверка разрешенности действий/инструментов
4. **Output policy** — проверка ответа модели

---

## 1. Input policy

Проверяет:
- нет ли попытки обойти системные правила;
- нет ли запроса на секреты, ключи, учетные данные;
- не является ли запрос попыткой генерации опасной команды;
- нет ли в запросе явных jailbreak/prompt injection паттернов.

### Примеры правил

- запретить запросы на вывод secret values;
- запретить инструкции «ignore previous rules»;
- пометить как high-risk запросы на destructive shell-команды;
- требовать human review для финансовых операций и прод-инфраструктуры.

---

## 2. Context policy

Проверяет:
- какие файлы включены в контекст;
- соответствуют ли они `.agentignore` / allow-list;
- не содержат ли секреты, PII, бинарные артефакты, большие логи;
- относятся ли они к задаче.

### Примеры правил

- запрещать включение `.env`, `secrets/`, `keys/`, `*.pem`, `*.key`;
- запрещать передачу дампов БД и логов без маскирования;
- ограничивать количество файлов и суммарный размер контекста;
- допускать trusted instructions только из `.ai/system/*`, `.ai/project/*`, `AGENTS.md`.

---

## 3. Tool policy

Проверяет:
- может ли агент использовать shell, git, DB client, kubectl, docker, vault, CI/CD;
- является ли операция read-only или mutating;
- допустимо ли действие в текущем режиме.

### Режимы

- `read_only`
- `safe_write`
- `human_approval_required`
- `blocked`

### Примеры правил

- shell по умолчанию только read-only;
- kubectl apply в production — только `human_approval_required`;
- чтение секретов из Vault запрещено агенту, если цель задачи не требует этого явно и нет отдельной роли;
- SQL write в production — только после human approval.

---

## 4. Output policy

Проверяет:
- нет ли в ответе секретов, токенов, PII;
- не содержит ли ответ dangerous commands;
- соблюдены ли правила secure development;
- не нарушены ли банковские требования (идемпотентность, audit trail, rollback, dual control).

### Примеры правил

- блокировать ответы, содержащие hardcoded credentials;
- блокировать Kubernetes manifests без resources/readiness/liveness для production-шаблонов;
- помечать SQL без параметризации как violation;
- блокировать код, отключающий TLS, auth, audit logging.

---

## Политики по severity

- `info`
- `warn`
- `block`
- `require_human_review`

Пример:

| Rule | Severity | Action |
|---|---|---|
| Secret in output | block | не показывать ответ |
| Prompt injection marker | warn/block | пересобрать контекст |
| Production infra change | require_human_review | не выполнять автоматически |
| Missing audit in banking flow | block | вернуть на доработку |

---

## Рекомендуемая модель правил

Политики удобно описывать как декларативные правила:

```yaml
rule_id: OUTPUT-SEC-001
scope: output
condition: hardcoded_secret_detected == true
severity: block
action: redact_and_fail
message: "Output contains a hardcoded secret"
```

---

## Минимальный policy set для production

Обязательно блокировать:
- секреты в output;
- PII без маскирования;
- hardcoded credentials;
- dangerous commands без explicit approval;
- prompt injection patterns в trusted context;
- отсутствие audit/idem potency в banking-critical flows.

---

## Связь с остальными документами

Policy engine должен использовать правила из:
- `docs/llm-threat-model.md`
- `docs/llm-testing-framework.md`
- `docs/audit-observability.md`
- `.ai/system/security-rules.md`
- `.ai/modules/banking.md`

---

## Вывод

LLM policy engine — обязательный слой для production-систем. Он не заменяет secure prompting и review, но позволяет остановить опасный запрос, опасный контекст, опасное действие и опасный output до возникновения инцидента.
