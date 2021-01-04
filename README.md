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
  
  Query 5
•	This query selects records that have matching values in both tables.

•	It shows the record of joining two tables.

•	SELECT customers.customer_id, customers.customer_unique_id, customers.customer_city
FROM customers
INNER JOIN orders ON customers.customer_id = orders.customer_id
ORDER BY orders.order_status;

Query 6
•	The operator OR displays a record if any of the conditions separated by OR is TRUE.

•	It is used to combine multiple conditions

•	SELECT payment_type
 FROM order_payments
 WHERE payment_type='voucher' OR payment_type='credit_card';
 
 Query 7
 
•	The AND operator displays a record if all the conditions separated by AND are TRUE.

•	It is used for combining more than one condition together.

•	SELECT customer_id
FROM customers
WHERE customer_city='sao paulo' AND customer_state='SP';

Query 8

•	This query count those records where record review field holds duplicate/triplicates (or more) data.

•	It helps to count duplicate data in specific table. 

•	SELECT review_id, COUNT( review_score ) x
 FROM order_reviews
 GROUP BY review_score
 HAVING x >1
 
 Query 9
 
 •	This query assigns a rank to each row within a partition of a result set.
 
 •	It helps to rank each row.
 
 •	SELECT order_id,
       payment_type,
       payment_value,
       ROW_NUMBER() OVER(ORDER BY payment_value)
       RowNumber
       FROM order_payments

  Query 10
  
•	It distributes rows of an ordered partition into a specified number of approximately equal groups, or buckets.

•	It assigns each group a bucket number starting from one

•	SELECT payment_value, 
       NTILE(3) OVER(ORDER BY payment_value DESC) Rank
       FROM order_payments
       ORDER BY payment_value;

 Query 11
 
 •	The BETWEEN operator selects values within a given range. The values can be numbers, text, or dates.

 •	This query used s used to compare a range of values.
 
 •	SELECT order_id , product_id , seller_id
FROM order_items
WHERE shipping_limit_date BETWEEN '2017-01-01' AND '2017-12-31'










