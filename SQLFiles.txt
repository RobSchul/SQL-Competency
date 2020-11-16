# Assessment4
SQL questions

ALL questions and queries here, in the SQLFILES.txt the same queries are in there as well as the database creation.

link to SQLFIDDLE here http://sqlfiddle.com/#!18/e1cbdd/15

--1. Write a SQL query to pull all customers.

SELECT * FROM customers

--2. Write a SQL query to pull all customers that have orders (no duplicates).


SELECT distinct(c.name), c.address,c.email FROM customers c
left join orders o on c.id = o.customerid
WHERE o.id is not  null

OR you can do 

SELECT *
FROM customers 
WHERE 
id IN (select customerid from orders)


--3. Write a SQL query to pull all customers that do not have orders.

SELECT distinct(c.name), c.address,c.email FROM customers c
left join orders o on c.id = o.customerid
WHERE o.id is  null

or you can do 

SELECT *
FROM customers 
WHERE 
id NOT IN (select customerid from orders)


--4. If you had to create an index on these tables, which fields would you most 
--likely index, and why?


i would place a clustered index on the customer id as both are referenced for both tables and would be used for quick lookups.


--5. Write a query that lists each customer name, email, and the number of orders 
--they have.

SELECT Name,Email,count(o.id) as OrderCount
FROM customers C
LEFT JOIN orders o on C.id = o.customerid
GROUP BY name,email

--6. Write a query that pulls all customers that have between 2 and 5 orders.

SELECT Name,Email,count(o.id) as OrderCount
FROM customers C
LEFT JOIN orders o on C.id = o.customerid
GROUP BY name,email
HAVING count(o.id) >= 2 and  count(o.id) <= 5

