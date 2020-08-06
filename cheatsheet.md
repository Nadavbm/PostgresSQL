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

`\q` - quit

#### basics

##### db

create database - ```CREATE DATABASE dbName;``` 

drop database - ```DROP DATABASE dbName;```

see which db - ```SELECT current_database();```

##### users

see which user connected - ```SELECT current_user();```

##### tables

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

drop table - ```DROP TABLE tableName;```

list table records:

``` SQL
SELECT  * FROM tableName;
```

###### insert queries

create the table to insert data to:
``` SQL
CREATE TABLE tableName (
    id  SERIAL     PRIMARY KEY,
    name    TEXT    NOT NULL,
    age     INT     NOT NULL,
    title   CHAR(50),
    address CHAR(50)
)
```

insert a record (we don't need to add id since it is auto increment - `SERIAL`):

``` SQL
INSERT INTO tableName (id, name, age, title, address) VALUES ('nadav', 36, 'devops', 'nakatomi plaza | john mclain 12')

INSERT INTO tableName (id, name, age, title, address) VALUES ('shimrit', 42, 'mashachnaasa', 'beersheva'), ('yoram', 'gizbar', 72, 'sde-nehemia'), ('ishtvan', 40, 'midfield', 'beitar');
```

#### relational databases
create the tables with relations:
``` SQL
CREATE TABLE people (pid serial primary key not null, name char(50) not null);
CREATE TABLE cars (cid serial primary key not null, car_type char(50) not null, car_license text not null);
CREATE TABLE rent_time (rid serial primary key not null, pid int references people(pid), cid int references cars(cid), rental_hours char(50));
```
insert some data:
``` SQL
insert into people(name) values ('shimon'), ('nehemia'), ('bezazek');
insert into cars(car_type, car_license) values ('shevrolet','123-123-33'), ('renault', '123-124-44');
insert into rent_time (pid, rid, rental_hours) value (1,1, '8.8.2020 17:00 - 12.8.2020 18:00'), (2,1, '20.7.2020 11:00 - 22.7.2020 17:00);
```

use inner join (second query uses alias):
``` SQL
SELECT * FROM people inner join rent_time on people.pid = rent_time.pid;

SELECT * FROM people a inner join rent_time b on a.pid = b.pid;
```