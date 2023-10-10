<div align="center">

![image](https://ashnik-images.s3.amazonaws.com/prod/wp-content/uploads/2021/02/20050444/Postgresql-w-400x106.png)

# PostgresSQL Session-3        
### — Tasks Documentation —    

_____________________________________________________________________________________                        

## 📚 Contents 📚

</div>

  - [Overview](#-introduction)  
  - Prerequisites](#prerequisites)  
  - [Creation Of Database](#creation-of-database)  
  - [Schema Design](#️-schema-design)  
      - [HR Schema](#-hr-schema)  
      - [Technical Schema](#-technical-schema)  
      - [Management Schema](#-management-schema)  
  - [Relationships](#-relationships)  
      - [Primary Keys](#primary-keys)    
      - [Foreign Keys](#foreign-keys)  
  - [CONCLUSION](#conclusion)  
 
_____________________________________________________________________________________      
<div align="center">
   
## 🪧 INTRODUCTION
</div>

Postgres is 
> This assignment has also been documented as a video and can be viewed by clicking the video below:
<div align="center">

replace this with custom gif 
[![IMAGE_ALT](https://img.youtube.com/vi/-LwI4HMR_Eg/0.jpg)](https://www.youtube.com/watch?v=-LwI4HMR_Eg)
   </div>

<div align="center">
   
## 📥 What Is RDBMS?
</div>

In an RDBMS or Relational Database Management System, the data is organised into tables with rows and columns - like it is done in a spreadsheet. The data entered in a row of the table would be associated with its respective column's header, making the data more structured and tidy. The main component of an RDBMS therefore consists of its capability of inputting data as tables and also allowing data interaction and management based on the relationship between the tables. 

For better understanding, lets assume there is a soft-drink refrigerator which stores different drinks. However, the manager of the store that this fridge is set up in, wishes to efficiently manage data related to the various soft drinks such as:
- Name of all the soft-drink brands
- Details related to supplier of the soft-drinks

In order to do so, he could utilise an RDBMS to help him store and manage data in the form of various tables. This could be done by creating one table called "Brands" and another called "Suppliers", and populating the related data into these tables. However, in order to check which supplier is in charge of supplying a specific soft-drink, a relation could be formed between the 2 tables for relating different brands with their suppliers, using the concept of foreign keys in the "Suppliers" table.

--------
<div align="center">

## ⚙️ What Is ACID?
</div>

ACID Compliance in the context of databases stands for Atomicity, Consistency, Isolation and Durability. These 4 components help with a stronger reliablility and integrity of data transactions, which is a logical unit of work done using database operations such as inserting, deleting or updating data. The components of ACID Compliance can therefore be understood better in the following way:

#### Atomicity 
According to this property, the entire transaction is either complete or none of it is. A transaction in this case works as a single unit and cannot be divided into sub-transactions, meaning that either the entire process of data interaction is going to succeed or the entire operation would be aborted and rolled back to the previous state. 

An example of such a case would be when an online transaction of money is done using PhonePay. As per the atomicty of a database, if any part of this process fails after the deduction from the sender's account but before the transfer to recipient's account, then the entire transaction is to be rolled back so that the sender does not lose their money.

#### Consistency
The property of Consitency ensures that the data is always available in a consistent state and that the rules set for data interaction, are not being violated during transactions. What this means is that the stored data is to remain reliable and as near accurate as possible. Going back to the previous example of making transactions using PhonePay, such a rule of consistency is that the sender would only be allowed to enter positive digits, when requesting transfer of money. Adding such constraints help keep the data remain in a reliable state. 

#### Isolation
According to the rule of Isolation, when operations are performed on the data through multiple transactions from multiple users, the transactions are carried out separately without affecting the other transactions. What this means is that if 2 operations are done on the same data then only one transaction would succeed and that the operation made slightly after would fail. For example, if a seat is being booked for a movie on [BookMyShow](www.bookmyshow.com) then multiple people would not be able to book the same seat and only the transaction that was done first would succeed. Isolation therefore ensures that multiple transactions do not mess up eachother's operations.

#### Durability
The durability property states that once a transaction has been carried out, then the data and the operations made would remain in a permanent state. Going back to the previous example of booking a seat for a movie using BookMyShow, the property of durability would ensure that once the transaction or the booking has been made, all the bookings would remain intact even after a server-failure at BookMyShow. Once the transaction has been done, it cannot be undone accidentally until and unless a request is made for it. 

--------

<div align="center">
   
## 🆚 RDBMS vs DBMS
</div>

As stated before, an **RDBMS** or Relational Database Management System is a management system of database where data is stored in tables and data interaction is done based on the relationship between these tables. An RDBMS is an advanced version of a simple **DBMS** or Database Management System, where the entire flow of data from its insertion, creation, updation and retrieval is taken care while maintaining uniformity of the database. We can therefore understand that an RDBMS is an advanced form of DBMS, as it also helps with managing databases where relations can be created between various data in the form of tables. 
  
Some of the key features and difference of and between RDBMS and DBMS are as follows:
| S. No. | RDBMS | DBMS |
|--- | --| -- |
| 1 | Stands for Relational Database Management System | Stands for Database Management System | 
| 2 | Data is stored as rows & columns in tables | Data is stored in the form of files |
| 3 | The stored data is always in a structured form | The stored data may or may not be structured|
| 4 | Data relation can be formed using primary & foregin keys | Data relation can be formed but not to the extent of an RDBMS |
| 5 | Many data elements can be accessed at the same time | Data elements have to be accessed individually |
| 6 | Keys and indexes disallow data redundancy | Data redundancy is very common |
| 7 | Usually used to handle large amount of data | Usually used for handling small data |
| 8 | Multiple levels of security measures are provided for data manipulation | Weak security measures provided for data manipulation |
| 9 | Data fetching is faster due to its relational approach | Data fetching can be fast but for small amount of data |
| 10 | Ideal for applications with structured data | Ideal for simpler storage needs |
| 11 | Example: PostgreSQL, MySQL, Oracle, etc. | Example: XML, Forxpro, Window Registry, etc. |

--------

<div align="center">
   
## 🔑 What Are Primary & Foreign Keys?
</div>

When it comes to maintaining a relationship between tables and uniquely identifying the data from a table, foreign key and primary keys, respectively can help us greatly in a Relational Database Management System. It should be noted that the primary key of one table is a foreign key to an another table, when it comes to forming relations of tables.                             

To understand better, lets assume that 2 tables called 'Brands' and 'Suppliers' have been created with 'Brand_ID' and 'Supplier_ID' as the primary keys. Additionally, the 'Suppliers' table will be containing the 'Brand_ID' from the 'Brands' table. 

#### Primary Keys       
In the above example, while 'Brand_ID' is a primary key for the 'Brands' table, 'Supplier_ID' is the primary key for the 'Suppliers' table. The main idea behind adding a primary key to tables is that they help ensure that the data related to different attributes or column, is always unique for each row. This uniqueness helps the process of data interaction immensely as all of the rows are allowed to be treated as an individual data inside the table. In the 2 tables that have been provided above, primary keys help uniquely identify the brands and suppliers from the 2 tables. 

#### Foreign Keys          
However, it is worth noting that in the 'Suppliers' table, the primary keys of the 'Brands' table are added as a column, which allows them to be treated as a foreign key in the 'Suppliers' table. Since the primary key of one table is the foreign key of another, adding the primary key of one table to another helps create a relation between these 2 tables and making sense of its data became easier. Therefore, a foreign key is a column (or a group of columns) that help create a relation between data in multiple tables. 

In conclusion, Primary Keys help with uniquely identifying a row in the table and when they are added to another table, they become Foreign Keys and help form relations between the table that they have been added to and the table that they originally belonged to.

--------

<div align="center">
   
## What is Indexing?

</div>

Indexing can be explained as an organised reference or shortcut that allows the DBMS to locate specific rows of data without having to scan the entire table. In order to better understand this, lets first take an example of an Index of a book. In such an Index, chapters/sections are associated with a specific page number on which they can be found. For this, One needs to simply go through the list of mentioned chapters/sections and check which page number is written in front of them. 

The Indexing in a DBMS works in a very similar way. In the context of a DBMS, an Index stores references to specific rows in a table based on the values in a column or various columns. The positives of Indexing therefore include faster data-retrieval operations and an efficient way to access the data. The negatives however mostly consists of the extra space taken by an index as well as the extra time taken to update and maintain an Index.

Some of the most common Indexing types are as follows:  

#### B-Tree Map Index
The main feature of such as Indexing type is that it speeds up queries which involve conditions related to equality and range. An example of an equality codition can be 'WHERE column = value and an example of an range conditions can be 'WHERE column BETWEEN x AND y'.
  
#### Unique Index
 Such an Indexing type helps ensuring that the values of the indexed columns remain unique across all rows in the table, preventing duplicate entries and possible redundancy. A use case for such an Indexing type can be creating a unique index column to remove duplicacy.
  
#### Bitmap Index
 Such types are are efficient for columns with a low number of distinct values and help when the queries involve multiple columns. For example, such Indexes represent each value in the index as a bitmap, meaning that each Bit would be associated with a row in the table. For example, the queries involving the usage of AND, OR, or NOT operations can be solved using this form of Indexing.

--------

<div align="center">
   
## CONCLUSION
</div>

