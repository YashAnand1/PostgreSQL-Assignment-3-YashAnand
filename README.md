<div align="center">


<!-- add technical charcha logo postgres session 3 -->
# PostgresSQL Session-3        
### — Tasks Documentation —    

_____________________________________________________________________________________                        

## Contents
</div>

- [Overview](#overview)
  - [Prerequisites](#prerequisites)
  - [Task 1: Creation Of Database](#task-1-creation-of-database)
  - [Task 2: Schema Design](#task-2-schema-design)
    - [2. Creating Schemas](#2-creating-schemas)
    - [2.1. Defining HR Schema](#21-defining-hr-schema)
    - [2.2. Defining Technical Schema](#22-defining-technical-schema)
    - [2.3. Defining Management Schema](#23-defining-management-schema)
  - [Task 3: Relationships](#task-3-relationships)(#managementdepartments--hremployees)
  - [Task 4: Queries \& Reporting](#task-4-queries--reporting)
  - [CONCLUSION](#conclusion)
 
_____________________________________________________________________________________      
<div align="center">
   
# Overview 
</div>

As a part of the third Technical Charcha session on PostgreSQL, the attendees were given an assignment comprising of 4 tasks to help gauge their understanding of PostgreSQL. This document serves as a documentation of these 4 tasks which involve the following:
- The creation of database, schemas, tables
- The querying of the created data

These completed tasks have been compiled into this single document with practical demonstrations. Through this document, one can aim to better understand how to <u>form relationships between data</u>, as it can be understood as the main theme of the assignment itself. 

For the completition of the majority of the assigned tasks, I referenced [this PostgreSQL tutorial](https://www.w3schools.com/postgresql/postgresql_intro.php) by W3School along with Prescott Computer Guy's YouTube tutorial on the same, which has been provided below:

<div align="center">     

[![IMAGE_ALT](https://img.youtube.com/vi/NvrpuBAMddw/maxresdefault.jpg)](https://www.youtube.com/watch?v=NvrpuBAMddw)
   </div>

<!-- Adding youtube videos
0 or 1 or 2 or 3 or 4, 0 (big) to 4 (small)
hqdefault.jpg <- high quality
mqdefault.jpg <- medium quality
sddefault.jpg <- standard definition
maxresdefault.jpg <- maximum resolution -->

_____________________________________________________________________________________     

<div align="center">
   
## Prerequisites
</div>



Before getting started with the assigned tasks, it was important to have PostgreSQL installed on my computer. In order to install this [Relational Database Management System](https://cloud.google.com/learn/what-is-a-relational-database) and its additional utilities, I had to run the following command:
```
sudo apt-get install postgresql postgresql-contrib
```

<div align="center">     

![image](https://ashnik-images.s3.amazonaws.com/prod/wp-content/uploads/2021/02/20050444/Postgresql-w-400x106.png)
   </div>

Next, I ensured that the status of the installed postgreSQL service was active. This was checked by runnning the following command:
```
service postgresql status
```
I was ready to get started with the assigned tasks as all of the conditions for the prerequisites had been met, when the output of the above command displayed PostgreSQL as an `active` service:
<div align="center">

![image](https://i.imgur.com/6cPtjnt.gif)
</div>

In the coming sections, the following assigned tasks will be performed and demonstrated:
- Task 1: Creation of Database
- Task 2: Schema Design
- Task 3: Relationships
- Task 4: Queries & Reporting

--------
<div align="center">

## Task 1: Creation Of Database
</div>

> Create a new PostgreSQL database named "keenable"         


Once ensuring that the PostgreSQL service was active on the system, I proceeded with the first task for creating a database called 'keenable'. However, I had to follow some specific steps before so that I could be able to create the specified database.

First, I assumed the identity of the `Postgres` user for performing the administrative tasks related to PostgreSQL that are permitted to the default Postgres user. Such tasks include managing PostgreSQL, starting the PSQL terminal and writing SQL queries, to name a few. Switching to this user was done using the following command:
```
sudo su postgres
```

Here, sudo su is a command that is used for switching user or `su` using the privileges of a superuser `sudo`. As explained earlier, `postgres` is the user we switch to. The output of running the above command was as follows:
<div align="center">

![image](https://i.imgur.com/3zqrnw3.png)
</div>

After switching the default Postgres user, I was able to gain the privilege of running PSQL terminal, where SQL queries can written for interacting with the database and make changes using keywords. The command for enabling this terminal is:
```
psql
```
The output of running this command displays the PSQL version and starts the PSQL terminal for allowing interaction with database using SQL queries:
 <div align="center">

![image](https://i.imgur.com/nknUGvT.png)
</div>

Once I had entered the PSQL terminal, it was possible to write SQL queries for performing the first task of creating a database. In order to create a database called 'keenable', I ran wrote the following query in the PSQL terminal:
```
CREATE DATABASE keenable;
```
Here the 'CREATE DATABASE' keywords of this query are self-explanatory as they are being used for creating a database. The third component of the query, `keenable`, is the name of the database that I was to create and most importantly, the `;` or semi-colon was used to tell SQL that I had completed the query. The output of running this entire query was:
<div align="center">

![image](https://i.imgur.com/uTaPAp2.png)
</div>

In order to ensure that the database had truly been created, I ran the following command as the final step in for the completion of this first task:
```
\l
```
This command is run for listing all the existing databases in Postgres and I was able to utilise it to list the newly created `keenable` database. The output of this command was as follows:
<div align="center">

![image](https://i.imgur.com/gWlwVnB.png)
</div>

With the `keenable` database created, this first task came to an end as it had been completed. In the following tasks, this newly created database was used for storing and creating schemas, tables and relationships. 

--------

<div align="center">
   
## Task 2: Schema Design
</div>

In databases, schemas can be understood as namespaces or groups, inside which tables are created for storing data. By default, Public is the schema created for a table that was created without a schema defined.

Provided below in this section is the demonstration of how I completed this second task by creating schemas, adding tables to them and forming relations between the tables. Though it had not been asked in the task itself, I also inserted values to the created tables in order to be able to make a better sense of the relations created. 

### 2. Creating Schemas   

>**Define three schemas within the database: "hr", "technical", and "management."**   

Before getting started with creating the schemas, I had to enter the newly created `keenable` database as it had specifically been stated in the task that the schemas were to be created in this database only. In order to enter the datbase, I ran the following command from the PSQL terminal:
```
\c keenable
``` 
Using this command, I was able to get connected with the newly created `keenable` database and this was proved by the following output of this command:
 <div align="center">

![image](https://i.imgur.com/2NcDhY8.png)
</div>

After connecting with the `keenable` database, I could start working on creating  schemas for the database, which are created using the following query:
```
CREATE SCHEMA <Schema_Name>;
```

In the query above, `CREATE SCHEMA` is used to instruct PostgreSQL to create a schema called with a specific name assigned by the user. The expected output is supposed to be `CREATE SCHEMA`, which would mean that the schema was created successfully. 

Using the `CREATE SCHEMA <Schema_Name>;` query, I was able to create the following schemas
- **HR Schema**   
  This schema was created using the `CREATE SCHEMA hr;`
<div align="center">

![image](https://i.imgur.com/41zCV5i.png)
</div>

- **Technical Schema**   
  This schema was created using the `CREATE SCHEMA technical;`
<div align="center">

![image](https://i.imgur.com/wRShvVb.png)
</div>

- **Management Schema**   
  This schema was created using the `CREATE SCHEMA management;`
<div align="center">

![image](https://i.imgur.com/ir77Ymg.png)
</div>

Since just knowing that these schemas had been created was not enough, I needed to ensure that they had truly been created. To do this, I utilised the following command for listing all the schemas inside the current database of `keenable`.
```
\dn+
```
The meaning of `dn` in this context is "Directory Name", which helps us view all the schemas in the present database. The `+` on the other hand is used to display a more detailed output. After running this command, the displayed output for me was as follows: 
<div align="center">

![image](https://i.imgur.com/qja7XOZ.png)
</div>

With all of the three schemas created successfully, the next goal was to define these created schemas. This was to be done by creating tables with relationships between eachother. As stated earlier, another goal for me in this task was to also insert some sample values into these tables as without them, it would have been difficult to understand the importance of these related tables.

### 2.1. Defining HR Schema 
>
>**Create the following tables in the "hr" schema:**  
2.1.1. "employees" to store employee information (employee_id, first_name, last_name, email, hire_date).   
2.1.2. "vacation_requests" to track employee vacation requests (request_id,
employee_id, start_date, end_date, status). 

Under this sub-task, the ask was to create 2 tables, namely `employees` and `vacation_requests` with the purpose of storing employee information and tracking their vacation requests, respectively. It should be noted that these tables were to be kept under the `HR Schema`. 

Therefore, the SQL queries provided below were written inside the `keenable` database using the PSQL terminal for the creation of the following tables:    

**2.1.1. `employees` Table**
  ```
  CREATE TABLE hr.employees (
    employee_id SERIAL PRIMARY KEY,
    first_name VARCHAR,
    last_name VARCHAR,
    email VARCHAR,
    hire_date DATE
    );
  ```
  **Output:** 
  <div align="center">

![image](https://i.imgur.com/bHSQwCb.png)
</div>


  In the query mentioned above, I created the `employees` table as a part of the `hr` schema using `CREATE TABLE hr.employees`. Here, I capitalised the SQL keywords that have been built in PostgreSQL but kept anything else added by me - such as names of columns - as lower-case. Though this is not an enforced rule, it is considered as a good practice for making the queries easier to understand.

  Inside `hr.employees`, I also created columns with specific data-types, which act as a constraint and decide what kind of data is to be allowed in a column. An explanation of the data types used in this table are as follows:
  - **`employee_id`**: This column was defined with the `SERIAL` data type, which is basically an integer that automatically adds 1 to the rows. Additionally, this column was also made the primary key as a unique identifier of this table, which was later used for forming relations with related tables.
  - **`first_name`**, **`last_name`**, **`email`**: This column was defined with the `VARCHAR` data type, without denoting a character length limit in the form of `VARCHAR(n)`. As explained [here by Hevodata](https://hevodata.com/learn/postgresql-varchar/#:~:text=In%20the%20PostgreSQL%20Varchar%20data,by%20PostgreSQL%20Varchar(n).), "If n is not specified, it defaults to a character of infinite length", meaning that these columns could store values with characters upto 255 bytes.
  - **`hire_date`**: This column was defined with the `DATE` data type, which allows the storage of date in the format of `YYYY-MM-DD`. 

In order to make sense of the created table when it would be retrieved later on, values were added to it using the following query:
```
INSERT INTO hr.employees (first_name, last_name, email, hire_date)
VALUES ('Yash', 'Anand', 'yash_anand@fosteringlinux.com', '2023-04-03'),
('Amartya', 'Sen', 'amartya.sen@gmail.com', '2013-01-12'
);
```

**2.1.2. `vacation_requests` Table**
  ```
  CREATE TABLE hr.vacation_requests (
    request_id SERIAL PRIMARY KEY,
    employee_id SERIAL,
    start_date DATE,
    end_date DATE,
    status VARCHAR,
    CONSTRAINT fk_employee_hr 
    FOREIGN KEY (employee_id) 
    REFERENCES hr.employees(employee_id)
);

  ```
  Output:
  <div align="center">

![image](https://i.imgur.com/b05wsZ6.png)
</div>

An explanation of the data types used in this table are as follows:
  - **`employee_id`**: This column was defined with the `SERIAL` data type, which is 

In order to make sense of the created table when it would be retrieved later on, values were added to it using the following query:
```
INSERT INTO hr.vacation_requests (start_date, end_date, status)
VALUES ('2023-10-01', '2023-10-10', 'Pending'),
('2023-10-05', '2023-10-20', 'Approved'
);
```

With this, the `vacation_requests` table was created successfully. In order to ensure that these tables had truly been become a part of the `hr` schema, I ran the following command to list the tables created under the `hr` schema:
```
\dt hr.*
```
**Output:** 
  <div align="center">

![image](https://i.imgur.com/Zn5u1L3.png)
</div>

In this command, we list all the tables using the `\dt`, which is used for displaying tables. However, we add a wildcard (*) after `hr.` to list all tables which come under this schema.

### 2.2. Defining Technical Schema  
> **Create the following tables in the "technical" schema:**  
2.2.1. "projects" to store project details (project_id, project_name, start_date,
end_date).  
2.2.2. "project_assignments" to associate employees with projects
(assignment_id, project_id, employee_id, assignment_date).  

Under this sub-task, the ask was to create 2 tables, namely `projects` and `project_assignments` with the purpose of storing employee information and tracking their vacation requests, respectively. It should be noted that these tables were to be kept under the `Technical Schema`. 

Therefore, the SQL queries provided below were written inside the `keenable` database using the PSQL terminal for the creation of the following tables:    

**2.2.1. `projects` Table**
```
CREATE TABLE technical.projects (
project_id SERIAL PRIMARY KEY,
project_name VARCHAR,
start_date DATE,
end_date DATE
);
```
  Output: 
  <div align="center">

![image](https://i.imgur.com/xfcJaeI.png)
</div>

  - **`employee_id`**: This column was defined with the `SERIAL` data type, which is 

In order to make sense of the created table when it would be retrieved later on, values were added to it using the following query:
```
INSERT INTO technical.projects (project_name, start_date, end_date)
VALUES ('IMS', '2022-03-25', '2023-10-12'),
('FINO', '2022-06-05', '2022-11-03'
);
```

**2.2.2. `project_assignments` Table**
  ```
CREATE TABLE technical.project_assignments (
assignment_id SERIAL PRIMARY KEY,
project_id SERIAL,
employee_id SERIAL,
assignment_date DATE,
CONSTRAINT fk_project_technical FOREIGN KEY (project_id) REFERENCES technical.projects(project_id),
CONSTRAINT fk_employee_technical FOREIGN KEY (employee_id) REFERENCES hr.employees(employee_id)
);
  ```
  Output:
  <div align="center">

![image](https://i.imgur.com/6cPtjnt.gif)
</div>

An explanation of the data types used in this table are as follows:
  - **`employee_id`**: This column was defined with the `SERIAL` data type, which is 
  - **`first_name`**, **`last_name`**, **`email`**: This column was defined with the `VARCHAR` data type, 
  - **`hire_date`**: This column was defined with the `DATE` data type, which allows 

In order to make sense of the created table when it would be retrieved later on, values were added to it using the following query:
```
INSERT INTO technical.project_assignments (assignment_date)
VALUES ('2023-10-16'),
('2023-11-02'
);

```

With this, the `project_assignments` table was created successfully. In order to ensure that these tables had truly been become a part of the `hr` schema, I ran the following command to list the tables created under the `hr` schema:
```
\dt technical.*
```
In this command, we list all the tables using the `\dt`, which is used for displaying tables. However, we add a wildcard (*) after `hr.` to list all tables which come under this schema.

### 2.3. Defining Management Schema

>**Create the following tables in the "management" schema:** 
2.3.1. "departments" to manage department information (department_id,
department_name, location).   
2.3.2. "department_employees" to track employee department assignments
(assignment_id, employee_id, department_id, start_date, end_date).  


**2.3.1. `departments` Table**
  ```
CREATE TABLE management.departments (
department_id SERIAL PRIMARY KEY,
department_name VARCHAR,
location VARCHAR
);

  ```
  Output:
  <div align="center">

![image](https://i.imgur.com/6cPtjnt.gif)
</div>

An explanation of the data types used in this table are as follows:
  - **`employee_id`**: This column was defined with the `SERIAL` data type, which is 

In order to make sense of the created table when it would be retrieved later on, values were added to it using the following query:
```
INSERT INTO management.departments (department_name, location)
VALUES('HR', 'Noida'),
('Fino', 'Gurgaon'
);
```

With this, the `project_assignments` table was created successfully. In order to ensure that these tables had truly been become a part of the `hr` schema, I ran the following command to list the tables created under the `hr` schema:
```
\dt management.*
```
In this command, we list all the tables using the `\dt`, which is used for displaying tables. However, we add a wildcard (*) after `hr.` to list all tables which come under this schema.


**2.3.2. `"department_employees"` Table**
  ```
CREATE TABLE management.department_employees (
assignment_id SERIAL PRIMARY KEY,
employee_id SERIAL,
department_id SERIAL,
start_date DATE,
end_date DATE,
CONSTRAINT fk_employee_management FOREIGN KEY (employee_id) REFERENCES hr.employees(employee_id),
CONSTRAINT fk_department_management FOREIGN KEY (department_id) REFERENCES management.departments(department_id)
);
  ```
  Output:
  <div align="center">

![image](https://i.imgur.com/6cPtjnt.gif)
</div>

An explanation of the data types used in this table are as follows:
  - **`employee_id`** **`assignment_id`**: This column was defined with the `SERIAL` data type, which is 

In order to make sense of the created table when it would be retrieved later on, values were added to it using the following query:
```
INSERT INTO management.department_employees (start_date, end_date)
VALUES ('2023-10-01', '2023-10-31'),
('2023-03-10', '2023-05-31'
);
```

With this, the `project_assignments` table was created successfully. In order to ensure that these tables had truly been become a part of the `hr` schema, I ran the following command to list the tables created under the `hr` schema:
```
\dt management.*
```
In this command, we list all the tables using the `\dt`, which is used for displaying tables. However, we add a wildcard (*) after `hr.` to list all tables which come under this schema.


--------



<div align="center">

## Task 3: Relationships 
</div>

As per this task, we have been asked to create relationships between tables after they have been created. In the second task, we have already formed various relations. However, in this task, I had to create relations using the `ALTER` SQL Keyword for updating or modifying existing tables. I tried to create relations using [this tutorial by PostgreSQLTutorial](https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-foreign-key/). The possible relations that I had planned on creating were:
- 

### `hr.employees` & `technical.projects`  

Suppose you want to create a relationship that associates employees with the projects they're assigned to. This would involve linking the "employee_id" in "hr.employees" with the "employee_id" in "technical.project_assignments." You can do this using ALTER TABLE statements.    

```
ALTER TABLE technical.projects
ADD COLUMN department_id SERIAL;

```

###  `management.departments` & `hr.employees`
If you want to associate employees with their respective departments, you can create a new relationship between "management.departments" and "hr.employees" using the "department_id" column.

```
ALTER TABLE hr.employees
ADD CONSTRAINT fk_department_management 
FOREIGN KEY (department_id)
REFERENCES management.departments(department_id);
```

--------

<div align="center">
   
## Task 4: Queries & Reporting

</div>

>Write SQL queries to retrieve information such as:
4.1. Employees in a specific department
4.2. Projects assigned to an employee
4.3. Vacation requests for an employee


As a part of the final and fourth task, we were assigned to run queries for retrieving the following information:

**4.1. Employees in a specific department**
Such a query could be deemed very useful for finding the employees from their respective departments and in order to find such an information, the following query was written:

```
SELECT employees.first_name, employees.last_name, departments.department_name
FROM hr.employees
JOIN management.department_employees ON employees.employee_id = department_employees.employee_id
JOIN management.departments ON department_employees.department_id = departments.department_id
WHERE departments.department_name = '<deptartment name>';
```
The output of running this query for finding the employee working for the HR department was as follow:
  <div align="center">

![image](https://i.imgur.com/6cPtjnt.gif)
</div>

--------
