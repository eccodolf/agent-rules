# Anti-Fraud DSL

## Назначение

DSL для описания антифрод правил.

---

## Пример

```yaml
rule: high_amount
condition: amount > 100000
action: flag
```

---

## Расширение

- multi-factor
- scoring

---

## Вывод

DSL позволяет формализовать риск-логику.
