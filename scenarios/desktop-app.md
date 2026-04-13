# Десктопное приложение

## Краткое описание

Сценарий для desktop-приложения с локальным UI, сервисным слоем, хранением настроек и опциональной синхронизацией с backend.

Подходит для:
- внутреннего операционного ПО;
- толстого клиента;
- desktop utility с локальными данными и удаленными API.

## Какие правила особенно важны

- `.ai/system/security-rules.md`
- `.ai/system/context-rules.md`
- `.ai/project/coding-rules.md`
- `.ai/project/testing-rules.md`
- `.ai/project/secrets-rules.md`
- `.ai/project/logging-rules.md`

Если приложение использует встроенный локальный прокси или API:
- `.ai/modules/fastapi.md` или `.ai/modules/flask.md`

## Целевая структура

```text
project-root/
  AGENTS.md
  .ai/
  src/
    app/
    ui/
    services/
    storage/
    security/
    logging/
    config/
  tests/
    unit/
    integration/
  assets/
  docs/
  scripts/
  pyproject.toml
  .env.example
```

## Команды для создания структуры

```powershell
New-Item -ItemType Directory -Force src, src\app, src\ui, src\services, src\storage, src\security, src\logging, src\config
New-Item -ItemType Directory -Force tests, tests\unit, tests\integration, assets, docs, scripts
New-Item -ItemType File -Force AGENTS.md, pyproject.toml, .env.example
```

```bash
mkdir -p src/app src/ui src/services src/storage src/security src/logging src/config
mkdir -p tests/unit tests/integration assets docs scripts
touch AGENTS.md pyproject.toml .env.example
```

## Что сказать Qwen Code после создания каркаса

```text
Соблюдай AGENTS.md, .ai/system/security-rules.md, .ai/project/coding-rules.md, .ai/project/testing-rules.md, .ai/project/secrets-rules.md и .ai/project/logging-rules.md.
Нужно развивать desktop-приложение так, чтобы секреты не попадали в конфиг, UI-логи и crash output.
Разделяй UI, сервисы и локальное хранилище.
```
