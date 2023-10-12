<div align="center">

![image](https://ashnik-images.s3.amazonaws.com/prod/wp-content/uploads/2021/02/20050444/Postgresql-w-400x106.png)
<!-- add technical charcha logo postgres session 3 -->
# PostgresSQL Session-3        
### — Tasks Documentation —    

_____________________________________________________________________________________                        

## 📚 Contents 📚

</div>

  - [Overview](#overview)
  - [Prerequisites](#prerequisites)
  - [Task 1: Creation Of Database](#task-1-creation-of-database)
  - [Task 2: Schema Design](#task-2-schema-design)
    - [2. Creating Schemas](#2-creating-schemas)
    - [2.1. Defining HR Schema](#21-defining-hr-schema)
    - [2.2. Defining Technical Schema](#22-defining-technical-schema)
    - [2.3. Defining Management Schema](#23-defining-management-schema)
  - [Task 3: Relationships](#task-3-relationships)
  - [Task 4: Queries \& Reporting](#task-4-queries--reporting)
  - [CONCLUSION](#conclusion)
 
_____________________________________________________________________________________      
<div align="center">
   
# Overview 
</div>

As a part of the third Technical Charcha session on PostgreSQL, the attendees were given an assignment comprising of 4 tasks to help gauge their understanding of PostgreSQL. This document serves as a documentation of these 4 tasks which involve the following:
- The creation of database, schemas, tables
- The querying of the created data

These completed tasks have been compiled into this single document with practical demonstrations, in the form of video and pictures. Through this document, one can aim to better understand how to <u>form relationships between data</u>, as it can be understood as the main theme of the assignment itself. 

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

![image](https://i.imgur.com/6cPtjnt.gif)
</div>

After switching the default Postgres user, I was able to gain the privilege of running PSQL terminal, where SQL queries can written for interacting with the database and make changes using keywords. The command for enabling this terminal is:
```
psql
```
The output of running this command displays the PSQL version and starts the PSQL terminal for allowing interaction with database using SQL queries:
 <div align="center">

![image](https://i.imgur.com/6cPtjnt.gif)
</div>

Once I had entered the PSQL terminal, it was possible to write SQL queries for performing the first task of creating a database. In order to create a database called 'keenable', I ran wrote the following query in the PSQL terminal:
```
CREATE DATABASE keenable;
```
Here the 'CREATE DATABASE' keywords of this query are self-explanatory as they are being used for creating a database. The third component of the query, `keenable`, is the name of the database that I was to create and most importantly, the `;` or semi-colon was used to tell SQL that I had completed the query. The output of running this entire query was:
<div align="center">

![image](https://i.imgur.com/6cPtjnt.gif)
</div>

In order to ensure that the database had truly been created, I ran the following command as the final step in for the completion of this first task:
```
\l
```
This command is run for listing all the existing databases in Postgres and I was able to utilise it to list the newly created `keenable` database. The output of this command was as follows:
<div align="center">

![image](https://i.imgur.com/6cPtjnt.gif)
</div>

With the `keenable` database created, this first task came to an end as it had been completed. In the following tasks, this newly created database was used for storing and creating schemas, tables and relationships. 

--------

<div align="center">
   
## Task 2: Schema Design
</div>

In databases, schemas are ............ hierarchy

Provided below in this section is the demonstration of how I completed this second task by creating schemas, adding tables to them and forming relations between the tables. Though it had not been asked in the task itself, I also inserted values to the created tables in order to be able to make a better sense of the relations created. 

### 2. Creating Schemas   

>**Define three schemas within the database: "hr", "technical", and "management."**   

Before getting started with creating the schemas, I had to enter the newly created `keenable` database as it had specifically been stated in the task that the schemas were to be created in this database only. In order to enter the datbase, I ran the following command from the PSQL terminal:
```
\c keenable
``` 
Using this command, I was able to get connected with the newly created `keenable` database and this was proved by the following output of this command:
 <div align="center">

![image](https://i.imgur.com/6cPtjnt.gif)
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

![image](https://i.imgur.com/6cPtjnt.gif)
</div>

- **Technical Schema**   
  This schema was created using the `CREATE SCHEMA technical;`
<div align="center">

![image](https://i.imgur.com/6cPtjnt.gif)
</div>

- **Management Schema**   
  This schema was created using the `CREATE SCHEMA management;`
<div align="center">

![image](https://i.imgur.com/6cPtjnt.gif)
</div>

Since just knowing that these schemas had been created was not enough, I needed to ensure that they had truly been created. To do this, I utilised the following command for listing all the schemas inside the current database of `keenable`.
```
\dn+
```
The meaning of `dn` in this context is "Directory Name", which helps us view all the schemas in the present database. The `+` on the other hand is used to display a more detailed output. After running this command, the displayed output for me was as follows: 
<div align="center">

![image](https://i.imgur.com/6cPtjnt.gif)
</div>

With all of the three schemas created successfully, the next goal was to define these created schemas. This was to be done by creating tables with relationships between eachother. As stated earlier, another goal for me in this task was to also insert some sample values into these tables as without them, it would have been difficult to understand the importance of these related tables.

### 2.1. Defining HR Schema 
>
>**Create the following tables in the "hr" schema:**  
2.1.1. "employees" to store employee information (employee_id, first_name,  
last_name, email, hire_date).   
2.1.2. "vacation_requests" to track employee vacation requests (request_id,
employee_id, start_date, end_date, status). 

Under this sub-task, the ask was to create  

### 2.2. Defining Technical Schema  
> **Create the following tables in the "technical" schema:**  
2.2.1. "projects" to store project details (project_id, project_name, start_date,
end_date).  
2.2.2. "project_assignments" to associate employees with projects
(assignment_id, project_id, employee_id, assignment_date).  


### 2.3. Defining Management Schema

>**Create the following tables in the "management" schema:** 
2.3.1. "departments" to manage department information (department_id,
department_name, location).   
2.3.2. "department_employees" to track employee department assignments
(assignment_id, employee_id, department_id, start_date, end_date).  



--------

<div align="center">

## Task 3: Relationships 
</div>

When it comes to maintaining a relationship between tables and uniquely identifying the data from a table, foreign key and primary keys, respectively can help us greatly in a Relational Database Management System. It should be noted that the primary key of one table is a foreign key to an another table, when it comes to forming relations of tables.     

--------

<div align="center">
   
## Task 4: Queries & Reporting

</div>

Indexing can be explained as an organised reference or shortcut that allows the DBMS to locate specific rows of data without having to scan the entire table. In order to better understand this, lets first take an example of an Index of a book. In such an Index, chapters/sections are associated with a specific page number on which they can be found. For this, One needs to simply go through the list of mentioned chapters/sections and check which page number is written in front of them. 

The Indexing in a DBMS works in a very similar way. In the context of a DBMS, an Index stores references to specific rows in a table based on the values in a column or various columns. The positives of Indexing therefore include faster data-retrieval operations and an efficient way to access the data. The negatives however mostly consists of the extra space taken by an index as well as the extra time taken to update and maintain an Index.

--------

<div align="center">
   
## CONCLUSION
</div>

