# 🪝 Grapple — Структура репозитория

**Метаданные файла**
- **Файл:** `STRUCTURE.md`
- **Версия:** 1.0
- **Дата создания:** 2026-06-02
- **Статус:** Активный
- **Тема:** Карта репозитория Grapple, назначение папок и файлов, поток данных, развёртывание

---

grapple/
│
├── .env.example                 # Шаблон переменных окружения (пароли, ключи, домены)
├── .env                         # Реальные переменные (не коммитить)
├── .gitignore                   # Исключаем .env, data/, бекапы
├── docker-compose.yml           # Оркестратор всех сервисов
├── docker-compose.dev.yml       # Версия для разработки
├── Makefile                     # Короткие команды: make up, make backup, make health
├── README.md                    # Быстрый старт и описание проекта
├── STRUCTURE.md                 # Этот файл
│
├── services/                    # Конфигурация каждого сервиса
│   ├── gitea/                   # Git-хостинг
│   │   └── app.ini              # Конфиг Gitea
│   │
│   ├── woodpecker/              # CI/CD
│   │   ├── server/              # Конфиг сервера Woodpecker
│   │   └── agent/               # Конфиг раннера Woodpecker
│   │
│   ├── mattermost/              # Чат команды
│   │   ├── config.json          # Конфиг Mattermost
│   │   └── plugins/             # Предустановленные плагины
│   │
│   ├── syncthing/               # P2P-синхронизация файлов
│   │   └── config.xml           # Конфиг Syncthing
│   │
│   ├── ntfy/                    # Push-уведомления
│   │   └── server.yml           # Конфиг ntfy
│   │
│   ├── uptime-kuma/             # Мониторинг
│   │   └── Dockerfile           # Кастомный образ
│   │
│   └── admin-panel/             # Веб-админка Grapple
│       ├── Dockerfile
│       ├── requirements.txt     # Python-зависимости
│       └── src/
│           ├── app.py           # Точка входа
│           ├── templates/       # HTML-шаблоны
│           └── static/          # CSS, JS, логотип
│
├── nginx/                       # Обратный прокси
│   ├── Dockerfile
│   ├── nginx.conf               # Основной конфиг nginx
│   └── sites/                   # Конфиги виртуальных хостов
│       ├── gitea.conf           # /git → Gitea
│       ├── woodpecker.conf      # /ci → Woodpecker
│       ├── mattermost.conf      # /chat → Mattermost
│       ├── uptime.conf          # /status → Uptime Kuma
│       └── admin.conf           # /admin → Admin Panel
│
├── scripts/                     # Утилиты управления
│   ├── setup.sh                 # Первичная настройка с нуля
│   ├── backup.sh                # Локальный бэкап данных
│   ├── restore.sh               # Восстановление из бэкапа
│   └── healthcheck.sh           # Проверка сервисов
│
├── docs/                        # Документация
│   ├── images/                  # Скриншоты и фото
│   ├── SETUP.md                 # Инструкция по развёртыванию
│   ├── MIGRATION.md             # Миграция с GitHub/GitLab
│   └── FAQ.md                   # Частые вопросы
│
└── data/                        # Данные сервисов (.gitignore)
├── postgres/                # Базы данных
├── gitea/                   # Репозитории Gitea
├── woodpecker/              # Состояние CI/CD
├── mattermost/              # Файлы Mattermost
├── syncthing/               # Индекс Syncthing
├── ntfy/                    # Кэш ntfy
└── uptime-kuma/             # Данные мониторинга
