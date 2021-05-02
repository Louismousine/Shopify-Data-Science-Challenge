# Shopify-Data-Science-Challenge

My submission for the [Fall 2021 Data Science Internship @ Shopify](https://docs.google.com/document/d/13VCtoyto9X1PZ74nPI4ZEDdb8hF8LAlcmLH1ZTHxKxE/edit#).
### Question 1
a. The problem is that the calculation does not consider the number of items per order. Orders that included multiple items skew up the average.

b. Instead of average order value, a more representative metric would be average order item value.

c. For this dataset, its value is 387.74. However, we can see that the shop with id 78 is significantly charging more than its competitors. If we ignore this outlier, we get that the average is 152.48.

My calculations and analysis were simple enough that I only used Excel. My worksheet can be accessed [here](https://docs.google.com/spreadsheets/d/1f9XJGomNKSI61WWFNTaTbmTv8U8BSSbPcJFd-ARJ9-I/edit?usp=sharing).



### Question 2
1. 
```
SELECT COUNT(OrderID) FROM Orders o 
LEFT JOIN Shippers s ON o.ShipperID = s.ShipperID 
WHERE s.ShipperName = 'Speedy Express';
```

Result: 54 

2. 
```
SELECT e.LastName, Count() AS number_orders FROM Orders o 
JOIN Employees e ON e.EmployeeID=o.EmployeeID
GROUP BY e.EmployeeID
ORDER BY number_orders DESC
LIMIT 1;
 ```

Result: Peacock with 40 orders

3. 
```
SELECT ProductName, SUM(od.Quantity) AS aggregate_quantity FROM OrderDetails od
JOIN Products p ON p.ProductID=od.ProductID
JOIN Orders o ON o.OrderID=od.OrderID
JOIN (SELECT CustomerID FROM Customers WHERE Country="Germany") c ON c.CustomerID=o.CustomerID
GROUP BY od.ProductID
ORDER BY aggregate_quantity DESC
LIMIT 1;
```
Result: Boston Crab Meat with 160 orders
