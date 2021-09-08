How to Deploy Django Applications on Heroku
===========================================
# Disclaimer
- Confirm that your application is running as expected before pushing, runtime errors will cause deployment to fail so make sure you have no bugs.
- Ignore every code/command followed by `#` in .env file.
- In section(s) where you are expected to input values do not include `<>` brackets after input
- Procedure works best with Django version 3 and above.
- Run all commands from virtual environment
# Install heroku CLI
If you don't have heroku, install and login

# Preparing the Application

Add the following to our project, we will cover each of them in detail in the below section

* Add a `Procfile` in the project root;
* Add `requirements.txt` file with all the requirements in the project root;
* Add `Gunicorn` to `requirements.txt`;
* A `runtime.txt` to specify the correct Python version in the project root;
* Configure `whitenoise` to serve static files.

## Procfile
Heroku apps include a `Procfile` that specifies the commands that are executed by the app’s dynos. 

For more information read on the [heroku documentation](https://devcenter.heroku.com/articles/procfile).

Create a file named `Procfile` in the project root with the following content:
```
web: gunicorn <your_project_name>.wsgi --log-file -
```
**NB:** Remember to remove the `<>` and replace them with your project name

Install gunicorn
```
pip install gunicorn && pip freeze > requirements.txt
```
## Runtime.txt
This file contains the python version you are using for heroku to use, create `runtime.txt` in your project root and add your python version in the following format. Make sure to copy it correct(lowercase).

```
python-3.6.4 
```
To check your python Version:
```
python --version
```
List of [Heroku Python Runtimes](https://devcenter.heroku.com/articles/python-runtimes).

## Whitenoise: Django Static Files settings
Lets first configure static related parameter in `settings.py`
```python 
BASE_DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))

# Static files (CSS, JavaScript, Images)
# https://docs.djangoproject.com/en/1.9/howto/static-files/
STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')
STATIC_URL = '/static/'

# Extra places for collectstatic to find static files.
STATICFILES_DIRS = (
    os.path.join(BASE_DIR, 'static'),
)
```
Turns out django does not support serving static files in production. However, WhiteNoise project can integrate into your Django application, and was designed with exactly this purpose in mind.

Lets first install Whitenoise   
```
pip install whitenoise && pip freeze > requirements.txt
```

Install `WhiteNoise` into your Django application. This is done in `settings.py’s middleware section` (at the top):
```python 
MIDDLEWARE = (
    # Simplified static file serving.
    # https://warehouse.python.org/project/whitenoise/
    'whitenoise.middleware.WhiteNoiseMiddleware',
    ...
```
Add the following setting to `settings.py` in the static files section to enable gzip functionality.
```python
# Simplified static file serving.
# https://warehouse.python.org/project/whitenoise/

STATICFILES_STORAGE = 'whitenoise.storage.CompressedManifestStaticFilesStorage'

# configuring the location for media
MEDIA_URL = '/static/'
MEDIA_ROOT = os.path.join(BASE_DIR, '<img folder name>')

# Configure Django App for Heroku.
django_heroku.settings(locals())
```

## Optional but very helpfull settings
### Django-Heroku
We then install Django-Heroku which will automatically configure `DATABASE_URL`, `ALLOWED_HOSTS`, `WhiteNoise` (for static assets), `Logging`, and `Heroku CI` for your application.
```bash
pip install django-heroku && pip freeze > requirements.txt
```
**NB:** Remember to remove `pkg-resources` from `requirements.txt` for easy deployment.

### python-decouple and dj-database-url
Python Decouple is a must have app if you are developing with Django. It’s important to keep your application credentials like API Keys, Amazon S3, email parameters, database parameters safe, specially if it’s an open source repository. Also no more development_settings.py and production_settings.py, use just one settings.py for your whole project.

Install decouple
```
pip install python-decouple && pip freeze > requirements.txt
```

dj-database-url is a simple Django utility allows you to utilize the 12factor inspired `DATABASE_URL` environment variable to configure your Django application.

Install db url
```
pip install dj-database-url && pip freeze > requirements.txt
```

Firts create a `.env` file and add it to `.gitignore` so you don’t commit any sensitive data to your remote repository.
below is an example of configurations you can add to the `.env` file.

```python
#just an example, dont share your .env settings
SECRET_KEY='your secret key, find it in settings'
DEBUG=False #set to true in development
DB_NAME='your database name'
DB_USER='postgres username'
DB_PASSWORD='postgres password'
DB_HOST='127.0.0.1'
MODE='prod' #set to 'dev' in production
ALLOWED_HOSTS='.localhost', '.herokuapp.com', '.127.0.0.1' #remove it in development
DISABLE_COLLECTSTATIC=1
```

**NB:** Remember not to include any comment in .env

We then edit `settings.py` to enable decouple to use the `.env` configurations.

 ```python
import os
import django_heroku
import dj_database_url
from decouple import config,Csv

MODE=config("MODE", default="dev")
SECRET_KEY = config('SECRET_KEY')
DEBUG = config('DEBUG', default=False, cast=bool)
 # development
if config('MODE')=="dev":
    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.postgresql_psycopg2',
            'NAME': config('DB_NAME'),
            'USER': config('DB_USER'),
            'PASSWORD': config('DB_PASSWORD'),
            'HOST': config('DB_HOST'),
            'PORT': '',
        }
        
    }
# production
else:
    DATABASES = {
        'default': dj_database_url.config(
            default=config('DATABASE_URL')
        )
    }

db_from_env = dj_database_url.config(conn_max_age=500)
DATABASES['default'].update(db_from_env)

ALLOWED_HOSTS = config('ALLOWED_HOSTS', cast=Csv())
```

# Lets deploy now
First make sure you are in the root directory of the repository you want to deploy

Next create the heroku app
```bash
heroku create <app-name>
```
Create a postgres addon to your heroku app
```bash
heroku addons:create heroku-postgresql:hobby-dev
```

Add all your configurations in `.env` file directly to heroku by running the this command.

```bash
heroku config:set $(cat .env | sed '/^$/d; /#[[:print:]]*$/d')
```

### pushing to heroku

Confirm  you have all the following `Procfile`, `requirements.txt` with all required packages and  `runtime.txt` .
Confirm that you have removed `pkg-resources` from `requirements.txt` 

```bash
git add .
git commit -m "deployment"
git push heroku master
```

 ### Run migrations
 ```bash
 heroku run python manage.py migrate
```

If you instead wish to push your postgres database data to heroku then run
```bash
heroku pg:push <The name of the db in the local psql> DATABASE_URL --app <heroku-app>
```
### Django Admin
Now add the superuser on Heroku.
```bash
(virtual)$ heroku run python manage.py createsuperuser
Username: <enter admin username>
Email address: <enter email address>
Password: <enter password>
Password (again):<retype password>
Superuser created successfully.
```
You can open your app through the link generated in your terminal or open app on heroku dashboard.

or run
```bash
(virtual)$ heroku open  --app <insert your heroku app name>
```





