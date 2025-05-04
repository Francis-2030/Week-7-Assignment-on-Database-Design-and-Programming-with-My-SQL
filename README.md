Question 1: Analysis - Unnormalized Table
CREATE TABLE ProductDetail (
    OrderID INT,
    CustomerName VARCHAR(100),
    Products VARCHAR(100)
);

-- Inserting sample data into ProductDetail table
INSERT INTO ProductDetail(OrderID, CustomerName, Products)
VALUES
(101, 'John Doe', 'Laptop'),
(101, 'John Doe', 'Mouse'),
(102, 'Jane Smith', 'Tablet'),
(102, 'Jane Smith', 'Keyboard'),
(102, 'Jane Smith', 'Mouse'),
(103, 'Emily Clark', 'Phone');

Question 2: Analysis - Normalized Tables
Table: Orders
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerName VARCHAR(100)
);

-- Inserting sample data into Orders table
INSERT INTO Orders (OrderID, CustomerName)
VALUES
(101, 'John Doe'),
(102, 'Jane Smith'),
(103, 'Emily Clark');

Table: Product
CREATE TABLE Product (
    OrderID INT,
    Product VARCHAR(100),
    Quantity INT,
    PRIMARY KEY (OrderID, Product),
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID)
);

-- Inserting sample data into Product table
INSERT INTO Product (OrderID, Product, Quantity)
VALUES
(101, 'Laptop', 2),
(101, 'Mouse', 1),
(102, 'Tablet', 3),
(102, 'Keyboard', 1),
(102, 'Mouse', 2),
(103, 'Phone', 1);


SQL QUERIES
1. List of all customers and the products they ordered
SELECT o.CustomerName, p.Product, p.Quantity
FROM Orders o
JOIN Product p ON o.OrderID = p.OrderID;

2. Get the total number of products ordered by each customer
SELECT o.CustomerName, SUM(p.Quantity) AS TotalProducts
FROM Orders o
JOIN Product p ON o.OrderID = p.OrderID
GROUP BY o.CustomerName;

3. Details of products ordered by 'Jane Smith'
SELECT o.CustomerName, p.Product, p.Quantity
FROM Orders o
JOIN Product p ON o.OrderID = p.OrderID
WHERE o.CustomerName = 'Jane Smith';
