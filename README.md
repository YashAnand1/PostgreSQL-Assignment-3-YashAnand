# PostgreSQL-Assignment-3-YashAnand

<div align="center">

# Documentation: PostgreSQL Tasks        
### — Database, Tables & Queries —    

_____________________________________________________________________________________                        

#### <u>INCLUDED TOPICS</u>  

</div>
<center>

Understanding & Setting-Up PostgreSQL                     
PostgreSQL: Q&A                       
TASK I - Database & Sample Table                        
TASK II - Table Data Retrieval & SQL Queries                          

<center>      

_____________________________________________________________________________________      

</center>
   

<center>

## Understanding & Setting-Up PostgreSQL

</center>

PostgreSQL or Postgres is a relational database management system (RDBMS). The data is organised here into tables with rows and columns. Additionally, the storing and retrieving of data is done using SQL on the basis of the relation between tables.

<div align="center">
<center>

![image](https://ashnik-images.s3.amazonaws.com/prod/wp-content/uploads/2021/02/20050444/Postgresql-w-400x106.png)

</div>
</center>

Some of the main features of Postgre include:   
- Storage & management of structured data 
- Efficient retrieval capabilities
- SQL for interacting with DB 

On my system, the installation of Postgres was done using this [YouTube Tutorial](https://www.youtube.com/watch?v=-LwI4HMR_Eg). Addiitonally, majority of the learnings that I have utilised for performing the assigned tasks came from this tutorial as well:

[![IMAGE_ALT](https://img.youtube.com/vi/-LwI4HMR_Eg/maxresdefault.jpg)](https://www.youtube.com/watch?v=-LwI4HMR_Eg)


The steps followed for the setting-up Postgres were as follows:   
- Installing PostgresSQL & additional utilities using **`sudo apt-get install postgresql postgresql-contrib`**

  **Output:**
<div align="center">

  ![image](https://i.imgur.com/wjfuUE2.png)

</div>

  
- Checking the status of Postgres using **`service postgresql status`**
  
  **Output:**
<div align="center">


  ![image](https://i.imgur.com/PT63rvh.png)

</div>

- Entering Postgres using **`sudo su postgres`**

  Output:      
<div align="center">


  ![image](https://i.imgur.com/BOhq5Yl.png)

</div>

  
- Launching PSQL terminal for interacting with the database using **`psql`**

  Output:        
<div align="center">


  ![image](https://i.imgur.com/37B5gkI.png)

</div>


- Creating user with **`CREATE USER yashanand WITH PASSWORD 'a';`** and listing all users with **`\du`**

  Output:  
<div align="center">
  
  ![image](https://i.imgur.com/NHEH3jw.png)

</div>

- Adding Superuser privilege to the new user using **`ALTER USER yashanand WITH SUPERUSER;`**
 
  Output:   
<div align="center">

  ![image](https://i.imgur.com/MKmzGyc.png)

</div>


--------------------------------
<center>

## PostgreSQL: Q&A    

</center>

After gaining a basic understanding and a working set-up of Postgres, I worked on giving answers to the 'True or False' questions as a part of our first assignment. It should be noted that these questions were based on the 'Technical Charcha On PostgreSQL' session that was conducted by Mr. Vinay Pawar on 24 September, 2023.

The answers to the 'True or False' questions asked are as follows:  

| Q.No. | Question | ANSWER |
|-----| ------------|------------|     
| 01 | PostgreSQL is an example of an RDBMS (Relational Database Management System). | True |
| 02 | PostgreSQL is known for features such as ACID compliance, extensibility, and high performance. | True |
| 03 | In PostgreSQL, a database is a collection of related tables. | True |
| 04 | A SELECT statement is used to retrieve data from a PostgreSQL table. | True |
| 05 | SQL queries can be used to modify data in a PostgreSQL database, including inserting, updating, and deleting records. | True |
| 06 | NOT NULL constraints cannot be applied to columns in PostgreSQL. | False |
| 07 | Unique constraints ensure that values in a column are unique across all records in a table. | True |
| 08 | CHECK constraints allow you to specify custom rules for data validation. | True |
| 09 | Data types in a database define the kind of values that can be stored in a column, such as integers, text, or dates. | True |
| 10 | Foreign keys are used to establish relationships between tables by referencing the primary key of another table. | True |

--------------------------------
<center>

## TASK I - Database & Sample Table 

</center>


| **Task: Create a new PostgreSQL database and set up a sample table.**  |
|----------------| 
| 1.1. Create a new database named "company."  |
| 1.2. Create a table named "employees" with columns for ID, first name, last name, and job title.   | 
| 1.3. Insert at least three sample employee records into the table.  |
______
As per the first task, it was required to have Postgres installed and set-up on my system. Therefore, I utilised the steps mentioned in the first section for installing and setting-up Postgres. Through these steps, I was able to successfully create a new user using the PSQL interactive terminal and was ready to get started with the tasks. 
  
## **Task 1.1. Create a new database named "company."**  
For creating a database, I referred to this [YouTube Tutorial](https://www.youtube.com/watch?v=-LwI4HMR_Eg) and [this article](https://www.tutorialspoint.com/postgresql/postgresql_create_database.htm) by Tutorial's Point. Inside the PSQL, I wrote the following SQL query for creating a database called "company":
```
CREATE DATABASE company;
``` 
**Output:**   
<div align="center">

![image](https://i.imgur.com/kLfWLC9.png)   
</div>

In this query, I created a new database without specifying the owner. If I was to specify the owner, the query would have been `CREATE DATABASE company WITH OWNER yashanand;`. Regardless, a database was still created with `postgres` as its default owner. It should be noted that it is important to add `;` at the end of a query for its termination.

In order to ensure that the database had been created, I utilised the `\l` command for listing the stored databases and the output  as follows:   

<div align="center">

![image](https://i.imgur.com/gBtfQuX.png)

</div>

## **Task 1.2. Create a table named "employees" with columns for ID, first name, last name, and job title.**  
In order to create a table, I first entered into the "company" database using `\c company`. As it was not specified in the task, I did not create a new schema by writing a query such as `CREATE SCHEMA companyschema;` and allowed essentially allowed the schema to be set as the default 'Public' schema.

For creating a table called "employees" inside the "company" database, with headers for "id", "first_name", "last_name" and "job title", I wrote the following query:
```
CREATE TABLE employees(
id int PRIMARY KEY,
first_name varchar,
last_name varchar,
job title varchar
);
```

**Output:**

<div align="center">

![image](https://i.imgur.com/K6Kp9id.png)

</div>

The reasoning behind declaring "id" as int type was that the values related to it were only going to be in integer values. Similarly, the rest of the headers were declared as varchar in order to store variable characters upto 255 bytes as values.

## **1.3. Insert at least three sample employee records into the table.**   
The three sample records that I created for inserting into the table were added to their specified headers by writing the following query:
```
INSERT INTO employees (id, first_name, last_name, job_title)
VALUES
(543, 'Yash', 'Anand', 'Contractor'),
(876, 'Puneet', 'Gupta', 'Employee'),
(234, 'Ankur', 'Kumar' , 'Intern');
```  

**Output:**

<div align="center">

![image](https://i.imgur.com/Q6aPCC7.png)

</div>


As explained in the previous sub-task, the first column for "id" included integers but the "first_name", "last_name" and "job_title" were created for storing varchar data types and therefore, consisted of variable characters.
____

<center>

## TASK II - Table Data Retrieval & SQL Queries 

</center>


| **Task: Write SQL queries to retrieve data from the "employees" table.**  |
|----------------| 
| 2.1. Retrieve all records from the "employees" table.  |
| 2.2. Retrieve only the first and last names of all employees. | 
| 2.3. Sort the employees by last name in alphabetical order. |
_____
In this task, SQL queries were to be utilised for interacting with the "employees" table that was created inside the "company" database. Inside the "company" database, that I had entered into using `\c company`, I worked on performing the sub-tasks provided below:  

## **Task  2.1. Retrieve all records from the "employees" table.**  
After having added sample records to the "employees" table, I retrieved all of the records from the table by running the following query:
```
SELECT * FROM employees
```
**Output:**   
<div align="center">

![image](https://i.imgur.com/FwOFJmx.png)

</div>


In this query, `SELECT *` is used for the retrieval of all records from a specific table of "employees" using `FROM employees` in the query. The `(3 rows)` under the displayed records shows that the displayed table consists of 3 rows.

## **Task  2.2. Retrieve only the first and last names of all employees.**  
In order to display selected columns of 'first_name' and 'last_name' from the "employees" table, I ran the following query for the display of specific columns: 
```
SELECT first_name, last_name FROM employees;
```

**Output:**   

<div align="center">

![image](https://i.imgur.com/pdYb4Uk.png)

</div>

Unlike the previous query where we were running `SELECT *` for retrieving all records, we used `SELECT first_name, last_name` for retrieving specific records. Similar to the previous query, `FROM employees` is used in the query to specify which table we want to retrieve records from. The `(3 rows)` displayed under the output again to signify the number of rows in the displayed table.


## **Task  2.3. Sort the employees by last name in alphabetical order.**  
After having retrieved all of the records as well as specifc records from the "employees" table, the records retrieval was to be done this time by sorting employees by their `last_name` in alphabetical order. In order to perform this task, I wrote the following query:
```
SELECT * FROM employees ORDER BY last_name;
```
**Output:**  
<div align="center">

![image](https://i.imgur.com/JeoUXWr.png)

</div>


As mentioned earlier, `SELECT *` is used in the query for retrieving all records and `FROM employees` is utilised for specifying the table which includes the records. The `ORDER BY last_name` part of the query helped sorting the `last_name` column alphabetically. By default, the sorting is done in ascending order but it can be changed to descending order by running the following query:
 ```
SELECT * FROM employees ORDER BY last_name DESC;
```

**Output:**    

<div align="center">

![image](https://i.imgur.com/y3Wfpgo.png)
</div>

-----------------------------------------------

## **Conclusion**: 
After looking into the answers for the 'True or False' questions and performing the 2 tasks, I have been able to successfully understand the basics of how databases are created and how they are used in Postgres. Inside these databases, I also learnt how to create tables and add records to it. Through the second task, I  have been able to understand the basics of writing queries for interacting with Postgres for mainly, data retrieval. 

--------------------------------
