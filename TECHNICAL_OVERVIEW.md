# Technical Overview

## Architecture

Rise of Legends — full-stack платформа на Next.js и Supabase. Next.js обслуживает публичные страницы, ролевые кабинеты и административный интерфейс. PostgreSQL является источником истины для участников, команд, заявок и турнирного состояния.

```text
User
  ↓
Next.js application
  ↓
Supabase services
  ↓
PostgreSQL
```

## Frontend

- Next.js 16 и App Router;
- React 19;
- TypeScript 6 в strict mode;
- адаптивные публичные и закрытые интерфейсы;
- серверная загрузка публичных данных с ревалидацией;
- обработка временной недоступности данных.

## Backend and Data

- Supabase Auth и Twitch OAuth;
- PostgreSQL Functions и RPC;
- Row Level Security;
- транзакционные операции для связанных изменений;
- Supabase Storage для пользовательских изображений;
- серверная email-интеграция через Resend.

## Security Approach

- разделение публичных, пользовательских и административных операций;
- проверка роли и владения данными на серверной стороне;
- ограничение критических записей специализированными операциями;
- одноразовые персональные приглашения;
- проверка подписей входящих webhook;
- серверные секреты хранятся только в production-окружении;
- ограничение размеров запросов и частоты чувствительных email-операций.

## Quality and Operations

- ESLint и TypeScript typecheck;
- production build;
- автоматический smoke-тест основных маршрутов и закрытого API-периметра;
- GitHub Actions для push и pull request;
- Dependabot с ручным рассмотрением обновлений;
- простой и глубокий health-check;
- PM2 и post-deployment log review.

## Deployment

Production работает на Ubuntu VPS как Next.js server под управлением PM2. Deployment остаётся контролируемым ручным процессом с проверкой сборки, состояния приложения, базы данных и журналов.

## Repository Boundary

Production-код, полная схема данных, миграции, приватные настройки и эксплуатационные детали находятся в закрытом репозитории. Публичный showcase предназначен для профессиональной презентации архитектурного подхода и результата.

