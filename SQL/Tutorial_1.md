# <center>Notebook 1</center>

## 1. Select

The **``SELECT``** statement is used to select data from a database.

Select some fields:

		SELECT column1, column2 FROM table_name;

Select all the fields:

		SELECT * FROM table_name;


The **``SELECT DISTINCT``** statement is used to return only distinct (different) values.

		SELECT DISTINCT column1, column2 FROM table_name;
		
## 2. WHERE
The **``WHERE``** clause is used to extract only those records that fulfill a specified condition.

	SELECT column1, column2 FROM table_name WHERE condition;
	
## 3. ADD, OR and NOT Operators
The WHERE clause can be combined with **``AND``**, **``OR``**, and **``NOT``** operators.	

AND Syntax

	SELECT column1, column2 FROM table_name WHERE condition1 AND condition2 AND condition3;
	
OR Syntax

	SELECT column1, column2 FROM table_name WHERE condition1 OR condition2 OR condition3;

NOT Syntax

	SELECT column1, column2 FROM table_name WHERE NOT condition1;

Combining AND, OR and NOT

	SELECT * FROM table_name WHERE column1 = 'xxx' AND (column2 = 'xxx' OR column2 = 'xxx');
	
	SELECT * FROM table_name WHERE NOT column1 = 'xxx' AND NOT column1 = 'xxx';
	
## 4. ORDER BY Keyword
The **``ORDER BY``** keyword sorts the records in ascending order by default. To sort the records in descending order, use the **``DESC``** keyword.

	SELECT column1, column2 FROM table_name ORDER BY column1, column2 DESC;
	
	SELECT * FROM table_name ORDER BY column1 ASC, column2 DESC;

## 5. INSERT INTO statement
The **``INSERT INTO``**  statement is used to insert new records in a table.

It is possible to write the INSERT INTO statement in two ways:

The first way specifies both the column names and the values to be inserted:

	INSERT INTO table_name (column1, column2, column3) VALUES (value1, value2, value3);

The second way is adding values for all the columns of the table, without specifying the column names in the SQL query.

	INSERT INTO table_name VALUES (value1, value2, value3);
	
## 6. NULL Values
A field with a **NULL** value is a field with no value.

If a field in a table is optional, it is possible to insert a new record or update a record without adding a value to this field. Then, the field will be saved with a NULL value

To test NULL value, we can use the **``IS NULL``** and **``IS NOT NULL``** operators.
	
	SELECT column1, column2 FROM table WHERE column1 IS NULL;
	
	SELECT column1, column2 FROM table WHERE column1 IS NOT NULL;
	
## 7. UPDATE Statement
The **``UPDATE``** statement is used to modify the existing records in a table.
	
	UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
	
## 8. DELETE Statement
The **``DELETE``** statement is used to delete existing records in a table.

	DELETE FROM table_name WHERE condition;

Delete all rows in a table without deleting the table.

	DELETE FROM table_name;

## 9. TOP, LIMIT or ROWNUM Clause

The **``SELECT TOP``** (**``LIMIT``** or **``ROWNUM``**) clause is used to specify the number of records to return. 

It is useful on large tables with thousands of records. Returning a large number of records can impact performance.

Database | Syntax
------------ | ------------- |
MySQL|	`SELECT column_name(s) FROM table_name WHERE condition LIMIT number;`
SQL Server| `SELECT TOP number (PERCENT) column_name(s) FROM table_name WHERE condition;`
Oracle Syntax| `SELECT column_name(s) FROM table_name WHERE ROWNUM <= number;`

## 10. MIN() and MAX() Functions

The **MIN()** function returns the smallest value of the selected column.

	SELECT MIN(column_name) FROM table_name WHERE condition;
	
The **MAX()** function returns the largest value of the selected column.

	SELECT MAX(column_name) FROM table_name WHERE condition;
	
## 11. COUNT(), AVG() and SUM() Functions

The **COUNT()** function returns the number of rows that matches a specified criteria.

	SELECT COUNT(column_name) FROM table_name WHERE condition;

The **AVG()** function returns the average value of a numeric column.
	
	SELECT AVG(column_name) FROM table_name WHERE condition;
	
The **SUM()** function returns the total sum of a numeric column.

	SELECT SUM(column_name) FROM table_name WHERE condition;
	
## 12. LIKE Operator
The **``LIKE``** operator is used in a WHERE clause to search for a specified pattern in a column.

There are two wildcards often used in conjunction with the LIKE operator:

* **%** - The percent sign represents zero, one, or multiple characters
* **_** - The underscore represents a single character

LIKE Operator | Description
------------- | -----------
	`LIKE '%a'`| Finds any values that start with "a"
	`LIKE 'a%'` | Finds any values that end with "a"
	`LIKE '%or%'` | Finds any values that have "or" in any position
	`LIKE '_r%'` | Finds any values that have "r" in the second position
	
	SELECT column1, column2 FROM table_name WHERE column1 LIKE pattern;
	
	