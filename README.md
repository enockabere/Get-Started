## Create Project Folder
Bellow are the steps when creating a new django application

#### Activate Virtual Environment
python3 -m venv virtual

#### Download Django
python3 -m pip install django && pip freeze > requirements.txt

#### Create a new Django project and call it xyz
django-admin startproject xyz .

#### Create third-party app (abc)then connect it to xyz project.
django-admin startapp abc

#### Adding Bootstrap
pip install django-bootstrap-v5 && pip freeze > requirements.txt

#### Install database dependency
pip install psycopg2 && pip freeze > requirements.txt

### Models

#### First we have to run checks to validate whether the models were defined properly.
python3 manage.py check

#### Make Migrations
python3 manage.py makemigrations

#### View Migration
python3 manage.py sqlmigrate 0001

#### Run Migration
python3 manage.py migrate

### Testing

#### Running Tests
python3 manage.py test abc

### Django Admin

#### Create Superuser
python manage.py createsuperuser

### Uploading Images
pip install pillow && pip freeze > requirements.txt

### NB:

### To alter Postgres Password
ALTER USER user_name WITH PASSWORD 'new_password';

### Expected Errors;

- TypeError: __init__() missing 1 required positional argument: 'on_delete'

        **add** on_delete=models.CASCADE (if you have a foreign key on your models)

- Field 'id' expected a number but got datetime.datetime(2021, 9, 4, 14, 42, 5, 316108, tzinfo=<UTC>)

        Go to migration files. Find 002 (or 003,004 etc )_auto.py files.
    
        Change field = models.ForeignKey(default = django.utils.timezone.now) to default = 1

- Fatal-the-remote-end-hung-up-unexpectedly

        git remote remove origin
        git remote add origin https://github.com/user/repo
        git push --set-upstream origin master

### Contact details
Have any recommendations and/or questions, feel free to email me:[anock.abere@student.moringaschool.com](mailto:anock.abere@student.moringaschool.com)