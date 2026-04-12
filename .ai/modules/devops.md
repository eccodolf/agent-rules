# DevOps module rules

## Основные принципы

- Infrastructure as Code
- Immutable infrastructure
- Reproducible builds
- Least privilege

## Безопасность

- Не выполнять destructive операции без подтверждения
- Ограничивать доступ к production
- Использовать audit logging

## Примеры промптов

### Простой

```text
Напиши Dockerfile для Python приложения.
```

### Средний

```text
Сгенерируй docker-compose для FastAPI + Postgres + Redis.
```

### Сложный

```text
Ты DevOps инженер банковской системы.

Задача:
Спроектировать CI/CD pipeline.

Ограничения:
- безопасность
- rollback
- audit

Формат:
- схема
- yaml
```
