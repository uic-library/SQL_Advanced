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




{% include links.md %}
