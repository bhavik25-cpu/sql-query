# sql-query
https://www.programiz.com/sql/online-compiler/

 Find the average amount of all amount form amount table
 ```javascript

SELECT AVG(amount) AS average_price FROM Orders;

 ```
______________________________________________________________________________________________________

Write a Query to Join Products and Categories with the INNER JOIN
keyword Below in sample table with small data
 ```javascript

-- Sample Categories table
 ```javascript
CREATE TABLE Categories (
  category_id INT PRIMARY KEY,
  category_name VARCHAR(255)
);
 ```

 ```javascript
INSERT INTO Categories (category_id, category_name)
VALUES
  (1, 'Electronics'),
  (2, 'Clothing'),
  (3, 'Books');
 ```

-- Sample Products table
 ```javascript
CREATE TABLE Products (
  product_id INT PRIMARY KEY,
  product_name VARCHAR(255),
  price DECIMAL(10, 2),
  category_id INT,
  FOREIGN KEY (category_id) REFERENCES Categories(category_id)
);
 ```

 ```javascript
INSERT INTO Products (product_id, product_name, price, category_id)
VALUES
  (1, 'Laptop', 1200.00, 1),
  (2, 'T-Shirt', 19.99, 2),
  (3, 'Smartphone', 800.00, 1),
  (4, 'Book', 12.50, 3);
 ```
 Query using INNER JOIN to retrieve product details with category names
 ```javascript
SELECT Products.product_id, Products.product_name, Products.price, Categories.category_name
FROM Products
INNER JOIN Categories ON Products.category_id = Categories.category_id;
 ```
_____________________________________________________________________________________________
Join 3 TABLES
 ```javascript

SELECT *
FROM Customers
JOIN Orders ON Customers.customer_id = Orders.order_id
JOIN Shippings ON Orders.order_id = Shippings.shipping_id;
 ```
________________________________________________________________________________________________
Write query to Lists the employees that have registered more than 10
orders. Below in sample table with small data

-- Sample Employees table
 ```javascript


CREATE TABLE Employees (
  employee_id INT PRIMARY KEY,
  employee_name VARCHAR(255)
);

 ```
 ```javascript

INSERT INTO Employees (employee_id, employee_name)
VALUES
  (1, 'John Doe'),
  (2, 'Jane Smith'),
  (3, 'Alice Johnson');
 ```

-- Sample Orders table
 ```javascript

CREATE TABLE Orders (
  order_id INT PRIMARY KEY,
  order_number VARCHAR(255),
  employee_id INT,
  FOREIGN KEY (employee_id) REFERENCES Employees(employee_id)
);
 ```
 ```javascript
INSERT INTO Orders (order_id, order_number, employee_id)
VALUES
  (1, 'ORD001', 1),
  (2, 'ORD002', 2),
  (3, 'ORD003', 1),
 ```

-- Query to list employees with more than 10 orders
 ```javascript
SELECT Employees.employee_id, Employees.employee_name, COUNT(Orders.order_id) AS order_count
FROM Employees
JOIN Orders ON Employees.employee_id = Orders.employee_id
GROUP BY Employees.employee_id, Employees.employee_name
HAVING order_count > 10;
 ```

__________________________________________________________________________________________________________________________
To retrieve the top 3 highest values from a column in a SQL database, from Orders

1 Assuming you have a Orders table with a 'amount' column
 ```javascript

SELECT item, amount
FROM Orders
ORDER BY amount DESC
LIMIT 3;
 ```

 ```javascript
2
SELECT * FROM Orders ORDER BY amount DESC LIMIT 1 OFFSET 2;
 ```
____________________________________________________________________________________________________
 ```javascript

SELECT first_name,last_name,SUM(age)
FROM
Customers
GROUP BY first_name
ORDER BY SUM(age)

 ```
_________________________________________________________________________________________
Consider a database containing customer information. The query below is executed to retrieve the sum of ages for each customer, along with their first name and last name. The results are then grouped by the first name and ordered by the sum of ages in ascending order.
 ```javascript

SELECT first_name,last_name,SUM(age)
FROM
Customers
GROUP BY first_name
ORDER BY SUM(age)

 ```
________________________________________________________________________________________
 The query below is executed to retrieve the sum of ages for each customer, along with their first name and last name. However, it excludes any customers with the first name "John" or those with a null first name. The results are then grouped by the first name.
 ```javascript

SELECT first_name, last_name, SUM(age)
FROM Customers
WHERE first_name != 'John' AND first_name IS NOT NULL
GROUP BY first_name;

 ```
_____________________________________________________________________________
Consider a database containing order information. The query below is executed to retrieve the count of orders for each item, along with the total amount, but only for items where the amount is greater than 2 The results are then ordered by the total count of orders for each item.
 ```javascript

SELECT item, amount, COUNT(*) AS Total
FROM Orders
GROUP BY item
HAVING amount > 2
ORDER BY Total;
 ```

__________________________________________________________________________________

What SQL command is used to create a table named "employees" with columns for employee ID, name, salary, department, and date of birth, where the ID serves as the primary key?


 ```javascript

CREATE TABLE employees(
id int PRIMARY KEY,
name VARCHAR(50) NOT NULL,
salary int(20),
department VARCHAR(50),
dob date
);


 ```
 ```javascript

Show Tables;
 ```

 ```javascript

INSERT INTO employee(id,name,salary,department,dob)
VALUES(101,'jack',2000,'HR','1997-05-19')

```
______________________________________________________________________________________________________________________

How does the provided SQL statement create a table named "employee" with columns for employee ID, name, address, and department ID, where the department ID references the "customer_id" column in the "Orders" table?
 ```javascript

CREATE TABLE employee(
ID int PRIMARY KEY,
NAME VARCHAR(50) NOT NULL,
ADDRESS int(20),
DEPT_ID VARCHAR(50),
FOREIGN KEY (DEPT_ID) REFERENCES Orders(customer_id)
);
 ```

______________________________________________________________________________________________________________________

Removes the table from the database,
 ```javascript
DROP TABLE table_name;

 ```
Removes one or more records from the table

 ```javascript
DELETE FROM table_name
WHERE condition;

 ```
Removes all the rows from the table, leaving the column names. The TRUNCATE command is a DDL command. 
 ```javascript
TRUNCATE TABLE table_name;

 ```

____________________________________________________________________________________________________________________
LEFT JOIN
 ```javascript


SELECT *
FROM Customers
LEFT JOIN Orders ON Customers.customer_id = Orders.customer_id
LEFT JOIN Shippings ON Customers.customer_id = Shippings.shipping_id;
 ```


____________________________________________________________________________________________________
RIGHT JOIN
 ```javascript

SELECT *
FROM Customers
RIGHT JOIN Orders ON Customers.customer_id = Orders.customer_id
RIGHT JOIN Shippings ON Customers.customer_id = Shippings.shipping_id;
 ```

__________________________________________________________________________________________

FULL OUTER JOIN 
 ```javascript

SELECT *
FROM Customers
FULL OUTER JOIN Orders ON Customers.customer_id	 = Orders.customer_id;

 ```
__________________________________________________________________________________________
"CROSS JOIN
 ```javascript

SELECT *
FROM Customers
CROSS JOIN Orders
CROSS JOIN Shippings;
 ```
_______________________________________________________________________________________
Delete Duplicate first_name sql query 
```javascript
DELETE FROM Customers
WHERE customer_id IN (
   SELECT customer_id
   FROM (
       SELECT 
           customer_id,
           ROW_NUMBER() OVER (PARTITION BY first_name ORDER BY customer_id) AS row_num
       FROM 
           Customers
   ) AS SubQuery
   WHERE row_num > 1
);


 ```
_____________________________________________________________________________________________________________
 Combine Two Tables


 ```javascript


SELECT 
    c.first_name,
    c.last_name,
    o.item,
    o.item
FROM 
    Customers c
LEFT JOIN 
    Orders o ON c.customer_id = o.customer_id;
 ```

_____________________________________________________________________________________________________________
 Department Highest Salary
 ```javascript

CREATE TABLE Departments (
    id INT PRIMARY KEY,
    department_name VARCHAR(255) NOT NULL
);

 ```

CREATE TABLE Employees (
    id INT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    salary DECIMAL(10, 2) NOT NULL,
    department_id INT,
    FOREIGN KEY (department_id) REFERENCES Departments(id)
);

 ```javascript

INSERT INTO Departments (id, department_name) VALUES
(1, 'Sales'),
(2, 'Marketing'),
(3, 'Finance');
 ```
 ```javascript

INSERT INTO Employees (id, name, salary, department_id) VALUES
(1, 'John Doe', 50000.00, 1),
(2, 'Jane Smith', 60000.00, 1),
(3, 'Michael Johnson', 55000.00, 2),
(4, 'Emily Brown', 65000.00, 2),
(5, 'David Jones', 70000.00, 3);

 ```

 ```javascript
SELECT d.department_name, MAX(e.salary) AS highest_salary
FROM Departments d
JOIN Employees e ON d.id = e.department_id
GROUP BY d.department_name
ORDER BY highest_salary DESC
LIMIT 1;
 ```

