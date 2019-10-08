## SE-Hands-On-lecture
Install Mysql &amp; Workbench

## Step 1. 
### 1.1 Install MySQL on macOS 
This procedure explains how to install [MySQL](https://www.mysql.com) using [Homebrew](http://brew.sh) on macOS

### 1.2 Install Homebrew
* Installing Homebrew is effortless, open Terminal and enter :  
 `$  /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`
* **Note:** Homebrew will download and install Command Line Tools for Xcode 8.0 as part of the installation process.

### 1.3 Install MySQL

* Enter the following command in your terminal : `$ brew info mysql`  
* Expected output (first line of the output): 
```
** mysql: stable 8.0.17 (bottled) **
```

To install MySQL enter : `$ brew install mysql`
  
After the installation
* Expected output (last lines of the output): 

```
To connect run:
    mysql -uroot

To have launchd start mysql now and restart at login:
  brew services start mysql
Or, if you don't want/need a background service you can just run:
  mysql.server start
```

### 1.4 Start MySQL Server

* Enter the following command : `$ mysql.server start`  
* Expected output: 
```
Starting MySQL
.. SUCCESS!

```

### 1.5 Setup Admin Password

* Enter the following command : `mysqladmin -u root password 'root'`  
* **Note:** I'm keeping it root for simplicity but you can use some other password as well.
* Expected output: 
```
mysqladmin: [Warning] Using a password on the command line interface can be insecure.
Warning: Since password will be sent to server in plain text, use ssl connection to ensure password safety.

```

### 1.6 Connect to Mysql 
* Enter the following command : `mysql -u root -p`  
* **Note:** It will prompt you to enter your password, just enter your password provided in the previous step.
* Expected output: 
```
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 11
Server version: 8.0.17 Homebrew

Copyright (c) 2000, 2019, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>
mysql>

```


## Step 2. 
### 1.1 Install Workbench
[Download Link for Workbench](https://dev.mysql.com/downloads/workbench/)

* It will download the dmg file of workbench, just install it will default config
 
### 1.2 Follow the steps in the ppt to know More.
* Workbench PPT in repository
   

## Install Mysql & Workbench on Windows
[Follow this youtube video for windows](https://www.youtube.com/watch?v=u96rVINbAUI)


## Mysql cheat sheet
### Show Databases

```sql
SHOW DATABASES;
```

### Create Database

```sql
CREATE DATABASE customer;
```

### Delete Database

```sql
DROP DATABASE customer;
```

### Select Database

```sql
USE customer;
```

### Create Table

```sql
CREATE TABLE users(
id INT AUTO_INCREMENT,
   first_name VARCHAR(100),
   last_name VARCHAR(100),
   email VARCHAR(50),
   password VARCHAR(20),
   location VARCHAR(100),
   dept VARCHAR(100),
   is_admin TINYINT(1),
   register_date DATETIME,
   PRIMARY KEY(id)
);
```

### Delete / Drop Table

```sql
DROP TABLE tablename;
```

### Show Tables

```sql
SHOW TABLES;
```

### Insert Row / Record

```sql
INSERT INTO users (first_name, last_name, email, password, location, dept, is_admin, register_date) values ('Brad', 'Traversy', 'brad@gmail.com', '123456','Massachusetts', 'development', 1, now());
```

### Insert Multiple Rows

```sql
INSERT INTO users (first_name, last_name, email, password, location, dept,  is_admin, register_date) values ('Fred', 'Smith', 'fred@gmail.com', '123456', 'New York', 'design', 0, now()), ('Sara', 'Watson', 'sara@gmail.com', '123456', 'New York', 'design', 0, now()),('Will', 'Jackson', 'will@yahoo.com', '123456', 'Rhode Island', 'development', 1, now()),('Paula', 'Johnson', 'paula@yahoo.com', '123456', 'Massachusetts', 'sales', 0, now()),('Tom', 'Spears', 'tom@yahoo.com', '123456', 'Massachusetts', 'sales', 0, now());
```

### Select

```sql
SELECT * FROM users;
SELECT first_name, last_name FROM users;
```

### Where Clause

```sql
SELECT * FROM users WHERE location='Massachusetts';
SELECT * FROM users WHERE location='Massachusetts' AND dept='sales';
SELECT * FROM users WHERE is_admin = 1;
SELECT * FROM users WHERE is_admin > 0;
```

### Delete Row

```sql
DELETE FROM users WHERE id = 6;
```

### Update Row

```sql
UPDATE users SET email = 'freddy@gmail.com' WHERE id = 2;

```

### Add New Column

```sql
ALTER TABLE users ADD age VARCHAR(3);
```

### Modify Column

```sql
ALTER TABLE users MODIFY COLUMN age INT(3);
```

### Order By (Sort)

```sql
SELECT * FROM users ORDER BY last_name ASC;
SELECT * FROM users ORDER BY last_name DESC;
```

### Concatenate Columns

```sql
SELECT CONCAT(first_name, ' ', last_name) AS 'Name', dept FROM users;

```

### Select Distinct Rows

```sql
SELECT DISTINCT location FROM users;

```

### Between (Select Range)

```sql
SELECT * FROM users WHERE age BETWEEN 20 AND 25;
```

### Like (Searching)

```sql
SELECT * FROM users WHERE dept LIKE 'd%';
SELECT * FROM users WHERE dept LIKE 'dev%';
SELECT * FROM users WHERE dept LIKE '%t';
SELECT * FROM users WHERE dept LIKE '%e%';
```

### Not Like

```sql
SELECT * FROM users WHERE dept NOT LIKE 'd%';
```

### IN

```sql
SELECT * FROM users WHERE dept IN ('design', 'sales');
```

## Some More examples that you can check out
[Download Link for Workbench](https://dev.mysql.com/doc/mysql-tutorial-excerpt/5.5/en/examples.html)


## Tutorial
```sql
** Create table and insert Values 

CREATE TABLE STUDENTS(
uga_id int,
first_name VARCHAR(100),
last_name VARCHAR(100),
age int,
email VARCHAR(50),
register_date DATE,
PRIMARY KEY(uga_id)
);

INSERT INTO STUDENTS (uga_id, first_name, last_name, age, email, register_date) values 
('8111169', 'Fred', 'Smith', '27', 'fred@gmail.com', '2018-01-07'), 
('8112129', 'Sara', 'Watson', '20', 'sara@gmail.com', '2019-01-07'),
('8113179', 'Will', 'Jackson', '22', 'will@yahoo.com', '2019-04-20'),
('8117559', 'Paula', 'Johnson', '19', 'paula@yahoo.com', '2018-01-07'),
('8119129', 'Tom', 'Spears', '23', 'tom@yahoo.com', '2017-05-07');

CREATE TABLE STUDENTADDRESS(
id INT AUTO_INCREMENT,
uga_id int,
address VARCHAR(100),
PRIMARY KEY(id),
FOREIGN KEY (uga_id) REFERENCES STUDENTS(uga_id)
);

INSERT INTO STUDENTADDRESS (uga_id, address) values 
('8111169', 'North Side View'), 
('8112129', 'Lakeside View Point'),
('8113179', 'River Drive'),
('8117559', '5-Point View'),
('8119129', 'Milege Avenue');

CREATE TABLE COURSES(
prefix VARCHAR(50),
code INT,
name VARCHAR(100),
PRIMARY KEY(prefix, code)
);

INSERT INTO COURSES (prefix, code, name) values 
('CSCI', '4760', 'Software Engineering'), 
('AGRI', '6750', 'Soil Science'),
('CSCI', '8770', 'Database Systems'),
('EDU', '7750', 'English Literature'),
('CHEM', '9110', 'BOOM BAAAM!');

** Foreign Key Error
INSERT INTO STUDENTADDRESS (uga_id, address) values ('8010169', 'North Side View');

Workbench Response: 
Error Code: 1452. Cannot add or update a child row: a foreign key constraint fails (`cinemaebooking`.`studentaddress`, CONSTRAINT `studentaddress_ibfk_1` FOREIGN KEY (`uga_id`) REFERENCES `student` (`uga_id`))


** SHOW TABLE Queries

SELECT * FROM STUDENTS;
SELECT * FROM STUDENTADDRESS;
SELECT * FROM COURSES;
SELECT * FROM STUDENTS ORDER BY last_name ASC;
SELECT * FROM STUDENTS WHERE age BETWEEN 20 AND 25;
SELECT * FROM STUDENTS WHERE email LIKE '%gmail.com%';

SELECT STUDENTS.uga_id, first_name, last_name, age, email, address FROM STUDENTS INNER JOIN STUDENTADDRESS
ON STUDENTS.uga_id = STUDENTADDRESS.uga_id;
  
```
