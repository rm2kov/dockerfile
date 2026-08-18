# Docker Compose: Voting App (учебный проект)

Учебный запуск многоконтейнерного приложения через Docker Compose.
Основано на официальном примере Docker [example-voting-app].

## Что делает
Поднимает 5 сервисов: голосование (Python) → Redis → воркер (.NET) → Postgres → результаты (Node.js).
Демонстрирует связку контейнеров через `links`/сеть и работу multi-service compose-файла.

## Как запустить
\`\`\`bash
docker compose up -d
\`\`\`
Голосование: http://localhost:5000
Результаты: http://localhost:5001

## Что понял / чему научился
- Как сервисы в compose видят друг друга по имени (redis:redis вместо IP).
- Разница между `links` и обычной docker-сетью (сейчас links — устаревший способ, стоит перейти на networks).
- Нашёл и починил битый отступ в environment-секции — YAML чувствителен к пробелам.

## Источник
Пример на основе [dockersamples/example-voting-app](https://github.com/dockersamples/example-voting-app)
