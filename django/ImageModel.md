Disappearing Images After Hosting
=================================
Deploying images to heroku can be difficult as the images end up disappearing as the database size explodes over time. Hence, images should be stored in a nexternal service like  Cloudinary, Amazon Web Service, S3 etc. Focus will be on Cloudinary because it's configuration is quick and easy.

**Disclaimer**

In this example my project will be called `photoProject` and third party app `photoApp`.

## Preliminaries

- Setup new django project
- Set up and activate virtual environment
- Create third party application(s)
- Add app to a list of installed apps on project settings.

[Follow Full Process Here](https://github.com/enockabere/Django-Get-Started/blob/master/django/get-started.md)

## Set Up Cloudinary

Head Over to [Cloudinary](https://cloudinary.com/) and create an account

## Installation
Install The Cloudinary module to your project, make sure your virtual environment is active.

```bash
pip install cloudinary && pip freeze > requirements.txt
```

## Project Settings.py

Include the following settings in your project (photoProject >) `settings.py`

```bash
import cloudinary
import cloudinary.uploader
import cloudinary.api
```
**Then**

Add Cloudinary to the List of Installed Apps

```bash
INSTALLED_APPS = [
    '....',
    'photos', # Your third Party Application
    'cloudinary' #Add
]
```
## Configuration

To use the Cloudinary Django library, we have to configure our cloud_name, api_key, and api_secret.

We can find our account-specific configuration credentials on the Dashboard page of the account console as shown below.
![Cloudinary](static/images/3.png)

Click on `Configure Your SDK` and you'll se a pop up with a number of configuration parameters to use. On the pop window choose python and copy the configuration below it.

Add the copied configurations to your (photoProject >) `settings.py` file

```bash
cloudinary.config( 
  cloud_name = "your cloud name", 
  api_key = "your api key", 
  api_secret = "your secret key", 
)
```
## Creating Models
in your third party application, head over to (photoApp >)  `models.py` and add the following lines:

```bash
from django.db import models
from cloudinary.models import CloudinaryField

class photos(models.Model):
    ....
    #image field
    image = CloudinaryField('image')
```

Run your migrations

```bash
python3 manage.py check
```
```bash
python3 manage.py makemigrations
```
```bash
python3 manage.py migrate
```

Create a superuser to allow you create,edit, manage, and delete data :

```bash
python manage.py createsuperuser 
```
### Register Models

Register your model in the third party application (photoApp >)`admin.py`:

```bash
from django.contrib import admin
from .models import photos

admin.site.register(photos)
```
Log int to your Django admin with the superuser you created and add an Image to your models.

## Creating a View Function
Create a view function in your app (PhotoApp >) `views.py` file

```bash
from django.shortcuts import render
from .models import photos #import photos model

def index(request):
    # imports photos and save it in database
    photo = photos.objects.all()
    # adding context 
    ctx = {'photo':photo}
    return render(request, 'index.html', ctx)

```
Create urls. py file in your app (PhotoApp >) `urls.py`

Create a new URL for the newly created view in your app (PhotoApp >) `urls.py` file.

```bash
from django.contrib import admin
from django.urls import path
from photos import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', views.index, name='index'),
]
```

HTML template in your app (PhotoApp > templates >) `index.html`  for displaying the image.

```bash
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Photoapp</title>
    </head>
    <body>
        <h2>Cloudinary Images</h2>
        <!-- loop through all the images -->
        {% for pic in photo %}
        <h2>{{pic.title}}</h2>
            <img src="{{pic.image.url}}" alt="fish">
        {% endfor %}
    </body>
</html>
```