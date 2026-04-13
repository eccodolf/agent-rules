# Prompt DSL examples

## 1. FastAPI endpoint

```text
ROLE:
Senior Python backend developer

CONTEXT:
- FastAPI service
- existing router/service/repository structure
- pydantic v2

TASK:
Add POST /customers endpoint with validation and duplicate protection.

CONSTRAINTS:
- keep diff minimal
- do not change existing response format
- add tests

SECURITY:
- no secrets
- do not log personal data
- parameterized SQL only

OUTPUT:
- file structure
- code by files
- tests
```

## 2. Django object state change

```text
ROLE:
Senior Django developer

CONTEXT:
- Django app with object-level permissions
- request status workflow already exists

TASK:
Implement safe status transition for approval flow.

CONSTRAINTS:
- use service layer
- keep backward compatibility
- use transaction.atomic

SECURITY:
- audit logging required
- no sensitive fields in logs
- validate permissions on object level

OUTPUT:
- approach
- code
- review checklist
```

## 3. Kubernetes rollout

```text
ROLE:
DevOps engineer

CONTEXT:
- Kubernetes deployment for internal API
- production-like environment

TASK:
Prepare safe deployment manifest update for a new image version.

CONSTRAINTS:
- fixed image tag
- readiness/liveness required
- rollback path must be explicit

SECURITY:
- do not weaken RBAC
- do not expose secrets

OUTPUT:
- yaml
- pre-checks
- post-checks
- rollback steps
```

## 4. Banking payment flow

```text
ROLE:
Backend architect for banking systems

CONTEXT:
- payment initiation service
- PostgreSQL + Celery + Redis

TASK:
Design payment processing flow with duplicate protection and audit trail.

CONSTRAINTS:
- idempotency required
- retry-safe async processing
- explicit transaction boundaries

SECURITY:
- no real client data
- do not expose anti-fraud thresholds
- audit logging mandatory

OUTPUT:
- architecture
- sequence of steps
- data consistency risks
- required tests
```
