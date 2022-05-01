## Workflow-статус:
[![Django-app workflow](https://github.com/corde1ia/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)](https://github.com/corde1ia/yamdb_final/actions/workflows/yamdb_workflow.yml/)

#### Инструменты и технологии:
Python 3, SQlite3, REST API. Django, Django Unittest, Django debug toolbar.

# Проект YaMDb
#### Описание

Проект YaMDb собирает отзывы пользователей на произведения. Произведения делятся на категории: «Книги», «Фильмы», «Музыка».
Сами произведения в YaMDb не хранятся, здесь нельзя посмотреть фильм или послушать музыку.

В каждой категории есть произведения: книги, фильмы или музыка.
Произведению может быть присвоен жанр (Genre) из списка предустановленных. Новые жанры может создавать только администратор.
Благодарные или возмущённые пользователи оставляют к произведениям текстовые отзывы (Review) и ставят произведению оценку в диапазоне от одного до десяти (целое число); из пользовательских оценок формируется усреднённая оценка произведения — рейтинг (целое число). На одно произведение пользователь может оставить только один отзыв.

#### Пользовательские роли

- Аноним — может просматривать описания произведений, читать отзывы и комментарии.
- Аутентифицированный пользователь (user) — может, как и Аноним, читать всё, дополнительно он может публиковать отзывы и ставить оценку произведениям (фильмам/книгам/песенкам), может комментировать чужие отзывы; может редактировать и удалять свои отзывы и комментарии. Эта роль присваивается по умолчанию каждому новому пользователю.
- Модератор (moderator) — те же права, что и у Аутентифицированного пользователя плюс право удалять любые отзывы и комментарии.
- Администратор (admin) — полные права на управление всем контентом проекта. Может создавать и удалять произведения, категории и жанры. Может назначать роли пользователям.
- Суперюзер Django — обладет правами администратора (admin).

#### Ресурсы API YaMDb

- Ресурс auth: аутентификация.
- Ресурс users: пользователи.
- Ресурс titles: произведения, к которым пишут отзывы (определённый фильм, книга или песенка).
- Ресурс categories: категории (типы) произведений («Фильмы», «Книги», «Музыка»).
- Ресурс genres: жанры произведений. Одно произведение может быть привязано к нескольким жанрам.
- Ресурс reviews: отзывы на произведения. Отзыв привязан к определённому произведению.
- Ресурс comments: комментарии к отзывам. Комментарий привязан к определённому отзыву.

#### Инструкция по установке
Клонируем репозиторий
```
git clone https://github.com/corde1ia/yamdb_final.git
```

Переходим в папку с проектом
```
api_yamdb/
```

Устанавливаем отдельное виртуальное окружение для проекта
```
python -m venv venv
```
Активируем виртуальное окружение
```
venv\Scripts\activate
```
Устанавливаем модули необходимые для работы проекта
```
pip install -r requirements.txt
```

#### Примеры

Примеры запросов по API:

- [GET] /api/v1//titles/{title_id}/reviews/ - Получить список всех отзывов.
- [POST]  /api/v1//titles/{title_id}/reviews/ - Добавить новый отзыв. Пользователь может оставить только один отзыв на произведение.
- [GET] /api/v1/titles/{title_id}/reviews/{review_id}/ - Получить отзыв по id для указанного произведения.
- [PATCH] /api/v1/titles/{title_id}/reviews/{review_id}/ - Частично обновить отзыв по id.
- [DELETE] /api/v1/titles/{title_id}/reviews/{review_id}/ - Удалить отзыв по id.






## Проект: запуск docker-compose

#### Установка Docker
https://docs.docker.com/engine/install/

#### Запуск проекта

#### Подготовка виртуального окружения:
Клонировать репозиторий, перейти в него в командной строке:
```
git clone https://github.com/chaplinskiy/infra_sp2.git
```
```
cd api_yamdb/
```
Войти на сервер Ubuntu и обновить пакеты командами:
```
sudo apt update
```
```
sudo apt -y upgrade
```
Чтобы управлять программными пакетами Python, установить pip командой:
```
sudo apt install -y python3-pip
```
Установить модуль venv (вирутальное окружение) командой:
```
sudo apt install -y python3-venv
```
Cоздать и активировать виртуальное окружение командами:
```
python3 -m venv env && source env/bin/activate
```
Установить зависимости из файла requirements.txt:
```
pip install -r requirements.txt
```
#### Запуск проекта
Запуск приложения в контейнерах:
*из директории `infra/`*
```
docker-compose up -d --build
```
Выполнить миграции:
*из директории `infra/`*
```
docker-compose exec web python manage.py migrate
```
Создать суперпользователя:
*из директории `infra/`*
```
docker-compose exec web python manage.py createsuperuser
```
Собрать статику:
*из директории `infra/`*
```
docker-compose exec web python manage.py collectstatic --no-input
```
После завершения работы остановить приложение в контейнерах:
*из директории `infra/`*
```
docker-compose down -v
```
Для проверки:
*Запустить модуль `pytest`:*
*при запущенном виртуальном окружении*
*из директории `infra/`*
```
pytest
```

#### Шаблон .env-файла для проекта "Запуск Docker-compose":
*заполните все поля, удалив <...> и комментарии*
Указываем, что работаем с postgresql
```
DB_ENGINE=<...>
```
Имя базы данных
```
DB_NAME=<...>
```
Логин для подключения к базе данных
```
POSTGRES_USER=<...>
```
Пароль для подключения к БД
```
POSTGRES_PASSWORD=<...>
```
Название сервиса (контейнера)
```
DB_HOST=<...> #
```
Порт для подключения к БД
```
DB_PORT=<...>
```
Ключ -> settings.py
```
SECRET_KEY=<...>
```
