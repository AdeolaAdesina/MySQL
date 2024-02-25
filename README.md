# MySQL

Step 1: Designing the Tables

1. Customers Table

Stores customer information.

```
CREATE TABLE Customers (
    CustomerID INT AUTO_INCREMENT PRIMARY KEY,
    Name VARCHAR(255) NOT NULL,
    Email VARCHAR(255) NOT NULL UNIQUE,
    Address VARCHAR(255) NOT NULL,
    City VARCHAR(100) NOT NULL,
    Province VARCHAR(100) NOT NULL,
    PostalCode VARCHAR(7) NOT NULL
);
```

2. Categories Table
Holds product categories.

```
CREATE TABLE Categories (
    CategoryID INT AUTO_INCREMENT PRIMARY KEY,
    CategoryName VARCHAR(100) NOT NULL
);
```

3. Products Table
Contains product details, linked to Categories by CategoryID.


```
CREATE TABLE Products (
    ProductID INT AUTO_INCREMENT PRIMARY KEY,
    Name VARCHAR(255) NOT NULL,
    Description TEXT,
    Price DECIMAL(10, 2) NOT NULL,
    CategoryID INT,
    FOREIGN KEY (CategoryID) REFERENCES Categories(CategoryID)
);
```


4. Orders Table
Records orders made by customers, linking to Customers by CustomerID.


```
CREATE TABLE Orders (
    OrderID INT AUTO_INCREMENT PRIMARY KEY,
    CustomerID INT,
    OrderDate DATE NOT NULL,
    Status VARCHAR(50),
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);
```

5. OrderDetails Table
Details of each order, linking to Orders by OrderID and to Products by ProductID.


```
CREATE TABLE OrderDetails (
    OrderDetailID INT AUTO_INCREMENT PRIMARY KEY,
    OrderID INT,
    ProductID INT,
    Quantity INT NOT NULL,
    Price DECIMAL(10, 2) NOT NULL,
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID),
    FOREIGN KEY (ProductID) REFERENCES Products(ProductID)
);
```


Step 2: Inserting Sample Data into the Tables

Now, let's insert some sample data into each table.

Insert into Customers


```
INSERT INTO Customers (Name, Email, Address, City, Province, PostalCode) VALUES
('John Doe', 'john.doe@example.com', '123 Maple Street', 'Toronto', 'Ontario', 'M5H 1A1'),
('Jane Smith', 'jane.smith@example.com', '456 Oak Avenue', 'Vancouver', 'British Columbia', 'V6J 3Z6'),
('Ahmed Khan', 'ahmed.khan@example.com', '789 Pine Road', 'Calgary', 'Alberta', 'T2N 1N4'),
('Maria Garcia', 'maria.garcia@example.com', '1010 Birch Place', 'Montreal', 'Quebec', 'H3B 2S2'),
('Chen Wei', 'chen.wei@example.com', '2020 Cedar Lane', 'Ottawa', 'Ontario', 'K1A 0B1'),
('Emily Johnson', 'emily.johnson@example.com', '3030 Maple Drive', 'Edmonton', 'Alberta', 'T5K 0L5'),
('Carlos Hernandez', 'carlos.hernandez@example.com', '4040 Oak Street', 'Winnipeg', 'Manitoba', 'R3J 0P9'),
('Aisha Patel', 'aisha.patel@example.com', '5050 Birch Park', 'Saskatoon', 'Saskatchewan', 'S7L 5P8'),
('Alexander Smith', 'alexander.smith@example.com', '6060 Pine View', 'Halifax', 'Nova Scotia', 'B3H 4R2'),
('Sophia Brown', 'sophia.brown@example.com', '7070 Spruce Road', 'St. John\'s', 'Newfoundland and Labrador', 'A1B 2C3');

```

Insert into Categories

```
INSERT INTO Categories (CategoryName) VALUES
('Electronics'),
('Books'),
('Home & Kitchen'),
('Fashion'),
('Beauty & Personal Care'),
('Sports & Outdoors'),
('Toys & Games'),
('Grocery'),
('Automotive'),
('Garden & Outdoor');

```


Insert into Products

```
INSERT INTO Products (Name, Description, Price, CategoryID) VALUES
('Laptop', 'A high-performance laptop suitable for all your needs.', 1200.00, 1),
('Database Management Systems Book', 'Comprehensive guide to database management.', 59.99, 2),
('Coffee Maker', 'Brews perfect coffee every time.', 99.99, 3),
('Running Shoes', 'Comfortable, durable running shoes.', 89.99, 4),
('Shampoo', 'Organic shampoo for all hair types.', 19.99, 5),
('Yoga Mat', 'Eco-friendly, non-slip yoga mat.', 50.00, 6),
('Board Game', 'Fun for the whole family.', 29.99, 7),
('Organic Almonds', 'Raw, organic almonds. 1lb bag.', 15.99, 8),
('Car Vacuum', 'High power, compact car vacuum.', 39.99, 9),
('Garden Hose', 'Durable, kink-free garden hose, 50ft.', 34.99, 10);

```


Insert into Orders


```
INSERT INTO Orders (CustomerID, OrderDate, Status) VALUES
(1, '2023-09-01', 'Shipped'),
(2, '2023-09-02', 'Processing'),
(3, '2023-09-03', 'Delivered'),
(4, '2023-09-04', 'Shipped'),
(5, '2023-09-05', 'Processing'),
(6, '2023-09-06', 'Delivered'),
(7, '2023-09-07', 'Shipped'),
(8, '2023-09-08', 'Processing'),
(9, '2023-09-09', 'Delivered'),
(10, '2023-09-10', 'Shipped');

```

Insert into OrderDetails

```
-- Assuming each order contains 2 different products for simplicity
INSERT INTO OrderDetails (OrderID, ProductID, Quantity, Price) VALUES
(1, 1, 1, 1200.00),
(1, 2, 2, 59.99),
(2, 3, 1, 99.99),
(2, 4, 1, 89.99),
(3, 5, 2, 19.99),
(3, 6, 1, 50.00),
(4, 7, 3, 29.99),
(4, 8, 2, 15.99),
(5, 9, 1, 39.99),
(5, 10, 1, 34.99),
(6, 1, 1, 1200.00),
(6, 2, 1, 59.99),
(7, 3, 1, 99.99),
(7, 4, 2, 89.99),
(8, 5, 1, 19.99),
(8, 6, 1, 50.00),
(9, 7, 1, 29.99),
(9, 8, 1, 15.99),
(10, 9, 1, 39.99),
(10, 10, 2, 34.99);

```





1. SELECT
Use Case: Retrieve all product names and prices.

```
SELECT Name, Price FROM Products;
```


2. SELECT DISTINCT
Use Case: List all unique cities where customers live to plan regional marketing campaigns.


```
SELECT DISTINCT City FROM Customers;
```


3. WHERE
Use Case: Find products that are priced over $100 for a premium products report.

```
SELECT Name, Price FROM Products WHERE Price > 100;
```


4. ORDER BY
Use Case: Order customers by name alphabetically for a customer directory.

```
SELECT Name, Email FROM Customers ORDER BY Name;
```


5. GROUP BY
Use Case: Count how many products are in each category for inventory summary.


```
SELECT CategoryID, COUNT(*) AS ProductCount FROM Products GROUP BY CategoryID;
```

6. LIMIT
Use Case: Get the top 5 most expensive products for a featured products section.


```
SELECT Name, Price FROM Products ORDER BY Price DESC LIMIT 5;
```

7. MIN and MAX
Use Case: Determine the cheapest and most expensive product prices for market analysis.


```
SELECT MIN(Price) AS CheapestProduct, MAX(Price) AS MostExpensiveProduct FROM Products;
```


8. COUNT
Use Case: Find out how many orders have been made to assess business activity.


```
SELECT COUNT(*) AS TotalOrders FROM Orders;
```


9. SUM and AVERAGE
Use Case: Calculate the total and average sales amount for financial reporting.


```
SELECT SUM(Price * Quantity) AS TotalSales, AVG(Price * Quantity) AS AverageSale FROM OrderDetails;
```


10. LIKE
Use Case: Search for all customers whose name contains "John" for a targeted email campaign.


```
SELECT Name, Email FROM Customers WHERE Name LIKE '%John%';
```


11. IN
Use Case: Select orders that were placed in either September or October for a seasonal sales analysis.


```
SELECT OrderID, OrderDate FROM Orders WHERE MONTH(OrderDate) IN (9, 10);
```


12. BETWEEN
Use Case: Identify products priced between $50 and $100 for a mid-range product promotion.


```
SELECT Name, Price FROM Products WHERE Price BETWEEN 50 AND 100;
```


13. AS (Alias)
Use Case: Simplify column names in output for better readability in reports.


```
SELECT Name AS ProductName, Price AS ProductPrice FROM Products;
```


14. Joins and Types
INNER JOIN
Use Case: Match each order with its customer name for order processing.

```
SELECT Orders.OrderID, Customers.Name FROM Orders INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID;
```


LEFT JOIN
Use Case: List all customers and their orders, including those who haven't made any orders.


```
SELECT Customers.Name, Orders.OrderID FROM Customers LEFT JOIN Orders ON Customers.CustomerID = Orders.CustomerID;
```


15. UNION
Use Case: Combine names of all products and categories into one list for a comprehensive catalog.


```
SELECT Name FROM Products
UNION
SELECT CategoryName AS Name FROM Categories;
```


16. Removing NULL Values
Use Case: Ensure no products are listed without a price for a complete pricing catalog.


```
SELECT Name, Price FROM Products WHERE Price IS NOT NULL;
```


17. Statistics (Mean, Median, Mode)
MySQL doesn't directly support median or mode calculations in a single function like mean (average). However, you can calculate the average easily:

Use Case for Mean: Calculate the average price of all products.


```
SELECT AVG(Price) AS AveragePrice FROM Products;
```



For median and mode, you'd typically need more complex queries or to process the data outside of MySQL, such as using application logic in Python or R.
