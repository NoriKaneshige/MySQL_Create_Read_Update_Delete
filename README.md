# MySQL_Creating_Database_and_Tables

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
