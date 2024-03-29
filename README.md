## Flask application

### Setting up Development environment

Requirements Docker, Docker-Compose

1. Make your own local compose file
```commandline
cp docker-compose_dev_sample.yml docker-compose.yml
```
2. Fill out an env file `.env.dev`
```
FLASK_APP=web/__init__.py
FLASK_ENV=development
DATABASE_URL=postgresql://username:password@db:5432/database_name
DEBUG_MODE=1
SQL_HOST=db
SQL_PORT=5432
DATABASE=postgres
```
Specify `username,password` and `database_name` for your PostgresSQL database
3. Build project
```commandline
docker-compose build
```
4. Run the project
```commandline
docker-compose up -d
```
5. Create database
```commandline
docker-compose exec web python manage.py create_db
```
6. Seed database with random data
```commandline
docker-compose exec web python manage.py seed_db
```

Check application. Open in browser http://localhost:5000.


You can print tables data with command
```commandline
docker-compose -f docker-compose-dev.yml exec web python manage.py print_all
```

### Setting up Production environment

1. Fill out an env file `.env.prod`
```
FLASK_APP=web/__init__.py
FLASK_ENV=development
DATABASE_URL=postgresql://username:password@db:5432/database_name
DEBUG_MODE=1
SQL_HOST=db
SQL_PORT=5432
DATABASE=postgres
```
Specify `username,password` and `database_name` for your PostgresSQL database
2. Fill out an env file `.env.prod.db`
```commandline
POSTGRES_DB=
POSTGRES_USER=
POSTGRES_PASSWORD=
```
3. Build the project
```commandline
docker-compose -f docker-compose_prod.yml build
```
4. Run the project
```commandline
docker-compose -f docker-compose_prod.yml  up -d
```
5. Create database
```commandline
docker-compose -f docker-compose_prod.yml exec web python manage.py create_db
```
6. Seed database with random data
```commandline
docker-compose -f docker-compose_prod.yml exec web python manage.py seed_db
```

Check application. Open in browser http://localhost:1337.

