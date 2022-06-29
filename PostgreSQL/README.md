### Setting up PostgreSQL 

```bash
sudo apt install postgresql-client-common
```

```bash
sudo apt-get install postgresql-contrib libpq-dev
```

```bash
sudo service postgresql start
```

```bash
sudo -u postgres createuser --superuser $USER
```

```bash
sudo -u postgres createdb $USER
```

```bash
touch .psql.history
```

```bash
psql
```