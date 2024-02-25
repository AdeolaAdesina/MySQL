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
('Jane Smith', 'jane.smith@example.com', '456 Oak Avenue', 'Vancouver', 'British Columbia', 'V6J 3Z6');
```

Insert into Categories

```
INSERT INTO Categories (CategoryName) VALUES
('Electronics'),
('Books');
```


Insert into Products

```
INSERT INTO Products (Name, Description, Price, CategoryID) VALUES
('Laptop', 'A high-performance laptop suitable for all your needs.', 1200.00, 1),
('Database Management Systems Book', 'Comprehensive guide to database management.', 59.99, 2);
```


Insert into Orders


```
INSERT INTO Orders (CustomerID, OrderDate, Status) VALUES
(1, '2023-09-01', 'Shipped'),
(2, '2023-09-02', 'Processing');
```

Insert into OrderDetails

```
INSERT INTO OrderDetails (OrderID, ProductID, Quantity, Price) VALUES
(1, 1, 1, 1200.00),
(2, 2, 2, 59.99);
```

