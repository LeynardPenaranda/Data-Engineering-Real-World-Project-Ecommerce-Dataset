# 🛒 Data Engineering Real-World Project: E-Commerce Dataset

Welcome to this **Data Engineering portfolio project** built using the **Brazilian E-Commerce Public Dataset by Olist**. 🚀  
This repository documents a step-by-step data engineering workflow, from **understanding raw data** to **distributed ingestion, transformation, optimization, and data serving**.

This project is designed to showcase practical skills in:

- 📂 Data Understanding  
- ⚡ Data Ingestion & Exploration  
- 🧹 Data Cleaning & Transformation  
- 🔗 Data Integration & Aggregation  
- 🚀 Process Optimization  
- 📊 Data Serving  

---

## 📌 Dataset Used

This project uses the **Brazilian E-Commerce Public Dataset by Olist**, which contains real-world e-commerce data such as:

- 👥 Customers  
- 📦 Orders  
- 🛍️ Order Items  
- 💳 Payments  
- ⭐ Reviews  
- 🏷️ Products  
- 🏪 Sellers  
- 🌍 Geolocation  
- 📝 Product Category Translation  

These datasets are interconnected and provide a strong foundation for building a complete data engineering pipeline.

---

# 1️⃣ Data Understanding

The first step of the project is to understand the **structure, schema, and contents** of the dataset before building the pipeline.

At this stage, I used **Google Colab** with **PySpark** to:

- Upload and extract the dataset
- Read CSV files into Spark DataFrames
- Create a new `SparkSession`
- Print the schema of each dataset
- Preview sample records
- Automate repetitive dataset inspection using **Gemini**

This step is important because it helps identify:

- the available tables
- column names and data types
- possible keys for joining datasets
- timestamp and numeric fields
- the overall structure of the e-commerce data

---

## 📂 Uploading the Dataset to Google Colab

The initial exploration was performed in **Google Colab**.  
The dataset was first downloaded and extracted into the Colab working directory.

### 🔹 Downloading the dataset
<p align="center">
  <img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/understanding-the-data/images/1.png?raw=true" width="900" alt="Downloading dataset in Google Colab">
</p>

### 🔹 Extracting the dataset
<p align="center">
  <img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/understanding-the-data/images/2.png?raw=true" width="900" alt="Extracting dataset in Google Colab">
</p>

### 🔹 Inspecting extracted files
This step verifies that all CSV files were successfully extracted.

<p align="center">
  <img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/understanding-the-data/images/3.png?raw=true" width="900" alt="Listing extracted CSV files">
</p>

### 📌 Extracted CSV files include:
- `olist_customers_dataset.csv`
- `olist_geolocation_dataset.csv`
- `olist_order_items_dataset.csv`
- `olist_order_payments_dataset.csv`
- `olist_order_reviews_dataset.csv`
- `olist_orders_dataset.csv`
- `olist_products_dataset.csv`
- `olist_sellers_dataset.csv`
- `product_category_name_translation.csv`

---

## 🤖 Automating Repetitive Dataset Inspection with Gemini

Since the Olist dataset contains multiple CSV files, manually repeating the same steps for every file would be inefficient.

To make the workflow faster, I used **Gemini** to help generate a script that automates the repetitive tasks. The script:

- scans the dataset directory
- finds all CSV files
- loads each file into a Spark DataFrame
- prints the schema
- shows sample rows for each table

### 🔹 Gemini-assisted automation code
<p align="center">
  <img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/understanding-the-data/images/8.png?raw=true" width="900" alt="Gemini automation code for repetitive PySpark tasks">
</p>

### 🔹 Automated output for all datasets
<p align="center">
  <img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/understanding-the-data/images/4.png?raw=true" width="900" alt="Creating Spark Session">
</p>

<p align="center">
  <img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/understanding-the-data/images/5.png?raw=true" width="900" alt="Reading dataset using PySpark">
</p>

<p align="center">
  <img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/understanding-the-data/images/6.png?raw=true" width="900" alt="Printing schema of dataset">
</p>

<p align="center">
  <img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/understanding-the-data/images/7.png?raw=true" width="900" alt="Showing sample rows of dataset">
</p> 

<p align="center">
  <img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/understanding-the-data/images/10.png?raw=true" width="900" alt="Automated schema and table preview output">
</p>

This automation improved efficiency and ensured that all datasets were inspected in a consistent way.

---

## 📊 Key Findings from Data Understanding

From the initial inspection, the following observations were identified:

- 📌 The dataset contains **9 interconnected tables**
- 🕒 Several tables include **timestamp columns** related to order purchase, approval, shipping, and delivery
- 💰 Financial fields such as `price` and `freight_value` are stored as numeric values
- 🔗 Important keys appear across multiple datasets, including:
  - `customer_id`
  - `order_id`
  - `product_id`
  - `seller_id`

These fields will play an important role in the next stages of the project, especially for **data integration, aggregation, and analytics**.

---

# 2️⃣ Data Ingestion & Exploration

In the next stage of the project, the raw datasets will be ingested into a **distributed processing environment**.

This phase will use:

- ☁️ **Google Cloud Dataproc**
- 🗂️ **Hadoop Distributed File System (HDFS)**
- ⚡ **Spark Cluster Computing**

### 🏗️ Planned Cluster Architecture
- **Master Node** – responsible for cluster coordination and job scheduling
- **Worker Nodes** – responsible for parallel data processing and execution

Using a distributed architecture makes it possible to process large datasets more efficiently and prepare the project for scalable data engineering workflows.

### 📌 This next step will focus on:
- uploading datasets to **HDFS**
- configuring the **Dataproc cluster**
- using **master and worker nodes**
- running distributed Spark jobs
- performing large-scale data exploration

---
