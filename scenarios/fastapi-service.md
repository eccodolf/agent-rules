# FastAPI-сервис

## Краткое описание

Сценарий для backend-сервиса на FastAPI с service layer, repository layer, PostgreSQL и опционально Celery/Redis.

Подходит для:
- внутренних API;
- интеграционных сервисов;
- CRUD и workflow API;
- банковских backend-сервисов.

## Какие правила особенно важны

- `.ai/system/security-rules.md`
- `.ai/system/context-rules.md`
- `.ai/project/coding-rules.md`
- `.ai/project/testing-rules.md`
- `.ai/project/logging-rules.md`
- `.ai/modules/fastapi.md`
- `.ai/modules/postgres.md`
- `.ai/modules/celery.md`, если есть async processing
- `.ai/modules/redis.md`, если есть cache или lock

## Целевая структура

```text
project-root/
  AGENTS.md
  .ai/
  app/
    main.py
    api/
      routers/
      dependencies/
    services/
    repositories/
    schemas/
    models/
    db/
      session.py
      migrations/
    workers/
    core/
      config.py
      logging.py
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
git sparse-checkout set .ai templates/scenarios/fastapi-service
Set-Location ..
Copy-Item -Recurse -Force _bootstrap\.ai .
Copy-Item -Recurse -Force _bootstrap\templates\scenarios\fastapi-service\* .
Remove-Item -Recurse -Force _bootstrap
```

```bash
repo="https://github.com/eccodolf/agent-rules.git"
git clone --depth 1 --filter=blob:none --sparse "$repo" _bootstrap
cd _bootstrap
git sparse-checkout set .ai templates/scenarios/fastapi-service
cd ..
cp -R _bootstrap/.ai ./
cp -R _bootstrap/templates/scenarios/fastapi-service/. ./
rm -rf _bootstrap
```

## Что сказать Qwen Code после создания каркаса

```text
Соблюдай AGENTS.md, .ai/system/security-rules.md, .ai/project/coding-rules.md, .ai/project/testing-rules.md, .ai/project/logging-rules.md, .ai/modules/fastapi.md и .ai/modules/postgres.md.
Нужно развивать только существующую структуру app/api, services, repositories, schemas.
Не пиши SQL в endpoint и не логируй персональные данные.
```
