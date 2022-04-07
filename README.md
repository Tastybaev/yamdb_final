# Учебный проект: API проекта "YamDB"
![workflow](https://github.com/Tastybaev/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)

## Используемые технологии
![](https://img.shields.io/badge/Python3-mediumblue) ![](https://img.shields.io/badge/Django-mediumvioletred) ![](https://img.shields.io/badge/DRF-Lime)  

## Задача учебного проекта
Задачей учебного проекта являлось создание API для сервиса сбора отзывов на произведения "YamDB" в соответствии с предоставленной спецификацией. Тесты расположенные в корне проекта не и спецификация по API являются частью задания и были предоставлены для проверки проекта в готовом виде.

## Описание проекта
Проект YaMDb собирает отзывы пользователей на произведения. Произведения делятся на категории: «Книги», «Фильмы», «Музыка» и т.д.
Сами произведения в YaMDb не хранятся, здесь нельзя посмотреть фильм или послушать музыку.
В каждой категории есть произведения: книги, фильмы или музыка. Например, в категории «Книги» могут быть произведения «Винни Пух и все-все-все» и «Дочь тысячи джеддаков», а в категории «Музыка» — песня «Thriller» Майкла Джексона и вторая сюита Баха. Произведению может быть присвоен жанр из списка предустановленных (например, «Сказка», «Рок» или «Артхаус»). Новые жанры может создавать только администратор.
Читатели оставляют к произведениям текстовые отзывы и выставляют произведению оценку в диапазоне от одного до десяти. Из множества оценок автоматически высчитывается средняя оценка произведения.

Доступные эндпоинты:

Эндпоинт | Mетод | Действие | Права доступа
--- | --- | --- | ---
`/api/v1/auth/email/` | POST | запрос кода подтверждения на эл. почту |  Any
`/api/v1/auth/token/` | POST | получение JWT-токена |  Any 
`/api/v1/users/` | GET | получение списка всех пользователей | Admin
| | POST | создание нового пользователя | Admin
`/api/v1/users/{username}/` | GET | получение информации о пользователе | Admin
| | PATCH | измененние данных пользователя | Admin
| | DELETE | удаление пользователя | Admin
`/api/v1/users/me/` | GET | получение данных своей учетной записи | Admin, Moderator, User
| | PATCH | изменение данных своей учетной записи | Admin, Moderator, User
`/api/v1/titles/` | GET | получение списка всех произведений | Any
| | POST | добавление нового произведенния | Admin
`/api/v1/titles/{titles_id}/` | GET | получение информации о произведении | Any
| | PATCH | измененние данных о произведении | Admin
| | DELETE | удаление произведения | Admin
`/api/v1/genres/` | GET | получение списка всех жанров | Any
| | POST | добавление нового жанра | Admin
`/api/v1/genres/{slug}/` | DELETE | удаление жанра | Admin 
`/api/v1/categories/` | GET | получение списка всех категорий | Any
| | POST | добавление новой категории | Admin  
`/api/v1/categories/{slug}/` | DELETE | удаление категории | Admin  
`/api/v1/titles/{title_id}/reviews/` | GET | получение списка всех отзывов о произведении | Any
| | POST | добавление нового отзыва о произведении | Admin, Moderator, User
`/api/v1/titles/{title_id}/reviews/{review_id}/` | GET | получение отзыва | Any
| | PATCH | изменение отзыва | Admin, Moderator, User(author)
| | DELETE | удаление отзыва | Admin, Moderator, User(author)
`/api/v1/titles/{title_id}/reviews/{review_id}/comments/` | GET | получение списка всех комментариев к отзыву | Any
| | POST | добавление нового комментария к отзыву | Admin, Moderator, User
`/api/v1/titles/{title_id}/reviews/{review_id}/ comments/{comment_id}/` | GET | получение комментария | Any
| | PATCH | изменение комментария | Admin, Moderator, User(author)
| | DELETE | удаление комментария | Admin, Moderator, User(author)

Спецификация API по всем доступным эндпоинтам, структурам данных и параметрам запросов будет доступна после запуска проекта по адресу http://localhost:8000/redoc/.

## Требования
![](https://img.shields.io/badge/python-v3.9-blue)

## Как развернуть
1. Склонируйте репозиторий:`https://github.com/palmage/api_yamdb.git`.
2. С помощью [инструкции](https://python-scripts.com/virtualenv) создайте 
и активируйте виртуальное окружение.
3. Установите зависимости: `pip install -r requirements.txt`.
4. Примените миграции: `python manage.py migrate`.
5. Для возможности отправки кодов подтверждения на адрес электронной почты пользователя заполните настройки в файле `api_yamdb/.env`.
6. Запустите сервер: `python manage.py runserver`, пройдите регистрацию и приступайте к работе с API!

## Как работать с API
Для работы с API подходят [CURL](https://losst.ru/kak-polzovatsya-curl) 
или [Postman](https://www.postman.com).

### Регистрация пользователей и получение access-токена
Для регистрации пользователя отправьте POST-запрос с параметром `email` и значением адреса электронной почты на `api/v1/auth/email/`. На указанный email придет письмо с кодом подтверждения. Код подтверждения (`confirmation_code`) и адрес почты (`email`) отправьте POST-запросом на `api/v1/token/`. В ответ получите `access-токен`.  
Для прохождения аутентификации при работе с API передавайте в заголовокe `Authorization` полученный токен в виде: `Bearer <access-токен>`.
Пример json:
{
  "username": "Tom",
  "email": "Tom@mail.com",
  "first_name": "Tom",
  "last_name": "Anderson",
  "bio": "dolore mollit do",
  "role": "admin"
}

Проект будет доступен по вашему IP-адресу.

Проект доступен по адресу: http://62.84.122.112/api/v1/

Образ на DockerHub: https://hub.docker.com/repository/docker/tastybaev/yamdb_final