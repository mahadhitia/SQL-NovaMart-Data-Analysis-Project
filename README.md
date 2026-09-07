# SQL-NovaMart-Data-Analysis-Project

Hi 👋, welcome friends!<br>
In SQL, we can transform raw data to find some useful insight.
So, in order to do that, using SQL to retrieve some of the data we need is important here.
My first project [here](https://github.com/mahadhitia/SQL-NovaMart-Database-Design-Project) is using SQL to create the infrastructure of the data,
but on this page we're going to focus on how to analyze data using SQL.

![](https://github.com/mahadhitia/SQL-NovaMart-Data-Analysis-Project/blob/main/images/NovaMart-Data-Analysis.png)

---

## Table of Contents

1. [Project Overview](#project-overview)
2. [Business Problem](#business-problem)
3. [Dataset Overview](#dataset-overview)
4. [Key Business Analysis](#key-business-analysis)
   - [Sales Performance](#sales-performance)
   - [Product Performance](#product-performance)
   - [Category Performance](#category-performance)
   - [Customer Analysis](#customer-analysis)
   - [Payment Analysis](#payment-analysis)
   - [Returns Analysis](#return-analysis)
   - [Operational Analysis](#operational-analysis)
5. [Conclusions](#conclusions)

---

## Project Overview

This project analyzes transactional data from a NovaMart, a fictional e-commerce company.
And, this project focuses on using Microsoft SQL Server to explore data.
The goal is to transform raw transactional data into meaningful business insights.

---

## Business Problem

NovaMart stores large amounts of transactional data accross many fields.
However, raw transactional records alone do not provide clear information about business performance.
The company needs an analytical view of its data to find what's happening behind the data itself.

---

## Dataset Overview

| Table      | Purpose                                   |
|------------|-------------------------------------------|
| Customers  | Customer information                      |
| Orders     | Customer orders and transaction values    |
| OrderItems | Products and quantities within each order |
| Products   | Product information and prices            |
| Categories | Product categories                        |
| Payments   | Payment transactions and statues          |
| Returns    | Product return records                    |
| Shipments  | Order shipment information                |
| Suppliers  | Product supplier information              |
| Inventory  | Product stock by warehouse                |
| Warehouses | Warehouse information                     |

---

## Key Business Analysis

### Sales Performance

``` sql
-- What is the overall sales performance of successfully delivered orders?
SELECT
	COUNT(OrderID) AS TotalDeliveredOrders,
	SUM(TotalAmount) AS TotalDeliveredSales
FROM dbo.Orders
WHERE OrderStatus = 'Delivered';
```

| Total Delivered Orders | Total Delivered Sales |
| ---------------------- | --------------------- |
|                    833 |    Rp3.791.581.844,90 |

---

### Product Performance

``` sql
-- Which products generate the strongest sales performance among successfully delivered orders?
SELECT TOP 10
	p.ProductName,
	SUM(oi.Quantity) AS TotalQuantitySold,
	SUM(
		oi.Quantity
		* oi.UnitPrice
		* (1 - oi.DiscountPercent / 100.0)
	) AS TotalSales
FROM dbo.Products AS p
INNER JOIN dbo.OrderItems AS oi
	ON p.ProductID = oi.ProductID
INNER JOIN dbo.Orders AS o
	ON oi.OrderID = o.OrderID
WHERE o.OrderStatus = 'Delivered'
GROUP BY
	p.ProductID,
	p.ProductName
ORDER BY TotalSales DESC;
```

| Product                   | Total Quantity Sold | Total Sales     |
| ------------------------- | ------------------- | --------------- |
| Portable SSD Premium      |                  22 | Rp83.254.534,00 |
| LED Monitor Premium       |                  18 | Rp74.881.862,00 |
| Portable SSD Pro          |                  19 | Rp72.930.882,00 |
| LED Monitor Plus          |                  16 | Rp64.912.500,00 |
| Wireless Mouse Plus       |                  22 | Rp61.334.558,00 |
| LED Monitor Pro           |                  12 | Rp48.777.083,00 |
| LED Monitor Basic         |                  13 | Rp46.613.848,00 |
| Portable SSD Basic        |                  13 | Rp45.526.960,00 |
| Mechanical Keyboard Basic |                  18 | Rp40.394.975,00 |
| Webcam Standard           |                  12 | Rp38.928.431,00 |

---

### Category Performance

``` sql
-- Which product categories contribute the most to successfully delivered sales?
SELECT
	c.CategoryName,
	SUM(oi.Quantity) AS TotalQuantitySold,
	SUM(
		oi.Quantity
		* oi.UnitPrice
		* (1 - oi.DiscountPercent / 100)
	) AS TotalSales
FROM dbo.Categories AS c
INNER JOIN dbo.Products AS p
	ON c.CategoryID = p.CategoryID
INNER JOIN dbo.OrderItems AS oi
	ON p.ProductID = oi.ProductID
INNER JOIN dbo.Orders AS o
	ON oi.OrderID = o.OrderID
WHERE o.OrderStatus = 'Delivered'
GROUP BY
	c.CategoryID,
	c.CategoryName
ORDER BY TotalSales DESC;
```

| Category               | Total Quantity Sold | Total Sales        |
| ---------------------- | ------------------- | ------------------ |
| Electronics            |                 586 | Rp1.253.653.921,00 |
| Sports & Outdoors      |                 628 |   Rp489.537.500,00 |
| Home & Kitchen         |                 550 |   Rp463.722.450,00 |
| Automotive             |                 617 |   Rp382.049.470,00 |
| Clothing               |                 675 |   Rp293.610.539,00 |
| Toys & Games           |                 595 |   Rp257.213.980,00 |
| Pet Supplies           |                 579 |   Rp236.659.705,00 |
| Beauty & Personal Care |                 674 |   Rp207.058.352,00 |
| Books & Stationery     |                 670 |   Rp118.076.436,00 |
| Groceries              |                 672 |    Rp89.999.487,00 |

---

















