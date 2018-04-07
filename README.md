# Django Restful Project with Docker

## Getting markdown styles
- https://dillinger.io/

## Create the project
- In the root file create: *Dockerfile, requirements.txt, docker-compose.yml*

* Build the image
```sh
$ docker-compose run web django-admin.py startproject project .
```

* Change the ownership of the new files
```sh
$ sudo chown -R $user .
```

* Configure project/settings.py
```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'postgres',
        'USER': 'postgres',
        'PASSWORD': 'postgres',
        'HOST': 'postgres',
        'PORT': 5432,
    }
}
```

* Run: *docker-compose up*

* To run the migration on django: *docker-compose run web python manage.py migrate*
or
* Enter on container and run *python manage.py migrate* (https://docs.djangoproject.com/pt-br/2.0/intro/tutorial02/)

* Access the app: *http://localhost:8000/*

* Create superuser: *python manage.py createsuperuser*

## Redo the project
- To erase what you've done so far:
```sh
$ docker-compose down
```

- remove the image of the project
```sh
$ docker rmi image_id --force

$ sudo rm -R manage.py project
```