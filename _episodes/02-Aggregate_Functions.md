---
title: "Aggregate Function"
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

![AF1](../fig/AF1.JPG)

```sql
SELECT Country, Count(CustomerID) AS CT
FROM Customers
GROUP BY Country
ORDER BY 2 DESC
```
![AF2](../fig/AF2.JPG)

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
![AF3](../fig/AF3.JPG)

```sql
SELECT CategoryID, SUM(Price) AS Sum_Price, MAX(Price) AS Max_Price, COUNT(Price) as CT
FROM Products
GROUP BY 1
```
![AF4](../fig/AF4.JPG)



{% include links.md %}
