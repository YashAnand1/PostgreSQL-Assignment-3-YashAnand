<div align="center">


<!-- add technical charcha logo postgres session 3 -->
# PostgresSQL Session-3        
### — Tasks Documentation —    

_____________________________________________________________________________________                        

## Contents
</div>

  - [**Overview**](#overview)
  - [**Prerequisites**](#prerequisites)
  - [**Task 1: Creation Of Database**](#task-1-creation-of-database)
  - [**Task 2: Schema Design**](#task-2-schema-design)
    - [**2.1. Defining HR Schema**](#21-defining-hr-schema)
    - [2.1.1. `employees` Table](#211-employees-table)
    - [2.1.2. `vacation_requests` Table](#212-vacation_requests-table)
    - [**2.2. Defining Technical Schema**](#22-defining-technical-schema)
    - [2.2.1. `projects` Table](#221-projects-table)
    - [2.2.2. `project_assignments` Table](#222-project_assignments-table)
    - [**2.3. Defining Management Schema**](#23-defining-management-schema)
    - [2.3.1. `departments` Table](#231-departments-table)
    - [2.3.2. `department_employees` Table](#232-department_employees-table)
  - [**Task 3: Relationships**](#task-3-relationships)
  - [**Task 4: Queries \& Reporting**](#task-4-queries--reporting)
    - [4.1. Employees in a specific department](#41-employees-in-a-specific-department)
    - [4.2. Projects assigned to an employee](#42-projects-assigned-to-an-employee)
    - [4.3. Vacation requests for an employee](#43-vacation-requests-for-an-employee)
  - [Conclusion](#conclusion)
 
_____________________________________________________________________________________      
<div align="center">
   
# **Overview** 
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
   
## **Prerequisites**
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

## **Task 1: Creation Of Database**
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
   
## **Task 2: Schema Design**
</div>

>**Define three schemas within the database: "hr", "technical", and "management."**   

In databases, schemas can be understood as namespaces or groups, inside which tables are created for storing data. By default, Public is the schema created for a table that was created without a schema defined.

Provided below in this section is the demonstration of how I completed this second task by creating schemas, adding tables to them and forming relations between the tables. Though it had not been asked in the task itself, I also inserted values to the created tables in order to be able to make a better sense of the relations created. 

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

  <div align="center">

______________
### **2.1. Defining HR Schema**
>
</div>

>**Create the following tables in the "hr" schema:**  
2.1.1. "employees" to store employee information (employee_id, first_name, last_name, email, hire_date).   
2.1.2. "vacation_requests" to track employee vacation requests (request_id,
employee_id, start_date, end_date, status). 

Under this sub-task, the ask was to create 2 tables, namely `employees` and `vacation_requests` with the purpose of storing employee information and tracking their vacation requests, respectively. It should be noted that these tables were to be kept under the `HR Schema`. 

Therefore, the SQL queries provided below were written inside the `keenable` database using the PSQL terminal for the creation of the following tables:    
__________________
  <div align="center">

### 2.1.1. `employees` Table
</div>

  In the query mentioned below, I created the `employees` table as a part of the `hr` schema using `CREATE TABLE hr.employees`. Here, I capitalised the SQL keywords that have been built in PostgreSQL but kept anything else added by me - such as names of columns - as lower-case. Though this is not an enforced rule, it is considered as a good practice for making the queries easier to understand.

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

![image](https://i.imgur.com/4feHcar.png)
</div>


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
The output of running the above query was `INSERT 0 2`, signifying that 2 rows had been successfully (0) created:   

**Output:**
<div align="center">

![image](https://i.imgur.com/YmrIs13.png)
</div>

Lastly, in order to ensure that the table had been created, I ran `SELECT * FROM hr.employees;` query for retrieving this newly creted table:

**Output:**
<div align="center">

![image](https://i.imgur.com/uF8lsOc.png)
</div>

Through the above query, we asked PostgreSQL to display all columns from the employees table, that was under the hr schema. Here, the '*' symbol or wildcard represented the 'all columns' that were to be retrieved. Additionally, the `(2 rows)` under the displayed table represented the number of rows in which data was being stored.  
_________________
  <div align="center">

### 2.1.2. `vacation_requests` Table
</div>


In the below mentioned query, I continued with creating another table inside the `hr` schema for storing data related to vacation requests made by employees. The name of this table was kept as `vacation_requests` and since it was to include the `employee_id` column from the `employees` table for relating these 2 tables, I used foreign keys for creating a relations.

  ```
CREATE TABLE hr.vacation_requests (
request_id SERIAL PRIMARY KEY,
employee_id SERIAL,
start_date DATE,
end_date DATE,
status VARCHAR,
FOREIGN KEY (employee_id) 
REFERENCES hr.employees(employee_id)
);
  ```
  **Output:**
  <div align="center">

![image](https://i.imgur.com/n3XRNEh.png)
</div>


Foreign keys can be understood as the primary keys of the referenced table, meaning that one tables primary key can be another table's foreign key. With the tables and their data related, it would become easier to relate the vacation requests with the employees using their `employee_id` 

An explanation of the query written above and the data types being used is as follows:
  - **`PRIMARY KEYS`**: `request_id` was given created as the primary key for associating unique identifiers with the data belonging in each row. 
  - **`FOREIGN KEY`**, **`REFERENCES`**: the `employee_id` column of the `employees` table was added to this table and chosen as the foreign key. Additionally, it was defined which table this newly added column `REFERENCES` in order to form the relation.   
  - **`SERIAL`**: This data type was assigned to the `employee_id` column and `request_id`, for automatically incrementing integers to work as unique identifiers for data.
  - **`DATE`**: The format of this data type is `YYYY-MM-DD` and this was used in the `start_date` and `end_date` columns for storing information related to the dates between which vacations had been requested for.
  - **`VARCHAR`**: This data type was used in the `status` column for storing information related to whether the request had been approved or not. This column was allowed to store character values upto 255 bytes.
  
For ensuring that the `employees` and `vacation_requests` tables had truly been related, I wrote the a query for inserting some sample data into the `vacation_requests` table. In this query, neither the foreign key and nor the primary key from this table were mentioned while inputting the data because these keys were of `SERIAL` data type and they were to be generated automatically. The written query was as follows:

```
INSERT INTO hr.vacation_requests (start_date, end_date, status)
VALUES ('2023-10-01', '2023-10-10', 'Pending'),
('2023-10-05', '2023-10-20', 'Approved'
);
```
**Output:** 
  <div align="center">

![image](https://i.imgur.com/UfCZ3g5.png)
</div>

As stated earlier, the `INSERT 0 2` output means that the query of inserting was run successfully (represented by `0`) and `2` rows were added. Given that the created `vacation_requests` table was supposed to be related to the `employees` table, it was important to ensure that this relation had truly been made and this was done by displaying the `vacation_requests` table:      

**Output:**
  <div align="center">

![image](https://i.imgur.com/RdD1D3r.png)
</div>

Even though we had not mentioned the `request_id` or `employee_id` while inserting the values, the output of running `SELECT * FROM hr.vacation_requests;` included these 2 columns, further proving that the relationship had truly been created between the `employees` and `vacation_requests` table. 

**Ensuring tables are part of HR Schema**   
With this, the `vacation_requests` table was created successfully. In order to ensure that these tables had truly become a part of the `hr` schema, I ran the following command to list the tables created under the `hr` schema:
```
\dt hr.*
```
**Output:** 
  <div align="center">

![image](https://i.imgur.com/Zn5u1L3.png)
</div>

In this command, we list all the tables using the `\dt`, which is used for displaying tables. However, we add a wildcard (*) after `hr.` to list all tables which come under this schema. Through the output of this command, I was able to verify that the tables created in this sub-task, had truly become a part of the `hr` schema.

_________________
  <div align="center">

### **2.2. Defining Technical Schema**  
</div>

> **Create the following tables in the "technical" schema:**  
2.2.1. "projects" to store project details (project_id, project_name, start_date,
end_date).  
2.2.2. "project_assignments" to associate employees with projects
(assignment_id, project_id, employee_id, assignment_date).  

As per the second sub-task, I needed to created 2 tables inside the `technical` schema and these were to be called `projects` and `project_assignments`. Here the second table, was to reference `projects` from this schema and also the `employees` table from the `hr` schema.

Provided below is a demonstration of how both of these tables were created and how relationships were maintained between them.

_________________
  <div align="center">

### 2.2.1. `projects` Table
</div>

The motive of creating this table was to store data related to projects, such as `project_id`, `project_name`, `start_date` and `end_date`. In order to create such a table, I wrote the following query for creating a table called `projects` while placing it under the `technical` schema.

```
CREATE TABLE technical.projects (
project_id SERIAL PRIMARY KEY,
project_name VARCHAR,
start_date DATE,
end_date DATE
);
```
  **Output:**
  <div align="center">

![image](https://i.imgur.com/j9GCQZS.png)
</div>

The `CREATE TABLE` displayed as the output after running this query, signified that the `projects` table had been created successfully. An explanation of the data types used in the above query is as follows:
- **`PRIMARY KEY`**, **`SERIAL`**: The `project_id` column was was given this data type in order to allow PostgreSQL to automatically assign unique integer values as identifiers for each row, that would be containing project related data.
- **`VARCHAR`**: This data type was solely and specifically used for the `project_name` column, in order to store the names of the related projects that were to be added into this table.
- **`DATE`**: The `end_date` and `start_date` columns were assigned to store the data using this data type, in the format of `YYYY-MM-DD`.

After the creation of the table, I proceeded with inserting values to this newly created `projects` table for making sense of the table when data retrieval was going to be done. This was done by writing the following query: 
```
INSERT INTO technical.projects (project_name, start_date, end_date)
VALUES ('IMS', '2022-03-25', '2023-10-12'),
('FINO', '2022-06-05', '2022-11-03'
);
```
  **Output:**
  <div align="center">

![image](https://i.imgur.com/VHrIzJL.png)
</div>

As stated in the previous section, the meaning of `INSERT 0 2` is that `2` rows have been added to the metioned table, successfully (`0`). With the `projects` table containing some sample data, I could now retrieve the data belonging to this table using the **`SELECT * FROM technical.projects;`** query for ensuring that the data had been entered correctly:

**Output:**
  <div align="center">

![image](https://i.imgur.com/LIs7buJ.png)
</div>
Given that the data of all the columns that were added to the table had been retrieved successfully, from the `projects` table that was part of the `technical` schema, this sub-task came to a conclusion.

_________________
  <div align="center">

### 2.2.2. `project_assignments` Table

</div>

As per the task, a table called `project_assignments` was also to be created under the `technical` schema. It was to act as a `child table` that would be referencing parent tables of `technical.projects` and `hr.employees`, in order to create relations between these 3 tables. The goal of making this table was to keep track of all the project assignments that have been assigned to the employees. To create a table like this, the following query was written:

  ```
CREATE TABLE technical.project_assignments (
assignment_id SERIAL PRIMARY KEY,
project_id SERIAL,
employee_id SERIAL,
assignment_date DATE,
FOREIGN KEY (project_id) 
REFERENCES technical.projects(project_id),
FOREIGN KEY (employee_id) 
REFERENCES hr.employees(employee_id)
);
  ```
  **Output:**
  <div align="center">

![image](https://i.imgur.com/hl4zBwM.png)
</div>

A brief explanation of the above query and the data types utilised while writing it, is as follows:
- **`PRIMARY KEY`**: In this table, the `assignment_id` column was chosen to act as the unique identifier of each row that would be containing related data.
- **`SERIAL`**: This data type was utilised by the primary key of this table to ensure that unique integers would be added to each row to better identify data. The foreign keys like `project_id` and `employee_id` were also assigned this data type in their respective tables and that is why, their data type was kept as same.
-  **`DATE`**: Used as the data type for the `assignment_date` column, which was created to store data related to dates.

Once this table had been created, I also wrote the following query for inserting data into the `project_assignments` table, so that verifying its relationship with the `employees` and `projects` table could be easier:
```
INSERT INTO technical.project_assignments (assignment_date)
VALUES ('2023-10-16'),
('2023-11-02'
);
```
**Output:**
  <div align="center">

![image](https://i.imgur.com/xRMoxiI.png)
</div>

It should be noted how data was inserted into only a single column in the above query. This was due to all the other columns of `SERIAL` data type, namely `assignment_id`, `project_id` and `employee_id`, already automatically incrementing unique integers for each row that was added. In order to ensure that the relationships were being correctly in this table, I ran the `SELECT * FROM technical.project_assignments;` query to display the created table:

**Output:**
  <div align="center">

![image](https://i.imgur.com/2S6zTjt.png)
</div>

Hence, it was verified that the `project_assignments` table had been created successfully, while perfectly maintaining all the relationships that had been created through the use of foreign keys.


**Ensuring tables are part of Technical Schema**

Although I had ensured that the foreign-key relationships in this table were being maintained as I wanted them to be, it was also necessary to check that the `projects` and `projects_assignmentss` were truly part of the `techinical` schema.  To verify this, I had to run the following command:
```
\dt technical.*
```
**Output:**
  <div align="center">

![image](https://i.imgur.com/mfdY9R1.png)
</div>

Through this command, I was able to list all the tables which were a part of the `technical` schema and also verify that the `projects` and `project_assignments` tables were truly part of the same schema.

_________________
  <div align="center">

### **2.3. Defining Management Schema**

</div>

>**Create the following tables in the "management" schema:**  
2.3.1. "departments" to manage department information (department_id,
department_name, location).   
2.3.2. "department_employees" to track employee department assignments
(assignment_id, employee_id, department_id, start_date, end_date).  

This third sub-task required the creation of 2 tables called `departments` and `department_employees`. These tables were to be created inside the `management` schema. The second table was to form relationship with the `departments` table from the same schema and also with the `employees` table from the `hr` schema.

A demonstration of how I was able to create these 2 tables and form the required relationships is being provided below.
_________________
  <div align="center">

### 2.3.1. `departments` Table
</div>

The goal of creating a table called `departments`, which would store information on the `department_id`, `department_name` and its `location`. In order to create a table such as this, I wrote the following query: 

```
CREATE TABLE management.departments (
department_id SERIAL PRIMARY KEY,
department_name VARCHAR,
location VARCHAR
);
  ```
  **Output:**
  <div align="center">

![image](https://i.imgur.com/GOavoUW.png)
</div>

A brief explanation of the above query and the data types utilised while writing it, is as follows:
- **`PRIMARY KEY`**, **`SERIAL`**: The `department_id` columns was chosen as the `PRIMARY KEY` of the `SERIAL` data type, in order to keep the data entered in this table uniquely identifiable.
-  **`VARCHAR`**: This data type was used for the `department_name` and `location` columns, meaning that the data entered to these columns could store character values upto 255.  
   
After the creation of this table, the following query was written by me for inserting data into this newly created table called `departments`, so that varifying that the data was correctly storing data could be possible:

```
INSERT INTO management.departments (department_name, location)
VALUES('HR', 'Noida'),
('Fino', 'Gurgaon'
);
```
**Output:**
  <div align="center">

![image](https://i.imgur.com/78bswI5.png)
</div>

The output of `INSERT 0 2` meant that `2` rows had been successfully (`0`) created. To verify that the data was being stored inside table correctly, I tried retrieving the stored data using the **`SELECT * FROM management.departments;`** query and its output was as follows:

**Output:**
  <div align="center">

![image](https://i.imgur.com/nTnJYGv.png)
</div>
As it could be seen that the stored data was being stored correctly, I was able to successfully verify that this table had been correctly created.

_________________
  <div align="center">

### 2.3.2. `department_employees` Table

</div>

In order to create the `department_employees` table, we needed to form relationships with the `employee` table from the `hr` schema and the `departments` table that would created in the preious section. In order to form the required relations, foreign keys were utilised by writing the following query:

```
CREATE TABLE management.department_employees (
assignment_id SERIAL PRIMARY KEY,
employee_id SERIAL,
department_id SERIAL,
start_date DATE,
end_date DATE,
FOREIGN KEY (employee_id) 
REFERENCES hr.employees(employee_id),
FOREIGN KEY (department_id) 
REFERENCES management.departments(department_id)
);
```
  **Output:**
  <div align="center">

![image](https://i.imgur.com/smZpPv9.png)
</div>

With the creation of the table verified by the `CREATE TABLE` output, it was important to also verify that the table could correctly stored data, while maintaining the relationships through foreign keys. In order to do this, I inserted data into this table by writing the following query:
```
INSERT INTO management.department_employees (start_date, end_date)
VALUES ('2023-10-01', '2023-10-31'),
('2023-03-10', '2023-05-31'
);
```
**Output:**
  <div align="center">

![image](https://i.imgur.com/DsRe8Th.png)
</div>

Given that columns such as `assignment_id`, `employee_id` and `department_id` were columns of `SERIAL` data type, it was not required to enter data for these columns since their values were to be added automatically by PostgreSQL. However, I did insert some sample data into the `start_date` and `end_date` columns.

To ensure that the data was being stored correctly, I wrote the `SELECT * FROM management.department_employees` query for displaying the stored data. The output of this query was as follows:  

**Output:**
  <div align="center">

![image](https://i.imgur.com/XWHvlqq.png)
</div>

The above output helped me verify that this table had been created correctly and that the relationships between `management` schema's `department_employees` and `departments`, along with `hr` schema's `employees` table was being maintained correctly.

**Ensuring tables are part of Technical Schema**

To verify that the created tables of `department_employees` and `departments` were part of the same `management` schema, I ran the following command to list all the tables under the mentioned schema:
```
\dt management.*
```
**Output:**   

  <div align="center">

![image](https://i.imgur.com/8DDpDCD.png)
</div>

The above `\dt` command helped me list all the tables which came under the `management` schema and hence, verified that I had successfully created the `department_employees` and `departments` under this schema.

Additionally, this also marked the closure of Task 2 as all of the mentioned tables had been created under their respective schemas. In the following section, I have demonstrated how I was able to form new relations between the tables that had been created under this very task.

--------

<div align="center">

## **Task 3: Relationships** 
</div>

>Establish appropriate foreign key relationships between tables to maintain
referential integrity. For example, link "project_assignments" to "projects" and
"employees."

As per this task, we have been asked to create relationships between tables after they have been created. In the second task, we have already formed various relations. However, in this task, I had to create relations using the `ALTER` SQL Keyword for updating or modifying existing tables because these tables had already been crated. 

In order to create relations after the tables had been created, I utilised [this tutorial by PostgreSQLTutorial](https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-foreign-key/) for establishing new relationships between the existing tables for enhancing their referential integrity. Provided below are some possible relationships that I was able to create between the tables:

**1. `project_assignment` table with `projects` table**  
**Use Case**: For finding assignment details from the `projects` table

In order to establish a relationship between and link the `project_assignment` table with `projects` table, I wrote the following query:    
```
ALTER TABLE technical.projects
ADD assignment_id SERIAL;
ALTER TABLE technical.projects
ADD CONSTRAINT fk_assignment_id
FOREIGN KEY (assignment_id)
REFERENCES technical.project_assignments(assignment_id);
```
**Output:**
  <div align="center">

![image](https://i.imgur.com/2mp7HdN.png)
</div>

In the above query, I first added a new column called `assignment_id` to the `projects` table, with the `SERIAL` data type. This was done because before defining the foreign key, its existence in the table was more important. The first `ALTER TABLE` output helped me understand that the column had been successfully created.

In the second part of the query, I worked on defining a constraint and the foreign key that was to be referenced from the `project_assignments` table. The second `ALTER TABLE` as the output of the second part of the query represented that the foreign key relations had been created successfully between the `technical.projects` and `technical.project_assignments`. 

In order to ensure that this relationship had been created, I ran the following `JOIN` query:
```
SELECT * FROM technical.projects
JOIN technical.project_assignments ON technical.project_assignments.assignment_id = technical.projects.assignment_id; 
```
**Output:**
  <div align="center">

![image](https://i.imgur.com/r9QvWtm.png)
</div>

Given that the joining of the `technical.projects` and `technical.project_assignments` had been done, I was able to conclude that I had successfully linked `project_assignments` with the `projects` table. 

**2. `project_assignment` table with `employees` table**    
**Use Case**: To find data related to assignments from the `employees` table

Based on the above use-case, I wrote the following query for linking the `project_assignment` table with the `employees` table:
```
ALTER TABLE hr.employees
ADD project_id SERIAL;
ALTER TABLE hr.employees
ADD CONSTRAINT fk_project_id
FOREIGN KEY (project_id)
REFERENCES technical.projects(project_id);
```
**Output:**
  <div align="center">

![image](https://i.imgur.com/gYkilsm.png)
</div>

Though a link had already been made earlier by using `employee_id` of the `hr.employees` table as the foreign key in the `project_assignment` table, I needed to create a reverse-reference by using the `assignment_id` as the foreign key in the `employees` table.

To do this, I first added a column of `SERIAL` data type to the `employees` table in the first part of the query mentioned above. Once the `ALTER TABLE` output had been displayed, signifying the successful addition of the column, I worked on adding the `assignment_id` as the foreign key which referenced to the `project_assignment` table. The second `ALTER TABLE` output showcased that the foreign key had been added successfuly.

In order to ensure that the link of `project_assignment` table had been made with the `employees` table, I joied the 2 tables by using the foreign key of `assignment_id` as the common column. This was done by writting the following `join` query:
```
SELECT * FROM hr.employees
JOIN technical.project_assignments ON technical.project_assignments.assignment_id = hr.employees.project_id;
```
**Output:**
  <div align="center">

![image](https://i.imgur.com/OL1JFZY.png)
</div>

GIven that I was able to successfully join the `employees` and `project_assignments` table, it could be concluded that I was able to successfully form relations from `project_assignments` with the `employees` table.    

--------

<div align="center">
   
## **Task 4: Queries & Reporting**

</div>

>Write SQL queries to retrieve information such as:     
4.1. Employees in a specific department     
4.2. Projects assigned to an employee     
4.3. Vacation requests for an employee      

<div align="center">

### 4.1. Employees in a specific department   

</div>

In order to create a query that would help retrieve the name of employees from a specific department, I was able to come up with a query. However, an issue with it was that it could not be used for 'finding' data from a specific keyword. In order to counter this, I did some reasearch and came to learn about the `WHERE` keyword of SQL from this [W3School Tutorial](https://www.w3schools.com/sql/sql_where.asp). 

Therefore, this usage of this keyword was included in my query as the last line of the statement for allowing data retrieval of employee names based on a specific department. The created query is as follows:
```
SELECT hr.employees.employee_id, hr.employees.first_name, hr.employees.last_name, management.departments.department_id, management.departments.department_name
FROM hr.employees
JOIN management.department_employees ON hr.employees.employee_id = management.department_employees.employee_id
JOIN management.departments ON management.department_employees.department_id = management.departments.department_id;
WHERE management.departments.department_name = '<department name>';
```
In the query mentioned above, it was made possible to retrieve the names of employees working from their respective department names. An example of running the above query could be trying to view all the employees working in the HR department. For this, the `'<department name'` was replaced with `'HR'` and I was able to successfully retrieve the name of the employee working in the HR department:     

**Output:**
  <div align="center">

![image](https://i.imgur.com/KJERb3c.png)
</div>

Please note that in the above screenshot, the lines appear to be flowing into the next line due to the zooming-in of the terminal. The query mentioned before was only used for retrieving the name of the employee working in the HR Department. 

  <div align="center">

### 4.2. Projects assigned to an employee
</div>

Quite like the previous query, here we were supposed to write a query for retrieving the names of the projects assigned to a specific employee, from their names. In order to retrieve a data such as this, I wrote the following query: 

```
SELECT hr.employees.employee_id, hr.employees.first_name, hr.employees.last_name, technical.projects.project_id, technical.projects.project_name
FROM technical.projects
JOIN technical.project_assignments ON technical.project_assignments.project_id = technical.projects.project_id
JOIN hr.employees ON technical.project_assignments.employee_id = hr.employees.employee_id
WHERE hr.employees.first_name = `'<first name>'` AND hr.employees.last_name = `'<last name>'`;
```

An another way of writing this query could have been retrieving project names from `employee_id` but for the sake of simplicity, I chose the above method for querying. As an example, if we were to find the projects assigned to 'Yash Anand', then the above query could be modified to add this 'Yash' as the `first name` and 'Anand' as the `last name` for retrieving the names of the projects from this query. The output of the modified query would therefore be as follows:     

**Output:**
  <div align="center">

![image](https://i.imgur.com/xjIJSyv.png)
</div>

In the above output, the names of the projects that an employee was assigned to were successfully retrieved. The `1 row` displayed under the table signified the number of rows that were displayed for this query, meaning that the data related to this query was only available in a single row. Therefore, through the use of the above query, I was able to successfully write a query for retrieving project names assiged to an employee.  

  <div align="center">

### 4.3. Vacation requests for an employee      
</div>

For this final sub-task, I was required to write the simplest query written so far anywehre in this document, for finding the vacation requests from employee name. Such a data retrieval was made possible by writing the following query:
```
SELECT hr.employees.employee_id, hr.employees.first_name, hr.employees.last_name, hr.vacation_requests.request_id, hr.vacation_requests.start_date, hr.vacation_requests.end_date, hr.vacation_requests.status
FROM hr.vacation_requests
JOIN hr.employees ON hr.vacation_requests.employee_id = hr.employees.employee_id
WHERE hr.employees.first_name = `'<first name>'` AND hr.employees.last_name = `'last name'`;
```

I wrote the above query with a possible use case of finding the vacation requests made by an employee. An example of running the above query for an employee with the first name of `Yash` and last name of `Anand`, would give the following output:

**Output:**     
  <div align="center">

![image](https://i.imgur.com/wTPKk8B.png)
</div>

The `1 row` mentioned under the displayed table of the output is used to suggest the number of rows in which data is related to an employee's vacation_request is placed in. In the written query, the `WHERE` SQL Keyword helps search for data belonging to specific columns and therefore, allowed me to search for the vacation_requests of a specific employee. 
_____________________________

  <div align="center">

## Conclusion
</div>

After the completion of these 4 tasks, which greatly depended on building relationships between tables, I was able to learn and understand the concept of primary keys, foreign keys, constraints, joins and alters. Through this document, I was also able to demonstrate and perform the assigned tasks, which helped me gain a lot of practical understanding of PostgreSQL and SQL.

--------
