# Django Restful Project with Docker

## Getting markdown styles
- https://dillinger.io/

## Create the project
- In the root file create: *Dockerfile, requirements.txt, docker-compose.yml*
- **Dockerfile**
```
FROM python:3
ENV PYTHONUNBUFFERED 1
RUN mkdir /code
WORKDIR /code
ADD requirements.txt /code/
RUN pip install -r requirements.txt
ADD . /code/
```
- **requeriments.txt**
```
Django==2.0.1
psycopg2
```
- **docker-compose.yml**
```
version: '3'

services:
  db:
    image: postgres
  web:
    build: .
    command: python3 manage.py runserver 0.0.0.0:8000
    volumes:
      - .:/code
    ports:
      - "8000:8000"
    depends_on:
      - db
```
* Build the image
```sh
docker-compose run web django-admin.py startproject project .
```

* Change the ownership of the new files
```sh
sudo chown -R $user .
```

* Configure project/settings.py
```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'postgres',
        'USER': 'postgres',
        'HOST': 'db',
        'PORT': 5432,
    }
}
```

* Run: *docker-compose up*

## Redo the project

- docker-compose down

- remove the image of the project

- docker rmi id_image

- sudo rm -R manage.py project