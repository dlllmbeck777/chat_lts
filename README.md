# Private Chat Platform

Это репозиторий проекта "Private Chat". Вся инфраструктура и оба сервиса (frontend и backend) настроены на работу в Docker.

## Требования
- Docker
- Docker Compose

## Инструкция по запуску и инициализации (Первый запуск)

Поскольку в репозитории пока только файлы Docker (Dockerfile, docker-compose.yml), сначала нужно сгенерировать файлы проектов NestJS и Next.js.
Вы можете сделать это через временные Docker-контейнеры.

**1. Инициализация Backend (NestJS):**
Откройте терминал в папке `D:\Projects\chats` и выполните:
```bash
docker run --rm -it -v "%cd%/backend:/usr/src/app" -w /usr/src/app node:18-alpine sh -c "npm install -g @nestjs/cli && nest new . --package-manager npm --strict --skip-git --directory ."
```

**2. Инициализация Frontend (Next.js):**
В той же папке выполните:
```bash
docker run --rm -it -v "%cd%/frontend:/usr/src/app" -w /usr/src/app node:18-alpine sh -c "npx create-next-app@latest . --ts --tailwind --eslint --app --src-dir --import-alias '@/*' --use-npm"
```

**3. Запуск всех сервисов (PostgreSQL, Backend, Frontend):**
```bash
docker-compose up --build -d
```

## Как это работает?
- `db`: База данных PostgreSQL (порт 5432)
- `backend`: NestJS API (порт 3001)
- `frontend`: Next.js интерфейс (порт 3000)

Код проброшен через `volumes`, поэтому любые изменения в папках `backend` или `frontend` будут автоматически отражаться (hot-reload) благодаря `npm run start:dev` и `npm run dev`.