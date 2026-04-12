# Runtime Guardrails для LLM-агента

## Назначение

Runtime guardrails — это механизмы контроля, которые работают во время выполнения запроса и ограничивают опасное поведение агента до того, как ответ будет показан пользователю или действие будет выполнено.

Guardrails применяются в runtime и дополняют:
- prompt engineering;
- policy engine;
- `.ai`-правила;
- аудит и наблюдаемость.

---

## Цели

- блокировать опасный output;
- запрещать небезопасные tool actions;
- предотвращать утечки данных;
- навязывать безопасный формат ответа;
- останавливать опасную автоматизацию до выполнения side effect.

---

## Уровни runtime guardrails

1. **Input guardrails**
2. **Context guardrails**
3. **Generation guardrails**
4. **Output guardrails**
5. **Action guardrails**

---

## 1. Input guardrails

Проверяют:
- jailbreak-паттерны;
- попытки override системных правил;
- запросы на секреты, приватные ключи, учетные данные;
- прямые destructive intent.

### Примеры

- блокировать `ignore previous instructions`;
- блокировать `show secrets`, `print env`, `read private key`;
- повышать risk score для `rm -rf`, `DROP DATABASE`, `kubectl delete`.

---

## 2. Context guardrails

Проверяют состав контекста до генерации:
- соответствует ли `.agentignore`;
- нет ли запрещенных файлов;
- нет ли секретов, PII, бинарей, логов без редактирования;
- не превышен ли budget по токенам.

### Примеры

- запрещать `.env`, `keys/`, `secrets/`, дампы БД;
- запрещать raw-логи с платежными реквизитами;
- вырезать чувствительные поля или заменять их масками.

---

## 3. Generation guardrails

Применяются в процессе генерации или сразу после chunk/stream этапа.

### Цели

- прервать генерацию при появлении опасных паттернов;
- обнаружить секреты, токены, ключи;
- остановить вывод запрещенных команд;
- навязать структуру output.

### Примеры

- если output содержит приватный ключ PEM — остановить и заменить на violation message;
- если выводится hardcoded password — прервать генерацию;
- если возникает shell-команда для production без approval flag — пометить как blocked.

---

## 4. Output guardrails

Проверяют финальный ответ перед показом:
- нет ли утечки секретов;
- нет ли PII без маскирования;
- нет ли нарушения secure-development правил;
- нет ли обязательных банковских контролей, которые пропущены.

### Контрольные проверки

- есть ли audit logging в финансовом сценарии;
- есть ли idempotency в платежных операциях;
- есть ли retry-safe pattern в асинхронной обработке;
- есть ли параметризация в SQL.

---

## 5. Action guardrails

Применяются перед выполнением инструментального действия:
- shell
- git write
- DB write
- Vault read
- docker/kubectl apply
- deployment / CI/CD actions

### Принцип

Каждое действие должно иметь:
- classification (`read_only`, `mutating`, `privileged`, `production_critical`)
- risk score
- policy decision (`allow`, `deny`, `require_human_review`)

---

## Режимы работы

### Soft mode

- пишет предупреждение;
- помечает нарушение;
- не блокирует действие автоматически.

### Strict mode

- блокирует запрещенный ответ;
- блокирует tool call;
- требует human review для high-risk действий.

Для банковского production рекомендуется strict mode.

---

## Формат violation response

Guardrail не должен просто «ломать» ответ. Он должен возвращать управляемое сообщение:

```json
{
  "status": "blocked",
  "reason_code": "OUTPUT_SECRET_DETECTED",
  "message": "Response blocked by runtime guardrail policy",
  "next_step": "Provide redacted context or request human review"
}
```

---

## Минимальный набор runtime guardrails

Обязательно:
- secret detector;
- PII detector;
- destructive command detector;
- SQL safety check;
- infra change approval gate;
- banking flow mandatory controls checker.

---

## Связь с policy engine

Policy engine определяет правила.
Runtime guardrails обеспечивают их применение во время выполнения.

Упрощенно:
- policy engine = policy brain
- runtime guardrails = enforcement layer

---

## Вывод

Без runtime guardrails агент остается слишком доверенным в момент выполнения. Для production и особенно для банковских сценариев runtime guardrails обязательны, если у агента есть доступ к инструментам, контексту проекта и операциям с побочным эффектом.
