# SQL-Database
## Brazilian E-Commerce Public Dataset by Olist

This dataset was generously provided by Olist, the largest department store in Brazilian marketplaces. Olist connects small businesses from all over Brazil to channels without hassle and with a single contract. Those merchants are able to sell their products through the Olist Store and ship them directly to the customers using Olist logistics partners.
![ERD_olist (3)](https://user-images.githubusercontent.com/72763859/103566665-5b46ef80-4efd-11eb-96a1-5733fa3b799e.png)

## Database Tables
1. Customers - This table shows information about the customer and its location. Use it to identify unique customers in the orders dataset and to find the orders delivery location.

2. Order Items - This table shows data about the items purchased within each order.

3. Order Payments - This table shows data about the orders payment options.

4. Order_reviews - This table shows data about the reviews made by the customers.

5. Orders - This table show data about orders. From each order you might find all other information

6. Products - This table shows data about the products sold by Olist.

7. Sellers - This table shows data about the sellers that fulfilled orders made at Olist. Use it to find the seller location and to identify which seller fulfilled each product.

8. Product Category - Translates the productcategoryname to english.

##  Database Dependency Diagram
![Data_Dependency_Diagram](https://user-images.githubusercontent.com/72763859/103567371-a6adcd80-4efe-11eb-9c25-26ba93d8e239.png)

## SQL queries

Query 1

 •	This query shows the customer’s city and state.
 
 •	It is important to know the customer’s location in the database.
 
 • SELECT DISTINCT customer_id , customer_city, customer_state
   FROM customers;


Query 2

•	This query shows the duplicate record of order and customer.

•	This is important to know the duplication of record.

•	SELECT
    order_id, customer_id, COUNT(*)
FROM
    orders
GROUP BY
    order_id, customer_id
HAVING 
    COUNT(*) > 1

Query 3 

•	This query shows the total sum of payments.

•	To know total payments.

• SELECT SUM(payment_value)
  FROM order_payments;

Query 4
•	This query show what review id and order id has a Null in the review comment title and review comment message.

•	It helps to determine NULL in the values.
•	SELECT review_id, order_id
  FROM order_reviews
  WHERE review_comment_title && review_comment_message IS NULL




