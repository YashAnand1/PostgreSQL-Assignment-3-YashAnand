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
    - [HR Schema](#hr-schema)
    - [Technical Schema](#technical-schema)
    - [Management Schema](#management-schema)
  - [Task 3: Relationships](#task-3-relationships)
  - [Task 4: Queries \& Reporting](#task-4-queries--reporting)
  - [CONCLUSION](#conclusion)
 
_____________________________________________________________________________________      
<div align="center">
   
## Overview 
</div>

As a part of the third Technical Charcha session on PostgreSQL, the attendees were given an assignment comprising of 4 tasks to help gauge their understanding of PostgreSQL. This document serves as a documentation of these 4 tasks which involve the creation of database, schemas, tables and relationships, as well as the querying of the created data.
<div align="center">     

![image](https://ashnik-images.s3.amazonaws.com/prod/wp-content/uploads/2021/02/20050444/Postgresql-w-400x106.png)
   </div>

These completed tasks have been compiled into this single document with practical demonstrations, in the form of video and pictures. Through this document, one can aim to better understand how to form relationships between data, as it can be understood as the main theme of the assignment itself. 

<div align="center">     

<!-- [![IMAGE_ALT](https://img.youtube.com/vi/-LwI4HMR_Eg/0.jpg)](https://www.youtube.com/watch?v=-LwI4HMR_Eg) -->
   </div>

<div align="center">
   
## Prerequisites
</div>

Before getting started with the assigned tasks, it was important to have PostgreSQL installed on my computer. In order to install this [Relational Database Management System](https://cloud.google.com/learn/what-is-a-relational-database) and its additional utilities, I had to run the following command:
```
sudo apt-get install postgresql postgresql-contrib
```
Next, I ensured that the status of the installed postgreSQL service was active. This was checked by runnning the following command:
```
service postgresql status
```
I was ready to get started with the assigned tasks as all of the conditions for the prerequisites had been met, when the output of the above command displayed PostgreSQL as an `active` service:
<div align="center">

![image](https://i.imgur.com/6cPtjnt.gif)
</div>

In the coming sections, we will be performing the following assigned tasks:
- Creation of Database

--------
<div align="center">

## Task 1: Creation Of Database
</div>

ACID Compliance in the context of databases stands for Atomicity, Consistency, Isolation and Durability. These 4 components help with a stronger reliablility and integrity of data transactions, which is a logical unit of work done using database operations such as inserting, deleting or updating data. The components of ACID Compliance can therefore be understood better in the following way:

--------

<div align="center">
   
## Task 2: Schema Design
</div>

As stated before, an **RDBMS** or Relational Database Management System is a management system of database where data is stored in tables and data interaction is done based on the relationship between these tables. An RDBMS is an advanced version of a simple **DBMS** or Database Management System, where the entire flow of data from its insertion, creation, updation and retrieval is taken care while maintaining uniformity of the database. We can therefore understand that an RDBMS is an advanced form of DBMS, as it also helps with managing databases where relations can be created between various data in the form of tables. 

### HR Schema
### Technical Schema
### Management Schema

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

