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

## Команды для получения каркаса из git

```powershell
$repo = "https://github.com/eccodolf/agent-rules.git"
git clone --depth 1 --filter=blob:none --sparse $repo _bootstrap
Set-Location _bootstrap
git sparse-checkout set .ai templates/scenarios/devops-pipeline
Set-Location ..
Copy-Item -Recurse -Force _bootstrap\.ai .
Copy-Item -Recurse -Force _bootstrap\templates\scenarios\devops-pipeline\* .
Remove-Item -Recurse -Force _bootstrap
```

```bash
repo="https://github.com/eccodolf/agent-rules.git"
git clone --depth 1 --filter=blob:none --sparse "$repo" _bootstrap
cd _bootstrap
git sparse-checkout set .ai templates/scenarios/devops-pipeline
cd ..
cp -R _bootstrap/.ai ./
cp -R _bootstrap/templates/scenarios/devops-pipeline/. ./
rm -rf _bootstrap
```

## Что сказать Qwen Code после создания каркаса

```text
Соблюдай AGENTS.md, .ai/system/security-rules.md, .ai/system/output-rules.md, .ai/project/infra-rules.md, .ai/project/logging-rules.md, .ai/project/secrets-rules.md и .ai/modules/devops.md.
Нужно генерировать только воспроизводимые и rollback-friendly pipeline changes.
Не ослабляй security controls и не пиши секреты в CI/CD-конфигурацию.
```
