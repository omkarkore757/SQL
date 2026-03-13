SQL Joins, Set Operators, and Subqueries Examples

This repository contains SQL query examples demonstrating commonly used database concepts such as:

Joins

Set Operators

Subqueries

The examples use simple sample tables (Customers and Orders) to explain how each SQL concept works.

Sample Tables Used
Customers
ID	Name	Manager_ID
1	Alice	NULL
2	Bob	1
3	Charlie	1
4	David	2
Orders
Order_ID	Customer_ID	Product
101	1	Laptop
102	2	Phone
103	2	Tablet
104	5	Monitor
1. SQL Joins
INNER JOIN

Returns only matching records from both tables.

SELECT Customers.ID, Customers.Name, Orders.Order_ID
FROM Customers
INNER JOIN Orders
ON Customers.ID = Orders.Customer_ID;
LEFT JOIN

Returns all records from the left table and matched records from the right table.

SELECT Customers.ID, Customers.Name, Orders.Order_ID
FROM Customers
LEFT JOIN Orders
ON Customers.ID = Orders.Customer_ID;
RIGHT JOIN

Returns all records from the right table and matched records from the left table.

SELECT Customers.ID, Customers.Name, Orders.Order_ID
FROM Customers
RIGHT JOIN Orders
ON Customers.ID = Orders.Customer_ID;
FULL OUTER JOIN

Returns all records when there is a match in either table.

SELECT Customers.ID, Customers.Name, Orders.Order_ID
FROM Customers
FULL OUTER JOIN Orders
ON Customers.ID = Orders.Customer_ID;
SELF JOIN

Used when a table references itself (e.g., employees and managers).

SELECT e1.Name AS Employee, e2.Name AS Manager
FROM Customers e1
LEFT JOIN Customers e2
ON e1.Manager_ID = e2.ID;
CROSS JOIN

Returns the Cartesian product of both tables.

SELECT Customers.Name, Orders.Product
FROM Customers
CROSS JOIN Orders;
NATURAL JOIN

Automatically joins tables based on common column names.

SELECT *
FROM Customers
NATURAL JOIN Orders;
2. Set Operators
UNION

Combines results and removes duplicates.

SELECT Name FROM Customers
UNION
SELECT Product FROM Orders;
UNION ALL

Combines results including duplicates.

SELECT Name FROM Customers
UNION ALL
SELECT Product FROM Orders;
INTERSECT

Returns only common values between queries.

SELECT ID FROM Customers
INTERSECT
SELECT Customer_ID FROM Orders;
MINUS

Returns rows from the first query not present in the second query.

SELECT ID FROM Customers
MINUS
SELECT Customer_ID FROM Orders;
3. Subqueries
Single-row Subquery
SELECT Name
FROM Customers
WHERE ID = (SELECT MAX(Customer_ID) FROM Orders);
Multi-row Subquery
SELECT Name
FROM Customers
WHERE ID IN (SELECT Customer_ID FROM Orders);
Using ANY / ALL
-- ANY
SELECT Name
FROM Customers
WHERE ID > ANY (SELECT Customer_ID FROM Orders);

-- ALL
SELECT Name
FROM Customers
WHERE ID > ALL (SELECT Customer_ID FROM Orders);
Using IN
SELECT Name
FROM Customers
WHERE ID IN (2,3);
