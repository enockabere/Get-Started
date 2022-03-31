<!-- @format -->

# Creating a new django application on Linux

Helpful Commands in creating a new django application

Remember to update your **requirements.txt** once you install a package in your virtual environment.

### Activate Virtual Environment

```bash
python3 -m venv virtual
```

To activate Virtual Environment

```bash
source virtual/bin/activate
```

### Download Django

```bash
python3 -m pip install django
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
pip install django-bootstrap-v5
```

or

Use Bootstrap CDN

### Install database dependency

```bash
pip install psycopg2
```

### Updating You project dependencies

Pip freeze saves all packages in the environment including those that you don’t use in your current project.

**pipreqs** only saves the packages that are installed in your virtual environment

```bash
pip install pipreqs
```

```bash
pipreqs>requirements.txt
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
pip install pillow
```

## Connecting .env variable to Django Settings

```bash
pip install python-decouple
```

## Django Authentication

```bash
pip install django-registration==2.4.1
```

## Install Rich Text Editor

```bash
pip install django-tinymce
```

## NB:

## To alter Postgres Password

    ALTER USER user_name WITH PASSWORD 'new_password';

# Creating a new django application on Windows

In windows: Press Windows (or Windows+R) and then type “cmd”: Run the Command Prompt in normal mode. The follow the processes below;

cd to project folder

```bash
cd C:\Users\user\Desktop\UserDjangoProject> pip install virtualenv
```

Create Virtual Environment

```bash
virtualenv -p python3 venv
```

or

```bash
py3  -m venv venv
```

- Activate virtualenv

```bash
venv\Scripts\activate
```

Install Django and other dependencies using pip (Command same as Linux)

Run migrations (Command same as Linux)

Update Requirements.txt file

```bash
pip install pipreqs
```

```bash
pipreqs>requirements.txt
```

Run the django project

```bash
./manage.py runserver
```
