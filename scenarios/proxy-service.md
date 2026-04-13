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

## Команды для получения каркаса из git

```powershell
$repo = "https://github.com/eccodolf/agent-rules.git"
git clone --depth 1 --filter=blob:none --sparse $repo _bootstrap
Set-Location _bootstrap
git sparse-checkout set .ai templates/scenarios/proxy-service
Set-Location ..
Copy-Item -Recurse -Force _bootstrap\.ai .
Copy-Item -Recurse -Force _bootstrap\templates\scenarios\proxy-service\* .
Remove-Item -Recurse -Force _bootstrap
```

```bash
repo="https://github.com/eccodolf/agent-rules.git"
git clone --depth 1 --filter=blob:none --sparse "$repo" _bootstrap
cd _bootstrap
git sparse-checkout set .ai templates/scenarios/proxy-service
cd ..
cp -R _bootstrap/.ai ./
cp -R _bootstrap/templates/scenarios/proxy-service/. ./
rm -rf _bootstrap
```

## Что сказать Qwen Code после создания каркаса

```text
Соблюдай AGENTS.md, .ai/system/security-rules.md, .ai/project/logging-rules.md, .ai/project/infra-rules.md и .ai/modules/nginx-apache.md.
Нужно развивать прокси-сервис без утечки токенов, заголовков авторизации и внутренней маршрутизации.
Все ошибки должны быть безопасно нормализованы.
```
