Serving Django App using Postgres With Apache and mod_wsgi on Linux Server(ubuntu/Centos)
=========================================================================================

I will demonstrate how to install and configure Postgres and Django in a Python virtual environment. We’ll then set up Apache in front of our application so that it can handle client requests directly before passing requests that require application logic to the Django app. We will do this using the mod_wsgi Apache module that can communicate with Django over the WSGI interface specification.

# Disclaimer
- Confirm that your application is running as expected before deploying, runtime errors will cause deployment to fail so make sure you have no bugs.
- Ignore every code/command followed by `#` in .env file.
- In section(s) where you are expected to input values do not include `<>` brackets after input
- Procedure works best with Django version 3 and above.
- For centos substitute `apt-get` with `yum`

# Install Required Packages

### Update linux packages

```
sudo apt-get update
```

### Install Latest Version of Python

```
sudo apt-get install python3
```

### Verify Python Installation

```
python3 --version
```

### Installing Apache (Centos/ubuntu)

#### CENTOS 7/8
Enable the EPEL repository to get pip
```
sudo yum install epel-release
```
```
sudo yum install httpd mod_wsgi
```
#### Ubuntu
```
sudo apt-get install apache2 libapache2-mod-wsgi-py3
```

### Set Up PostgreSQL for Django 
To start off, we need to initialize the PostgreSQL database.

```
sudo postgresql-setup initdb
```

After the database has been initialized, we can start the PostgreSQL service by typing:

```
sudo systemctl start postgresql
```

With the database started, we actually need to adjust the values in one of the configuration files that has been populated. Use your editor and the sudo command to open the file now:

```
sudo nano /var/lib/pgsql/data/pg_hba.conf
```

Configure this by modifying the two host lines at the bottom of the file. Change the last column (the authentication method) to md5. This will allow password authentication.
When you are finished, save and close the file.

With our new configuration changes, we need to restart the service. We will also enable PostgreSQL so that it starts automatically at boot.

```
sudo systemctl restart postgresql
sudo systemctl enable postgresql
```

#### Create the PostgreSQL Database and User

```
sudo su - postgres
```

Type `psql` to get the PostgreSQL prompt where we can set up your requirements (Database, Database user and Privileges)


# Preparing the Application

Add the following to our project, we will cover each of them in detail in the below section

* Pull your project from the remote repository.
* Configure your project virtual environment and install all the required dependencies including `psycopg2`
* Configure your `.env` file
* Make migrations
* Create admin super user. `./manage.py createsuperuser`
* Configure `whitenoise` to serve static files.
* Run `./manage.py collectstatic`  to collect all of the static content 
* Run your project on the server and make sure that there is no runtime error(s)


## Configure Apache
To configure the WSGI pass, we’ll need to create a new configuration file that defines the WSGI pass. Create and open a file with sudo privileges within the /etc/httpd/conf.d directory. We will call this file django.conf:

```bash
sudo nano /etc/httpd/conf.d/django.conf
```
**NB:** Add the changes to the file then save and close

```
Alias /path /to/your/project/static
<Directory /path /to/your/project/static>
    Require all granted
</Directory>

<Directory /path/to/your/project folder which has settings.py>
    <Files wsgi.py>
        Require all granted
    </Files>
</Directory>

WSGIDaemonProcess myproject python-path=/home/user/myproject:/home/user/myproject/myprojectenv/lib/python3.9/site-packages
WSGIProcessGroup myproject
WSGIScriptAlias / /home/user/myproject/myproject/wsgi.py
```

### Wrapping Up Some Permissions Issues
Add the apache user to your group. Substitute your own username for the user in the command:

```
sudo usermod -a -G <user> apache
```

Now, we can give our user group execute permissions on our home directory. This will allow the Apache process to enter and access content within:

```
chmod 710 </home/user>
```

Once these steps are done, you are ready to start the Apache service. To do so, type:

```python
sudo systemctl start httpd
```

You should now be able to access your Django site by going to your server’s domain name or IP address without specifying a port. The regular site and the admin interface should function as expected.

If everything works as expected, you can enable the Apache service so that it starts automatically at boot:

 ```python
sudo systemctl enable httpd
```




