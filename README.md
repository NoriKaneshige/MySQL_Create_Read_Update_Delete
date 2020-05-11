# MySQL_Creating_Database_and_Tables

## Start the CLI:
```
mysql-ctl cli; 
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



```
root@goorm:/workspace/mysql# mysql-ctl stop
 * Stopping MySQL database server mysqld
   ...done.
root@goorm:/workspace/mysql#
```
