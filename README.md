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
  <img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/understanding-the-data/images/4.png?raw=true" width="900" alt="Creating Spark Session">
</p>

<p align="center">
  <img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/understanding-the-data/images/5.png?raw=true" width="900" alt="Reading dataset using PySpark">
</p>

<p align="center">
  <img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/understanding-the-data/images/6.png?raw=true" width="900" alt="Printing schema of dataset">
</p>

### 🔹 Automated output for all datasets

<p align="center">
  <img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/understanding-the-data/images/7.png?raw=true" width="900" alt="Showing sample rows of dataset">
</p> 

<p align="center">
  <img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/understanding-the-data/images/8.png?raw=true" width="900" alt="Gemini automation code for repetitive PySpark tasks">
</p>

<p align="center">
  <img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/understanding-the-data/images/10.png?raw=true" width="900" alt="Automated schema and table preview output">
</p>

This automation improved efficiency and ensured that all datasets were inspected in a consistent way.

---

## 📊 Key Findings from Data Understanding

From the initial inspection, the following observations were identified:

- 📌 The dataset contains **9 interconnected tables** representing different parts of the Brazilian e-commerce ecosystem such as customers, orders, products, payments, sellers, and reviews.

- 🕒 Several tables include **timestamp columns** related to order lifecycle events such as:
  - `order_purchase_timestamp`
  - `order_approved_at`
  - `order_delivered_carrier_date`
  - `order_delivered_customer_date`

- 💰 Financial fields such as `price` and `freight_value` are stored as **numeric data types**, which will later allow aggregation and revenue analysis.

- 🔗 Important relational keys appear across multiple datasets, enabling joins between tables:
  - `customer_id`
  - `order_id`
  - `product_id`
  - `seller_id`

- ⚠️ Some CSV files contain **null or missing values** in certain columns (especially timestamps and optional attributes).  
  These missing values will need to be handled during the **Data Cleaning and Transformation stage** to ensure data quality and accurate analysis.

These fields will play an important role in the next stages of the project, especially for **data integration, aggregation, and analytics**.

---

2️⃣ Data Ingestion & Exploration

After understanding the dataset structure, the next step is to move the data into a distributed processing environment and begin performing large-scale exploration using Apache Spark.

This stage focuses on two main objectives:

Ingesting the raw datasets into HDFS

Exploring the data using distributed Spark processing

This workflow was implemented using the following technologies:

☁️ Google Cloud Dataproc

🗂️ Hadoop Distributed File System (HDFS)

⚡ Apache Spark (PySpark)

📓 JupyterLab on Dataproc

Using this architecture allows the project to simulate a real-world data engineering environment, where data is stored in distributed storage and processed using parallel computation.

📥 Data Ingestion to HDFS

Instead of processing the data locally, the datasets were uploaded into Hadoop Distributed File System (HDFS).

HDFS provides:

distributed storage

fault tolerance

scalable data processing

This ensures that Spark jobs can efficiently read and process data from multiple nodes in the cluster.

The ingestion process included:

Creating the HDFS directory

Uploading the CSV files to HDFS

Verifying the uploaded datasets

Reading the datasets using Spark

🔹 Uploading datasets to HDFS
<p align="center"> <img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/data-Ingestion-%26-Exploration/images/data-ingestion-to-hdfs.png?raw=true" width="900" alt="Uploading dataset to HDFS"> </p> <p align="center"> <img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/data-Ingestion-%26-Exploration/images/data-ingestion-hdfs.png?raw=true" width="900" alt="HDFS directory containing ingested datasets"> </p>

This step ensures that all datasets are stored in a distributed storage system instead of the local filesystem.

⚡ Creating the Spark Environment

Once the datasets were stored in HDFS, a Spark environment was initialized inside the Dataproc cluster.

Spark allows distributed processing across multiple worker nodes, making it suitable for handling large-scale datasets.

🔹 Starting Spark Session
<p align="center"> <img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/data-Ingestion-%26-Exploration/images/starting-spark-session.png?raw=true" width="900" alt="Starting Spark Session in Dataproc"> </p>

The Spark session initializes the Spark driver, which coordinates distributed tasks across the cluster.

📂 Reading Data from HDFS using PySpark

After initializing Spark, the datasets stored in HDFS were loaded into Spark DataFrames.

This allows distributed queries and transformations to be performed efficiently.

🔹 Reading datasets from HDFS
<p align="center"> <img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/data-Ingestion-%26-Exploration/images/reading-data-from-hdfs.png?raw=true" width="900" alt="Reading dataset from HDFS using PySpark"> </p>

Each dataset was read using:

spark.read.csv()

header=True

inferSchema=True

This automatically detects the data structure and creates Spark DataFrames for analysis.

🔎 Distributed Data Exploration (PySpark)

Once the datasets were loaded into Spark DataFrames, several data exploration tasks were performed to better understand the dataset and detect potential data quality issues.

The exploration included:

Checking dataset sizes

Identifying duplicate records

Detecting null values

Analyzing payment methods

Examining order status distribution

Identifying top-selling products

Calculating delivery time between purchase and delivery

These insights help validate the data before moving to the data cleaning and transformation stage.

📊 Data Quality Checks
🔹 Checking for Data Leakage or Missing Rows
<p align="center"> <img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/data-Ingestion-%26-Exploration/images/Data-exploration-check-data-Lekage-or-drop.png?raw=true" width="900" alt="Checking dataset row counts"> </p>

This step verifies that no data was lost during ingestion into HDFS.

🔹 Checking for Duplicate Records
<p align="center"> <img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/data-Ingestion-%26-Exploration/images/Data-exploration-check-duplicates.png?raw=true" width="900" alt="Checking duplicate records"> </p>

Duplicate checks were performed on key identifiers such as:

customer_id

order_id

product_id

This ensures data integrity before further processing.

🔹 Checking for Null Values in Columns
<p align="center"> <img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/data-Ingestion-%26-Exploration/images/Data-exploration-check-nulls-in-every-columns.png?raw=true" width="900" alt="Checking null values in dataset columns"> </p>

Null analysis helps identify columns that require data cleaning or imputation in later stages.

📈 Exploratory Analysis

In addition to data quality checks, several exploratory analyses were performed.

🔹 Most Preferred Payment Method
<p align="center"> <img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/data-Ingestion-%26-Exploration/images/Data-exploration-most-preferred-payment.png?raw=true" width="900" alt="Payment method distribution"> </p>

The analysis shows the distribution of payment types used by customers.

🔹 Order Status Distribution
<p align="center"> <img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/data-Ingestion-%26-Exploration/images/Data-exploration-Order-status-distribution.png?raw=true" width="900" alt="Order status distribution"> </p>

This analysis provides insight into how many orders were:

delivered

shipped

canceled

unavailable

processing

🔹 Top Selling Products
<p align="center"> <img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/data-Ingestion-%26-Exploration/images/data-exploration-top-selling-products.png?raw=true" width="900" alt="Top selling products analysis"> </p>

Product sales were aggregated using Spark to identify the highest revenue-generating products.

🔹 Total Delivery Time Analysis
<p align="center"> <img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/data-Ingestion-%26-Exploration/images/data-exploration-total-delivery-time.png?raw=true" width="900" alt="Delivery time analysis"> </p>

Delivery time was calculated using:

delivery_time = order_delivered_customer_date - order_purchase_timestamp

This analysis helps evaluate logistics performance and delivery delays.

🚀 Next Step

The next stage of this project will focus on:

🧹 Data Cleaning & Transformation

This includes:

handling missing values

correcting inconsistent data

transforming timestamps

preparing datasets for integration and analytics

These steps will ensure that the data is clean, reliable, and ready for large-scale analytics and data warehousing.
