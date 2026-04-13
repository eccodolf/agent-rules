# Examples

Этот каталог содержит короткие, но прикладные примеры для настройки policy engine, формирования prompt-ов и безопасного логирования.

Что здесь лежит:
- `policy-rules.yaml` — декларативные policy rules для input, context, tools и output.
- `prompt-dsl-examples.md` — примеры хорошо сформулированных запросов для backend, DevOps и banking-задач.
- `prompt-compiler-examples.md` — примеры преобразования DSL в нормализованный prompt.
- `logging-examples.md` — примеры безопасного логирования и redaction.
- `observability-examples.md` — примеры метрик, trace и alerting.
- `decision-logging-examples.md` — примеры decision log для allow, block и approval required.
- `runtime-guardrails-examples.md` — примеры guardrail-решений и violation responses.
- `testing-examples.md` — примеры prompt, scenario, regression и security tests.
- `synthetic-test-data-examples.md` — примеры безопасных synthetic datasets и masking.
- `simulation-environment-examples.md` — примеры безопасного simulation-контура и сценариев.
- `banking-scenarios.md` — примеры обязательных контролей для платежных и антифрод-сценариев.
- `anti-fraud-dsl-examples.md` — примеры правил anti-fraud DSL и безопасной абстракции порогов.
- `module-end-to-end-examples.md` — примеры, какие `.ai`-правила подключать для типовых end-to-end задач.
- `.agentignore.example` — пример безопасного `.agentignore`.

Как использовать:
- брать как шаблон и адаптировать под свой контур;
- не копировать примеры без проверки под конкретный стек и политику доступа;
- не вставлять в примеры реальные секреты, персональные данные, банковскую или коммерческую тайну.
