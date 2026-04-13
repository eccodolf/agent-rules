# Kubernetes rules

## Основные принципы

- всегда задавать resources
- использовать readiness/liveness probes
- не использовать latest

## Безопасность

- не хардкодить секреты
- использовать secrets

## Практика

- использовать namespaces
- ограничивать права

## Логирование

- Логировать версию манифеста, namespace, release identifier и outcome применения изменений.
- Не выводить содержимое secret manifests, токены и чувствительные env values.
- Для rollout проблем логирование должно позволять отличить scheduling issues, readiness failures, image pull errors и runtime crashes.
- Для production-изменений нужен audit-friendly контекст: кто применял, что применялось и с каким результатом.
