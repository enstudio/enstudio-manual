Install PostgresSQL

```
$ sudo apt-get update
$ sudo apt-get install postgresql postgresql-contrib
```

Enter psql as 'postgres' user
```
$ sudo -u postgres psql
```

Create database

specify collation to c for correct ordering
```
postgres=# CREATE DATABASE myproject TEMPLATE template0 LC_COLLATE 'C';
```

Create user
```
postgres=# CREATE USER myprojectuser WITH PASSWORD 'password';
```

Set the default encoding to UTF-8
Block reads from uncommitted transactions
```
postgres=# ALTER ROLE myprojectuser SET client_encoding TO 'utf8';
postgres=# ALTER ROLE myprojectuser SET default_transaction_isolation TO 'read committed';
```

Grant privileges
```
postgres=# GRANT ALL PRIVILEGES ON DATABASE myproject TO myprojectuser;
```

Exit
```
postgres=# \q
```
