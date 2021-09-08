How to Deploy Flask Applications on Heroku
===========================================
# Disclaimer
- Confirm that your application is running as expected before pushing, runtime errors will cause deployment to fail so make sure you have no bugs.
- In section(s) where you are expected to input values do not include `<>` brackets after input
- Run all commands from virtual environment
# Install heroku CLI
If you don't have heroku, install and login

# Preparing the Application

Add the following to your project, we will cover each of them in detail in the below section

* Add a `Procfile` in the project root;
* Add `requirements.txt` file with all the requirements in the project root;
* Add `Gunicorn` to `requirements.txt`;

## Procfile
Heroku apps include a `Procfile` that specifies the commands that are executed by the app’s dynos. 

For more information read on the [heroku documentation](https://devcenter.heroku.com/articles/procfile).

Create a file named `Procfile` in the project root with the following content:
```
web: gunicorn manage:app
```
**NB:** manage is the mudule name of your application

Install gunicorn
```
pip install gunicorn && pip freeze > requirements.txt
```
## Config Settings
Add the `If` statement on your production class that changes the `DATABASE_URI` variable from postgres to postgresql on production environment.
```bash
import  os
class Config:
    '''
    General configuration parent class
    '''
    SECRET_KEY= os.environ.get('SECRET_KEY')
    SQLALCHEMY_TRACK_MODIFICATIONS = True
    
class DevConfig(Config):
    SQLALCHEMY_DATABASE_URI = 'postgresql+psycopg2://enock:Maeba1995@localhost/pitch'       
    DEBUG = True    

class ProdConfig(Config):
    
    SQLALCHEMY_DATABASE_URI = os.environ.get("DATABASE_URL") 
     if SQLALCHEMY_DATABASE_URI.startswith("postgres://"):
         SQLALCHEMY_DATABASE_URI = SQLALCHEMY_DATABASE_URI.replace("postgres://", "postgresql://", 1)


config_options = {
    'development': DevConfig,
    'production': ProdConfig
}
```
**NB:** Remove the `IF` statements on development environment.

Change your configuration settings from  development to  production. Like in the example below (manage.py file)
```bash
from app import create_app,db
from flask_script import Manager,Server
from app.models import User
from  flask_migrate import Migrate, MigrateCommand

# Creating app instance
app = create_app('production')

manager = Manager(app)
migrate = Migrate(app,db)

manager.add_command('server',Server)
manager.add_command('db',MigrateCommand)

@manager.command
def test():
    """Run the unit tests."""
    import unittest
    tests = unittest.TestLoader().discover('tests')
    unittest.TextTestRunner(verbosity=2).run(tests)

@manager.shell
def make_shell_context():
    return dict(app = app,db = db,User = User )

if __name__ == '__main__':
    manager.run()
```
## Run migrations
```bash
python3 manage.py db migrate -m "Initial Migration"
```
Run Upgrade

```bash
python3.6 manage.py db upgrade
```
## Heroku Addons
Create a postgres addon to your heroku app
```bash
heroku addons:create heroku-postgresql
```
Add all your configurations to heroku by running this command.
```bash
heroku config:set SECRET_KEY=blablablabla
```
# Push to Heroku
```bash 
git add .
git commit -m "deploying"
git push heroku master
```
# Heroku Upgrade
```bash
heroku run python3 manage.py db upgrade
```
You can open your app through the link generated in your terminal or open app on heroku dashboard.

or run
```bash
(virtual)$ heroku open  --app <insert your heroku app name>
```

