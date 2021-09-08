Common Django Errors
=====================
Common django errors that you are probably going to encounter during development, versioning or deployment of your django app.

# Development Errors

## Models
Errors coming from your models
- TypeError: __init__() missing 1 required positional argument: 'on_delete'

**`solution`**

**Add** `on_delete=models.CASCADE` where you have a foreign key on your models.

Example:
```bash
class Article(models.Model):
    title = models.CharField(max_length=60)
    post = HTMLField()
    editor = models.ForeignKey(User, on_delete=models.CASCADE)
```
- Field 'id' expected a number but got datetime.datetime(2021, 9, 4, 14, 42, 5, 316108, tzinfo=<UTC>)

**`solution`**

- Go to `migration files`. Find 002 (or 003,004 etc )_auto.py files
- Change field = models.ForeignKey(default = `django.utils.timezone.now`) to default = `1`

# Code Versioning Errors

## Pushing To GIthub
- Fatal-the-remote-end-hung-up-unexpectedly

**`solution`**

```bash
git remote remove origin
git remote add origin https://github.com/user/repo
git push --set-upstream origin master
```






    