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

## Команды для создания структуры

```powershell
New-Item -ItemType Directory -Force app, app\api, app\api\routers, app\api\dependencies, app\services, app\repositories, app\schemas, app\models, app\db, app\db\migrations, app\workers, app\core
New-Item -ItemType Directory -Force tests, tests\unit, tests\integration, docs, scripts
New-Item -ItemType File -Force AGENTS.md, pyproject.toml, .env.example
New-Item -ItemType File -Force app\main.py, app\db\session.py, app\core\config.py, app\core\logging.py
```

```bash
mkdir -p app/api/routers app/api/dependencies app/services app/repositories app/schemas app/models app/db/migrations app/workers app/core
mkdir -p tests/unit tests/integration docs scripts
touch AGENTS.md pyproject.toml .env.example
touch app/main.py app/db/session.py app/core/config.py app/core/logging.py
```

## Что сказать Qwen Code после создания каркаса

```text
Соблюдай AGENTS.md, .ai/system/security-rules.md, .ai/project/coding-rules.md, .ai/project/testing-rules.md, .ai/project/logging-rules.md, .ai/modules/fastapi.md и .ai/modules/postgres.md.
Нужно развивать только существующую структуру app/api, services, repositories, schemas.
Не пиши SQL в endpoint и не логируй персональные данные.
```
