# Nginx / Apache rules

## Основные принципы

- включать TLS
- не открывать лишние порты

## Практика

- rate limiting
- logging

## Логирование

- Логировать только те поля доступа, которые реально нужны для диагностики и аудита.
- Не логировать authorization headers, session tokens и чувствительные query parameters.
- Для proxy errors логировать upstream, status class и timing без утечки внутренних деталей.
- При настройке access logs учитывать требования по персональным данным, банковской и коммерческой тайне.
