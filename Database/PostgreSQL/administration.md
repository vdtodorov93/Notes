# Installation
## With Homebrew run:

```shell
brew update
brew install postgresql
postgres --version
```


## Create a physical database

```
initdb /usr/local/var/postgres
```

# Administrating PostgreSQL

## Start/Stop a database

```
pg_ctl -D /usr/local/var/postgres start
pg_ctl -D /usr/local/var/postgres stop
``` 

## Create/Drop database

```
createdb mydatabasename
dropdb mydatabasename
```

## Run the shell
```
psql mydatabasename

CREATE DATABASE mydatabasename;
DROP DATABASE mydatabasename;

```

# Useful shell commands
`\l` lists all databases  
`\c dbname` connects to a specific database  
`\dt` lists tables in the current database  
`\d table_name` describes a table  
`\du` lists users and roles  
`create user mavoktest with password 'mavoktest';` creates a user  
`grant all privileges on database test to mavoktest`  
`\s` command history  
`\conninfo` connection info  
`\dt schema_name.*` lists all tables in `schema_name`  


# SQL
## Creating a table
```
CREATE TABLE weather (
    city            varchar(80),
    temp_lo         int,           -- low temperature
    temp_hi         int,           -- high temperature
    prcp            real,          -- precipitation
    date            date
);
```
