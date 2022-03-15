---
title: "Introduction"
teaching: 0
exercises: 0
questions:
- "Key question (FIXME)"
objectives:
- "First learning objective. (FIXME)"
keypoints:
- "First key point. Brief Answer to questions. (FIXME)"
---
FIXME

## GROUP BY & COUNT

The GROUP BY function is used to group (or) combine similar entries in one column into a  single  record.  This  function  helps  identify  all  the  unique  values  under  a  column  and  helps provides  statistical  results  based  on  the  combined  aggregation  function  (discussed  next).  The GROUP BY function is generally combined with an aggregate function and one such function is COUNT. The COUNT function when used in combination with GROUP BY provides the count of number of times each vale appears in a column.

#### Syntax
```sql
SELECT column_to_group_by, AGGREGATE_FUNCTION(column),...................
FROM table_name
GROUP BY column_to_group_by
```

#### Example
Consider the below CUSTOMERS table with a few sample records

FIXME -  a1.jpg

```sql
SELECT Country, Count(CustomerID) AS CT
FROM Customers
GROUP BY Country
ORDER BY 2 DESC
```
FIXME -  a2.jpg

## AGGREGATE FUNCTIONS

The aggregate functions are generally used in combination with the GROUP BY function to perform the required aggregation function on the required column. The various aggregation functions are:

* COUNT()

* MAX()

* MIN()

* SUM()

* AVG()

#### Syntax
```sql
SELECT column_to_group_by, AGGREGATE_FUNCTION(column),...................
FROM table_name
GROUP BY column_to_group_by
```
#### Example
Consider the below PRODUCTS table with a few sample records
FIXME -  a3.jpg

```sql
SELECT CategoryID, SUM(Price) AS Sum_Price, MAX(Price) AS Max_Price, COUNT(Price) as CT
FROM Products
GROUP BY 1
```
FIXME -  a4.jpg

## HAVING

The HAVING function performs a similar function as WHERE function and helps to filter out data in the result. The AGGREGATE functions cannot be used in WHERE clause and can only be  used  in  the HAVING clause.  Thus HAVING  clause  is  generally  preceded  by  the GROUP  BY function.

FIXME -  a5.jpg
#### Syntax
```sql
SELECT column
FROM table_name
GROUP BY column
HAVING condition
```
#### Example

```sql
SELECT CategoryID, SUM(Price) AS Sum_Price
FROM Products
GROUP BY 1
```
FIXME -  a6.jpg

```sql
SELECT CategoryID, SUM(Price) AS Sum_Price
FROM Products
GROUP BY 1
HAVING SUM(Price) > 300
```
FIXME -  a7.jpg

## CASE

The CASE function/clause is used to perform an action based on a condition(s).It is similar to SWITCH CASE statement in programming languages

#### Syntax
```sql
SELECT column1, column2,
CASE WHEN condition1 THEN action1
WHEN condition2 THEN action2
ELSE action3 END
FROM table_name
```
#### Example

```sql
SELECT CategoryID,
CASE WHEN CategoryID < 4 THEN "Less than 4"
WHEN CategoryID = 4 THEN "Equal to 4"
ELSE "Greater than 4" END AS ID_Text
FROM Categories
```
FIXME -  a8.jpg

## IF (MySQL)

The IF functions is similar to the CASE function but performs only one of two actions based on a condition. If the condition is true then one action is performed else it automatically performs the other action.

Note: The IF function is available in MySQL and not the standard SQL language

#### Syntax
```sql
SELECT IF(condition, action_if_condition_true, action_if_condition_false)
FROM table_name
```
#### Example

```sql
SELECT DISTINCT Quantity, IF(Quantity>4, "MORE", "LESS") AS Quantity_String
FROM OrderDetails
```
FIXME -  a9.jpg

## NULL ----FIX ME

The NULL function can be used in the WHERE clause to identify rows which have null values. For example, consider the below “person” table.

#### Syntax
```sql
SELECT column
FROM table_name
WHERE column IS NOT NULL
```
#### Example

```sql
SELECT *
FROM Persons
```

## BETWEEN

The BETWEEN function is used to specify a range of values. Both the start and end values are inclusive in the range. It can be used along with numbers, text, or dates.

#### Syntax
```sql
SELECT column(s)...................
FROM table_name
WHERE column_to_filter_on BETWEENs tart_range AND end_range
```
#### Example

```sql
SELECT ProductID, ProductName, Price
FROM Products
WHERE Price BETWEEN 10 AND 14
ORDER BY 3
```
FIXME -  result

## LIKE

The LIKE function is used to search the columns using the specified pattern.
• % - Multiple characters
• _ - Single Character Syntax

#### Syntax
```sql
SELECT column(s)...................
FROM table_name
WHERE column_to_filter_on LIKE pattern
```
#### Example

```sql
SELECT CustomerID, CustomerName
FROM Coustomers
WHERE CustomerName LIKE 'a%'
```
FIXME -  result
FIXME - other commands

## SUBQUERY

A  subquery  is  also  a  query,  but the  output  of  the  subquery  is  used  as  input  to  another query to fetch the necessary results. A subquery is always enclosed inside a parenthesis ().

For example, we can fetch the maximum value in a column using he below query

```sql
SELECT MAX(price) FROM Products
```
FIXME -  result

The result from the above query can be used as input to another query to filter out the particular rows matching the above result.
```sql
SELECT ProductID, ProducName, Unit, Price
From prodcuts
WHERE price = (SELECT MAX(price) FROM Products)
```
FIXME -  result

## IN

When  the  results  of  a  subquery has a  single  value  we  can  use  the  equal  to  (=)  sign  to match the values. When the subquery has more than one value in it’s result we can use the IN function. The IN functions checks if the results of the primary query match any one of the results of the subquery.

Consider the below two tables:
PRODUCTS – Contains details about the various products in a store
ORDERS – Contains details about the various orders, one line per product per order

FIXME - Products table
FIXME - Orders table

In order to select all the OrderID which contains a product whose price is greater than 50:

Step 1 : Select the ProductID from PRODUCTS table whose price is greater than 50

```sql
SELECT ProductID FROM Products
Where Price > 50
```
FIXME -  result

Step 2 : Select all records from ORDERS table where the ProductID contains any one of the values present above

```sql
SELECT *
From OrderDetails
WHERE ProductID IN (SELECT ProductID FROM Products Where Price > 50)
```
FIXME -  result

## WINDOW FUNCTIONS

The window function is similar to an aggregate function, but it splits (partitions) the data into multiple groups based on the query and then performs an aggregation (or) function on these segments and returns a value for each row in the table.

FIXME - Image

The window function is used mostly in the select statement, partitions the data and perform some function across each partition. Some common window functions are:
•OVER
•ROW_NUMBER()
•RANK()
•DENSE_RANK()

#### Syntax
```sql
SELECT column(s), FUNCTION(column) OVER(PARTITION BY column ORDER BY column) FROM table_name
```

For example, consider a table q1 sales which has quarter1 sales details of a company. To find the average sales of the entire quarter:
FIXME - Image

## OVER

The over function helps to print the  result  of the  aggregate function  for each  record in the final output. Thus, the final output is not just one row which gives the aggregation result, but rather the entire table selected along with a new column where the aggregation result is printed once for each row.

FIXME - Image

Thus, the overall average of the sales column has been calculated and the result is presented in a new column called “avgsales”. All the records in this column comprise of the same value which is the average sales seen in the previous query.

## PARTITIONBY

The PARTITIONBY function is used to split the data into multiple partitions and then perform the aggregation function on each of these partitions.

FIXME - Image

In the above example, the dataset is partitioned based on dealer_id.

FIXME - Image

## ORDER BY

The ORDER BY clause helps to order the results in ascending or descending order inside each partition.

FIXME - Image

{% include links.md %}
