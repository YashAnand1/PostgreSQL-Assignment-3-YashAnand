<div align="center">

![image](https://ashnik-images.s3.amazonaws.com/prod/wp-content/uploads/2021/02/20050444/Postgresql-w-400x106.png)

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

> This assignment has also been documented as a video and can be viewed by clicking the video below:

<div align="center">

replace this with custom gif 
[![IMAGE_ALT](https://img.youtube.com/vi/-LwI4HMR_Eg/0.jpg)](https://www.youtube.com/watch?v=-LwI4HMR_Eg)
   </div>

<div align="center">
   
## Prerequisites
</div>

In an RDBMS or Relational Database Management System, the data is organised into tables with rows and columns - like it is done in a spreadsheet. The data entered in a row of the table would be associated with its respective column's header, making the data more structured and tidy. The main component of an RDBMS therefore consists of its capability of inputting data as tables and also allowing data interaction and management based on the relationship between the tables. 

For better understanding, lets assume there is a soft-drink refrigerator which stores different drinks. However, the manager of the store that this fridge is set up in, wishes to efficiently manage data related to the various soft drinks such as:
- Name of all the soft-drink brands
- Details related to supplier of the soft-drinks

In order to do so, he could utilise an RDBMS to help him store and manage data in the form of various tables. This could be done by creating one table called "Brands" and another called "Suppliers", and populating the related data into these tables. However, in order to check which supplier is in charge of supplying a specific soft-drink, a relation could be formed between the 2 tables for relating different brands with their suppliers, using the concept of foreign keys in the "Suppliers" table.

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

