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
|------------------------|-----------------------|
| 833                    | Rp3.791.581.844,90    |

---

### Product Performance









