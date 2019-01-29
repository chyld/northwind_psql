# Northwind database for Postgres

A simple sql script that will populate a database with the famous northwind example, adapted for postgres.

## Docker

```
alias runpg='docker run
  --name raptor
  -d
  -e POSTGRES_PASSWORD=abc
  -p 5432:5432
  -v /Users/chyld/Data/postgres/data:/var/lib/postgresql/data
  postgres'

docker exec -it --user postgres raptor bash
```

## Script

```
#!/bin/bash

dropdb --if-exists northwind
dropuser --if-exists northwind_user

createdb northwind
psql northwind < northwind.sql

psql template1 -c "create user northwind_user;"
psql template1 -c "alter user northwind_user password 'thewindisblowing';"
psql template1 -c "grant all on DATABASE northwind to northwind_user;"
psql northwind -c "GRANT ALL on ALL tables IN SCHEMA public to northwind_user"
```
