1. Count total number of customers
SELECT COUNT(*) AS TotalCustomers FROM Customers;

 2. Find average price of all products
SELECT AVG(Price) AS AverageProductPrice FROM Products;

 3. Find total stock available
SELECT SUM(Stock) AS TotalStock FROM Products;

 4. Count how many orders each customer has placed
SELECT CustomerID, COUNT(OrderID) AS OrderCount
FROM Orders
GROUP BY CustomerID;

 5. Find total number of orders for each product
SELECT ProductID, COUNT(*) AS TotalOrders
FROM Orders
GROUP BY ProductID;

 6. Find total stock value per product (Price * Stock)
SELECT ProductName, (Price * Stock) AS StockValue
FROM Products;

 7. Find total value of stock grouped by price range
SELECT 
  CASE 
    WHEN Price < 100 THEN 'Below 100'
    WHEN Price BETWEEN 100 AND 500 THEN '100-500'
    ELSE 'Above 500'
  END AS PriceRange,
  SUM(Stock) AS TotalStockInRange
FROM Products
GROUP BY PriceRange;

 8. Filter groups using HAVING: show products ordered more than once
SELECT ProductID, COUNT(*) AS TimesOrdered
FROM Orders
GROUP BY ProductID
HAVING COUNT(*) > 1;

 9. Average price per city (assuming Customers.Address holds city)
SELECT Address AS City, AVG(Price) AS AvgProductPrice
FROM Orders
JOIN Customers ON Orders.CustomerID = Customers.CustomerID
JOIN Products ON Orders.ProductID = Products.ProductID
GROUP BY Address;
