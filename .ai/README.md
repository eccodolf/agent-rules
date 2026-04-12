# Шаблон директории `.ai/` для проектов в банковском секторе

Этот каталог содержит готовый шаблон правил для локальных AI-агентов, работающих с проектами на стеке:
- Python
- FastAPI / Django / Flask
- Vault
- Celery
- PostgreSQL
- Redis
- boto3
- Yandex Cloud
- VPS / DevOps
- Nginx / Apache
- Oracle Linux
- Docker / Docker Compose
- Kubernetes

Шаблон ориентирован на использование в проектах банковского сектора, где действуют повышенные требования к:
- защите данных;
- безопасной разработке;
- аудиту;
- минимизации контекста;
- воспроизводимости действий агента.

## Рекомендуемая структура

```text
.ai/
  README.md
  system/
    platform-rules.md
    security-rules.md
    secure-development.md
    prompting-rules.md
    context-rules.md
    output-rules.md
  project/
    repository-rules.md
    architecture-rules.md
    coding-rules.md
    testing-rules.md
    api-rules.md
    database-rules.md
    infra-rules.md
    secrets-rules.md
    logging-rules.md
    review-checklist.md
    prompt-templates.md
  modules/
    fastapi.md
    django.md
    flask.md
    celery.md
    postgres.md
    redis.md
    vault.md
    boto-yandex-cloud.md
    docker-compose.md
    kubernetes.md
    nginx-apache.md
    devops.md
    banking.md
```

## Как использовать

1. Начинать чтение с `AGENTS.md` в корне проекта.
2. Затем подключать `.ai/system/*`.
3. Потом `.ai/project/*`.
4. И только после этого — нужный модульный файл из `.ai/modules/*`.
5. Не включать в контекст весь `.ai/` целиком без необходимости.

## Приоритет инструкций

1. `.ai/system/*`
2. `.ai/project/*`
3. `.ai/modules/*`
4. локальный запрос пользователя

При конфликте побеждает более высокий уровень.

## Обязательные правила

- Не передавать в модель секреты, реальные ключи, пароли, токены, сертификаты, закрытые ключи.
- Не доверять результатам модели без проверки.
- Любой сгенерированный код должен проходить review, тестирование и статический анализ.
- Любые инфраструктурные и эксплуатационные изменения должны быть обратимыми.
- Любые действия, влияющие на безопасность, должны быть явно помечены и проверены человеком.
