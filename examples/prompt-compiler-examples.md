# Prompt compiler examples

## 1. Simple backend example

### DSL input

```text
ROLE: Senior Python backend developer
CONTEXT: FastAPI service
TASK: Add GET /health endpoint
CONSTRAINTS: keep diff minimal
SECURITY: no secrets
OUTPUT: code only
```

### Compiled prompt

```text
Ты Senior Python backend developer.

Контекст:
FastAPI service

Задача:
Add GET /health endpoint

Ограничения:
keep diff minimal

Требования безопасности:
no secrets

Формат ответа:
code only
```

## 2. DevOps example

### DSL input

```text
ROLE: DevOps engineer
CONTEXT: Kubernetes deployment for internal API
TASK: Prepare rollout for new image tag
CONSTRAINTS:
- fixed image tag
- readiness/liveness required
- rollback required
SECURITY:
- do not expose secrets
- do not weaken RBAC
OUTPUT:
- yaml
- pre-checks
- post-checks
```

### Compiled prompt

```text
Ты DevOps engineer.

Контекст:
Kubernetes deployment for internal API

Задача:
Prepare rollout for new image tag

Ограничения:
- fixed image tag
- readiness/liveness required
- rollback required

Требования безопасности:
- do not expose secrets
- do not weaken RBAC

Формат ответа:
- yaml
- pre-checks
- post-checks
```

## 3. Banking example

### DSL input

```text
ROLE: Backend architect
CONTEXT:
- payment initiation service
- PostgreSQL + Celery + Redis
TASK: Design payment flow with duplicate protection
CONSTRAINTS:
- idempotency
- retry safe
- explicit transaction boundaries
SECURITY:
- no real client data
- audit logging mandatory
- do not expose anti-fraud thresholds
OUTPUT:
- architecture
- risks
- tests
```

### Compiled prompt

```text
Ты Backend architect.

Контекст:
- payment initiation service
- PostgreSQL + Celery + Redis

Задача:
Design payment flow with duplicate protection

Ограничения:
- idempotency
- retry safe
- explicit transaction boundaries

Требования безопасности:
- no real client data
- audit logging mandatory
- do not expose anti-fraud thresholds

Формат ответа:
- architecture
- risks
- tests
```
