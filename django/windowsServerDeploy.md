Serving Django App using Postgres With IIS on Windows Server
=============================================================

I will demonstrate how to install and configure Postgres and Django in a Python virtual environment. We’ll then set up Apache in front of our application so that it can handle client requests directly before passing requests that require application logic to the Django app. We will do this using the mod_wsgi Apache module that can communicate with Django over the WSGI interface specification.

# Disclaimer
- Confirm that your application is running as expected before deploying, runtime errors will cause deployment to fail so make sure you have no bugs.
- In section(s) where you are expected to input values do not include `<>`
- Procedure works best with Django version 3 and above.
- For centOS substitute `apt-get` with `yum`

# Download and Install Required Packages/Apps
- Git Bash
- Download your project repository and save it to C:\inetpub\wwwroot
- CGI in IIS
- Postgres
- Download Python and add it to path
- pip install wfastcgi

Once wfastcgi and IIS are installed, run `wfastcgi-enable` as an administrator to enable wfastcgi in the IIS configuration. This will configure a CGI application that can then be specified as a route handler.

### Setup your virtual environment and ran your code locally



### Create a web.config File on Root Folder
- Specify path to your FastCGI
- Specify your PYTHONPATH
- Add WSGI_HANDLER
- Add DJANGO_SETTINGS_MODULE


### Install all required dependencies to the VM using PIP

```
pip install -r requirements.txt
```

### ADD  IIS AppPool\DefaultAppPool to your PYTHON Security Properties and Allow all Permissions as well as your project directory.

#### OPen IIS and Create Your Site and Add the following
- Site name
- Physical Path - path to your project directory
- Add binding and port number

### Right Click on your site and add virtual directory
- alias = 'static'
- physical path = '/path to your static folder/'

#### Confirm site is working from server web browser

localhost:'port number'



# Expose Port by creating an inbound rule on server firewall settings

Perform the following actions while on the server;

* Pull/fork/clone your project from the remote repository using the linux terminal.
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




