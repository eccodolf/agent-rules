# Anti-fraud DSL examples

## 1. Simple rule

```yaml
rule_id: high_amount
condition:
  amount_gt: 100000
action: flag
```

Интерпретация:
- если сумма операции больше 100000, операция помечается как подозрительная.

## 2. Multi-factor rule

```yaml
rule_id: unusual_device_and_amount
condition:
  all:
    - amount_gt: 50000
    - device_is_new: true
    - country_not_in_profile_history: true
action: step_up_auth
```

Интерпретация:
- операция требует дополнительного подтверждения, если совпали несколько факторов риска.

## 3. Scoring example

```yaml
rule_id: transfer_risk_score
scoring:
  factors:
    - if: amount_gt_200000
      add: 40
    - if: device_is_new
      add: 20
    - if: ip_is_anonymous_proxy
      add: 25
    - if: transfer_outside_business_hours
      add: 10
thresholds:
  warn: 30
  block: 60
actions:
  warn: manual_review
  block: reject
```

## 4. Unsafe example

```yaml
rule_id: secret_threshold_rule
condition:
  score_gt: 57.3
metadata:
  internal_comment: "Actual production block threshold for VIP segment"
action: reject
```

Почему это плохо:
- раскрывает внутренний порог;
- может содержать коммерческую тайну;
- не подходит для общих примеров и prompt-ов.

## 5. Safe abstraction example

```yaml
rule_id: score_threshold_rule
condition:
  score_gt: HIGH_RISK_THRESHOLD
action: reject
```

Почему это лучше:
- не раскрывает реальные production thresholds;
- годится для архитектурного обсуждения и тестов.
