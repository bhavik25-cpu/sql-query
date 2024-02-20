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


