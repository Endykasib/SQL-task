# SQL-task
use test529
go 
CREATE SCHEMA Sales;
go
CREATE TABLE Employees (
    ID INT primary key,
    Name VARCHAR(100) unique,
    Salary DECIMAL(10,2)
    (ID) REFERENCES Projects(ProjectID);
);
ALTER TABLE Employees
ADD Department VARCHAR(50);
ALTER TABLE Employees
DROP COLUMN Salary;
execute sp_rename 'Employees.Department', 'DeptName', 'COLUMN';
CREATE TABLE Projects (
    ProjectID INT,
    ProjectName VARCHAR(100)
);
ALTER TABLE Employees
DROP (ID) REFERENCES Projects(ProjectID);
CREATE TABLE Customers (
    CustomerID INT,
    FirstName VARCHAR(20) unique,
    LastName VARCHAR(20) unique,
    Email VARCHAR(40),
    Status VARCHAR(15) default ('Active')
);
CREATE TABLE Orders (
    OrderID INT,
    CustomerID INT,
    OrderDate DATETIME2,
    TotalAmount DECIMAL(10,2) CHECK (TotalAmount > 0)
);
ALTER SCHEMA Sales
TRANSFER Orders;
execute sp_rename 'Sales.Orders' , 'Sales. SalesOrders' ;
select*
from Employees;
select Name , Salary 
from Employees;
select distinct DeptName('Ali')
from Employees;
select top 5*
from Employees;
select*
from Employees
order by Salary Descending; 
select*
from Employees
order by ID
offset 2 rows next 10 rows only;
select avg(Salary) as avgsalary
from Employees;
select 
    max(Salary) AS maxsalary,
    min(Salary) as minsalary
FROM Employees;
select top 3 Salary
from Employees
order by Salary Descending; 

select*
from Employess
order by Name Ascending;

select*
from Employees
order by Salary Descending;
offset 1 rows next 5 rows only;

select sum(Salary) as  TotalSalary
from Employees;
select*
from Employees
where Salary between 40000 and 60000
order by Salary Ascending;
--------------------------------------------
search task:
-1. Referential Actions (Foreign Key Options)
When you create a FOREIGN KEY, you can control what happens when the parent table is updated or deleted.
- DELETE
DELETE FROM Employees
WHERE ID = 1;
Features:
Deletes row by row
Can use WHERE
Can be rolled back (inside transaction)
Fires triggers
Slower
- TRUNCATE
TRUNCATE TABLE Employees;
Features:
Deletes all rows only
No WHERE
Faster (minimal logging)
Resets identity (auto increment)
Cannot be used if FK exists
Cannot be rolled back (in most cases)
-----------------------------------------------------
