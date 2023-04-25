# "API для проекта YaMDb"
## Яндекс.Практикум Спринт - 15.
## Проект YaMDb собирает отзывы пользователей на произведения. 
### Произведения делятся на категории, такие как «Книги», «Фильмы», «Музыка». Например, в категории «Книги» могут быть произведения «Винни-Пух и все-все-все» и «Марсианские хроники», а в категории «Музыка» — песня «Давеча» группы «Жуки» и вторая сюита Баха. Список категорий может быть расширен (например, можно добавить категорию «Изобразительное искусство» или «Ювелирка»).   

### Как запустить проект:

Клонировать репозиторий и перейти в него в командной строке:

```
git clone https://github.com/Brideshead/infra_sp2
cd infra_sp2
cd api_yamdb
```

Переходим в папку с файлом docker-comppse.yaml:

```
cd infra
```

Поднять контейнеры (infra_db_1, infra_web_1, infra_nginx_1):

```
docker-compose up -d --build
```

Выполнить миграции:

```
docker-compose exec web python manage.py makemigrations reviews
docker-compose exec web python manage.py makemigrations users
docker-compose exec web python manage.py migrate
docker-compose exec web python manage.py loaddata infra/fixtures.json
```

Создать суперпользователя:

```
docker-compose exec web python manage.py createsuperuser
```

Собрать статику:

```
docker-compose exec web python manage.py collectstatic --no-input
```

Создать дамп базы данных (нет в текущем репозитории):

```
docker-compose exec web python manage.py dumpdata > dumpPostrgeSQL.json
```

Останавливаем контейнеры:

```
docker-compose down -v
```

Запустить проект:

```
python3 manage.py runserver
```

### Шаблон наполнения .env (не включен в текущий репозиторий) расположенный по пути infra/.env

```
DB_ENGINE=django.db.backends.postgresql
DB_NAME=postgres
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
DB_HOST=db
DB_PORT=5432
```

### Документация к API расположена по адресу:

```
http://localhost/redoc/
```

### Команда, ответственная за проект:
```
Богоевич Александр - архитектура проекта, API регистрации и авторизации пользователей, контейнеризация
Евгений Кудрявцев - API отзывов и комментариев к произведениям
```
