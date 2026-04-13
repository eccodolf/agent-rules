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

## Команды для создания структуры

```powershell
New-Item -ItemType Directory -Force app, docs, tests, scripts, requirements
New-Item -ItemType Directory -Force app\config, app\config\settings, app\apps, app\apps\customers, app\apps\customers\tests, app\apps\audit, app\apps\audit\tests
New-Item -ItemType File -Force AGENTS.md, pyproject.toml, .env.example
New-Item -ItemType File -Force app\manage.py, app\config\urls.py, app\config\wsgi.py, app\config\asgi.py
New-Item -ItemType File -Force app\config\settings\base.py, app\config\settings\dev.py, app\config\settings\prod.py
New-Item -ItemType File -Force app\apps\customers\models.py, app\apps\customers\views.py, app\apps\customers\services.py, app\apps\customers\selectors.py, app\apps\customers\forms.py, app\apps\customers\urls.py
New-Item -ItemType File -Force app\apps\audit\models.py, app\apps\audit\services.py
```

```bash
mkdir -p app/config/settings app/apps/customers/tests app/apps/audit/tests docs tests scripts requirements
touch AGENTS.md pyproject.toml .env.example
touch app/manage.py app/config/urls.py app/config/wsgi.py app/config/asgi.py
touch app/config/settings/base.py app/config/settings/dev.py app/config/settings/prod.py
touch app/apps/customers/models.py app/apps/customers/views.py app/apps/customers/services.py app/apps/customers/selectors.py app/apps/customers/forms.py app/apps/customers/urls.py
touch app/apps/audit/models.py app/apps/audit/services.py
```

## Что сказать Qwen Code после создания каркаса

Пример запроса:

```text
Соблюдай AGENTS.md, .ai/system/security-rules.md, .ai/project/coding-rules.md, .ai/project/testing-rules.md, .ai/modules/django.md и .ai/modules/postgres.md.
Нужно реализовать Django app customers без нарушения текущей структуры.
Не смешивай бизнес-логику с views.
```
