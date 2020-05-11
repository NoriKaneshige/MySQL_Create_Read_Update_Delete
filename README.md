# MySQL_Creating_Database_and_Tables

## Start the CLI:
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

```
