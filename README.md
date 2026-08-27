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
## Known issues
На Windows + WSL2 (Docker Desktop) сервисы `db`/`worker`/`vote` падают с `exec format error` —
похоже на проблему архитектуры/эмуляции конкретно в этом окружении, а не в самом compose-файле
(конфиг проходит `docker compose config` без ошибок). Не воспроизводилось на Linux-хосте.


## CI/CD
Добавлен пайплайн `.github/workflows/validate.yml` — запускается на каждый push,
проверяет `docker compose config` (ловит синтаксические ошибки в compose-файле).

Проверено на реальной ошибке: сломал `services:` → `servicess:`, запушил —
пайплайн упал за 6 секунд с ошибкой "additional properties 'servicess' not allowed".
Значит проверка реально работает, а не просто формальность.