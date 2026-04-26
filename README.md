
# 🛒 E-Commerce Dataset Analysis

> **IBM Proof of Concept (POC) · BCA Big Data Analytics · Lovely Professional University**  
> Guided by: **Ms. Gurpreet Kaur** | Course: BCA (Big Data Analytics in association with IBM)

---

## 📌 Overview

This project is a Big Data analysis of a real-world UK-based e-commerce dataset using **Apache Hive on Hadoop**. The goal was to solve 5 business problem statements using HiveQL queries, MapReduce jobs, and visualize results using MS Excel and IBM Cognos-style charts.

The dataset contains over **500,000 retail transactions** from 01/12/2010 to 09/12/2011 for a UK-based non-store online retailer.

---

## 📂 Dataset

| Attribute | Description |
|-----------|-------------|
| `InvoiceNo` | 6-digit invoice number |
| `StockCode` | Product stock code |
| `Description` | Product description |
| `Quantity` | Number of units purchased |
| `InvoiceDate` | Date and time of invoice |
| `UnitPrice` | Price per unit |
| `CustomerID` | Unique customer identifier |
| `Country` | Country of the customer |

**Source:** [Kaggle — E-Commerce Data](https://www.kaggle.com/datasets/carrie1/ecommerce-data)  
Originally from: UCI Machine Learning Repository (Dr. Daqing Chen, London South Bank University)

---

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| **Apache Hive** | SQL-like querying on Hadoop |
| **Hadoop / MapReduce** | Distributed data processing |
| **HiveQL** | Query language for data analysis |
| **Shell Script** | Automation of pipeline tasks |
| **MS Excel** | Data visualization & dashboards |

---

## ❓ Problem Statements & Solutions

### 1️⃣ Top 10 Quantities Across the Dataset
```sql
SELECT Quantity
FROM ecomer
WHERE Quantity IS NOT NULL
ORDER BY Quantity ASC
LIMIT 10;
```
**Result:** Identified extreme quantity values ranging from -74,215 to -3,100, highlighting return/cancellation patterns.

---

### 2️⃣ Bottom 10 Quantity Based on Country
```sql
SELECT Quantity, Country
FROM ecomer
ORDER BY Quantity DESC
LIMIT 10;
```
**Result:** United Kingdom dominated with values between 3,114 and 74,215 units.

---

### 3️⃣ Top 10 Unit Price in UK (Descending Order)
```sql
SELECT UnitPrice, Country
FROM ecomer
WHERE Country = 'United Kingdom'
ORDER BY UnitPrice DESC
LIMIT 10;
```
**Result:** Highest unit price was **£38,970** in the UK market.

---

### 4️⃣ Average Unit Price in France
```sql
SELECT AVG(UnitPrice) AS avg_sale_price
FROM ecomer
WHERE Country = 'France' AND UnitPrice IS NOT NULL;
```
**Result:** Average unit price in France = **£5.04**

---

### 5️⃣ Top 15 Unit Price by Description
```sql
SELECT Description, UnitPrice
FROM ecomer
ORDER BY UnitPrice DESC
LIMIT 15;
```
**Result:** "Manual" had the highest unit price at £38,970, followed by multiple AMAZON FEE entries (~£17,836).

---

## ⚙️ How to Run

### Prerequisites
- Hadoop installed and running
- Apache Hive configured
- Dataset loaded into HDFS

### Steps

```bash
# Step 1: Start Hadoop services
start-all.sh

# Step 2: Load dataset into HDFS
hdfs dfs -put ecommerce-data.csv /user/hive/warehouse/

# Step 3: Launch Hive
hive

# Step 4: Create the database and table
CREATE DATABASE ecommerce_db;
USE ecommerce_db;

CREATE TABLE ecomer (
  invNo INT,
  StockCod STRING,
  DESCRI STRING,
  Quantity INT,
  invDate STRING,
  UnitPrice FLOAT,
  CID INT,
  Country STRING
)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ','
LINES TERMINATED BY '\n'
STORED AS TEXTFILE;

# Step 5: Run the Shell Script to execute all queries
bash run_queries.sh
```

---

## 📊 Key Insights

- 🇬🇧 **United Kingdom** accounts for the largest volume of transactions
- 📦 **Negative quantities** reveal a significant number of returns/cancellations
- 💰 **Manual billing entries** had the highest unit prices (£38,970)
- 🇫🇷 **France** average unit price: ~£5.04 — competitive pricing market
- 🌍 Customers span **37+ countries** globally

---

## 🗂️ Project Structure

```
ecommerce-analysis/
│
├── data/
│   └── ecommerce-data.csv        # Raw dataset (download from Kaggle)
│
├── hive/
│   ├── create_table.hql          # Table creation script
│   ├── problem1_top10_qty.hql    # Query 1
│   ├── problem2_bottom10.hql     # Query 2
│   ├── problem3_uk_price.hql     # Query 3
│   ├── problem4_france_avg.hql   # Query 4
│   └── problem5_top15_desc.hql   # Query 5
│
├── scripts/
│   └── run_queries.sh            # Shell script to automate all queries
│
├── output/
│   └── results/                  # CSV outputs from Hive
│
├── visualizations/
│   └── dashboards/               # Excel charts and visualizations
│
└── README.md
```



---

## 📬 Contact

**Samiksha Barnwal**  
📧 [099samiksha@gmail.com](mailto:099samiksha@gmail.com)  
🐙 [github.com/wildtigress](https://github.com/wildtigress)  
💼 [linkedin.com/in/samiksha4](https://linkedin.com/in/samiksha4)

---

*Made with ❤️ using Apache Hive, Hadoop & IBM Big Data tools*
