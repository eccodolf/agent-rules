# DevOps-пайплайн

## Краткое описание

Сценарий для репозитория с CI/CD, инфраструктурой и operational automation, где Qwen Code помогает с пайплайнами, deploy-конфигурацией и безопасными скриптами.

Подходит для:
- платформенных репозиториев;
- deployment repos;
- infrastructure automation;
- CI/CD templates.

## Какие правила особенно важны

- `.ai/system/security-rules.md`
- `.ai/system/output-rules.md`
- `.ai/project/infra-rules.md`
- `.ai/project/logging-rules.md`
- `.ai/project/secrets-rules.md`
- `.ai/modules/devops.md`
- `.ai/modules/kubernetes.md`
- `.ai/modules/docker-compose.md`
- `.ai/modules/vault.md`

## Целевая структура

```text
project-root/
  AGENTS.md
  .ai/
  ci/
    pipelines/
    templates/
  deploy/
    docker/
    compose/
    kubernetes/
    nginx/
  scripts/
    release/
    rollback/
    checks/
  docs/
    runbooks/
  tests/
    smoke/
  .env.example
  Makefile
  pyproject.toml
```

## Команды для создания структуры

```powershell
New-Item -ItemType Directory -Force ci, ci\pipelines, ci\templates
New-Item -ItemType Directory -Force deploy, deploy\docker, deploy\compose, deploy\kubernetes, deploy\nginx
New-Item -ItemType Directory -Force scripts, scripts\release, scripts\rollback, scripts\checks, docs, docs\runbooks, tests, tests\smoke
New-Item -ItemType File -Force AGENTS.md, .env.example, Makefile, pyproject.toml
```

```bash
mkdir -p ci/pipelines ci/templates
mkdir -p deploy/docker deploy/compose deploy/kubernetes deploy/nginx
mkdir -p scripts/release scripts/rollback scripts/checks docs/runbooks tests/smoke
touch AGENTS.md .env.example Makefile pyproject.toml
```

## Что сказать Qwen Code после создания каркаса

```text
Соблюдай AGENTS.md, .ai/system/security-rules.md, .ai/system/output-rules.md, .ai/project/infra-rules.md, .ai/project/logging-rules.md, .ai/project/secrets-rules.md и .ai/modules/devops.md.
Нужно генерировать только воспроизводимые и rollback-friendly pipeline changes.
Не ослабляй security controls и не пиши секреты в CI/CD-конфигурацию.
```
