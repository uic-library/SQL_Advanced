---
title: "Selection Queries"
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

## Quick Review

- SELECT
- WHERE
- DISTINCT
- ORDER BY

## NULL

The NULL function can be used in the WHERE clause to identify rows which have null values. For example, consider the below “person” table.

#### Syntax
```sql
SELECT column
FROM table_name
WHERE column IS NOT NULL
```
#### Example

```sql
SELECT CustomerName, ContactName, Address
FROM Customers
WHERE Address IS NOT NULL;
```

![SQ1](../fig/SQ1.JPG)

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
![SQ2](../fig/SQ2.JPG)

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
FROM Customers
WHERE CustomerName LIKE 'a%'
```
![SQ3](../fig/SQ3.JPG)
![SQ4](../fig/SQ4.JPG)

## SUBQUERY

A  subquery  is  also  a  query,  but the  output  of  the  subquery  is  used  as  input  to  another query to fetch the necessary results. A subquery is always enclosed inside a parenthesis ().

For example, we can fetch the maximum value in a column using he below query

```sql
SELECT MAX(price) FROM Products
```
![SQ5](../fig/SQ5.JPG)

The result from the above query can be used as input to another query to filter out the particular rows matching the above result.
```sql
SELECT ProductID, ProductName, Unit, Price
From Products
WHERE price = (SELECT MAX(price) FROM Products)
```
![SQ6](../fig/SQ6.JPG)

## IN

When  the  results  of  a  subquery has a  single  value  we  can  use  the  equal  to  (=)  sign  to match the values. When the subquery has more than one value in it’s result we can use the IN function. The IN functions checks if the results of the primary query match any one of the results of the subquery.

Consider the below two tables:
PRODUCTS – Contains details about the various products in a store
ORDERS – Contains details about the various orders, one line per product per order

![SQ7](../fig/SQ7.JPG)

In order to select all the OrderID which contains a product whose price is greater than 50:

Step 1 : Select the ProductID from PRODUCTS table whose price is greater than 50

```sql
SELECT ProductID FROM Products
Where Price > 50
```
![SQ8](../fig/SQ8.JPG)

Step 2 : Select all records from ORDERS table where the ProductID contains any one of the values present above

```sql
SELECT *
From OrderDetails
WHERE ProductID IN (SELECT ProductID FROM Products Where Price > 50)
```
![SQ9](../fig/SQ9.JPG)

{% include links.md %}
