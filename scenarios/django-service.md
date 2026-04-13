# Django-сервис

## Краткое описание

Сценарий для внутреннего Django-сервиса с API, административным интерфейсом, service layer и PostgreSQL.

Подходит для:
- внутренних порталов;
- workflow-систем;
- approval flows;
- сервисов с объектными правами и audit trail.

## Какие правила особенно важны

- `.ai/system/security-rules.md`
- `.ai/system/context-rules.md`
- `.ai/project/coding-rules.md`
- `.ai/project/testing-rules.md`
- `.ai/project/database-rules.md`
- `.ai/modules/django.md`
- `.ai/modules/postgres.md`
- `.ai/modules/banking.md`, если есть финансовый или approval-critical контур

## Целевая структура

```text
project-root/
  AGENTS.md
  .ai/
  app/
    manage.py
    config/
      settings/
        base.py
        dev.py
        prod.py
      urls.py
      wsgi.py
      asgi.py
    apps/
      customers/
        models.py
        views.py
        services.py
        selectors.py
        forms.py
        urls.py
        tests/
      audit/
        models.py
        services.py
        tests/
  docs/
  tests/
  scripts/
  requirements/
  pyproject.toml
  .env.example
```

## Команды для получения каркаса из git

```powershell
$repo = "https://github.com/eccodolf/agent-rules.git"
git clone --depth 1 --filter=blob:none --sparse $repo _bootstrap
Set-Location _bootstrap
git sparse-checkout set .ai templates/scenarios/django-service
Set-Location ..
Copy-Item -Recurse -Force _bootstrap\.ai .
Copy-Item -Recurse -Force _bootstrap\templates\scenarios\django-service\* .
Remove-Item -Recurse -Force _bootstrap
```

```bash
repo="https://github.com/eccodolf/agent-rules.git"
git clone --depth 1 --filter=blob:none --sparse "$repo" _bootstrap
cd _bootstrap
git sparse-checkout set .ai templates/scenarios/django-service
cd ..
cp -R _bootstrap/.ai ./
cp -R _bootstrap/templates/scenarios/django-service/. ./
rm -rf _bootstrap
```

## Что сказать Qwen Code после создания каркаса

Пример запроса:

```text
Соблюдай AGENTS.md, .ai/system/security-rules.md, .ai/project/coding-rules.md, .ai/project/testing-rules.md, .ai/modules/django.md и .ai/modules/postgres.md.
Нужно реализовать Django app customers без нарушения текущей структуры.
Не смешивай бизнес-логику с views.
```
