<!-- @format -->

# Quick Solutions

Common django fixes that you are probably going to need during development, versioning or deployment of your django app.

# Development Errors

## Models Errors

**Fix:** GIT PUSH: **init** without saving remote repository

**_`solution`_**

```bash
git push -u https://github.com/username/repository.git master

```

**Fix:** To stop tracking a git file that was accidentally tracked/committed

**_`solution`_**

```bash
rm -rf .vscode
```
