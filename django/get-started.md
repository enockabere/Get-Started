Creating a new django application
=================================
Helpful Commands in creating a new django application

### Activate Virtual Environment

```bash
python3 -m venv virtual
```

### Download Django
```bash
python3 -m pip install django && pip freeze > requirements.txt
```

### Create a new Django project and call it xyz
```bash
django-admin startproject xyz .
```

### Create third-party app (abc)then connect it to xyz project.
```bash
django-admin startapp abc
```

### Adding Bootstrap
```bash
pip install django-bootstrap-v5 && pip freeze > requirements.txt
```

### Install database dependency
```bash
pip install psycopg2 && pip freeze > requirements.txt
```

## Models

### First we have to run checks to validate whether the models were defined properly.
```bash
python3 manage.py check
```
### Make Migrations
```bash
python3 manage.py makemigrations
```
### View Migration
```bash
python3 manage.py sqlmigrate 0001
```
### Run Migration
```bash
python3 manage.py migrate
```
## Testing

### Running Tests
```bash
python3 manage.py test abc
```
## Django Admin

### Create Superuser
```bash
python manage.py createsuperuser
```
## Uploading Images
```bash
pip install pillow && pip freeze > requirements.txt
```
## Connecting .env variable to Django Settings
```bash
pip install python-decouple && pip freeze > requirements.txt
```

## Django Authentication

```bash
pip install django-registration==2.4.1 && pip freeze > requirements.txt
```

## Install Rich Text Editor
```bash
pip install django-tinymce && pip freeze > requirements.txt
```

## NB:

## To alter Postgres Password
    ALTER USER user_name WITH PASSWORD 'new_password';

## Contact details
Have any recommendations and/or questions, feel free to email me:[anock.abere@student.moringaschool.com](mailto:anock.abere@student.moringaschool.com)