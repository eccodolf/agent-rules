# DevOps module rules

## Основные принципы

- Infrastructure as Code
- Immutable infrastructure
- Reproducible builds
- Least privilege
- Observable deployments

## Безопасность

- Не выполнять destructive операции без подтверждения.
- Ограничивать доступ к production.
- Использовать audit logging.
- Не хранить секреты в pipeline config и shell history.
- Не ослаблять verification и rollout controls ради скорости.

## Надежность и эксплуатация

- Любой pipeline должен иметь понятные pre-checks и post-checks.
- Для deploy нужен rollback path.
- Для release нужно фиксировать версии артефактов и зависимостей.
- Для критичных задач нужен health verification после применения.
- Не полагаться на ручные шаги, если они могут быть автоматизированы безопасно.

## Что должен учитывать output

- среду применения;
- риск и blast radius;
- порядок шагов;
- условия отката;
- что проверять после выката.

## Что запрещено

- команды, которые меняют production без подтверждения;
- небезопасные `curl | sh` и аналогичные паттерны;
- деплой без observability и health checks;
- mutable infra-паттерны без обоснования.
