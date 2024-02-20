# sql-query

 Find the average price of all products form products table
 ```javascript

 SELECT AVG(price) AS average_price FROM products;

 ```
______________________________________________________________________________________________________

Write Query to Join Products and Categories with the INNER JOIN
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



