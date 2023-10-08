<!-- @format -->

# MICROSOFT SINGLE SIGN ON

Microsoft Office 365 login in your Django application

## Install Required Packages

Make sure you have the necessary packages installed in your Django project:

```bash
pip install django-auth-adfs requests

```

### Configure Django Settings:

Update your `settings.py` with the following configurations:

```bash
INSTALLED_APPS = [
    ...
    "django_auth_adfs",
]

```

```bash
MIDDLEWARE = [
    ...
    "django_auth_adfs.middleware.LoginRequiredMiddleware",
]

```

```bash
AUTHENTICATION_BACKENDS = (
    "django_auth_adfs.backend.AdfsAuthCodeBackend",
)

```

```bash
LOGIN_URL = "django_auth_adfs:login"
LOGIN_REDIRECT_URL = "/"
AZURE_AD_CLIENT_ID = "YOUR_CLIENT_ID"
AZURE_AD_CLIENT_SECRET = "YOUR_CLIENT_SECRET"
AZURE_AD_TENANT_ID = "YOUR_TENANT_ID"

```

```bash

AUTH_ADFS = {
    "AUDIENCE": AZURE_AD_CLIENT_ID,
    "CLIENT_ID": AZURE_AD_CLIENT_ID,
    "CLIENT_SECRET": AZURE_AD_CLIENT_SECRET,
    "CLAIM_MAPPING": {
        "first_name": "given_name",
        "last_name": "family_name",
        "email": "upn",
    },
    "GROUPS_CLAIM": "roles",
    "MIRROR_GROUPS": True,
    "USERNAME_CLAIM": "upn",
    "TENANT_ID": AZURE_AD_TENANT_ID,
    "RELYING_PARTY_ID": AZURE_AD_CLIENT_ID,
}

```

### Update URLs

In your `urls.py`, include the URLs for Microsoft login:

```bash
path("oauth2/", include("django_auth_adfs.urls")),
path("auth/callback/", views.azure_ad_callback.as_view(), name="azure_ad_callback"),
path("logout/", views.logout_view, name="logout"),

```

### Implement CallBack View

```bash
from django.shortcuts import redirect

class azure_ad_callback(UserObjectMixins, View):
    async def get(self, request):
        try:
            # ... Your business logic...

            # Redirect the user to a different URL after processing
            return redirect("/some-other-url/")
        except:
            pass

```

### Implement Logout View

```bash
from django.contrib.auth import logout
from django.shortcuts import redirect

def logout_view(request):
    # Log the user out
    logout(request)

    # Redirect to a specific URL or back to the home page
    return redirect("home")  # You can change "home" to the desired URL


```
