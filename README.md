https://github.com/DmitriyMikhalev/yamdb_final/actions/workflows/yamdb_workflow/badge.svg?event=push

# api_yamdb
Проект **YaMDb** собирает отзывы пользователей на различные произведения.

# Как запустить проект через Docker:

Клонировать репозиторий и перейти в него в командной строке:

```

git clone https://github.com/DmitriyMikhalev/infra_sp2
cd infra_sp2/infra
```

Изучите пример файла переменных окружения, заполните его аналогичным образом:
```
cat sample.env
```

Запустите процесс развертывания контейнеров

```
docker-compose up -d
```

Выполните миграции:

```
docker-compose exec web python manage.py migrate
```

Соберите статику:

```
docker-compose exec web python manage.py collectstatic
```

Загрузите фикстуры в базу данных:

```
docker-compose exec web python manage.py loaddata fixtures.json
```

Готово. Сервис доступен по адресу **http://localhost:80/**

# Регистрация нового пользователя
```
POST http://127.0.0.1:8000/api/v1/auth/signup/

{
  "email": "string",
  "username": "string"
}
```
**Получение JWT-токена в обмен на username и confirmation code(Из письма).**
```
POST http://127.0.0.1:8000/api/v1/auth/token/

{
  "username": "string",
  "confirmation_code": "string"
}
```
**Редактирование, удаление и создание категорий жанров и произведений доступно только Администратору**
# Примеры запросов
## Получение списка всех категорий

```
GET http://127.0.0.1:8000/api/v1/categories/
```
## Добавление новой категории

```
POST http://127.0.0.1:8000/api/v1/categories/

{
  "name": "string",
  "slug": "string"
}
```

## Получение списка всех жанров

```
GET http://127.0.0.1:8000/api/v1/genres/
```
## Добавление жанра

```
POST http://127.0.0.1:8000/api/v1/genres/

{
  "name": "string",
  "slug": "string"
}
```

## Получение списка всех произведений
```
GET http://127.0.0.1:8000/api/v1/titles/
```
## Добавление произведения
```
POST http://127.0.0.1:8000/api/v1/titles/

{
"name": "string",
"year": 0,
"description": "string",
"genre": [
"string"
],
"category": "string"
}
```
## Получение информации о произведении
```
GET http://127.0.0.1:8000/api/v1/titles/{titles_id}/
```
## Получение списка всех отзывов
```
GET http://127.0.0.1:8000/api/v1/titles/{title_id}/reviews/
```
## Добавление нового отзыва
```
POST http://127.0.0.1:8000/api/v1/titles/{title_id}/reviews/

{
  "text": "string",
  "score": 1
}
```
## Полуение отзыва по id
```
GET http://127.0.0.1:8000/api/v1/titles/{title_id}/reviews/{review_id}/
```
## Получение списка всех комментариев к отзыву
```
GET http://127.0.0.1:8000/api/v1/titles/{title_id}/reviews/{review_id}/comments/
```
## Добавление комментария к отзыву
```
POST http://127.0.0.1:8000/api/v1/titles/{title_id}/reviews/{review_id}/comments/

{
  "text": "string"
}
```
## Получение комментария к отзыву
```
GET http://127.0.0.1:8000/api/v1/titles/{title_id}/reviews/{review_id}/comments/{comment_id}/
```
## Получение данных своей учетной записи
```
GET http://127.0.0.1:8000/api/v1/users/me/
```
## Изменение данных своей учетной записи
```
PATCH http://127.0.0.1:8000/api/v1/users/me/

{
  "username": "string",
  "email": "user@example.com",
  "first_name": "string",
  "last_name": "string",
  "bio": "string"
}
```

# Работа с USERS (Права доступа: **Администратор**)
## Получение списка всех пользователей
```
GET http://127.0.0.1:8000/api/v1/users/
```
## Добавление пользователя
```
POST http://127.0.0.1:8000/api/v1/users/

{
  "username": "string",
  "email": "user@example.com",
  "first_name": "string",
  "last_name": "string",
  "bio": "string",
  "role": "user"
}
```
## Получение пользователя по username
```
GET http://127.0.0.1:8000/api/v1/users/{username}/
```
