# MySQL_CRUD (Ceate, Read, Update, Delete)

## Start the CLI (Command-line interface):
```
mysql-ctl cli; 
```
## Quit the CLI:
```
exit
```

## Start/Stop server:
```
mysql-ctl start
mysql-ctl stop
```

## List available databases:
```
show databases; 
```
## The general command for creating a database:
```
CREATE DATABASE database_name; 
```
## To drop a database:
```
DROP DATABASE database_name;
```

## Using Databases (tell MySQL we want to be working with)
```
USE <database name>;
 
-- example:
USE dog_walking_app;
```
## How to check what database we are currently using
``` 
SELECT database();
```

## How Do We Create Tables?
```
CREATE TABLE tablename
  (
    column_name data_type,
    column_name data_type
  );
CREATE TABLE cats
  (
    name VARCHAR(100),
    age INT
  );

```

## How Do We Know It Worked?
```
SHOW TABLES;
 
SHOW COLUMNS FROM tablename;
 
DESC tablename;
```

## Dropping Tables
```
DROP TABLE <tablename>; 
```


## Example, Creating/Checking/Deleting Databases/Tables
```
Database changed
mysql> CREATE TABLE pastries (name VARCHAR(50), quantity INT);
Query OK, 0 rows affected (0.14 sec)

mysql> SHOW TABLES;
+---------------------+
| Tables_in_ann_arbor |
+---------------------+
| pastries            |
+---------------------+
1 row in set (0.00 sec)

mysql> DESC pastries;
+----------+-------------+------+-----+---------+-------+
| Field    | Type        | Null | Key | Default | Extra |
+----------+-------------+------+-----+---------+-------+
| name     | varchar(50) | YES  |     | NULL    |       |
| quantity | int(11)     | YES  |     | NULL    |       |
+----------+-------------+------+-----+---------+-------+
2 rows in set (0.01 sec)

mysql> DROP TABLE pastries;
Query OK, 0 rows affected (0.13 sec)

mysql> SHOW TABLES;
Empty set (0.00 sec)

mysql>
```

## Inserting Data (setting up)
```
| ann_arbor          |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
5 rows in set (0.05 sec)

mysql> SELECT database();
+------------+
| database() |
+------------+
| NULL       |
+------------+
1 row in set (0.00 sec)

mysql> USE ann_arbor;
Database changed
mysql> SHOW TABLES;
Empty set (0.00 sec)

mysql> CREATE TABLE cats(name VARCHAR(50),age INT);
Query OK, 0 rows affected (0.10 sec)

mysql> INSERT INTO cats(name,age) VALUES ('Jetson',7)
    -> ;
Query OK, 1 row affected (0.01 sec)
```

## How do we know it worked
```
mysql> SELECT * FROM cats;
+--------+------+
| name   | age  |
+--------+------+
| Jetson |    7 |
+--------+------+
1 row in set (0.00 sec)
```

## Multiple insert
```
mysql> INSERT INTO cats(name,age)
    -> VALUES ('peanut',7)
    -> ,('butter',2)
    -> ,('jelly',5);
Query OK, 3 rows affected (0.12 sec)
Records: 3  Duplicates: 0  Warnings: 0

mysql> SELECT * FROM cats;
+--------+------+
| name   | age  |
+--------+------+
| Jetson |    7 |
| peanut |    7 |
| butter |    2 |
| jelly  |    5 |
+--------+------+
4 rows in set (0.13 sec)
```

## What happens if we insert incomplete data? (we get NULL)
```
mysql> INSERT INTO cats(name) VALUES('Alabama');
Query OK, 1 row affected (0.12 sec)

mysql> SHOW WARNINGS;
Empty set (0.00 sec)

mysql> SELECT * FROM cats;
+---------+------+
| name    | age  |
+---------+------+
| Jetson  |    7 |
| peanut  |    7 |
| butter  |    2 |
| jelly   |    5 |
| Alabama | NULL |
+---------+------+
5 rows in set (0.01 sec)

mysql> INSERT INTO cats() VALUES();
Query OK, 1 row affected (0.10 sec)

mysql> SELECT * FROM cats;
+---------+------+
| name    | age  |
+---------+------+
| Jetson  |    7 |
| peanut  |    7 |
| butter  |    2 |
| jelly   |    5 |
| Alabama | NULL |
| NULL    | NULL |
+---------+------+
6 rows in set (0.00 sec)
```

## How to set NOT NULL
```
mysql> CREATE TABLE cats2
    ->   (
    ->     name VARCHAR(100) NOT NULL,
    ->     age INT NOT NULL
    ->   );
Query OK, 0 rows affected (0.14 sec)

mysql> DESC cats2;
+-------+--------------+------+-----+---------+-------+
| Field | Type         | Null | Key | Default | Extra |
+-------+--------------+------+-----+---------+-------+
| name  | varchar(100) | NO   |     | NULL    |       |
| age   | int(11)      | NO   |     | NULL    |       |
+-------+--------------+------+-----+---------+-------+
2 rows in set (0.10 sec)

mysql> INSERT INTO cats2(name) VALUES('Texas');
Query OK, 1 row affected, 1 warning (0.01 sec)

mysql> SELECT * FROM cats2;
+-------+-----+
| name  | age |
+-------+-----+
| Texas |   0 |
+-------+-----+
1 row in set (0.00 sec)

mysql> INSERT INTO cats2(age) VALUES(7);
Query OK, 1 row affected, 1 warning (0.02 sec)

mysql> DESC cats2;
+-------+--------------+------+-----+---------+-------+
| Field | Type         | Null | Key | Default | Extra |
+-------+--------------+------+-----+---------+-------+
| name  | varchar(100) | NO   |     | NULL    |       |
| age   | int(11)      | NO   |     | NULL    |       |
+-------+--------------+------+-----+---------+-------+
2 rows in set (0.01 sec)

mysql> SELECT * FROM cats2;
+-------+-----+
| name  | age |
+-------+-----+
| Texas |   0 |
|       |   7 |
+-------+-----+
2 rows in set (0.00 sec)
```

## How to set Default values
```
mysql> CREATE TABLE cats4
    ->   (
    ->     name VARCHAR(20) NOT NULL DEFAULT 'unnamed',
    ->     age INT NOT NULL DEFAULT 99
    ->   );
Query OK, 0 rows affected (0.27 sec)

mysql> SELECT * FROM cats4;
Empty set (0.00 sec)

mysql> DESC cats4;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| name  | varchar(20) | NO   |     | unnamed |       |
| age   | int(11)     | NO   |     | 99      |       |
+-------+-------------+------+-----+---------+-------+
2 rows in set (0.00 sec)

mysql> INSERT INTO cats4() VALUES();
Query OK, 1 row affected (0.01 sec)

mysql> SELECT * FROM cats4;
+---------+-----+
| name    | age |
+---------+-----+
| unnamed |  99 |
+---------+-----+
1 row in set (0.00 sec)

mysql> INSERT INTO cats4(name, age) VALUES('Cali', NULL);
ERROR 1048 (23000): Column 'age' cannot be null
```

## How to add primary keys with auto-increment
```
mysql> CREATE TABLE unique_cats2 (
    ->     cat_id INT NOT NULL AUTO_INCREMENT,
    ->     name VARCHAR(100),
    ->     age INT,
    ->     PRIMARY KEY (cat_id)
    -> );
Query OK, 0 rows affected (0.07 sec)

mysql> DESC unique_cats2;
+--------+--------------+------+-----+---------+----------------+
| Field  | Type         | Null | Key | Default | Extra          |
+--------+--------------+------+-----+---------+----------------+
| cat_id | int(11)      | NO   | PRI | NULL    | auto_increment |
| name   | varchar(100) | YES  |     | NULL    |                |
| age    | int(11)      | YES  |     | NULL    |                |
+--------+--------------+------+-----+---------+----------------+
3 rows in set (0.00 sec)

mysql> INSERT INTO unique_cats2(name, age) VALUES('Skippy', 4);
Query OK, 1 row affected (0.02 sec)

mysql> INSERT INTO unique_cats2(name, age) VALUES('Jiff', 3);
Query OK, 1 row affected (0.01 sec)

mysql> INSERT INTO unique_cats2(name, age) VALUES('Jiff', 3);
Query OK, 1 row affected (0.02 sec)

mysql> INSERT INTO unique_cats2(name, age) VALUES('Jiff', 3);
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO unique_cats2(name, age) VALUES('Skippy', 4);
Query OK, 1 row affected (0.01 sec)

mysql> SELECT * FROM unique_cats2;
+--------+--------+------+
| cat_id | name   | age  |
+--------+--------+------+
|      1 | Skippy |    4 |
|      2 | Jiff   |    3 |
|      3 | Jiff   |    3 |
|      4 | Jiff   |    3 |
|      5 | Skippy |    4 |
+--------+--------+------+
5 rows in set (0.00 sec)
```

## Example, adding primary keys that increment
```
mysql> CREATE TABLE employees (
    ->     id INT AUTO_INCREMENT NOT NULL PRIMARY KEY,
    ->     first_name VARCHAR(255) NOT NULL,
    ->     last_name VARCHAR(255) NOT NULL,
    ->     middle_name VARCHAR(255),
    ->     age INT NOT NULL,
    ->     current_status VARCHAR(255) NOT NULL DEFAULT 'employed'
    -> );
Query OK, 0 rows affected (0.10 sec)

mysql> INSERT INTO employees(first_name, last_name, age) VALUES
    -> ('Dora', 'Smith', 58);
Query OK, 1 row affected (0.01 sec)

mysql> SELECT * FROM employees;
+----+------------+-----------+-------------+-----+----------------+
| id | first_name | last_name | middle_name | age | current_status |
+----+------------+-----------+-------------+-----+----------------+
|  1 | Dora       | Smith     | NULL        |  58 | employed       |
+----+------------+-----------+-------------+-----+----------------+
1 row in set (0.00 sec)
```

## More Example, SELECT
```
mysql> CREATE TABLE cats
    ->   (
    ->      cat_id INT NOT NULL AUTO_INCREMENT,
    ->      name   VARCHAR(100),
    ->      breed  VARCHAR(100),
    ->      age    INT,
    ->      PRIMARY KEY (cat_id)
    ->   );
Query OK, 0 rows affected (0.14 sec)

mysql> DESC cats;
+--------+--------------+------+-----+---------+----------------+
| Field  | Type         | Null | Key | Default | Extra          |
+--------+--------------+------+-----+---------+----------------+
| cat_id | int(11)      | NO   | PRI | NULL    | auto_increment |
| name   | varchar(100) | YES  |     | NULL    |                |
| breed  | varchar(100) | YES  |     | NULL    |                |
| age    | int(11)      | YES  |     | NULL    |                |
+--------+--------------+------+-----+---------+----------------+
4 rows in set (0.06 sec)

mysql> INSERT INTO cats(name, breed, age)
    -> VALUES ('Ringo', 'Tabby', 4),
    ->        ('Cindy', 'Maine Coon', 10),
    ->        ('Dumbledore', 'Maine Coon', 11),
    ->        ('Egg', 'Persian', 4),
    ->        ('Misty', 'Tabby', 13),
    ->        ('George Michael', 'Ragdoll', 9),
    ->        ('Jackson', 'Sphynx', 7);
Query OK, 7 rows affected (0.04 sec)
Records: 7  Duplicates: 0  Warnings: 0

mysql> SELECT * FROM cats;
+--------+----------------+------------+------+
| cat_id | name           | breed      | age  |
+--------+----------------+------------+------+
|      1 | Ringo          | Tabby      |    4 |
|      2 | Cindy          | Maine Coon |   10 |
|      3 | Dumbledore     | Maine Coon |   11 |
|      4 | Egg            | Persian    |    4 |
|      5 | Misty          | Tabby      |   13 |
|      6 | George Michael | Ragdoll    |    9 |
|      7 | Jackson        | Sphynx     |    7 |
+--------+----------------+------------+------+
7 rows in set (0.00 sec)

mysql> SELECT age FROM cats;
+------+
| age  |
+------+
|    4 |
|   10 |
|   11 |
|    4 |
|   13 |
|    9 |
|    7 |
+------+
7 rows in set (0.00 sec)

mysql> SELECT age, breed, name, cat_id FROM cats;
+------+------------+----------------+--------+
| age  | breed      | name           | cat_id |
+------+------------+----------------+--------+
|    4 | Tabby      | Ringo          |      1 |
|   10 | Maine Coon | Cindy          |      2 |
|   11 | Maine Coon | Dumbledore     |      3 |
|    4 | Persian    | Egg            |      4 |
|   13 | Tabby      | Misty          |      5 |
|    9 | Ragdoll    | George Michael |      6 |
|    7 | Sphynx     | Jackson        |      7 |
+------+------------+----------------+--------+
7 rows in set (0.00 sec)
```

## WHERE
```
mysql> SELECT * FROM cats WHERE age=4;
+--------+-------+---------+------+
| cat_id | name  | breed   | age  |
+--------+-------+---------+------+
|      1 | Ringo | Tabby   |    4 |
|      4 | Egg   | Persian |    4 |
+--------+-------+---------+------+
2 rows in set (0.03 sec)

mysql> SELECT name, age FROM cats WHERE breed='Tabby';
+-------+------+
| name  | age  |
+-------+------+
| Ringo |    4 |
| Misty |   13 |
+-------+------+
2 rows in set (0.00 sec)

mysql> SELECT cat_id, age FROM cats WHERE cat_id=age;
+--------+------+
| cat_id | age  |
+--------+------+
|      4 |    4 |
|      7 |    7 |
+--------+------+
2 rows in set (0.06 sec)
```
## Aliases
```
mysql> SELECT cat_id AS id, name FROM cats;
+----+----------------+
| id | name           |
+----+----------------+
|  1 | Ringo          |
|  2 | Cindy          |
|  3 | Dumbledore     |
|  4 | Egg            |
|  5 | Misty          |
|  6 | George Michael |
|  7 | Jackson        |
+----+----------------+
7 rows in set (0.15 sec)

mysql> SELECT name AS 'cat name', breed AS 'kitty breed' FROM cats;
+----------------+-------------+
| cat name       | kitty breed |
+----------------+-------------+
| Ringo          | Tabby       |
| Cindy          | Maine Coon  |
| Dumbledore     | Maine Coon  |
| Egg            | Persian     |
| Misty          | Tabby       |
| George Michael | Ragdoll     |
| Jackson        | Sphynx      |
+----------------+-------------+
7 rows in set (0.01 sec)
```

## UPDATE
```
mysql> SELECT * FROM cats WHERE name='Jackson';
+--------+---------+--------+------+
| cat_id | name    | breed  | age  |
+--------+---------+--------+------+
|      7 | Jackson | Sphynx |    7 |
+--------+---------+--------+------+
1 row in set (0.09 sec)

mysql> UPDATE cats SET name='Jack' WHERE name='Jackson';
Query OK, 1 row affected (0.08 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> SELECT * FROM cats WHERE name='Jackson';
Empty set (0.00 sec)

mysql> SELECT * FROM cats WHERE name='Jack';
+--------+------+--------+------+
| cat_id | name | breed  | age  |
+--------+------+--------+------+
|      7 | Jack | Sphynx |    7 |
+--------+------+--------+------+
1 row in set (0.01 sec)


mysql> SELECT * FROM cats WHERE breed='Maine Coon';
+--------+------------+------------+------+
| cat_id | name       | breed      | age  |
+--------+------------+------------+------+
|      2 | Cindy      | Maine Coon |   10 |
|      3 | Dumbledore | Maine Coon |   11 |
+--------+------------+------------+------+
2 rows in set (0.01 sec)

mysql> UPDATE cats SET age=12 WHERE breed='Maine Coon';
Query OK, 2 rows affected (0.01 sec)
Rows matched: 2  Changed: 2  Warnings: 0

mysql> SELECT * FROM cats WHERE breed='Maine Coon';
+--------+------------+------------+------+
| cat_id | name       | breed      | age  |
+--------+------------+------------+------+
|      2 | Cindy      | Maine Coon |   12 |
|      3 | Dumbledore | Maine Coon |   12 |
+--------+------------+------------+------+
2 rows in set (0.01 sec)
```

## DELETE (syntax is the same as SELECT)
```
mysql> SELECT *  FROM cats WHERE cat_id=age;
+--------+------+---------+------+
| cat_id | name | breed   | age  |
+--------+------+---------+------+
|      4 | Egg  | Persian |    4 |
|      7 | Jack | Sphynx  |    7 |
+--------+------+---------+------+
2 rows in set (0.00 sec)

mysql> DELETE FROM cats WHERE cat_id=age;
Query OK, 2 rows affected (0.06 sec)

mysql> SELECT * FROM cats;
+--------+----------------+------------+------+
| cat_id | name           | breed      | age  |
+--------+----------------+------------+------+
|      1 | Ringo          | Tabby      |    4 |
|      2 | Cindy          | Maine Coon |   12 |
|      3 | Dumbledore     | Maine Coon |   12 |
|      5 | Misty          | Tabby      |   13 |
|      6 | George Michael | Ragdoll    |    9 |
+--------+----------------+------------+------+
5 rows in set (0.00 sec)

mysql> DELETE FROM cats;
Query OK, 5 rows affected (0.05 sec)

mysql> SELECT * FROM cats;
Empty set (0.00 sec)
```

# CRUD Challange Example
## 1) Create Database and Table
```
mysql> CREATE DATABASE shirts_db;
Query OK, 1 row affected (0.03 sec)

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| ann_arbor          |
| mysql              |
| performance_schema |
| shirts_db          |
| sys                |
+--------------------+
6 rows in set (0.01 sec)

mysql> use shirts_db;
Database changed
mysql> SELECT database();
+------------+
| database() |
+------------+
| shirts_db  |
+------------+
1 row in set (0.00 sec)


mysql> CREATE TABLE shirts
    ->   (
    ->     shirt_id INT NOT NULL AUTO_INCREMENT,
    ->     article VARCHAR(100),
    ->     color VARCHAR(100),
    ->     shirt_size VARCHAR(100),
    ->     last_worn INT,
    ->     PRIMARY KEY(shirt_id)
    ->   );
Query OK, 0 rows affected (0.14 sec)

mysql> DESC shirts;
+------------+--------------+------+-----+---------+----------------+
| Field      | Type         | Null | Key | Default | Extra          |
+------------+--------------+------+-----+---------+----------------+
| shirt_id   | int(11)      | NO   | PRI | NULL    | auto_increment |
| article    | varchar(100) | YES  |     | NULL    |                |
| color      | varchar(100) | YES  |     | NULL    |                |
| shirt_size | varchar(100) | YES  |     | NULL    |                |
| last_worn  | int(11)      | YES  |     | NULL    |                |
+------------+--------------+------+-----+---------+----------------+
5 rows in set (0.06 sec)
5 rows in set (0.06 sec)

mysql> INSERT INTO shirts(article, color, shirt_size, last_worn) VALUES
    -> ('t-shirt', 'white', 'S', 10),
    -> ('t-shirt', 'green', 'S', 200),
    -> ('polo shirt', 'black', 'M', 10),
    -> ('tank top', 'blue', 'S', 50),
    -> ('t-shirt', 'pink', 'S', 0),
    -> ('polo shirt', 'red', 'M', 5),
    -> ('tank top', 'white', 'S', 200),
    -> ('tank top', 'blue', 'M', 15);
Query OK, 8 rows affected (0.09 sec)
Records: 8  Duplicates: 0  Warnings: 0

mysql> SELECT * FROM shirts;
+----------+------------+-------+------------+-----------+
| shirt_id | article    | color | shirt_size | last_worn |
+----------+------------+-------+------------+-----------+
|        1 | t-shirt    | white | S          |        10 |
|        2 | t-shirt    | green | S          |       200 |
|        3 | polo shirt | black | M          |        10 |
|        4 | tank top   | blue  | S          |        50 |
|        5 | t-shirt    | pink  | S          |         0 |
|        6 | polo shirt | red   | M          |         5 |
|        7 | tank top   | white | S          |       200 |
|        8 | tank top   | blue  | M          |        15 |
+----------+------------+-------+------------+-----------+
8 rows in set (0.00 sec)

mysql> INSERT INTO shirts(color, article, shirt_size, last_worn)
    -> VALUES('purple', 'polo shirt', 'medium', 50);
Query OK, 1 row affected (0.02 sec)

mysql> SELECT * FROM shirts;
+----------+------------+--------+------------+-----------+
| shirt_id | article    | color  | shirt_size | last_worn |
+----------+------------+--------+------------+-----------+
|        1 | t-shirt    | white  | S          |        10 |
|        2 | t-shirt    | green  | S          |       200 |
|        3 | polo shirt | black  | M          |        10 |
|        4 | tank top   | blue   | S          |        50 |
|        5 | t-shirt    | pink   | S          |         0 |
|        6 | polo shirt | red    | M          |         5 |
|        7 | tank top   | white  | S          |       200 |
|        8 | tank top   | blue   | M          |        15 |
|        9 | polo shirt | purple | medium     |        50 |
+----------+------------+--------+------------+-----------+
9 rows in set (0.00 sec)
```
## 2) READ Database and Table
```

mysql> SELECT article, color FROM shirts;
+------------+--------+
| article    | color  |
+------------+--------+
| t-shirt    | white  |
| t-shirt    | green  |
| polo shirt | black  |
| tank top   | blue   |
| t-shirt    | pink   |
| polo shirt | red    |
| tank top   | white  |
| tank top   | blue   |
| polo shirt | purple |
+------------+--------+
9 rows in set (0.00 sec)

mysql> SELECT * FROM shirts WHERE shirt_size='M';
+----------+------------+-------+------------+-----------+
| shirt_id | article    | color | shirt_size | last_worn |
+----------+------------+-------+------------+-----------+
|        3 | polo shirt | black | M          |        10 |
|        6 | polo shirt | red   | M          |         5 |
|        8 | tank top   | blue  | M          |        15 |
+----------+------------+-------+------------+-----------+
3 rows in set (0.08 sec)

mysql> SELECT article, color, shirt_size, last_worn FROM shirts WHERE shirt_size='M';
+------------+-------+------------+-----------+
| article    | color | shirt_size | last_worn |
+------------+-------+------------+-----------+
| polo shirt | black | M          |        10 |
| polo shirt | red   | M          |         5 |
| tank top   | blue  | M          |        15 |
+------------+-------+------------+-----------+
3 rows in set (0.00 sec)
```
## 3) UPDATE Table
```

mysql> SELECT * FROM shirts WHERE color='white';
+----------+----------+-------+------------+-----------+
| shirt_id | article  | color | shirt_size | last_worn |
+----------+----------+-------+------------+-----------+
|        1 | t-shirt  | white | S          |        10 |
|        7 | tank top | white | S          |       200 |
+----------+----------+-------+------------+-----------+
2 rows in set (0.00 sec)

mysql> UPDATE shirts SET color='off white', shirt_size='XS' WHERE color='white';
Query OK, 2 rows affected (0.02 sec)
Rows matched: 2  Changed: 2  Warnings: 0

mysql> SELECT * FROM shirts WHERE color='white';
Empty set (0.00 sec)

mysql> SELECT * FROM shirts WHERE color='off white';
+----------+----------+-----------+------------+-----------+
| shirt_id | article  | color     | shirt_size | last_worn |
+----------+----------+-----------+------------+-----------+
|        1 | t-shirt  | off white | XS         |        10 |
|        7 | tank top | off white | XS         |       200 |
+----------+----------+-----------+------------+-----------+
2 rows in set (0.00 sec)

mysql> SELECT * FROM shirts;
+----------+------------+-----------+------------+-----------+
| shirt_id | article    | color     | shirt_size | last_worn |
+----------+------------+-----------+------------+-----------+
|        1 | t-shirt    | off white | XS         |        10 |
|        2 | t-shirt    | green     | S          |       200 |
|        3 | polo shirt | black     | M          |        10 |
|        4 | tank top   | blue      | S          |        50 |
|        5 | t-shirt    | pink      | S          |         0 |
|        6 | polo shirt | red       | M          |         5 |
|        7 | tank top   | off white | XS         |       200 |
|        8 | tank top   | blue      | M          |        15 |
|        9 | polo shirt | purple    | medium     |        50 |
+----------+------------+-----------+------------+-----------+
9 rows in set (0.00 sec)
```
## 4) Delete
```

mysql> SELECT * FROM shirts WHERE last_worn=200;
+----------+----------+-----------+------------+-----------+
| shirt_id | article  | color     | shirt_size | last_worn |
+----------+----------+-----------+------------+-----------+
|        2 | t-shirt  | green     | S          |       200 |
|        7 | tank top | off white | XS         |       200 |
+----------+----------+-----------+------------+-----------+
2 rows in set (0.00 sec)

mysql> DELETE FROM shirts WHERE last_worn=200;
Query OK, 2 rows affected (0.06 sec)

mysql> SELECT * FROM shirts WHERE article='tank top';
+----------+----------+-------+------------+-----------+
| shirt_id | article  | color | shirt_size | last_worn |
+----------+----------+-------+------------+-----------+
|        4 | tank top | blue  | S          |        50 |
|        8 | tank top | blue  | M          |        15 |
+----------+----------+-------+------------+-----------+
2 rows in set (0.00 sec)

mysql> DELETE FROM shirts WHERE article='tank top';
Query OK, 2 rows affected (0.07 sec)

mysql> SELECT * FROM shirts WHERE article='tank top';
Empty set (0.00 sec)

mysql> SELECT * FROM shirts;
+----------+------------+-----------+------------+-----------+
| shirt_id | article    | color     | shirt_size | last_worn |
+----------+------------+-----------+------------+-----------+
|        1 | t-shirt    | off white | XS         |        10 |
|        3 | polo shirt | black     | M          |        10 |
|        5 | t-shirt    | pink      | S          |         0 |
|        6 | polo shirt | red       | M          |         5 |
|        9 | polo shirt | purple    | medium     |        50 |
+----------+------------+-----------+------------+-----------+
5 rows in set (0.00 sec)

mysql> DELETE FROM shirts;
Query OK, 5 rows affected (0.02 sec)

mysql> SELECT * FROM shirts;
Empty set (0.00 sec)

mysql> DROP TABLE shirts;
Query OK, 0 rows affected (0.17 sec)

mysql> show tables;
Empty set (0.00 sec)

mysql> DESC shirts;
ERROR 1146 (42S02): Table 'shirts_db.shirts' doesn't exist
```
