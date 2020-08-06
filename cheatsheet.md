### postgres cheatsheet

#### pgsql commands

terminal connect to db with pgcli \ psql:
``` 
$ pgcli local_database

$ psql postgres://amjith:passw0rd@example.com:5432/app_db

$ pgcli -h localhost -p 5432 -U amjith app_db
```

in db commands:

`\l` - list databases

`\c` - connect to database

`\dt` - list tables

`\d+ tableName` - describe table

`\du` - list users 

`\df` - list functions

`'df+ functionName` describe function

#### CREATE queries

create database - ```CREATE DATABASE dbName;``` 

create table - ```CREATE TABLE tableName (val1  type1, val2 type2);```

create table example:
``` SQL
CREATE TABLE tableName (
    code        char(5) CONSTRAINT firstkey PRIMARY KEY,
    title       varchar(40) NOT NULL,
    id          integer NOT NULL,
    date        date
);
```


``` SQL
SELECT  * FROM tableName;
```