# Прокси-сервис

## Краткое описание

Сценарий для сервиса-прокси или gateway, который маршрутизирует запросы к внутренним и внешним сервисам, добавляет auth, rate limiting, observability и безопасную обработку ошибок.

Подходит для:
- API gateway;
- BFF;
- internal proxy;
- integration facade.

## Какие правила особенно важны

- `.ai/system/security-rules.md`
- `.ai/project/infra-rules.md`
- `.ai/project/logging-rules.md`
- `.ai/modules/fastapi.md` или `.ai/modules/flask.md`
- `.ai/modules/nginx-apache.md`
- `.ai/modules/devops.md`

## Целевая структура

```text
project-root/
  AGENTS.md
  .ai/
  gateway/
    main.py
    routes/
    clients/
    middleware/
    security/
    observability/
      logging.py
      metrics.py
    config.py
  deploy/
    nginx/
    docker/
    k8s/
  tests/
    unit/
    integration/
  docs/
  scripts/
  pyproject.toml
  .env.example
```

## Команды для создания структуры

```powershell
New-Item -ItemType Directory -Force gateway, gateway\routes, gateway\clients, gateway\middleware, gateway\security, gateway\observability
New-Item -ItemType Directory -Force deploy, deploy\nginx, deploy\docker, deploy\k8s, tests, tests\unit, tests\integration, docs, scripts
New-Item -ItemType File -Force AGENTS.md, pyproject.toml, .env.example
New-Item -ItemType File -Force gateway\main.py, gateway\config.py, gateway\observability\logging.py, gateway\observability\metrics.py
```

```bash
mkdir -p gateway/routes gateway/clients gateway/middleware gateway/security gateway/observability
mkdir -p deploy/nginx deploy/docker deploy/k8s tests/unit tests/integration docs scripts
touch AGENTS.md pyproject.toml .env.example
touch gateway/main.py gateway/config.py gateway/observability/logging.py gateway/observability/metrics.py
```

## Что сказать Qwen Code после создания каркаса

```text
Соблюдай AGENTS.md, .ai/system/security-rules.md, .ai/project/logging-rules.md, .ai/project/infra-rules.md и .ai/modules/nginx-apache.md.
Нужно развивать прокси-сервис без утечки токенов, заголовков авторизации и внутренней маршрутизации.
Все ошибки должны быть безопасно нормализованы.
```
