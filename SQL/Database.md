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


### 1. Add a **``UNIQUE``** constraint on a column when creating the table:

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

Define a **``UNIQUE``** constraint on multiple columns (In **MysSQL / SQL Server / Oracle / MS Access**):
	
	CREATE TABLE table_name (
		column1 datatype NOT NULL
		column2 datatype,
		...
		CONSTRAINT unique_constraint_name UNIQUE (column1, column2)
	);


### 2. Add a **``UNIQUE``** constraint on a column when the table is already created:

	ALTER TABLE table_name ADD UNIQUE(column1);

On multiple columns:

	ALTER TABLE table_name ADD CONSTRAINT unique_constraint_name UNIQUE (column1, column2);


### 3. Drop a UNIQUE Constraint:

**MySQL**:
	
	ALTER TABLE table_name DROP INDEX unique_constraint_name;

**SQL Server / Oracle / MS Access**

	ALTER TABLE table_name DROP CONSTRAINT unique_constraint_name;

## 10. PRIMARY KEY Constraint

The **``PRIMARY KEY``** constraint uniquely identifies each record in a table.

A table can have only **ONE** primary key; and in the table, this primary key can consist of single or multiple columns (fields).

### 1. PRIMARY KEY on CREATE TABLE

Create a **PRIMARY KEY** on one column
**SQL Server / Oracle / MS Access**:

	CREATE TABLE table_name (
		column1 datatype NOT NULL,
		column2 datatype Not NULL,
		PRIMARY KEY(column1)
	);
**MySQL**:

	CREATE TABLE table_name (
		column1 datatype NOT NULL PRIMARY KEY,
		column2 datatyoe NOT NULL
	);

Define a **PRIMARY KEY** constraint on multiple columns.

	CREATE TABLE table_name(
		column1 datatype NOT NULL,
		column2 datatyoe NOT NULL,
		CONSTRAINT PK_name PRIMARY KEY(column1, column2)
	);
	

### 2. PRIMARY KEY on ALTER TABLE
On one column:

	ALTER TABLE table_name ADD PRIMARY KEY(column1);
	
On multiple columns:

	ALTER TABLE table_name ADD CONSTRAINT PK_name PRIMARY KEY(column1, column2);

### 3. DROP a PRIMARY KEY Constraint

**MySQL**:
	
	ALTER TABLE table_name DROP PRIMARY KEY;
	
**SQL Server / Oracle / MS Access**:

	ALTER TABLE table_name DROP CONSTRAINT PK_name;


## 11. FOREIGN KEY Constraint

A **``FOREIGN KEY``** is a key used to link two tables together.

A **``FOREIGN KEY``** is a field (or collection of fields) in one table that refers to the **``PRIMARY KEY``** in another table.

The table containing the foreign key is called the child table, and the table containing the candidate key is called the referenced or parent table.

The **``FOREIGN KEY``** constraint is used to prevent actions that would destroy links between tables.

The **``FOREIGN KEY``** constraint also prevents invalid data from being inserted into the foreign key column, because it has to be one of the values contained in the table it points to.


### 1. FOREIGN KEY on CREATE TABLE

On one column:

**MySQL**:

	CREATE TABLE table_name_1 (
		column1 datatype NOT NULL,
		column2 datatype NOT NULL,
		column3 datatype,
		PRIMARY KEY(column1),
		FOREIGN KEY(column3) REFERENCES table_name_2(column3)
	);

**SQL Server / Oracle / MS Access**:

	CREATE TABLE table_name_1 (
		column1 datatype NOT NULL PRIMARY KEY,
		column2 datatype NOT NULL,
		column3 datatype FOREIGN KEY REFERENCES table_name2(column3)
	);

To allow naming and on multiple columns:

	CREATE TABLE table_name_1 (
		column1 datatype NOT NULL,
		column2 datatype NOT NULL,
		column3 datatyoe,
		PRIMARY KEY(column1),
		CONSTRAINT FK_name FOREIGN KEY(column3) REFERENCES table_name_2(column3)
	);
	
### 2. FOREIGN KEY on ALTER TABLE
On one column:

	ALTER TABLE table_name_1 ADD FOREIGN KEY(column1) REFERENCES table_name_2(column1);
	
On multiple columns:

	ALTER TABLE table_name_1 ADD CONSTRAINT FK_name FORIGN KEY(column1) REFERENCES table_name_2(column1);
	
### 3. DROP a FOREIGN KEY Constraint

**MySQL**: 
	
	ALTER TABLE table_name DROP FOREIGN KEY FK_name;
	
**SQL Server / Oracle / MS Access**:

	ALTER TABLE table_name DROP CONSTRAINT FK_name;


## 12. CHECK Constraint

The **``CHECK``** constraint is used to limit the value range that can be placed in a column.

If you define a **``CHECK``** constraint on a single column it allows only certain values for this column.

If you define a **``CHECK``** constraint on a table it can limit the values in certain columns based on values in other columns in the row.

### 1. CHECK on CREATE TABLE

On one column:

**MySQL**:
	
	CREATE TABLE table_name (
		column1 datatype NOT NULL,
		column2 datatype,
		column3 datatype,
		CHECK (column >= value)
	);
	
**SQL Server / Oracle / MS Access**:
	
	CREATE TABLE table_name (
		column1 datatype NOT NULL,
		column2 datatype,
		column3 datatype CHECK (column3 >= value)
	);
	
On multiple columns:

	CREATE TABLE table_name (
		column1 datatype NOT NULL,
		column2 datatype,
		column3 datatype,
		CONSTRAINT CHK_name CHECK (column2 > value AND column3 = value)
	);
	
### 2. CHECK on ALTER TABLE

On one column:

	ALTER TABEL table_name ADD CHECK (column1 > 18);
	
On multiple columns:
	
	ALTER TABLE table_name ADD CONSTRAINT CHK_name CHECK (column2 > value AND column3 = value);

### 3. DROP a CHECK Constraint

**MySQL**:
	
	ALTER TABLE table_name DROP CHECK CHK_name;

**SQL Server / Oracle / MS Access**:

	ALTER TABLE table_name DROP CONSTRAINT CHK_name;

## 13. DEFAULT Constraint

The **``DEFAULT``** constraint is used to provide a default value for a column.

The default value will be added to all new records IF no other value is specified.

### 1. DEFAULT on CREATE TABLE

	CREATE TABLE table_name (
		column1 datatype NOT NULL,
		column2 datatype NOT NULL
		column3 datatype DEFAULE value
	);
	
The **``DEFAULT``** constraint can also be used to insert system values, by using functions like **GETDATE()**

	CREATE TABLE table_name (
	column1 datatype NOT NULL,
	column2 datatype NOT NULL,
	column3 datatype DEFAULT GETDATE()
	);

### 2. DEFAULT on ALTER TABLE

Database | Example 
--- | ---
MySQL | ``ALTER TABLE table_name ALTER column SET DEFAULT value;``
SQL Server | ``ALTER TABLE table_name ADD CONSTRAINT df_name DEFAULT value FOR column1;``
MS Access | ``ALTER TABLE table_name ALTER COLUMN column1 SET DEFAULT value;``
Oracle | ``ALTER TABLE table_name MODIFY column1 DEFAULT value;``


### 3. DROP a DEFAULT Constraint
**MySQL**:
	
	ALTER TABLE table_name ALTER column1 DROP DEFAULT;

**SQL Server / Oracle / MS Access**:
	
	ALTER TABLE table_name ALTER COLUMN column1 DROP DEFAULT;

## 14. CREATE INDEX Statement

The **``CREATE INDEX``** statement is used to create indexes in tables.

Indexes are used to retrieve data from the database very fast. The users cannot see the indexes, they are just used to speed up searches/queries.

CREATE INDEX Syntax

	CREATE INDEX index_name ON table_name (column, column2, ...);

CREATE UNIQUE INDEX Syntax

	CREATE UNIQUE INDEX index_name ON table_name (column1, column2, ...);

DROP INDEX Statemnt

Database | Syntax
--- | ---
MySQL | `ALTER TABLE table_name DROP INDEX index_name;`
SQL Server | `DROP INDEX table_name.index_name;`
MS Access | `DROP INDEX index_name ON table_name;`

## 15. AUTO INCREMENT Field

Auto-increment allows a unique number to be generated automatically when a new record is inserted into a table.

Often this is the primary key field that we would like to be created automatically every time a new record is inserted.

Syntax for MySQL 

	CREATE TABLE table_name (
		column1 datatype NOT NULL AUTO_INCREMENT,
		column2 datatype NOT NULL,
		column3 datatype
		PRIMARY KEY (column1)
	);

To let the **``AUTO_INCREMENT``** sequence start with another value, use the following SQL statement:

	ALTER TABLE table_name AUTO_INCREMENT = 100;

## 16. Dates

**MySQL:** 

Type | Format
---  | ---
**``DATE``** | YYYY-MM-DD
**``DATETIME``** | YYYY-MM-DD HH:MI:SS
**``TIMESTAMP``** | YYYY-MM-DD HH:MI:SS
**``YEAR``** | YYYY

**SQL Server:**

Type | Format
--- | ---
**``DATE``** | YYYY-MM-DD
**``DATETIME``** | YYYY-MM-DD HH:MI:SS
**``SMALLDATETIME``** | YYYY-MM-DD HH:MI:SS
**``TIMESTAMP``** | a unique number