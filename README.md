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
