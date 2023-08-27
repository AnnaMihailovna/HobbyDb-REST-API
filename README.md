# *HobbyDb* 📖🎥🎼
## Описание

**HobbyDb** - проект, который собирает **отзывы** пользователей на **произведения**. Сами произведения в **HobbyDb** не хранятся, здесь нельзя посмотреть фильм или послушать музыку.
Произведения делятся на **категории**, такие как «Книги», «Фильмы», «Музыка».
Благодарные или возмущённые пользователи оставляют к произведениям текстовые отзывы и ставят произведению оценку в диапазоне от одного до десяти (целое число); из пользовательских оценок формируется усреднённая оценка произведения — рейтинг (целое число). На одно произведение пользователь может оставить только один отзыв.
Пользователи могут оставлять комментарии к отзывам.

## 📝 **Ключевые собенности:**

🔸 Система регистрации при помощи JWT-токена

🔸 Пользовательские роли: **Аноним**, **Аутентифицированный пользователь**, **Модератор**, **Администратор**

🔸 Категории **categories** и жанры **genres** произведений

🔸 Возможность оставлять отзывы **reviews** с оценками и комментарии **comments** к ним пользователями **users**

## Технологический стек
[![Python](https://img.shields.io/badge/-Python-464646?style=flat&logo=Python&logoColor=56C0C0&color=cd5c5c)](https://www.python.org/)
[![Django REST Framework](https://img.shields.io/badge/-Django%20REST%20Framework-464646?style=flat&logo=Django%20REST%20Framework&logoColor=56C0C0&color=0095b6)](https://www.django-rest-framework.org/)
[![SQLite](https://img.shields.io/badge/-SQLite-464646?style=flat&logo=PostgreSQL&logoColor=56C0C0&color=cd5c5c)](https://www.sqlite.org/)


## 🚀 Запуск проекта: 

Клонировать репозиторий и перейти в него в командной строке:

```
git clone git@github.com:AnnaMihailovna/HobbyDb-REST-API.git
```

Cоздать и активировать виртуальное окружение:

```
python3.9 -m venv venv
```

```
source venv/bin/activate
```

Установить зависимости из файла requirements.txt:

```
python -m pip install --upgrade pip
```

```
pip install -r requirements.txt
```

```
cd yatube_api
```

Выполнить миграции:

```
python manage.py makemigrates
python manage.py migrate
```

Запустить проект:

```
python manage.py runserver
```


## 🏢 База данных:

Для загрузки данных, получаемых вместе с проектом, используйте management-команду, добавляющую данные в БД через Django ORM. Предварительно надо удалить базу: если у вас уже есть файл **db.sqlite3**, удалите его. Затем подготовьте и проведите миграции:
```
python manage.py makemigrations
python manage.py migrate
```
Затем  management-команда:
```
python manage.py import
```
Результатом успешного импорта данных из файлов csv в БД будет строка, выведенная в терминал:
```
$ Данные успешно загружены
```

## 📋 Документация к API:

После запуска dev-сервера доступ к подробной документация по адресу:
 <http://127.0.0.1:8000/redoc/>

### Регистация нового пользователя:
```POST /api/v1/auth/signup/```


```json
{
  "email": "string",
  "username": "string"
}

```

### Получение JWT-токена:

```POST /api/v1/auth/token/```

```json
{
  "username": "string",
  "confirmation_code": "string"
}
```
## 💻 Примеры запросов:
### Для авторизованных пользователей:
➕ **Добавление категории:**
- Права доступа: **Администратор**.

```POST /api/v1/categories/```

```json
{
  "name": "string",
  "slug": "string"
}
```

➖ **Удаление категории:**
- Права доступа: **Администратор.**

```DELETE /api/v1/categories/{slug}/```

➕ **Добавление жанра:**

- Права доступа: **Администратор.**

```POST /api/v1/genres/```

```json
{
  "name": "string",
  "slug": "string"
}
```

➖ **Удаление жанра:**

- Права доступа: **Администратор**.

```DELETE /api/v1/genres/{slug}/```


🔄 **Обновление публикации:**

```PUT /api/v1/posts/{id}/```

```json
{
"text": "string",
"image": "string",
"group": 0
}
```

➕ **Добавление произведения:**
- Права доступа: **Администратор**. 
- Нельзя добавлять произведения, которые еще не вышли (год выпуска не может быть больше текущего).

```POST /api/v1/titles/```

```json
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

➕ **Добавление произведения:**

- Права доступа: **Доступ без токена**.

```GET /api/v1/titles/{titles_id}/```

```json
{
  "id": 0,
  "name": "string",
  "year": 0,
  "rating": 0,
  "description": "string",
  "genre": [
    {
      "name": "string",
      "slug": "string"
    }
  ],
  "category": {
    "name": "string",
    "slug": "string"
  }
}
```

♻️ **Частичное обновление информации о произведении:**
- Права доступа: **Администратор**.

```PATCH /api/v1/titles/{titles_id}/```


```json
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

♻️ **Частичное обновление информации о произведении:**
- Права доступа: **Администратор**.

```DEL /api/v1/titles/{titles_id}/```

### Работа с пользователями:

📃 **Список пользователей:**
- Права доступа: **Администратор**.

```GET /api/v1/users/ - Получение списка всех пользователей```

👨👩 **Добавление пользователя:**


- Права доступа: **Администратор**.
- Поля **email** и **username** должны быть уникальными.

```POST /api/v1/users/ - Добавление пользователя```

```json
{
"username": "string",
"email": "user@example.com",
"first_name": "string",
"last_name": "string",
"bio": "string",
"role": "user"
}
```

📛 **Получение пользователя по username:**

- Права доступа: **Администратор**.

```GET /api/v1/users/{username}/ - Получение пользователя по username```


✏️ **Изменение данных пользователя по username:**

- Права доступа: **Администратор**.

```PATCH /api/v1/users/{username}/ - Изменение данных пользователя по username```


```json
{
  "username": "string",
  "email": "user@example.com",
  "first_name": "string",
  "last_name": "string",
  "bio": "string",
  "role": "user"
}
```

➖ **Удаление пользователя по username:**

- Права доступа: **Администратор**.

```DELETE /api/v1/users/{username}/ - Удаление пользователя по username```


✋ **Получение данных своей учетной записи:**

- Права доступа: **Любой авторизованный пользователь**.

```GET /api/v1/users/me/ - Получение данных своей учетной записи```


📝 **Изменение данных своей учетной записи:**

- Права доступа: **Любой авторизованный пользователь**.

```PATCH /api/v1/users/me/ # Изменение данных своей учетной записи```

### 😎 Авторы проекта:
#### Дежурко Анна
```Github:```<https://github.com/AnnaMihailovna>
#### Жугрин Олег
```Github:```<https://github.com/theslayah>
#### Миндугулов Мансур
```Github:```<https://github.com/Mans-Mans>
