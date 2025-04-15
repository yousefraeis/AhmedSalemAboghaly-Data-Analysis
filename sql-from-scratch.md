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

---
