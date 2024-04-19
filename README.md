# Vendas-Pizzas-Sql-Power-BI

## Parte SQL
### A. KPI’s
***1. Receita Total:***
A soma do preço total de todos os pedidos de pizza.
![image](https://github.com/lagmagalhaes/Vendas-Pizzas-Sql-Power-BI/assets/166879716/92463c42-18bb-4258-a3b3-48b0296ac1ec)

***2. Valor Médio do Pedido:***
O valor médio gasto por pedido, calculado dividindo a receita total pelo número total de pedidos.
![image](https://github.com/lagmagalhaes/Vendas-Pizzas-Sql-Power-BI/assets/166879716/902cdf4d-bcc8-4313-a537-db11e452d85e)


***3. Total de Pizzas Vendidas:***
Soma das quantidades de todas as pizzas vendidas.
![image](https://github.com/lagmagalhaes/Vendas-Pizzas-Sql-Power-BI/assets/166879716/b06e485c-2678-4e7c-a919-e99dfcfe4618)


***4. Total de Pedidos:***
O número total de pedidos feitos.
![image](https://github.com/lagmagalhaes/Vendas-Pizzas-Sql-Power-BI/assets/166879716/0f5b51c6-42e9-48d4-a10b-49134a44491e)


***5. Média de Pizzas por Pedido:***
Quantidade média de pizzas vendidas por pedido, calculada dividindo o número 
total de pizzas vendidas pelo número total de pedidos.
![image](https://github.com/lagmagalhaes/Vendas-Pizzas-Sql-Power-BI/assets/166879716/84305f8d-9b45-4a27-a105-3dd59e1c61d7)




--B. GRÁFICOS
--1. Tendência diaria para total de pedidos:

SELECT DATENAME(DW, order_date) AS order_day,
COUNT(DISTINCT order_id) AS total_orders 
FROM pizza_sales
GROUP BY DATENAME(DW, order_date)

-- 2. Tendência mensal para total de pedidos:

select DATENAME(MONTH,
order_date) as Month_Name, 
COUNT(DISTINCT order_id) as Total_Orders
from pizza_sales
GROUP BY DATENAME(MONTH, order_date)

-- 3. Porcentagem de vendas por categoria de pizza:
SELECT pizza_category, 
CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price)from pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_category



-- 4. Porcentagem de vendas por tamanho de pizza:

SELECT pizza_size,
CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_size
ORDER BY pizza_size



-- 5. Total de pizzas vendidas por categoria de pizza:
SELECT pizza_category,
SUM(quantity) as Total_Quantity_Sold
FROM pizza_sales
WHERE MONTH(order_date) = 2
GROUP BY pizza_category
ORDER BY Total_Quantity_Sold DESC

-- 6. Os 5 mais vendidos por receita, quantidade total e total de pedidos
SELECT Top 5 pizza_name, SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue DESC


-- 7. Os 5 mais vendidos por receita, quantidade total e total de pedidos
SELECT Top 5 pizza_name, SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue ASC

-- 8. Os 5 mais vendidos por quantidade
SELECT Top 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold DESC

SELECT Top 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders DESC

SELECT Top 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders ASC
