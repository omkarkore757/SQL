Tables Used As Examples

Customers
| ID | Name    | Manager_ID |
| -- | ------- | ----------- |
| 1  | Alice   | NULL        |
| 2  | Bob     | 1           |
| 3  | Charlie | 1           |
| 4  | David   | 2           |

Orders
| Order_ID | Customer_ID | Product |
| --------- | ------------ | ------- |
| 101       | 1            | Laptop  |
| 102       | 2            | Phone   |
| 103       | 2            | Tablet  |
| 104       | 5            | Monitor |

---

1️⃣ Joins
a) INNER JOIN
SELECT Customers.ID, Customers.Name, Orders.Order_ID
FROM Customers
INNER JOIN Orders 
ON Customers.ID = Orders.Customer_ID;
Result: Returns only matching rows (IDs 1 & 2).

b) LEFT JOIN
SELECT Customers.ID, Customers.Name, Orders.Order_ID
FROM Customers
LEFT JOIN Orders 
ON Customers.ID = Orders.Customer_ID;
Result: Returns all customers and matched orders. Unmatched orders appear as NULL.

c) RIGHT JOIN
SELECT Customers.ID, Customers.Name, Orders.Order_ID
FROM Customers
RIGHT JOIN Orders 
ON Customers.ID = Orders.Customer_ID;
Result: Returns all orders and matched customers. Unmatched customers appear as NULL.

d) FULL OUTER JOIN
SELECT Customers.ID, Customers.Name, Orders.Order_ID
FROM Customers
FULL OUTER JOIN Orders 
ON Customers.ID = Orders.Customer_ID;
Result: Returns all customers and all orders, matched and unmatched.

e) SELF JOIN (e.g., Employees and Managers)
SELECT e1.Name AS Employee, e2.Name AS Manager
FROM Customers e1
LEFT JOIN Customers e2
ON e1.Manager_ID = e2.ID;
Result: Shows employee with their manager.

f) CROSS JOIN
SELECT Customers.Name, Orders.Product
FROM Customers
CROSS JOIN Orders;
Result: Every customer combined with every order (Cartesian product).

g) NATURAL JOIN (assuming column names are same in both tables)
SELECT * 
FROM Customers
NATURAL JOIN Orders;
Result: Automatically joins on common column `ID` / `Customer_ID`.


2️⃣ Set Operators

a) UNION
SELECT Name FROM Customers
UNION
SELECT Product FROM Orders;
Result: All distinct names and products combined.

b) UNION ALL
SELECT Name FROM Customers
UNION ALL
SELECT Product FROM Orders;
Result: All names and products including duplicates.

c) INTERSECT
SELECT ID FROM Customers
INTERSECT
SELECT Customer_ID FROM Orders;
Result: Only common IDs between Customers and Orders (IDs 1 & 2).

d) MINUS
SELECT ID FROM Customers
MINUS
SELECT Customer_ID FROM Orders;
Result: IDs in Customers but **not** in Orders (IDs 3 & 4).

3️⃣ Subqueries

a) Single-row subquery
SELECT Name 
FROM Customers 
WHERE ID = (SELECT MAX(Customer_ID) FROM Orders);
Result: Returns customer whose ID matches the highest Customer\_ID in Orders.

b) Multi-row subquery
SELECT Name 
FROM Customers 
WHERE ID IN (SELECT Customer_ID FROM Orders);
Result:Returns all customers who have placed orders.

c) Nested subquery with ANY / ALL
-- ANY
SELECT Name 
FROM Customers 
WHERE ID > ANY (SELECT Customer_ID FROM Orders);

-- ALL
SELECT Name 
FROM Customers 
WHERE ID > ALL (SELECT Customer_ID FROM Orders);

d) Using IN
SELECT Name 
FROM Customers 
WHERE ID IN (2,3);
Result: Returns Bob and Charlie.
