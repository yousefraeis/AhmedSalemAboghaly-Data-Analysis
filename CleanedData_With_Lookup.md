# **Step-by-Step Instructions for Cleaning Data and Creating a Pivot Table in Excel**

### 1. **Select All Table Cells**
- Go to your worksheet with data.
- Press `Ctrl + A` to select all data.

### 2. **Remove Duplicates**
- On the top ribbon, go to **Data** > **Remove Duplicates**.
- Select the columns you want to check for duplicates, then click **OK**.

### 3. **Create a Table (Optional but recommended)**
- With your data selected, press `Ctrl + T` to create a table.
- Ensure the "My table has headers" option is checked.

### 4. **Insert a Pivot Table**
- Go to the **Insert** tab on the ribbon.
- Click **Pivot Table**.
- Choose **New Worksheet** to insert the pivot table into a new sheet.
- Click **OK**.

### 5. **Customize Pivot Table Options**
- In the new Pivot Table sheet:
  - Right-click on the Pivot Table.
  - Choose **PivotTable Options**.
  - Go to the **Display** tab.
  - Check **Classic PivotTable layout** (if you want drag-and-drop style fields).

### 6. **Using Lookup Formulas**
- In another sheet (e.g., Sheet3), use a `LOOKUP` or `VLOOKUP` formula:
  ```excel
  =VLOOKUP(A3, TableRange, ColumnIndex, FALSE)
  ```
  - Replace `TableRange` with the actual table range.
  - `A3` is the lookup value.

### 7. **Make Sure Pivot Table Is Selected**
- Go to your Pivot Table.
- On the ribbon, under **PivotTable Analyze**, make sure the table is active.

### 8. **Show Formulas (Optional)**
- To view all formulas in a sheet:
  - Press `Ctrl + ~` (tilde key) to toggle formula view.
  - Or go to the **Formulas** tab > **Show Formulas**.

---

## 🎯 **Income Brackets & Percentages**
| **Income (C3)** | **Percent**      |
|-----------------|------------------|
| `< 10000`       | `0`              |
| `>= 10000`      | `2%`             |
| `>= 20000`      | `3%`             |
| `>= 40000`      | `4%`             |
| `>= 50000`      | **Special Case** |

---

## ✅ **Final Excel Formula**
```excel
=IF(C3<10000, 0,
 IF(C3<20000, C3*0.02,
 IF(C3<40000, C3*0.03,
 IF(C3<50000, C3*0.04,
 "Special Case"))))
```

---

## 🔍 **How It Works**
- If `C3 < 10000` → return `0`
- If between `10000` and `<20000` → 2%
- If between `20000` and `<40000` → 3%
- If between `40000` and `<50000` → 4%
- If `>= 50000` → shows **"Special Case"**

---

## 📝 **Note:**
Make sure to apply the correct income percentage based on the income slice. Use the formula to calculate the result dynamically based on the value in cell `C3`.

> **Don’t forget to name the cell that holds the percentage values** to avoid issues when copying formulas or referencing across sheets. Naming the cell (e.g., `IncPerc`) makes your formulas cleaner and less prone to errors.

---
