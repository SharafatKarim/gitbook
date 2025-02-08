---
icon: server
cover: >-
  https://images.unsplash.com/photo-1662026911591-335639b11db6?crop=entropy&cs=srgb&fm=jpg&ixid=M3wxOTcwMjR8MHwxfHNlYXJjaHwyfHxteXNxbHxlbnwwfHx8fDE3MzgzODg1NDl8MA&ixlib=rb-4.0.3&q=85
coverY: 53
layout:
  cover:
    visible: true
    size: full
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# My SQL

## My SQL

This is a cheat sheet of MySQL for easier references. MySQL is an open-source relational database management system. It is a central component of the LAMP open-source web application software stack. MySQL is used by many database-driven web applications, including Drupal, Joomla, phpBB, and WordPress.

### Installation

To get started with MySQL, you can download it from [here](https://dev.mysql.com/downloads/mysql/) or, simply use [xampp](https://www.apachefriends.org/download.html), which uses `maria-db`, a drop in replacement of MySQL. To run MySQL, in linux environment or, docker/ podman container, I've a guide for you!

* [Database setup with podman/ Docker containers](https://sharafat.pages.dev/database-containers/)

### User

#### Login

```bash
mysql -u root -p
```

#### Show Users

```sql
SELECT 
    User, 
    Host 
FROM 
    MYSQL.USER;
```

#### Create User

```sql
CREATE USER 'someuser'@'localhost' 
IDENTIFIED BY 'somepassword';
```

#### Grant All Privileges On All Databases

```sql
GRANT ALL PRIVILEGES ON * . * 
TO 'someuser'@'localhost';
FLUSH PRIVILEGES;
```

#### Show Grants

```sql
SHOW GRANTS FOR 'someuser'@'localhost';
```

#### Remove Grants

```sql
REVOKE ALL PRIVILEGES, GRANT OPTION 
FROM 'someuser'@'localhost';
```

#### Delete User

```sql
DROP USER 'someuser'@'localhost';
```

#### Exit

```sql
EXIT;
```

## Database

### General Commands

To run SQL files

```sql
SOURCE <filename>.sql;
```

### Data Types

#### Integers

```sql
INT
```

```sql
TINYINT
```

```sql
SMALLINT
```

```sql
MEDIUMINT
```

```sql
BIGINT
```

#### Float

```sql
FLOAT(M,D)
```

#### Double

```sql
DOUBLE(M,D)
```

#### Decimal

```sql
DECIMAL(M,D)
```

#### Date

```sql
DATE -- Format - (YYYY-MM-DD)
```

#### Date Time

```sql
DATETIME -- Format - (YYYY-MM-DD HH:MM:SS)
```

#### Time

```sql
TIME -- Format - (HH:MM:SS)
```

#### String

```sql
CHAR(M)
```

```sql
VARCHAR(M)
```

```sql
BLOB or TEXT
```

### Comments

```sql
/* Multi
line
comment */
```

```sql
# Single Line Comment
```

```sql
-- Single Line Comment
```

## Data Definition Language (DDL)

### Create Database

```sql
CREATE DATABASE cheatsheet;
```

### Show Databases

```sql
SHOW DATABASES;
```

### Use Database

```sql
USE cheatsheet;
```

### Create Table

```sql
CREATE TABLE employee (
    employee_id INT PRIMARY KEY,              -- Setting primary key(1st method)
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    dept_number INT,
    age INT,
    salary REAL
);

CREATE TABLE department (
    dept_number INT,
    dept_name VARCHAR(50),
    dept_location VARCHAR(50),
    emp_id INT,
    PRIMARY KEY(dept_number)                -- Setting primary key(2nd method)
);
```

### Show Tables

```sql
SHOW TABLES;
```

### Describe Table

```sql
DESCRIBE employee;
DESC employee;
SHOW COLUMNS IN employee;
```

### Rename Table

```sql
RENAME TABLE employee TO employee_table;
ALTER TABLE employee_table RENAME TO employee;
```

### Renaming Column

```sql
ALTER TABLE employee 
CHANGE COLUMN employee_id emp_id INT;
```

### Add Constraint to Column

```sql
ALTER TABLE employee 
CHANGE COLUMN first_name first_name VARCHAR(50) NOT NULL;
```

### Add Column

```sql
ALTER TABLE employee 
ADD COLUMN salary REAL;
```

### Drop Column

```sql
ALTER TABLE employee 
DROP COLUMN salary;
```

### Modify the Datatype of column

```sql
ALTER TABLE employee 
MODIFY COLUMN salary INT;
```

### Truncate Table

```sql
TRUNCATE employee;
```

> Trancute means to delete all the rows from the table but the table structure remains the same.

### Drop Table

```sql
DROP TABLE department;
```

### Drop Database

```sql
DROP DATABASE cheatsheet;
```

## Data Manipulation Language (DML)

### Insertion (Complete)

```sql
INSERT INTO employee (
    employee_id, 
    first_name, 
    last_name, 
    dept_number, 
    age, 
    salary
) VALUES (
    1, 
    "Anurag", 
    "Peddi", 
    1, 
    20, 
    93425.63
);

INSERT INTO employee VALUES (
    2, 
    "Anuhya", 
    "Peddi", 
    2, 
    20, 
    83425.63
);
```

### Insertion (Partial)

```sql
INSERT INTO employee (
    employee_id, 
    first_name
) VALUES (
    3, 
    "Vageesh"
);
```

### Updating all rows

```sql
UPDATE employee 
SET salary = 1.1 * salary;
```

### Updating a specified row

```sql
UPDATE employee 
SET salary = 1.2 * salary 
WHERE employee_id = 1;
```

### Delete a specified row

```sql
DELETE FROM employee 
WHERE employee_id = 2;
```

### Delete all rows

```sql
DELETE FROM employee;
```

## Data Query Language (DQL)

### Display Table

```sql
SELECT * 
FROM employee;
```

### Select only specified columns

```sql
SELECT 
    employee_id, 
    first_name 
FROM 
    employee;
```

### Select only few rows

```sql
SELECT 
    employee_id, 
    first_name 
FROM 
    employee 
WHERE 
    age > 25;
```

### Select with condition

```sql
select ID, 
    case
	when name=score < 40 then "F"
        when name=score < 60 then "C"
        when name=score < 80 then "B"
        else "A"
    end
from marks;
```

### Where Clause

#### Greater than(>)

```sql
SELECT * 
FROM employee 
WHERE salary > 3100;
```

#### Greater than equal to(>=)

```sql
SELECT * 
FROM employee 
WHERE salary >= 3100;
```

#### Less than(<)

```sql
SELECT * 
FROM employee 
WHERE salary < 4500;
```

#### Less than equal to(<=)

```sql
SELECT * 
FROM employee 
WHERE salary <= 4350;
```

#### Range

```sql
SELECT * 
FROM employee 
WHERE salary > 3000 
AND salary < 4000;
```

#### BETWEEN and AND

```sql
SELECT * 
FROM employee 
WHERE salary BETWEEN 3000 AND 4000;
```

#### OR

```sql
SELECT * 
FROM employee 
WHERE salary = 3000 
OR salary = 4000;
```

#### Null

```sql
SELECT * 
FROM employee 
WHERE salary IS NULL;
```

#### Not null

```sql
SELECT * 
FROM employee 
WHERE salary IS NOT NULL;
```

#### ORDER BY Clause

```sql
SELECT * 
FROM employee 
ORDER BY salary DESC;
```

**Like Operator**

```sql
SELECT * 
FROM employee 
WHERE name LIKE '%Jo%';          -- Similar to *Jo* in regrex
```

```sql
SELECT * 
FROM employee 
WHERE name LIKE 'Jo_';           -- Similar to Jo. in regrex
```

## Views

### Create a view

```sql
CREATE VIEW personal_info AS 
SELECT 
    first_name, 
    last_name, 
    age 
FROM 
    employees;
```

### Displaying view

```sql
SELECT * 
FROM personal_info;
```

### Updating in view

```sql
UPDATE personal_info 
SET salary = 1.1 * salary;
```

### Deleting record from view

```sql
DELETE FROM personal_info 
WHERE age < 40;
```

### Droping a view

```sql
DROP VIEW personal_info;
```

## Joins

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

Here are the different types of the JOINs in SQL:

* `(INNER) JOIN`: Returns records that have matching values in both tables
* `LEFT (OUTER) JOIN`: Returns all records from the left table, and the matched records from the right table
* `RIGHT (OUTER) JOIN`: Returns all records from the right table, and the matched records from the left table
* `FULL (OUTER) JOIN`: Returns all records when there is a match in either left or right table

### Inner join

```sql
SELECT 
    e.fname, 
    p.pname 
FROM 
    employees AS e 
INNER JOIN project AS p 
ON e.eid = p.eid;

-- or

SELECT 
    e.fname, 
    p.pname 
FROM 
    employees AS e 
JOIN project AS p 
ON e.eid = p.eid;
```

### Full outer join

```sql
SELECT 
    e.fname, 
    p.pname 
FROM 
    employees AS e 
LEFT OUTER JOIN project AS p 
ON e.eid = p.eid
UNION
SELECT 
    e.fname, 
    p.pname 
FROM 
    employees AS e 
RIGHT OUTER JOIN project AS p 
ON e.eid = p.eid;
```

### Left outer join

```sql
SELECT 
    e.fname, 
    p.pname 
FROM 
    employees AS e 
LEFT OUTER JOIN project AS p 
ON e.eid = p.eid;
```

### Right outer join

```sql
SELECT 
    e.fname, 
    p.pname 
FROM 
    employees AS e 
RIGHT OUTER JOIN project AS p 
ON e.eid = p.eid;
```

### Left outer join - inner join

```sql
SELECT 
    e.fname, 
    p.pname 
FROM 
    employees AS e 
LEFT OUTER JOIN project AS p 
ON e.eid = p.eid 
WHERE p.pname IS NULL;
```

### Right outer join - inner join

```sql
SELECT 
    e.fname, 
    p.pname 
FROM 
    employees AS e 
RIGHT OUTER JOIN project AS p 
ON e.eid = p.eid 
WHERE e.fname IS NULL;
```

## Aggregation

### Sum function

```sql
SELECT 
    SUM(population) 
FROM 
    city 
GROUP BY population;
```

### Average function

```sql
SELECT 
    AVG(population) 
FROM 
    city 
GROUP BY population;
```

### Count function

```sql
SELECT 
    district, 
    COUNT(district) 
FROM 
    city 
GROUP BY district;
```

### Maximum function

```sql
SELECT 
    MAX(population) 
FROM 
    city 
GROUP BY population;
```

### Minimum function

```sql
SELECT 
    MIN(population) 
FROM 
    city 
GROUP BY population;
```

### Standard deviation function

```sql
SELECT 
    STDDEV(population) 
FROM 
    city 
GROUP BY population;
```

### Group concat function

```sql
SELECT 
    GROUP_CONCAT(population) 
FROM 
    city 
GROUP BY population;
```

> Only COUNT function considers NULL values

## Procedure

### Creating procedure

```sql
CREATE PROCEDURE display_dbs()
SHOW DATABASES;
```

### Calling procedure

```sql
CALL display_dbs();
```

#### Drop procedure

```sql
DROP PROCEDURE display_dbs;
```

## Transaction

### Begin transaction

```sql
START TRANSACTION;
```

### Create savepoint

```sql
SAVEPOINT sv_pt;
```

```sql
DELETE FROM city;       -- changing data in table
```

### Rollback

```sql
ROLLBACK TO sv_pt;
```

### Releasing savepoint

```sql
RELEASE SAVEPOINT sv_pt;
```

### Commiting changes

```sql
COMMIT;
```

## Constraints

### Not Null

```sql
ALTER TABLE Employee
CHANGE
    Age
    Age INT NOT NULL;
```

### Unique

```sql
ALTER TABLE Employee
ADD CONSTRAINT u_q UNIQUE(ID);
```

```sql
ALTER TABLE Employee -- drop the constraint
DROP CONSTRAINT u_q;
```

### Primary Key

```sql
ALTER TABLE Employee
ADD CONSTRAINT p_k PRIMARY KEY(ID);
```

```sql
ALTER TABLE Employee -- drop the constraint
DROP CONSTRAINT p_k;
```

### Check

```sql
ALTER TABLE Employee
ADD CONSTRAINT Age CHECK (age>=30);
```

```sql
ALTER TABLE Employee -- drop the constraint
DROP CHECK Age;
```

### Default

```sql
ALTER TABLE Employee
ALTER Age SET DEFAULT 10;
```

```sql
ALTER TABLE Employee -- drop the constraint
ALTER Age DROP DEFAULT;
```

### Cloning

### Duplicate a Table Schema

```sql
CREATE TABLE emp_dup LIKE employee;
```

### Duplicate a Table

```sql
CREATE TABLE emp_dup SELECT * FROM employee;
```

## Access Controls

### Creating New User

```sql
CREATE USER 'username'@'localhost' 
IDENTIFIED BY 'password';
```

the hostname part is set to `localhost`, so the user will be able to connect to the MySQL server only from the localhost.\
To grant access from another host, change the hostname part with the remote machine IP.

```sql
CREATE USER 'username'@'172.8.10.5' 
IDENTIFIED BY 'user_password';
```

To create a user that can connect from any host, '%' is used in the hostname part:

```sql
CREATE USER 'username'@'%' 
IDENTIFIED BY 'user_password';
```

### Grant All Permissions

```sql
GRANT ALL PRIVILEGES ON * . * 
TO 'username'@'localhost';
```

Asterisks(\*) refers to the database and table names respectively.\
By using asterisks we can give access of all the databases **or** tables to the user.

### Flush Privileges

```sql
FLUSH PRIVILEGES
```

All the changes won't be in effect unless this query is fired.

### Specific User Permissions

```sql
GRANT type_of_permission 
ON database_name.table_name 
TO 'username'@'localhost';
```

`type_of_permission` may have one of these value:

* **ALL PRIVILEGES** - Allows user full access to a designated database (or if no database is selected, global access across the system).
* **CREATE** - allows them to create new tables or databases.
* **DROP** - allows them to them to delete tables or databases.
* **DELETE** - allows them to delete rows from tables.
* **INSERT** - allows them to insert rows into tables.
* **SELECT** - allows them to use the `SELECT` command to read through databases.
* **UPDATE** - allow them to update table rows.
* **GRANT OPTION** - allows them to grant or remove other users’ privileges.\
  Multiple permissions are given with commas.

### Revoking permissions

```sql
REVOKE type_of_permission 
ON database_name.table_name 
FROM 'username'@'localhost';
```

### Show User's Current Permissions

```sql
SHOW GRANTS FOR 'username'@'localhost';
```

### Delete a User

```sql
DROP USER 'username'@'localhost';
```

### Set new password to a user

```sql
USE mysql;
UPDATE user 
SET authentication_string=PASSWORD("<new2-password>") 
WHERE User='<user>';
FLUSH PRIVILEGES;
```

### Reset Root Password

Stop MySQL service

```
sudo systemctl stop mysql
```

Restart MySQL service without loading grant tables

```bash
sudo mysqld_safe --skip-grant-tables &
```

The apersand (&) will cause the program to run in the background and `--skip-grant-tables` enables everyone to to connect to the database server without a password and with all privileges granted. Login to shell

```
mysql -u root
```

Set new password for root

```sql
ALTER USER 'root'@'localhost' 
IDENTIFIED BY 'MY_NEW_PASSWORD';
FLUSH PRIVILEGES;
```

Stop and start the server once again

```
mysqladmin -u root -p shutdown
sudo systemctl start mysql
```

## Programming

### Declare variables

```sql
SET @num = 10;
SET @name = 'Anurag';
```

### Print them

```sql
SELECT @name;
```

### For loop

```sql
SET @n = 21;
SELECT REPEAT("* ", @n := @n - 1) 
FROM information_schema.tables 
WHERE @n > 0;
```

## Miscellaneous

### Enabling foreign key checks

```sql
SET foreign_key_checks = 1;
```

### Disabling foreign key checks

```sql
SET foreign_key_checks = 0;
```

### Round

```sql
SELECT ROUND(3.141596, 3);
```

### Repeated concatenation

```sql
SELECT REPEAT("* ", 20);
```

### Random float

```sql
SELECT RAND();
```

### Typecast to Int

```sql
SELECT CAST(23.01245 AS SIGNED);
```

### Concatenation

```sql
SELECT CONCAT("Mahesh", " ", "Chandra", " ", "Duddu", "!");
```

### Extract Month

```sql
SELECT MONTH("1998-12-30");
```

### Extract Year

```sql
SELECT YEAR("1998-12-30");
```

## Also thanks to

* [https://github.com/Cheatsheet-lang/MySQL-cheatsheet](https://github.com/Cheatsheet-lang/MySQL-cheatsheet)
* [https://github.com/GunaPalanivel/The-MySQL-Code-Sheet](https://github.com/GunaPalanivel/The-MySQL-Code-Sheet)
* [https://github.com/AbdGhazall/MySQL-Cheat-Sheet](https://github.com/AbdGhazall/MySQL-Cheat-Sheet)
* [https://gist.github.com/bradtraversy/c831baaad44343cc945e76c2e30927b3](https://gist.github.com/bradtraversy/c831baaad44343cc945e76c2e30927b3)
