# **Lecture 1: Working with Databases in SQL**

#### **Using a Different Database**
If you want to switch to another database, run the following commands:

```sql
USE master;
GO
```

Then click **Execute**.

#### **Creating a Database**
To create a new database called `company`:

```sql
CREATE DATABASE company;
```

> Think of a database like an Excel workbook — it can contain many tables (similar to sheets).

#### **Renaming a Database**
To rename the database `company` to `newcompany`:

```sql
ALTER DATABASE company
MODIFY NAME = newcompany;
```

#### **Deleting a Database**
To delete the `newcompany` database:

```sql
DROP DATABASE newcompany;
```


# Lecture 2 


### **Check if a Database Supports Arabic Characters**

#### **Step-by-Step:**

1. **Right-click** on your **database name** in SQL Server Management Studio (SSMS).
2. Choose **Properties**.
3. Go to the **Options** page.
4. Find the **Collation** setting.
5. Set it to:  
   ```
   Arabic_100_CI_AS
   ```
   > This collation ensures the database supports Arabic characters and is case-insensitive (`CI`) and accent-sensitive (`AS`).

---

### **Create a Table That Supports Arabic Text**

```sql
CREATE TABLE company (
    first_name NCHAR(100) NOT NULL,
    secound_name CHAR(100),
    age FLOAT
);
```

> Note: Use `NCHAR` or `NVARCHAR` for Arabic or any Unicode characters. `N` before the data type means "National" (Unicode).

---

### **Insert Data into the Table**

```sql
INSERT INTO company (first_name, secound_name, age)
VALUES (N'samy', 'ahmed', 23);
```

> Tip: Prefix the Arabic (or any Unicode) string with **N** to ensure it is stored properly.

---

# **Working with Tables in SQL Server**

#### **1. Create a New Database**

```sql
CREATE DATABASE NewCompany;
```

#### **2. Use the New Database**

```sql
USE NewCompany;
GO
```

---

### **3. Create a Table**

```sql
CREATE TABLE Employs (
    firstN CHAR(100) NOT NULL,
    lastN CHAR(100) NOT NULL,
    age INT
);
```

---

### **4. Edit Table – Add a New Column**

```sql
ALTER TABLE Employs 
ADD email CHAR(100);
```

> Adds a new column called `email` to the `Employs` table.

---

### **5. View All Data in a Table**

```sql
SELECT * FROM Employs;
```

---

### **6. Delete a Table**

```sql
DROP TABLE Employs;
```

> Be careful — this permanently deletes the table and its data.

---

### **7. Query Data from the Table**

```sql
-- Select all rows and columns
SELECT * FROM Employs;

-- Select just the first names
SELECT firstN FROM Employs;

-- Select first names and ages
SELECT firstN, age FROM Employs;

-- Select rows where first name is 'mnal'
SELECT * FROM Employs
WHERE firstN = 'mnal';
```

> Use single quotes `' '` for string values in SQL.

---

### **8. Delete a Specific Record**

```sql
DELETE FROM Employs
WHERE firstN = 'mnal';
```

---

# **Lecture 3: Working with Data in SQL**

### ✅ **Select All Data from a Table**

```sql
USE NewCompany;
GO

SELECT * FROM Company;
```

---

### ✍️ **How to Add Data to a Table**

```sql
INSERT INTO Company (firstName, lastName, age, salary)
VALUES ('Amira', 'Yousef', 20, 10122);
```

---

### 🗑️ **How to Delete Specific Rows**

```sql
DELETE FROM Company
WHERE firstName = 'Loay';
```

---

### ✏️ **How to Update / Edit Data**

```sql
-- Change lastName where it's 'Yousef'
UPDATE Company 
SET lastName = 'Ahmed' 
WHERE lastName = 'Yousef';

-- Update age where firstName AND lastName match
UPDATE Company 
SET age = 23 
WHERE firstName = 'alaa' AND lastName = 'Magar';
```

> You can use logical operators like `AND` / `OR` in the `WHERE` clause.

---

### 🔎 **Select Specific Columns**

```sql
SELECT firstName FROM Company;

SELECT firstName, age 
FROM Company 
WHERE firstName = 'Sameh';
```

---

### 🙅‍♂️ **Select Without Repetition**

```sql
SELECT DISTINCT * 
FROM Company;
```

> `DISTINCT` doesn't remove data — it just hides duplicates in the result.

---

### 🔢 **Count Entries**

```sql
-- Count all first names
SELECT COUNT(firstName) 
FROM Company;

-- Count distinct first names (no repeats)
SELECT COUNT(DISTINCT firstName) 
FROM Company;
```

---

### 💰 **Aggregate Functions (Salary Column)**

```sql
-- Total Salary
SELECT SUM(salary) 
FROM Company;

-- Average Salary
SELECT AVG(salary) 
FROM Company;

-- Maximum Salary
SELECT MAX(salary) 
FROM Company;

-- Minimum Salary
SELECT MIN(salary) 
FROM Company;
```

---

### 🎯 **Using `IN`, `LIKE`, and `BETWEEN`**

```sql
-- Match specific values
SELECT * 
FROM Company 
WHERE firstName IN ('alaa', 'Yousef');

-- Pattern Matching with LIKE
SELECT * FROM Company WHERE firstName LIKE 'a%';   -- starts with 'a'
SELECT * FROM Company WHERE firstName LIKE '%a';   -- ends with 'a'
SELECT * FROM Company WHERE firstName LIKE '%a%';  -- contains 'a'

-- Range filter
SELECT * 
FROM Company 
WHERE age BETWEEN 23 AND 26;
```

---

### 📊 **Sorting Data**

```sql
-- Order by Salary ascending (low to high)
SELECT * 
FROM Company 
WHERE age > 23 
ORDER BY salary ASC;

-- Descending order
SELECT * 
FROM Company 
ORDER BY salary DESC;
```

---

### 📝 **SQL Comments**

```sql
-- This is a single-line comment

/* This is 
   a multi-line comment */
```
---
# **Lecture 4 **

```sql
-- Create a new database
CREATE DATABASE NewDatabase;
GO

-- Use the newly created database
USE NewDatabase;
GO

/* 
   -- Setting a Primary Key in SSMS:
   1. Open the table in Design view.
   2. Select the column (e.g., CustomerId).
   3. Right-click and choose "Set Primary Key".
   4. In the Column Properties pane, scroll to "Identity Specification".
   5. Set "Is Identity" to Yes to auto-increment.
*/

-- Creating Customers and Orders tables (Option 1: Without identity)
CREATE TABLE Customers (
    CustomersId INT NOT NULL,  -- Primary Key
    CustName CHAR(100),
    Email CHAR(100)
);

CREATE TABLE Orders (
    OrderId INT NOT NULL,      -- Primary Key
    OrderDate DATETIME,
    CustomersId INT
);

-- Alternative way (Option 2: With Identity and Primary Key set inline)
CREATE TABLE Customers (
    CustomersId INT NOT NULL PRIMARY KEY IDENTITY(1,1),  -- Auto-incrementing PK
    CustName CHAR(100),
    Email CHAR(100)
);

CREATE TABLE Orders (
    OrderId INT NOT NULL PRIMARY KEY IDENTITY(1,1),      -- Auto-incrementing PK
    OrderDate DATETIME,
    CustomersId INT,
    FOREIGN KEY (CustomersId) REFERENCES Customers(CustomersId)
);

-- Basic JOIN examples

-- Select all data from both tables individually
SELECT * FROM Company;
SELECT * FROM Salary;

-- Inner join example
SELECT * 
FROM Salary
JOIN Company 
    ON Salary.Code = Company.id_code;

-- Using aliases for better readability
SELECT S.Code, C.first_name, C.age 
FROM Salary AS S
JOIN Company AS C
    ON S.Code = C.id_code;
```
