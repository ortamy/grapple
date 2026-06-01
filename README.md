# 🪝 Grapple Box

> *«Grapple your code. Hold your ground.»*

**Автономная инфраструктура для команды разработчиков.**
Никаких облаков. Никаких санкций. Ваш код остаётся у вас. Навсегда.

---

## Что внутри

- **Gitea** — Git-хостинг, Issues, Wiki (вместо GitHub/GitLab)
- **Woodpecker CI** — пайплайны CI/CD (вместо GitHub Actions)
- **Mattermost** — чат команды (вместо Slack/Discord)
- **Syncthing** — P2P-синхронизация файлов (вместо Google Drive)
- **Ntfy** — push-уведомления на телефон
- **Uptime Kuma** — мониторинг сервисов
- **Admin Panel** — единая админка для управления пользователями

Всё в Docker-контейнерах. Одна команда — и инфраструктура готова.

---

## Системные требования

- Raspberry Pi 5 (8 GB) / Intel N100 / любой x86 с 4+ GB RAM
- 128+ GB дискового пространства (SSD)
- Debian 12, Ubuntu 22.04+ или Raspberry Pi OS
- Docker и Docker Compose v2

---

## Быстрый старт

### 1. Установите Docker

```bash
curl -fsSL https://get.docker.com | sh
sudo usermod -aG docker $USER
newgrp docker
```

2. Склонируйте репозиторий

```bash
git clone https://github.com/grapple/grapple-box.git
cd grapple-box
```

3. Настройте переменные

```bash
cp .env.example .env
nano .env
```

Обязательно смените:

· DB_PASSWORD
· ADMIN_PASSWORD
· WOODPECKER_AGENT_SECRET

4. Запустите

```bash
make up
```

5. Откройте админ-панель

```
http://ваш-ip/admin
```

Логин: admin
Пароль: тот, что указали в ADMIN_PASSWORD

---

Основные команды

```bash
make up          # Запустить
make down        # Остановить
make restart     # Перезапустить
make logs        # Логи всех сервисов
make backup      # Создать бэкап данных
make health      # Проверить статус
```

---

Доступ к сервисам

После запуска всё доступно через nginx на 80-м порту:

· http://ваш-ip/git — Gitea
· http://ваш-ip/ci — Woodpecker CI
· http://ваш-ip/chat — Mattermost
· http://ваш-ip/status — Uptime Kuma
· http://ваш-ip/admin — Админ-панель

Syncthing и Ntfy настраиваются отдельно через свои интерфейсы.

---

Архитектура одной строкой

```
nginx (прокси) → Gitea, Woodpecker, Mattermost, Admin Panel → PostgreSQL (единая БД)
Syncthing, Ntfy, Uptime Kuma — автономные сервисы
```

Все данные хранятся локально в ./data/. Ничего не уходит вовне.

---

Безопасность

· Регистрация в Gitea отключена — пользователей добавляет администратор
· Ntfy запрещает анонимный доступ по умолчанию
· Все сервисы за обратным прокси nginx
· Смените все пароли по умолчанию перед использованием

---

Для кого

IT-команды, стартапы, образовательные проекты, фрилансеры — все, кто хочет полный контроль над своей инфраструктурой без облаков и внешних рисков.

---

Контакты

· Email: hello@grapplebox.io
· Telegram: @grapple_box

---

MIT © Grapple Box, 2026.

```

Убрал таблицы, оставил главное и путь запуска. Дальше — `admin-panel/app.py` или `scripts/setup.sh`?