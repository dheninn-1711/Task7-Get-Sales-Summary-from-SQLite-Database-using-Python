# 📊 SQL Sales Data Analysis

## 🎯 Objective
Use `SQL` inside Python to pull simple sales info (like total quantity sold, total revenue), and display it using basic print statements and a simple bar chart.

---

## 🧾 Overview

This project demonstrates how to use **SQLite** for managing sales data, perform data analysis using **SQL queries**, and visualize the results using **Python libraries** such as **Pandas** and **Matplotlib**.

The notebook includes:
- Creating an SQLite database
- Inserting sample sales data
- Querying the data using `SQL`
- Generating visualizations for analysis

---

## 📚 Table of Contents

- Installation
- Usage
- Features
- Data Structure
- Sample Data
- Visualizations
- License

---

## 🛠️ Installation

To run this notebook, ensure you have the following installed:

- Python 3.x
- Jupyter Notebook

---

### Required Python Libraries

- `sqlite3`
- `pandas`
- `matplotlib`

---

▶️ Usage
1. Clone the repository or download the notebook file (`SQL_Sales_data.ipynb`).
2. Open the Jupyter Notebook:

```bash
jupyter notebook SQL_Sales_data.ipynb
```

3. Run the cells sequentially to:
  - Connect with the database
  ```python
  # Create connection and Connect to SQLite database
  conn = sqlite3.connect("sales_data.db")
  cursor = conn.cursor()
  cursor
  ```
  - Create sales table
  ```python
  # Create a new 'sales' table
  cursor.execute("""
  CREATE TABLE sales (
    id INTEGER PRIMARY KEY,
    product TEXT,
    quantity INTEGER,
    price REAL
  )
  """)
  ```
  - Insert sales data
  ```python
  # Sample data with products and categories
  sample_data = [
    ("Apple", 10, 0.5),
    ("Banana", 5, 0.2),
    ("Orange", 8, 0.3),
    ("Apple", 6, 0.5),
    ("Banana", 9, 0.2)
  ]

  # Insert data
  cursor.executemany("INSERT INTO sales (product, quantity, price) VALUES (?, ?, ?)",sample_data)
  ```
  - Import pandas to query the database and matplotlib for visuals
  ```python
  import pandas as pd
  import matplotlib.pyplot as plt
  ```
  - Query the data using SQL
  ```python
  # SQL query to get total quantity and revenue per product
  query = """
  SELECT product, 
       SUM(quantity) AS total_qty, 
       SUM(quantity * price) AS revenue 
  FROM sales 
  GROUP BY product
  """
  ```
  - Read queries into a dataframe and display
  ```python
  # Read query results into a DataFrame
  df = pd.read_sql_query(query, conn)
  conn.close()
  # Display the DataFrame
  print("Sales Summary:")
  print(df)
  ```
  - Generate visual summaries with bar charts
  ```python
  # Basic bar chart for revenue by product
  df.plot(kind='bar', x='product', y='revenue', legend=False, color='skyblue')
  plt.title("Revenue by Product")
  plt.xlabel("Product")
  plt.ylabel("Revenue")
  plt.tight_layout()
  plt.savefig("sales_chart.png")  # Optional: saves chart as PNG
  plt.show()
  ```
4. For adding more products and a category column
  - Start with a new connection
  ```python
  # Always start with a new connection
  conn1 = sqlite3.connect("sales_data.db")
  cursor1 = conn1.cursor()
  ```
  - Drop the existing table
  ```python
  # Drop table if exists (for clean run in notebook)
  cursor1.execute("DROP TABLE IF EXISTS sales")
  ```
  - Create a updated sales table with category column
  ```python
  # Create the updated 'sales' table with category
  cursor1.execute("""
  CREATE TABLE sales (
    id INTEGER PRIMARY KEY,
    product TEXT,
    category TEXT,
    quantity INTEGER,
    price REAL
  )
  """)
  ```
  - Insert updated sales data
  ```python
  # Insert expanded product data with categories
  sample_data = [
    ("Apple", "Fruits", 10, 0.5),
    ("Banana", "Fruits", 5, 0.2),
    ("Orange", "Fruits", 8, 0.3),
    ("Apple", "Fruits", 6, 0.5),
    ("Banana", "Fruits", 9, 0.2),
    ("Broccoli", "Vegetables", 4, 0.8),
    ("Carrot", "Vegetables", 7, 0.6),
    ("Spinach", "Vegetables", 5, 0.9),
    ("Milk", "Dairy", 10, 1.5),
    ("Cheese", "Dairy", 3, 2.5),
    ("Yogurt", "Dairy", 6, 1.2),
    ("Bread", "Bakery", 8, 1.0),
    ("Croissant", "Bakery", 4, 1.8)
  ]

  # Insert data
  cursor1.executemany("INSERT INTO sales (product, category, quantity, price) VALUES (?, ?, ?, ?)",sample_data)
```
  - Now query with category and continue the same process as mentioned in step 3.
 
---

## ✨ Features
  - Database Creation: Initializes an SQLite database and a `sales` table.
  - Data Insertion: Adds multiple rows of sample sales data with categories.
  - SQL Querying: Calculates total quantity sold and total revenue per product.
  - Data Visualization: Produces bar charts to visually represent revenue by product and category.

---

## 🧱 Data Structure
### Table: `sales`
| Column   | Type    | Description             |
|----------|---------|-------------------------|
| `id`       | INTEGER | Primary key             |
| `product` | TEXT    | Name of the product     |
| `category` | TEXT    | Category of the product |
| `quantity` | INTEGER | Units sold              |
| `price`    | REAL    | Price per unit          |

---

## 🍎 Sample Data
The inserted data includes products from four categories:

- Fruits: Apple, Banana, Orange
- Vegetables: Broccoli, Carrot, Spinach
- Dairy: Milk, Cheese, Yogurt
- Bakery: Bread,  Croissant

Each entry includes quantity and unit price, allowing for revenue calculation using `quantity * price`.

---

## 📈 Visualizations
The notebook generates the following bar charts using `matplotlib`:

1. Revenue by Product

   ![download](https://github.com/user-attachments/assets/65b7a7c7-05f6-40b4-872d-f3b8b64393b7)

      A bar chart showing the total revenue generated by each individual product.

2. Revenue by Product (Grouped by Category)

   ![download](https://github.com/user-attachments/assets/1c37f0d9-5402-4226-99c5-cde838b6429e)


      A more detailed view showing revenue categorized by product type (Fruits, Vegetables, Dairy, Bakery).

---

## 📄 License
This project is provided for educational and learning purposes. You are free to use, modify, and share with proper attribution.
