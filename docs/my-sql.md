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

## Intro

This is a cheat sheet of MySQL for easier references.

## User

### Login

```
mysql -u root -p
```

### Show Users

```
SELECT User, Host FROM mysql.user;
```

### Create User

```
CREATE USER 'someuser'@'localhost' IDENTIFIED BY 'somepassword';
```

### Grant All Privileges On All Databases

```
GRANT ALL PRIVILEGES ON * . * TO 'someuser'@'localhost';
FLUSH PRIVILEGES;
```

### Show Grants

```
SHOW GRANTS FOR 'someuser'@'localhost';
```

### Remove Grants

```
REVOKE ALL PRIVILEGES, GRANT OPTION FROM 'someuser'@'localhost';
```

### Delete User

```
DROP USER 'someuser'@'localhost';
```

### Exit

```
exit;
```

## Database

### Data Types



**Integers**



```
INT
```

```
TINYINT
```

```
SMALLINT
```

```
MEDIUMINT
```

```
BIGINT
```

**Float**



```
FLOAT(M,D)
```

**Double**



```
DOUBLE(M,D)
```

**Decimal**



```
DECIMAL(M,D)
```

**Date**



```
DATE -- Format - (YYYY-MM-DD)
```

**Date Time**



```
DATETIME -- Format - (YYYY-MM-DD HH:MM:SS)
```

**Time**



```
TIME -- Format - (HH:MM:SS)
```

**String**



```
CHAR(M)
```

```
VARCHAR(M)
```

```
BLOB or TEXT
```

### Comments

```
/* Multi
line
comment */
```

```
# Single Line Comment
```

```
-- Single Line Comment
```

### Data Definition Language (DDL)

**Create Database**

```
create database cheatsheet;
```

**Use Database**

```
use cheatsheet;
```

**Show Databases**

```
show databases;
```

**Create Table**

```
create table employee
(
    employee_id int primary key,              -- Setting primary key(1st method)
    first_name varchar(50),
    last_name varchar(50),
    dept_number int,
    age int,
    salary real
);

create table department
(
    dept_number int,
    dept_name varchar(50),
    dept_location varchar(50),
    emp_id int,
    primary key(dept_number)                -- Setting primary key(2nd method)
);
```

**Show Tables**

```
show tables;
```

**Describe Table**

```
describe employee;
desc employee;
show columns in employee;
```

**Rename Table**

```
rename table employee to employee_table;
alter table employee_table rename to employee;
```

**Renaming Column**

```
alter table employee change column employee_id emp_id int;
```

**Add Constraint to Column**

```
alter table employee change column first_name first_name varchar(50) not null;
```

**Add Column**

```
alter table employee add column salary real;
```

**Drop Column**

```
alter table employee drop column salary;
```

**Modify the Datatype of column**

```
alter table employee modify column salary int;
```

**Truncate Table**

```
truncate employee;
```

**Drop Table**

```
drop table department;
```

**Drop Database**

```
drop database cheatsheet;
```

### Data Manipulation Language (DML)

**Insertion (Complete)**

```
insert into employee (employee_id, first_name, last_name, dept_number, age, salary) values (1, "Anurag", "Peddi", 1, 20, 93425.63);

insert into employee values (2, "Anuhya", "Peddi", 2, 20, 83425.63);
```

**Insertion (Partial)**

```
insert into employee (employee_id, first_name) values (3, "Vageesh");
```

**Updating all rows**

```
update employee set salary = 1.1 * salary;
```

**Updating a specified row**

```
update employee set salary = 1.2 * salary where employee_id = 1;
```

**Delete a specified row**

```
delete from employee where employee_id = 2;
```

**Delete all rows**

```
delete from employee;
```

**Enabling foreign key checks**

```
set foreign_key_checks = 1;
```

**Disabling foreign key checks**

```
set foreign_key_checks = 0;
```

### Data Query Language (DQL)

**Display Table**

```
select * from employee;
```

**Select only specified columns**

```
select employee_id, first_name from employee;
```

**Select only few rows**

```
select employee_id, first_name from employee where age > 25;
```

#### Where Clause

**Greater than(>)**

```
select * from employee where salary > 3100;
```

**Greater than equal to(>=)**

```
select * from employee where salary >= 3100;
```

**Less than(<)**

```
select * from employee where salary < 4500;
```

**Less than equal to(<=)**

```
select * from employee where salary <= 4350;
```

**Range**

```
select * from employee where salary > 3000 and salary < 4000;
```

**BETWEEN and AND**

```
select * from employee where salary between 3000 and 4000;
```

#### OR

```
select * from employee where salary = 3000 or salary = 4000;
```

**Null**

```
select * from employee where salary is NULL;
```

**Not null**

```
select * from employee where salary is NOT NULL;
```

#### ORDER BY Clause

```
select * from employee ORDER BY salary DESC;
```

**Like Operator**

```
select * from employee where name like '%Jo%';          -- Similar to *Jo* in regrex
```

```
select * from employee where name like 'Jo_';           -- Similar to Jo. in regrex
```

### Views

**Create a view**

```
create view personal_info as select first_name, last_name, age from employees;
```

**Displaying view**

```
select * from personal_info;
```

**Updating in view**

```
update personal_info set salary = 1.1 * salary;
```

**Deleting record from view**

```
delete from personal_info where age < 40;
```

**Droping a view**

```
drop view personal_info;
```

### Joins

**Inner join**

```
select e.fname, p.pname from employees as e inner join project as p on e.eid = p.eid;

-- or

select e.fname, p.pname from employees as e join project as p on e.eid = p.eid;
```

**Full outer join**

```
select e.fname, p.pname from employees as e left outer join project as p on e.eid = p.eid
union
select e.fname, p.pname from employees as e right outer join project as p on e.eid = p.eid;
```

**Left outer join**

```
select e.fname, p.pname from employees as e left outer join project as p on e.eid = p.eid;
```

**Right outer join**

```
select e.fname, p.pname from employees as e right outer join project as p on e.eid = p.eid;
```

**Left outer join - inner join**

```
select e.fname, p.pname from employees as e left outer join project as p on e.eid = p.eid where p.pname is null;
```

**Right outer join - inner join**

```
select e.fname, p.pname from employees as e right outer join project as p on e.eid = p.eid where e.fname is null;
```

### Aggregation

**Sum function**

```
select sum(population) from city group by population;
```

**Average function**

```
select avg(population) from city group by population;
```

**Count function**

```
select district, count(district) from city group by district;
```

**Maximum function**

```
select max(population) from city group by population;
```

**Minimum function**

```
select min(population) from city group by population;
```

**Standard deviation function**

```
select stddev(population) from city group by population;
```

**Group concat function**

```
select group_concat(population) from city group by population;
```

> Only COUNT function considers NULL values

### Procedure

**Creating procedure**

```
create procedure display_dbs()
show databases;
```

**Calling procedure**

```
call display_dbs();
```

**Drop procedure**

```
drop procedure display_dbs;
```

### Transaction

**Begin transaction**

```
start transaction;
```

**Create savepoint**

```
savepoint sv_pt;
```

```
delete from city;       -- changing data in table
```

**Rollback**

```
rollback to sv_pt;
```

**Releasing savepoint**

```
release savepoint sv_pt;
```

**Commiting changes**

```
commit;
```

### Constraints

**Not Null**

```
alter table Employee
change
    Age
    Age int NOT NULL;
```

**Unique**

```
alter table Employee
add constraint u_q unique(ID);
```

```
alter table Employee -- drop the constraint
drop constraint u_q;
```

**Primary Key**

```
alter table Employee
add constraint p_k primary key(ID);
```

```
alter table Employee -- drop the constraint
drop constraint p_k;
```

**Check**

```
alter table Employee
add constraint Age check (age>=30);
```

```
alter table Employee -- drop the constraint
drop check Age;
```

**Default**

```
alter table Employee
alter Age set default 10;
```

```
alter table Employee -- drop the constraint
alter Age drop default;
```

### Cloning

**Duplicate a Table Schema**

```
create table emp_dup like employee;
```

**Duplicate a Table**

```
create table emp_dup select * from employee;
```

### Access Controls

**Creating New User**

```
CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';
```

the hostname part is set to `localhost`, so the user will be able to connect to the MySQL server only from the localhost.\
To grant access from another host, change the hostname part with the remote machine IP.

```
CREATE USER 'username'@'172.8.10.5' IDENTIFIED BY 'user_password';
```

To create a user that can connect from any host, '%' is used in the hostname part:

```
CREATE USER 'username'@'%' IDENTIFIED BY 'user_password';
```

**Grant All Permissions**

```
GRANT ALL PRIVILEGES ON * . * TO 'username'@'localhost';
```

Asterisks(\*) refers to the database and table names respectively.\
By using asterisks we can give access of all the databases **or** tables to the user.

**Flush Privileges**

```
FLUSH PRIVILEGES
```

All the changes won't be in effect unless this query is fired.

**Specific User Permissions**

```
GRANT type_of_permission ON database_name.table_name TO 'username'@'localhost';
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

**Revoking permissions**

```
REVOKE type_of_permission ON database_name.table_name FROM 'username'@'localhost';
```

**Show User's Current Permissions**

```
SHOW GRANTS FOR 'username'@'localhost';
```

**Delete a User**

```
DROP USER 'username'@'localhost';
```

**Set new password to a user**

```
use mysql;
update user set authentication_string=PASSWORD("<new2-password>") where User='<user>';
flush privileges;
```

### Reset Root Password

Stop MySQL service

```
sudo systemctl stop mysql
```

Restart MySQL service without loading grant tables

```
sudo mysqld_safe --skip-grant-tables &
```

The apersand (&) will cause the program to run in the background and `--skip-grant-tables` enables everyone to to connect to the database server without a password and with all privileges granted. Login to shell

```
mysql -u root
```

Set new password for root

```
ALTER USER 'root'@'localhost' IDENTIFIED BY 'MY_NEW_PASSWORD';
FLUSH PRIVILEGES;
```

Stop and start the server once again

```
mysqladmin -u root -p shutdown
sudo systemctl start mysql
```

### Programming

**Declare variables**

```
set @num = 10;
set @name = 'Anurag';
```

**Print them**

```
select @name;
```

**For loop**

```
set @n = 21;
select repeat("* ", @n := @n - 1) from information_schema.tables where @n > 0;
```

### Miscellaneous

**Round**

```
select round(3.141596, 3);
```

**Repeated concatenation**

```
select repeat("* ", 20);
```

**Random float**

```
select rand();
```

**Typecast to Int**

```
select cast(23.01245 as signed);
```

**Concatenation**

```
select concat("Mahesh", " ", "Chandra", " ", "Duddu", "!");
```

**Extract Month**

```
select month("1998-12-30");
```

**Extract Year**

```
select year("1998-12-30");
```

## Also thanks to

* [https://github.com/GunaPalanivel/The-MySQL-Code-Sheet](https://github.com/GunaPalanivel/The-MySQL-Code-Sheet)&#x20;
* [https://github.com/AbdGhazall/MySQL-Cheat-Sheet](https://github.com/AbdGhazall/MySQL-Cheat-Sheet)&#x20;
* [https://github.com/Cheatsheet-lang/MySQL-cheatsheet](https://github.com/Cheatsheet-lang/MySQL-cheatsheet)&#x20;
* [https://gist.github.com/bradtraversy/c831baaad44343cc945e76c2e30927b3](https://gist.github.com/bradtraversy/c831baaad44343cc945e76c2e30927b3)
