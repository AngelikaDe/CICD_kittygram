# CICD_kittygram
The workflow was build using github actions checkouts, for example:
### Tests
- Trigger: This job is triggered whenever there is a push to the main branch.
- Runs on: Ubuntu latest
- Services: This job runs a PostgreSQL service using the postgres:13.10 image.
- Steps:
* Checks out the repository using actions/checkout@v3.
* Sets up Python using actions/setup-python@v4 and installs the required dependencies.
* Runs flake8 linting and Django tests to ensure the application is functioning correctly.

## **Стэк технологий**

* Django==3.2.3
* djangorestframework==3.12.4
* djoser==2.1.0
* webcolors==1.11.1
* psycopg2-binary==2.9.3
* Pillow==9.0.0
* pytest==6.2.4
* pytest-django==4.4.0
* pytest-pythonpath==0.7.3
* PyYAML==6.0
*gunicorn==20.1.0

## Локальный запуск проекта

Клонировать репозиторий и перейти в него в командной строке:

```
git clone https://github.com/iultina/kittygram_final.git
cd kittygram_final
```

Cоздать и активировать виртуальное окружение, установить зависимости:

```
 python3 -m venv venv && \ 
 source venv/scripts/activate && \
 python -m pip install --upgrade pip && \
 pip install -r backend/requirements.txt
```

Установите [docker compose](https://www.docker.com/) на свой компьютер.

Запустите проект через docker-compose:

```
docker compose -f docker-compose.yml up --build -d
```

Выполнить миграции:

```
docker compose -f docker-compose.yml exec backend python manage.py migrate
```

Соберите статику и скопируйте ее:

```
docker compose -f docker-compose.yml exec backend python manage.py collectstatic  && \
docker compose -f docker-compose.yml exec backend cp -r /app/static_backend/. /backend_static/static/
```

## .env

В корне проекта создайте файл .env.


## Automatic deployment
B репозитории GitHub Actions `Settings/Secrets/Actions` прописать Secrets - переменные окружения для доступа к сервисам:

```
SECRET_KEY                     # стандартный ключ, который создается при старте проекта

DOCKER_USERNAME                # имя пользователя в DockerHub
DOCKER_PASSWORD                # пароль пользователя в DockerHub
HOST                           # ip_address сервера
USER                           # имя пользователя
SSH_KEY                        # приватный ssh-ключ (cat ~/.ssh/id_rsa)
PASSPHRASE                     # кодовая фраза (пароль) для ssh-ключа

TELEGRAM_TO                    # id телеграм-аккаунта (можно узнать у @userinfobot, команда /start)
TELEGRAM_TOKEN                 # токен бота (получить токен можно у @BotFather, /token, имя бота)
```
