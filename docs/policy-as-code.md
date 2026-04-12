# Policy-as-Code для LLM

## Назначение

Policy-as-code — это подход, при котором политики безопасности и поведения агента описываются как код (например YAML/JSON), а не как текстовая документация.

---

## Пример

```yaml
rule_id: INPUT-001
condition: contains("ignore previous instructions")
action: block
```

---

## Преимущества

- версионирование
- автоматизация
- тестируемость

---

## Интеграция

- policy engine
- runtime guardrails

---

## Вывод

Policy-as-code — основа масштабируемых AI систем.
