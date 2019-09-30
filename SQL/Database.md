## 1. CREATE DATABASE Statement

The **``CREATE DATABASE``** statement is used to create a new SQL database.

	CREATE DATABASE database_name;

## 2. DROP DATABASE Statement

The **``DROP DATABASE``** statement is used to drop an existing SQL database.

	DROP DATABASW database_name;
	
## 3. BACKUP DATABASE for SQL Server

The **``BACKUP DATABASE``** statement is used in **SQL Server** to create a full back up of an existing SQL database.

	BACKUP DATABASE database_name TO DISK = 'filepath';

The SQL **``BACKUP WITH DIFFERENTIAL``** Statement. A differential back up only backs up the parts of the database that have changed since the last full database backup.

	BACKUP DATABASW database_name TO DISK = 'filepath' WITH DIFFERENTIAL;
	
## 4. CREATE TABLE Statement

The **``CREATE TABLE``** statement is used to create a new table in a database.

	CREATE TABLE new_table_name (
		column1 datatype,
		column2 datatype, 
		column3 datatype,
		...
	);
	
A copy of an existing table can also be created using **``CREATE TABLE``**.

The new table gets the same column definitions. All columns or specific columns can be selected.

If you create a new table using an existing table, the new table will be filled with the existing values from the old table.

	CREATE TABLE new_table_name AS SELECT column1, column2 FROM existing_table_name WHERE condition;

## 5. DROP TABLE Statement

The **``DROP TABLE``**  statement is used to drop an existing table in a database.

	DROP TABLE table_name;

The **``TRUNCATE TABLE``** statement is used to delete the data inside a table, but not the table itself.
	
	TRUNCATE TABLE table_name;

## 6. ALTER TABLE Statement

The **``ALTER TABLE``** statement is used to add, delete, or modify columns in an existing table.

**``ADD``** Column:
	
	ALTER TABLE table_name ADD column_name datatype;
	
**``DROP COLUMN``**:

	ALTER TABLE table_name DROP COLUMN column_name;

**``ALTER/MODIFY COLUMN``**:


Database |Syntax|Example
---| --- | ---
SQL Server | **``ALTER COLUMN``**| ``ALTER TABLE table_name ALTER COLUMN column name;``
My SQL|**``MODIFY COLUMN``**|  ``ALTER TABLE table_name MODIFY COLUMN column datetype;``
Oracle|**``MODIFY``**|  ``ALTER TABLE table_name MODIFY column_name datatype;``

## 7. Constraints
SQL constrains are used to specify rules for data in a table

Constraints are used to limit the type of data that can go into a table. This ensures the accuracy and reliability of the data in the table. If there is any violation between the constraint and the data action, the action is aborted.

Constraints can be column level or table level. Column level constraints apply to a column, and table level constraints apply to the whole table.

The following constraints are commonly used in SQL:

Constraint | Explanation
--- | ---
**``NOT NULL``** | Ensures that a column cannot have a NULL value
**``UNIQUE``** | Ensures that all values in a column are different
**``PRIMARY KEY``** | A combination of a **NOT NULL** and **UNIQUE**. Uniquely identifies each row in a table
**``FOREIGN KEY``** | Uniquely identifies a row/record in another table
**``CHECK``** | Ensures that all values in a column satisfies a specific condition
**``DEFAULT``** | Sets a default value for a column when no value is specified
**``INDEX``** | Used to create and retrieve data from the database very quickly


Constraints can be specified when the table is created with the **``CREATE TABLE``** statement, or after the table is created with the **``ALTER TABLE``** statement.

	CREATE TABLE table_name (
		column1 datatype constraint,
		column2 datatype constraint,
		column3 datatype constraint,
		...
	);
	

## 8. NOT NULL Constraint

By default, a column can hold NLL values. The **``NOT NULL``** constraint enforces a column to NOT accept NULL value

This enforces a field always contain a value, which means that we cannot insert a new record, or update a record without adding a value to this field.

Add NOT NULL constraint when creating the table:

	CREATE TABLE table_name (
		column1 datatype NOT NULL,
		...
	);
	
Add NOT NULL when the table is alreay created:
	
	AlTER TABLE table_name MODIFY column1 datatype NOT NULL:

## 9. UNIQUE Constraint

The **``UNIQUE``** constraint ensures that all values in a column are different.

A **``PRIMARY KEY``** constraint automatically has a **``UNIQUE``** constraint.
	
However, you can have many **``UNIQUE``** constraints per table, but only one **``PRIMARY KEY``** constraint per table.

---
Add a **``UNIQUE``** constraint on a column when creating the table:

**SQL Server / Oracle / MS Access**:
	
	CREATE TABLE table_name (
		column1 datatype NOT NULL UNIQUE,
		column2 datatype,
		...
	);
	
**MySQL:**
	
	CREATE TABLE table_name (
		column1 datatype NOT NULL
		column2 datatype,
		...
		UNIQUE (column1)
	);

Define a **``UNIQUE``** constraint on multiple columns (In MysSQL / SQL Server / Oracle / MS Access):
	
	CREATE TABLE table_name (
		column1 datatype NOT NULL
		column2 datatype,
		...
		CONSTRAINT unique_constraint_name UNIQUE (column1, column2)
	);

---
Add a **``UNIQUE``** constraint on a column when the table is already created:

	ALTER TABLE table_name ADD UNIQUE(column1);

On multiple columns:

	ALTER TABLE table_name ADD CONSTRAINT unique_constraint_name UNIQUE (column1, column2);

---	
Drop a UNIQUE Constraint:

**MySQL**:
	
	ALTER TABLE table_name DROP INDEX unique_constraint_name;

**SQL Server / Oracle / MS Access**

	ALTER TABLE table_name DROP CONSTRAINT unique_constraint_name;

