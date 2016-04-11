# Assignment

No 1
SELECT Customers.*, Orders.*, Emplyees.*
FROM Customers
Join Orders
On Customers.Customer.ID=Orders.Customer.ID
Join Employees
On Orders.Employee.ID=Employees.Employee.ID;


No 2
Table1
CREATE TABLE samples
(
SampleID int,
Age float,
Sex int);

Table2
CREATE TABLE mutations
(
SampleID int,
Mutations varchar(50),
CHR varchar(5),
Position int,
GT varchar(3));
