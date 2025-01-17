
# 🍕 Pizza Orders Analysis Report

Welcome to the Pizza Orders Analysis project! This repository contains a comprehensive SQL analysis of pizza orders, utilizing data from `orders.csv`, `order_details.csv`, `pizza.csv`, and `pizza_type.csv`. The project aims to derive key insights from the data, such as the top 3 most ordered pizza types based on revenue for each pizza category.

## 📝 Overview

This project demonstrates advanced SQL querying techniques to analyze pizza orders and derive valuable business insights. The analysis was performed using MySQL Workbench and the results are documented in a detailed PDF report.

## 📖 Description

The data used in this analysis comes from four main CSV files:
- **orders.csv**: Contains order details including order ID, date, and time.
- **order_details.csv**: Contains detailed information about each order, including the quantity of each pizza ordered.
- **pizza.csv**: Contains information about each pizza, including its ID and price.
- **pizza_type.csv**: Contains information about pizza types, including category and name.

The main objective of this analysis is to identify the top-performing pizza types within each category based on revenue.
![Screenshot 2024-08-04 180017](https://github.com/user-attachments/assets/f0a6fc13-0c6d-4723-80cf-3a3c07f7c0d1)
![Screenshot 2024-08-04 180039](https://github.com/user-attachments/assets/efe6acab-8614-4006-a9f3-32bfefb1972c)

## 📊 Key Insights

### Top 3 Most Ordered Pizza Types by Revenue for Each Category
### Provided insights that can help in making informed business decisions related to menu optimization and marketing strategies

The following SQL query was used to determine the top 3 most ordered pizza types by revenue for each category:

```sql
SELECT category, name, revenue
FROM (
    SELECT 
        pizza_types.category, 
        pizza_types.name, 
        SUM(order_details.quantity * pizzas.price) AS revenue,
        RANK() OVER (PARTITION BY pizza_types.category ORDER BY SUM(order_details.quantity * pizzas.price) DESC) AS rn
    FROM 
        pizza_types
    JOIN 
        pizzas ON pizza_types.pizza_type_id = pizzas.pizza_type_id
    JOIN 
        order_details ON order_details.pizza_id = pizzas.pizza_id
    GROUP BY 
        pizza_types.category, pizza_types.name
) AS ranked_pizzas
WHERE rn <= 3;'''


