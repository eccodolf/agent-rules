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

## Команды для получения каркаса из git

```powershell
$repo = "https://github.com/eccodolf/agent-rules.git"
git clone --depth 1 --filter=blob:none --sparse $repo _bootstrap
Set-Location _bootstrap
git sparse-checkout set .ai templates/scenarios/desktop-app
Set-Location ..
Copy-Item -Recurse -Force _bootstrap\.ai .
Copy-Item -Recurse -Force _bootstrap\templates\scenarios\desktop-app\* .
Remove-Item -Recurse -Force _bootstrap
```

```bash
repo="https://github.com/eccodolf/agent-rules.git"
git clone --depth 1 --filter=blob:none --sparse "$repo" _bootstrap
cd _bootstrap
git sparse-checkout set .ai templates/scenarios/desktop-app
cd ..
cp -R _bootstrap/.ai ./
cp -R _bootstrap/templates/scenarios/desktop-app/. ./
rm -rf _bootstrap
```

## Что сказать Qwen Code после создания каркаса

```text
Соблюдай AGENTS.md, .ai/system/security-rules.md, .ai/project/coding-rules.md, .ai/project/testing-rules.md, .ai/project/secrets-rules.md и .ai/project/logging-rules.md.
Нужно развивать desktop-приложение так, чтобы секреты не попадали в конфиг, UI-логи и crash output.
Разделяй UI, сервисы и локальное хранилище.
```
