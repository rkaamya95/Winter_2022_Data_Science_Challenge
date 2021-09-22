# Winter_2022_Data_Science_Challenge


Question 1: Given some sample data, write a program to answer the following: click here to access the required data set

On Shopify, we have exactly 100 sneaker shops, and each of these shops sells only one model of shoe. We want to do some analysis of the average order value (AOV). When we look at orders data over a 30 day window, we naively calculate an AOV of $3145.13. Given that we know these shops are selling sneakers, a relatively affordable item, something seems wrong with our analysis. 

Think about what could be going wrong with our calculation. Think about a better way to evaluate this data. 

The average order value of $3145.13 is calculated by dividing the sum of order_amount by the number of items (in the case of this dataset, it is 5000) instead of sum(total_items) and that gives an incorrect Average Order Value.

What metric would you report for this dataset?
Average Order Value : Sum(order_amount) / Sum(total_items)

What is its value?
Average Order Value (AOV) : $357.92


Question 2: For this question you’ll need to use SQL. Follow this link to access the data set required for the challenge. Please use queries to answer the following questions. Paste your queries along with your final numerical answers below.

How many orders were shipped by Speedy Express in total?

 Query : SELECT count(distinct orderid) as Total_orders_shipped from orders where shipperid in (select shipperid from shippers where shippername="Speedy Express");

Output : 
Total_orders_shipped
54


What is the last name of the employee with the most orders?

Query : 

with cte as
(select employeeid, count(orderid) as total_orders from orders group by employeeid order by total_orders desc)

select lastname from employees where employeeid in (select employeeid from cte where total_orders in (select max(total_orders) from cte))

Output :


LastName
Peacock


What product was ordered the most by customers in Germany?

Query:

with cte as
(SELECT * FROM [OrderDetails] where orderid in (select orderid from orders where customerid in (select customerid from customers where country="Germany") order by customerid) order by productid)

select p.productname, sum(a.quantity) as total_count_of_product_ordered from cte a, products p
where p.productid=a.productid
group by a.productid
order by total_count_of_product_ordered desc
limit 1


ProductName
total_count_of_product_ordered


Boston Crab Meat
160


