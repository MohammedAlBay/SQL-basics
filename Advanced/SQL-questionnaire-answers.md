# SQL questionnaire

## Setup
Import this [fake database content](mysqlsampledatabase.zip) into your database.

Below you will find a list of questions.

Find out the answer to each question using the dummy data in your database.

**Copy this file** (see: copy raw content) and fill in your queries + answer on the given location in each question.

## START !

### 1) How many customers do we have?
```
SELECT COUNT(*)
FROM customers
```

solution: `122`


### 2) What is the customer number of Mary Young?
```
SELECT customerNumber
FROM customers
WHERE contactFirstName = 'Mary' && contactLastName = 'young'
```

solution: `219`

### 3) What is the customer number of the person living at Magazinweg 7, Frankfurt 60528?
```
SELECT customerNumber
FROM customers
WHERE addressLine1 = 'Magazinweg 7' && city = 'Frankfurt' && postalCode = '60528'
```

solution: `247`


### 4) If you sort the employees on their last name, what is the email of the first employee?
```
SELECT email FROM employees
ORDER BY lastName
LIMIT 1
```

solution: `gbondur@classicmodelcars.com`

### 5) If you sort the employees on their last name, what is the email of the last employee?
```
SELECT email FROM employees
ORDER BY lastName desc
LIMIT 1
```

solution: `gvanauf@classicmodelcars.com`


### 6) What is first the product code of all the products from the line 'Trucks and Buses', sorted first by productscale, then by productname.
```
SELECT productCode FROM products
WHERE productLine = 'Trucks and Buses'
ORDER BY productScale, productName
LIMIT 1
```

solution: `S12_4473`

### 7) What is the email of the first employee, sorted on their last name that starts with a 't'?
```
SELECT email FROM employees
WHERE lastName LIKE 't%'
ORDER BY lastName
LIMIT 1
```

solution: `lthompson@classicmodelcars.com`


### 8) Which customer (give customer number) payed by check on 2004-01-19?
```
SELECT customerNumber FROM payments
WHERE paymentDate = DATE('2004-01-19')
```

solution: `177`

### 9) How many customers do we have living in the state Nevada or New York?
```
SELECT COUNT(*) FROM customers
WHERE state in('NV','NY')
```

solution: `7`


### 10) How many customers do we have living in the state Nevada or New York or outside the united states?
```
SELECT COUNT(*) FROM customers
WHERE state in ('NV','NY') OR country <> 'USA'
```

solution: `93`

### 11) How many customers do we have with the following conditions (only 1 query needed):  - Living in the state Nevada or New York OR - Living outside the USA or the customers and with a credit limit above 1000 dollar?
```
SELECT COUNT(*) FROM customers
WHERE (state in ('NV','NY')) OR (country <> 'USA' and creditLimit > 1000)
```

solution: `70` 


### 12) How many customers don't have an assigned sales representative?
```
SELECT COUNT(*) FROM customers
WHERE salesRepEmployeeNumber is NULL
```

solution: `22`

### 13) How many orders have a comment?
```
SELECT COUNT(*) FROM orders
WHERE comments is not NULL
```

solution: `80`


### 14) How many orders do we have where the comment mentions the word "caution"?
```
SELECT COUNT(*) FROM orders
WHERE comments LIKE '%caution%'
```

solution: `4`

### 15) What is the average credit limit of our customers from the USA? (rounded)
```
SELECT round(AVG(creditLimit)) AS 'average credit'
FROM customers
WHERE country = 'usa'
```

solution: `78103`


### 16) What is the most common last name from our customers?
```
SELECT contactLastName
FROM customers
GROUP BY contactLastName
ORDER BY COUNT(*) DESC
LIMIT 1
```

solution: `Young`

### 17) What are valid statuses of the orders?
- [x] Resolved

- [x] Cancelled

- [ ] Broken

- [x] On Hold

- [x] Disputed

- [x] In Process

- [ ] Processing

- [x] Shipped

```
SELECT DISTINCT status
FROM orders
```

solution: `shipped, resolved, cancelled, on hold, disputed, in process`


### 18) In which countries don't we have any customers?
- [ ] Austria

- [ ] Canada

- [x] China

- [ ] Germany

- [x] Greece

- [ ] Japan

- [ ] Philippines

- [x] South Korea

```
WITH countries AS (
	SELECT 'Austria' as country
	union
	SELECT 'canada'
	union
	SELECT 'china'
	union
	SELECT 'germany'
	union
	SELECT 'greece'
	union
	SELECT 'japan'
	union
	SELECT 'philippines'
	union
	SELECT 'south korea'
)
SELECT distinct country FROM countries
EXCEPT 
SELECT country FROM customers
```

solution: `china, greece, south korea`


### 19) How many orders where never shipped?
```
SELECT COUNT(*) FROM orders
WHERE STATUS <> 'shipped'
```

solution: `23` 

### 20) How many customers does Steve Patterson have with a credit limit above 100 000 EUR?
```
SELECT COUNT(*)
FROM customers
INNER JOIN employees ON customers.salesRepEmployeeNumber = employees.employeeNumber
WHERE employees.lastName = 'Patterson' AND employees.firstName = 'Steve' AND customers.creditLimit > 100000
```

solution: `3`

### 21) How many orders have been shipped to our customers?
```
SELECT COUNT(*) FROM orders
WHERE STATUS = 'shipped'
```

solution: `303`


### 22) How much products does the biggest product line have? And which product line is that?
```
SELECT COUNT(*),productLine 
from products
GROUP BY productLine
ORDER BY COUNT(*) DESC
LIMIT 1
```

solution: `38, Classic cars`

### 23) How many products are low in stock? (below 100 pieces)
```
SELECT COUNT(*) FROM products
WHERE quantityInStock < 100
```

solution: `2`

### 24) How many products have more the 100 pieces in stock, but are below 500 pieces.
```
SELECT COUNT(*) FROM products
WHERE quantityInStock between 101 and 499
```

solution: `3`


### 25) How many orders did we ship between and including June 2004 & September 2004
```
SELECT COUNT(*) FROM orders
WHERE STATUS = 'shipped' AND shippedDate BETWEEN '2004-06-01' AND '2004-09-30'
```

solution: `42`

### 26) How many customers share the same last name as an employee of ours?
```
SELECT COUNT(*) FROM customers
INNER JOIN employees ON customers.contactLastName = employees.lastName
```

solution: `9`

### 27) Give the product code for the most expensive product for the consumer?
```
SELECT productcode from products
ORDER BY msrp desc
LIMIT 1
```

solution: `S10_1949`


### 28) What product (product code) offers us the largest profit margin (difference between buyPrice & MSRP).
```
SELECT productcode FROM products
ORDER BY (msrp - buyprice) desc
LIMIT 1
```

solution: `S10_1949`

### 29) How much profit (rounded) can the product with the largest profit margin (difference between buyPrice & MSRP) bring us.
```
SELECT ROUND(msrp - buyprice) FROM products
WHERE productcode = 'S10_1949'
```

solution: `116`

### 30) Given the product number of the products (separated with spaces) that have never been sold?
```
SELECT productcode FROM products
EXCEPT
SELECT productcode FROM orderdetail
```

solution: `S18_3233`


### 31) How many products give us a profit margin below 30 dollar?
```
SELECT COUNT(*) AS profitmargin
FROM products
WHERE (msrp - buyprice) < 30
```

solution: `23`

### 32) What is the product code of our most popular product (in number purchased)?
```
SELECT productcode FROM orderdetails
GROUP BY productcode
ORDER BY sum(quantityordered) DESC
LIMIT 1
```

solution: `S18_3232`

### 33) How many of our popular product did we effectively ship?
```
SELECT SUM(quantityordered) FROM orderdetails
INNER JOIN orders ON orders.orderNumber = orderdetails.orderNumber
WHERE productcode = 'S18_3232' AND orders.STATUS = 'shipped'
GROUP BY productcode
```

solution: `1720`


### 34) Which check number paid for order 10210. Tip: Pay close attention to the date fields on both tables to solve this.  
```
SELECT checknumber FROM payments
INNER JOIN orders ON orders.customernumber = payments.customerNumber
WHERE ordernumber = 10210 AND paymentdate BETWEEN orderdate AND shippeddate
```

solution: `CI381435`

### 35) Which order was paid by check CP804873?
```
SELECT ordernumber FROM orders 
INNER JOIN payments ON orders.customerNumber = payments.customerNumber
WHERE checknumber = 'CP804873' AND paymentdate BETWEEN orderdate AND shippeddate
```

solution: `10330`

### 36) How many payments do we have above 5000 EUR and with a check number with a 'D' somewhere in the check number, ending the check number with the digit 9?
```
SELECT COUNT(*) FROM payments
WHERE amount > 5000 AND checknumber LIKE '%d%9'
```

solution: `3`


### 38) In which country do we have the most customers that we do not have an office in?
```
SELECT country FROM customers
WHERE country NOT IN (SELECT country FROM offices)
GROUP BY country
ORDER BY COUNT(*) DESC
LIMIT 1
```

solution: `Germany`

### 39) What city has our biggest office in terms of employees?
```
SELECT city FROM offices
INNER JOIN employees ON offices.officeCode = employees.officeCode
GROUP BY city
ORDER BY COUNT(*) DESC
LIMIT 1
```

solution: `San Francisco`

### 40) How many employees does our largest office have, including leadership?

```
SELECT COUNT(*) FROM offices
INNER JOIN employees ON offices.officeCode = employees.officeCode
GROUP BY city
ORDER BY COUNT(*) DESC
LIMIT 1
```

solution: `6`


### 41) How many employees do we have on average per country (rounded)?
```
WITH amountPerCountry AS (
	SELECT COUNT(*) AS average FROM offices
	INNER JOIN employees ON offices.officeCode = employees.officeCode
	GROUP BY country
)
SELECT round(AVG(average)) FROM amountPerCountry
```

solution: `5`

### 42) What is the total value of all shipped & resolved sales ever combined?
```
SELECT round(SUM(priceeach * quantityordered)) FROM orderdetails
inner join orders ON orders.orderNumber = orderdetails.orderNumber
WHERE STATUS IN ('shipped','resolved')
```

solution: `8.999.331`

### 43) What is the total value of all shipped & resolved sales in the year 2005 combined? (based on shipping date)
```
SELECT round(SUM(priceeach * quantityordered)) FROM orderdetails
inner join orders ON orders.orderNumber = orderdetails.orderNumber
WHERE STATUS IN ('shipped','resolved') AND shippeddate BETWEEN '2005-01-01' AND '2005-12-31'
```

solution: `1427945`


### 44) What was our most profitable year ever (based on shipping date), considering all shipped & resolved orders?
```
```

solution: ``

### 45) How much revenue did we make on in our most profitable year ever (based on shipping date), considering all shipped & resolved orders?
```
```

solution: ``

### 46) What is the name of our biggest customer in the USA of terms of revenue?
```
```

solution: ``


### 47) How much has our largest customer inside the USA ordered with us (total value)?
```
```

solution: ``

### 48) How many customers do we have that never ordered anything?
```
SELECT count(customerNumber) FROM customers
WHERE customernumber NOT IN (SELECT customernumber FROM orders)
```

solution: ``

### 49) What is the last name of our best employee in terms of revenue?
```
```

solution: ``


### 50) What is the office name of the least profitable office in the year 2004?
```
```

solution: ``


## Are you done? Amazing!
![](../_assets/clap-clap-clap.gif)