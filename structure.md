# 🪝 Grapple — Структура репозитория

**Метаданные файла**
- **Файл:** `STRUCTURE.md`
- **Версия:** 1.0
- **Дата создания:** 2026-06-02
- **Статус:** Активный
- **Тема:** Карта репозитория Grapple, назначение папок и файлов, поток данных, развёртывание

---

.env.example                 # Шаблон переменных окружения (пароли, ключи, домены)
.env                         # Реальные переменные (не коммитить)
.gitignore                   # Исключаем .env, data/, бекапы
docker-compose.yml           # Оркестратор всех сервисов
docker-compose.dev.yml       # Версия для разработки
Makefile                     # Короткие команды: make up, make backup, make health
README.md                    # Быстрый старт и описание проекта
STRUCTURE.md                 # Этот файл

services/

    gitea/
        app.ini              # Конфиг Gitea (домен, БД, отключение регистрации)

    woodpecker/
        server/              # Конфиг сервера Woodpecker
        agent/               # Конфиг раннера Woodpecker

    mattermost/
        config.json          # Преднастроенный конфиг Mattermost
        plugins/             # Предустановленные плагины

    syncthing/
        config.xml           # Базовая конфигурация Syncthing

    ntfy/
        server.yml           # Конфиг ntfy (запрет анонимного доступа)

    uptime-kuma/
        Dockerfile           # Кастомный образ при необходимости

    admin-panel/
        Dockerfile
        requirements.txt     # Python-зависимости
        src/
            app.py           # Точка входа (Flask/FastAPI)
            templates/       # HTML-шаблоны админки
            static/          # CSS, JS, логотип

nginx/
    Dockerfile
    nginx.conf               # Основной конфиг nginx
    sites/
        gitea.conf           # /git → Gitea
        woodpecker.conf      # /ci → Woodpecker
        mattermost.conf      # /chat → Mattermost
        uptime.conf          # /status → Uptime Kuma
        admin.conf           # /admin → Admin Panel

scripts/
    setup.sh                 # Первичная настройка с нуля
    backup.sh                # Локальный бэкап всех данных
    restore.sh               # Восстановление из бэкапа
    healthcheck.sh           # Проверка работоспособности сервисов

docs/
    images/                  # Скриншоты и фото
    SETUP.md                 # Подробная инструкция по развёртыванию
    MIGRATION.md             # Как мигрировать с GitHub/GitLab
    FAQ.md                   # Частые вопросы и ответы

data/
    postgres/                # Базы данных
    gitea/                   # Репозитории и настройки Gitea
    woodpecker/              # Состояние CI/CD
    mattermost/              # Файлы и сообщения Mattermost
    syncthing/               # Индекс и состояние Syncthing
    ntfy/                    # Кэш и база ntfy
    uptime-kuma/             # Данные мониторинга