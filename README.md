# Assessment4
SQL questions

ALL questions and queries here, in the SQLFILES.txt the same queries are in there as well as the database creation.

link to SQLFIDDLE here http://sqlfiddle.com/#!18/e1cbdd/15

--1. Write a SQL query to pull all customers.

select * from customers

--2. Write a SQL query to pull all customers that have orders (no duplicates).

select *
from customers s
where 
id in (select customerid from orders)

--3. Write a SQL query to pull all customers that do not have orders.

select *
from customers s
where 
id not in (select customerid from orders)


--4. If you had to create an index on these tables, which fields would you most 
--likely index, and why?


i would place a clustered index on the customer id as both are referenced for both tables and would be used for quick lookups.


--5. Write a query that lists each customer name, email, and the number of orders 
--they have.

select Name,Email,count(o.id) as OrderCount
from customers C
left join orders o on C.id = o.customerid
group by name,email

--6. Write a query that pulls all customers that have between 2 and 5 orders.

select Name,Email,count(o.id) as OrderCount
from customers C
left join orders o on C.id = o.customerid
group by name,email
having count(o.id) >= 2 and  count(o.id) <= 5

