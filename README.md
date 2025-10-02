# Task7
# Sales Analysis Project - README

## Overview

This project demonstrates how to store, analyze, and visualize sales data using Python, SQLite, pandas, and Matplotlib. The workflow includes creating a database, inserting data, querying it, and generating a revenue bar chart.

---

## Steps

### 1. Import Libraries

```python
import pandas as pd
import sqlite3
import matplotlib.pyplot as plt
```

* pandas: For data manipulation.
* sqlite3: To connect and interact with SQLite database.
* matplotlib: To plot charts.

### 2. Create Database & Table

```python
conn = sqlite3.connect("Sales_2025.db")
cursor = conn.cursor()
cursor.execute('''CREATE TABLE IF NOT EXISTS sales_datasets(...)''')
```

* Connects to an SQLite database `Sales_2025.db`.
* Creates a table `sales_datasets` if it doesn’t exist.

### 3. Insert Data

```python
cursor.executemany("INSERT INTO sales_datasets ...", data)
conn.commit()
```

* Inserts multiple product sales records into the table.
* Commits changes to save them permanently.

### 4. Query & Load Data

```python
query = """
SELECT product,
       SUM(quantity) AS total_qty,
       SUM(quantity * price) AS revenue
FROM sales_datasets
GROUP BY product
"""
df = pd.read_sql_query(query, conn)
```

* Uses SQL to calculate total quantity sold and total revenue per product.
* Loads the result into a pandas DataFrame.

### 5. Plot Revenue Bar Chart

```python
df.plot(kind="bar", x="product", y="revenue", legend=False)
plt.xlabel("Product")
plt.ylabel("Revenue (₹)")
plt.title("Revenue by Product")
plt.tight_layout()
plt.savefig("sales_chart.jpg")
plt.show()
```

* Creates a bar chart of revenue by product.
* Adds labels and title.
* Saves the chart as `sales_chart.jpg`.
* Displays the chart on screen.

### 6. Notes

* `conn.close()` should be called to actually close the database connection.
* `plt.savefig()` is called before `plt.show()` to ensure the chart is saved properly.

---

## Summary

This workflow allows you to:

* Store sales data in SQLite.
* Summarize total quantity and revenue per product.
* Visualize revenue by product using a bar chart.

The generated chart and summarized DataFrame can be used for reports and presentations.
