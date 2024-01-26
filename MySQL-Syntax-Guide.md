
#                   **Welcome**
##                MySQL Syntax Guide
####                 Created by Grrham
##### This cheat sheet presents basic MySQL commands with practical examples, covering fundamental operations such as database creation, table management, data manipulation, and more. It includes both simplified examples for learning purposes and real-world scenarios for practical application.

###    How to Log into mySQL from terminal

```bash
mysql -u your_username -p
```

###    How to SHOW USERS

```bash
SHOW USERS;
```

### How to CREATE USERS

```bash
CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';

```

### How to GRANT PRIVILEGES, Show granted privileges, and remove

```bash
-- Grant privileges
GRANT SELECT, INSERT ON database_name.* TO 'username'@'localhost';

-- Show granted privileges
SHOW GRANTS FOR 'username'@'localhost';

-- Remove privileges
REVOKE SELECT, INSERT ON database_name.* FROM 'username'@'localhost';
```

### How to SHOW, DELETE & CREATE DATABASES & SELECT DATABASES

```bash
-- Show databases
SHOW DATABASES;

-- Create database
CREATE DATABASE database_name;

-- Delete database
DROP DATABASE database_name;

-- Select database
USE database_name;
```

### How to CREATE a TABLE with Columns and their data types

```bash
CREATE TABLE table_name (
    column1_name datatype1,
    column2_name datatype2,
    ...
);
```

```bash
CREATE TABLE employee_info (
    employee_id INT PRIMARY KEY,
    employee_name VARCHAR(255),
    department_id INT
);
```

### How to SHOW, DELETE & DROP Tables

```bash
-- Show tables
SHOW TABLES;
```
```bash
-- Delete table
DELETE FROM employee_info WHERE employee_id = 101;
```
```bash
-- Drop table
DROP TABLE employee_info;
```

### How to Insert ROWS & RECORDS (single and multiple)
This is how you add information to a table.

```bash
-- Insert a single row into the 'employees' table
INSERT INTO employees (employee_id, employee_name, department_id) VALUES
(105, 'Eva Rodriguez', 2);
```
```bash
-- Insert multiple rows
INSERT INTO employees (employee_id, employee_name, department_id) VALUES
(106, 'Carlos Martinez', 3),
(107, 'Sophie Brown', 1);
```

### How to SELECT with the WHERE Clause
The `SELECT` statement is used to retrieve data from a table. The `WHERE` clause is used to filter the results based on a specified condition.

```bash
SELECT * FROM table_name WHERE condition;
```
```bash
-- Select employees from the 'HR' department
SELECT * FROM employees WHERE department_id = 1;
```

### How to SELECT with the WHERE Clause using a range
You can use the `BETWEEN` keyword to select rows within a specified range. 

```bash
SELECT * FROM table_name WHERE column BETWEEN value1 AND value2;
```
```bash
-- Select employees with an employee_id between 103 and 105
SELECT * FROM employees WHERE employee_id BETWEEN 103 AND 105;
```

### How to DELETE an individual ROW

```bash
DELETE FROM table_name WHERE condition;
```
```bash
-- Delete an employee from the 'employees' table
DELETE FROM employees WHERE employee_id = 107;
```

### How to UPDATE a ROW

```bash
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
```bash
-- Update the department_id for an employee in the 'employees' table
UPDATE employees SET department_id = 3 WHERE employee_id = 105;
```

### How to add a new column and modify it

```bash
Add a new column
ALTER TABLE table_name ADD COLUMN new_column datatype;

-- Add a new column 'position' to the 'employees' table
ALTER TABLE employees ADD COLUMN position VARCHAR(50);
```

```bash

Modify column
ALTER TABLE table_name MODIFY COLUMN column_name new_datatype;

-- Modify the 'position' column in the 'employees' table
UPDATE employees SET position = 'Manager' WHERE employee_id = 105
```

### How to Order by and use Distinct
The `ORDER` BY clause is used to sort the result set in ascending or descending order based on one or more columns. The `DISTINCT` keyword is used to eliminate duplicate rows from the result set.

```bash
Order by
SELECT * FROM table_name ORDER BY column_name DESC;

-- Order employees by their salary in descending order
SELECT * FROM employees ORDER BY salary DESC;
```

```bash
Distinct
SELECT DISTINCT column_name FROM table_name;

-- Select distinct department_ids from the 'employees' table
SELECT DISTINCT department_id FROM employees;
```

### How to Concatenate Columns
`CONCATENATE` is the process of combining two or more strings into a single string. It's often used to join the values of different columns or add a separator between them. It's a common operation when you want to display or manipulate data in a specific format.

```bash
SELECT CONCAT(column1, ' ', column2) AS concatenated_column FROM table_name;
```
```bash
-- Concatenate 'employee_name' and 'position' in the 'employees' table
SELECT CONCAT(employee_name, ' - ', position) AS employee_position FROM employees;
```

### How to Select Distinct Rows
`DISTINCT` is used to ensure that the result set only contains unique combinations of values in the specified columns, useful for obtaining a distinct set of data.

```bash
SELECT DISTINCT * FROM table_name WHERE condition;
```
```bash
-- Select distinct rows based on 'department_id' and 'salary' in the 'employees' table
SELECT DISTINCT department_id, salary FROM employees;
```

### How to use LIKE to Search
The `LIKE` operator is a comparison operator in MySQL that is used to match a specified pattern against values in a column.

```bash
SELECT * FROM table_name WHERE column_name LIKE 'pattern';

-- Search for employees whose names start with 'S'
SELECT * FROM employees WHERE employee_name LIKE 'S%';
```

### How Select using IN
The `IN` operator is a comparison operator in MySQL used to check if a value matches any value in a specified list.

```bash
SELECT * FROM table_name WHERE column_name IN (value1, value2, ...);
```
```bash
-- Select employees in the 'HR' and 'IT' departments
SELECT * FROM employees WHERE department_id IN (1, 3);
```

### How to Create & Remove Index
Creating an index in a database involves generating a data structure that enhances the speed of data retrieval operations on a specific column or set of columns in a table.

```bash
Create index
CREATE INDEX index_name ON table_name (column_name);

-- Create an index on the 'employee_name' column in the 'employees' table
CREATE INDEX idx_employee_name ON employees(employee_name);
```

```bash
Remove index
DROP INDEX index_name ON table_name;

-- Remove the index on the 'employee_name' column in the 'employees' table
DROP INDEX idx_employee_name ON employees;
```

### Create Two Tables demonstrating a one to many relationship that shows a Primary key & Foreign key

```bash
-- Creating the 'departments' table
CREATE TABLE departments (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(255)
);

-- Creating the 'employees' table with a foreign key referencing 'departments'
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    employee_name VARCHAR(255),
    department_id INT,
    FOREIGN KEY (department_id) REFERENCES departments(department_id)
);
```
In this example, the departments table has a primary key `department_id`, and the employees table has a foreign key `department_id` referencing the primary key of the departments table.
This is a one to many relationship beacuse one department can have many employyes but employyes ccant have many different departments.
```bash
-- Inserting data into the 'departments' table
INSERT INTO departments (department_id, department_name) VALUES
(1, 'HR'),
(2, 'Finance'),
(3, 'IT');

-- Inserting data into the 'employees' table
INSERT INTO employees (employee_id, employee_name, department_id) VALUES
(101, 'John Doe', 1),
(102, 'Jane Smith', 1),
(103, 'Bob Johnson', 2),
(104, 'Alice Williams', 3);
```

###  How to use Inner Join

Suppose we want to retrieve information about employees along with their department names using INNER JOIN:

```bash
SELECT employees.employee_id, employees.employee_name, departments.department_name
FROM employees
INNER JOIN departments ON employees.department_id = departments.department_id;
```
In this example, we are selecting the `employee_id`, `employee_name`, `salary`, and `department_name` from the employees and departments tables. The INNER JOIN connects the two tables based on the common `department_id`.

### How to JOIN Multiple Tables

Let's extend the previous example by adding a tasks table and retrieving information about employees, their department names, and the tasks assigned to them. 
```bash
-- Creating the 'tasks' table with a foreign key referencing 'employees'
CREATE TABLE tasks (
    task_id INT PRIMARY KEY,
    task_description VARCHAR(255),
    employee_id INT,
    FOREIGN KEY (employee_id) REFERENCES employees(employee_id)
);
```
```bash
-- Inserting data into the 'tasks' table
INSERT INTO tasks (task_id, task_description, employee_id) VALUES
(1, 'Complete HR Training', 101),
(2, 'Financial Report Submission', 103),
(3, 'Database Maintenance', 104);

-- Retrieve employee information with department names and tasks using INNER JOIN
SELECT employees.employee_id, employees.employee_name, departments.department_name, tasks.task_description
FROM employees
INNER JOIN departments ON employees.department_id = departments.department_id
INNER JOIN tasks ON employees.employee_id = tasks.employee_id;
```
In this example, we are selecting the `employee_id`, `employee_name`, `department_name`, and `task_description` from the employees, departments, and tasks tables. The INNER JOIN connects the tables based on their respective foreign and primary keys.
