# Decision Logging для LLM-агента

## Назначение

Decision logging фиксирует не только результат, но и процесс принятия решения агентом.

---

## Что логировать

- входной запрос (обезличенный)
- используемые источники
- выбранные правила (.ai/*)
- принятые ограничения
- итоговое решение

---

## Пример

```json
{
  "task": "generate endpoint",
  "rules_used": ["fastapi.md", "security-rules.md"],
  "constraints": ["no secrets", "audit logging"],
  "decision": "used service layer pattern"
}
```

---

## Требования

- без секретов
- без персональных данных
- структурированный формат

---

## Вывод

Decision logging нужен для explainability и аудита.
