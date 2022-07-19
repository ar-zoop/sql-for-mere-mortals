1. Design a Database and create required tables. For e.g. Bank, College Database

```
create database testDB;
use testDB;
create table Persons
 (
  PersonID int,
  LastName varchar(255),
  FirstName varchar(255),
  Address varchar(255),
  City varchar(255),
  Age int
);

create table Orders(
   OrderID	int(11) Primary Key,
   CustomerID	int(11)		,
   EmployeeID	int(11)		,	
   OrderDate	date		,	
   ShipperID int(11)
);

create table Customers
(
    CustomerID	int(11) auto_increment primary key,
    CustomerName varchar(255),
    ContactName	varchar(255),
    Address	varchar(255),
    City varchar(255),
    PostalCode varchar(255),
    Country varchar(255)
);

```
2. Apply the constraints like Primary Key, Foreign key, NOT NULL to the tables
   
```
Alter table Orders
    Add foreign key (CustomerID)
    References Customers (CustomerID);
```

3. Write a SQL statement for implementing ALTER,UPDATE, INSERTION and DELETE.

```
Alter table Persons
    add birthday date;

Alter table Persons
drop column Birthday;

We created the table Customers in Ques 1. To update its data we must fill it with data first.

Insert into Customers (CustomerID, CustomerName,	ContactName,	Address,	City,	PostalCode,	Country)
values 
    (1, "Alfreds Futterkiste",	"Maria Anders"	,"Obere Str. 57"	,"Berlin"	,"12209", "Germany"),
    (2, "Ana Trujillo Emparedados y helados",	"Ana Trujillo",	"Avda. de la Constitución" ,"México D.F."	,"05021"	,"Mexico"),
    (3,	Antonio Moreno, Taquería,	Antonio Moreno	Mataderos, 2312,	México D.F.,	05023,	Mexico),
    (4	,Around the Horn	,Thomas Hardy	,120 Hanover Sq.	,London	,WA1 1DP	,UK),
    (5	,Berglunds snabbköp,	Christina Berglund,	Berguvsvägen 8	,Luleå,	S-958 22,	Sweden)
;

Update Customers
set City = 'Oslo'
WHERE CustomerID = 1;

Delete from Customers WHERE CustomerName='Alfreds Futterkiste';

```
4. Write the queries to implement the joins.

To perform joins, Orders table must have data in it. Lets add data to it.
```
Insert into orders(OrderID,	CustomerID	,EmployeeID	,OrderDate	,ShipperID)
values
   (10248	,2	,5,	1996-07-04	,3),
   (10249,	3,	6	,1996-07-05	,1),
   (10250,	4,	4	,1996-07-08,	2),
   (10251	,5	,3	,1996-07-08,	1),
   (10252	,	2,4,	1996-07-09,	2),
   (10253	,3	,3	,1996-07-10	,2),
   (10254	,4	,5	,1996-07-11	,2),
   (10255,	5	,9	,1996-07-12	,3);

```
INNER JOIN
```
select  Orders.OrderID, Orders.CustomerID, Customers.CustomerName
from Orders
Inner join Customers
on Orders.CustomerID = Customers.CustomerID;        
```
## Make changes in the table for this
LEFT JOIN
```
Select Customers.CustomerID, Orders.OrderID, Orders.EmployeeID
from Customers
Left join Orders on Customers.CustomerID=Orders.CustomerID;
```
## Make change sin the table for this
RIGHT JOIN
```
Select Customers.CustomerID, Orders.OrderID, Orders.EmployeeID
from Customers
Right join Orders on Customers.CustomerID=Orders.CustomerID;
```

5. Write the query for implementing the following functions: MAX (), MIN (), AVG () 
and COUNT ().

I need to create another table `OrderDetails` to do get the number of orders per customer.

count()
```
SELECT count(OrderDetailID) as NoOfOrder , Orders.CustomerID
FROM OrderDetails 
INNER JOIN Orders
ON Orders.OrderID=OrderDetails.OrderID
group by Orders.OrderID;
```
max()
```
CREATE VIEW transactions AS
SELECT count(OrderDetailID) as NoOfOrders, Orders.CustomerID as CustomerID
FROM OrderDetails 
INNER JOIN Orders
ON Orders.OrderID=OrderDetails.OrderID
group by Orders.OrderID;

select max(NoOfOrders) as MaxOrders ,CustomerID from transactions;
```
min()
```
select min(NoOfOrders) as MinOrders ,CustomerID from transactions;
```
avg()
```
SELECT avg(Price) as AvgPrice FROM Products;
```

6. Write the query to implement the concept of Integrity constrains.
Constraints: NOT NULL, UNIQUE, CHECK, DEFAULT, CREATE INDEX

NOT NULL
```
ALTER TABLE Persons
MODIFY Age int NOT NULL;
```

UNIQUE
```
ALTER TABLE Persons
ADD CONSTRAINT Uc_person UNIQUE (FirstName,LastName,ID);
```

CHECK
```
ALTER TABLE Persons
ADD CHECK (Age>=18);
```

DEFAULT
```
ALTER TABLE Persons
ALTER City SET DEFAULT 'Udaipur';
```

CREATE INDEX
```
CREATE INDEX idx_lastname
ON Persons (LastName);
```
7. Write the query to create the views.
```
CREATE VIEW transactions AS
SELECT count(OrderDetailID) as NoOfOrders, Orders.CustomerID as CustomerID
FROM OrderDetails 
INNER JOIN Orders
ON Orders.OrderID=OrderDetails.OrderID
group by Orders.OrderID;
```
8. Perform the queries for triggers.
9.  Perform the following operation for demonstrating the insertion , updation and deletion.
10.Using the referential integrity constraints.
11.Write the query for creating the users and their role.
