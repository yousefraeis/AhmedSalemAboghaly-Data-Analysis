## **Lecture 1: Working with Databases in SQL**

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


## Lecture 2: 


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

