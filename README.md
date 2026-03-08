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

# 2️⃣ Data Ingestion & Exploration

After understanding the dataset structure, the next step is to move the data into a **distributed processing environment** and begin performing **large-scale exploration using Apache Spark**.

This stage focuses on two main objectives:

- 📥 **Ingesting the raw datasets into HDFS**
- 🔎 **Exploring the data using distributed Spark processing**

---

## ⚙️ Technologies Used

This workflow was implemented using the following technologies:

- ☁️ **Google Cloud Dataproc**
- 🗂️ **Hadoop Distributed File System (HDFS)**
- ⚡ **Apache Spark (PySpark)**
- 📓 **JupyterLab on Dataproc**

Using this architecture allows the project to simulate a **real-world data engineering environment**, where:

- data is stored in **distributed storage**
- data processing is executed using **parallel computation**
- large datasets can be handled **efficiently and reliably**

---

# 📥 Data Ingestion to HDFS

Instead of processing the data locally, the datasets were uploaded into **Hadoop Distributed File System (HDFS)**.

### 📌 HDFS provides:

- 🗂️ **Distributed storage**
- 🛡️ **Fault tolerance**
- ⚡ **Scalable data processing**

This ensures that **Spark jobs can efficiently read and process data across multiple nodes in the cluster**.

---

## 🔄 Data Ingestion Workflow

The ingestion process included the following steps:

1. 📁 **Creating the HDFS directory**
2. ⬆️ **Uploading the CSV files to HDFS**
3. 🔎 **Verifying the uploaded datasets**
4. ⚡ **Reading the datasets using Spark**

---

### 🔹 Uploading datasets to HDFS

<p align="center">
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/data-Ingestion-%26-Exploration/images/data-ingestion-to-hdfs.png?raw=true" width="900" alt="Uploading dataset to HDFS">
</p>

<p align="center">
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/data-Ingestion-%26-Exploration/images/data-ingestion-hdfs.png?raw=true" width="900" alt="HDFS directory containing ingested datasets">
</p>

This step ensures that all datasets are stored in a **distributed storage system instead of the local filesystem**.

---

# ⚡ Creating the Spark Environment

Once the datasets were stored in HDFS, a **Spark environment** was initialized inside the Dataproc cluster.

Spark allows distributed processing across **multiple worker nodes**, making it suitable for handling **large-scale datasets**.

### 🔹 Starting Spark Session

<p align="center">
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/data-Ingestion-%26-Exploration/images/starting-spark-session.png?raw=true" width="900" alt="Starting Spark Session in Dataproc">
</p>

The Spark session initializes the **Spark Driver**, which coordinates distributed tasks across the cluster.

---

# 📂 Reading Data from HDFS using PySpark

After initializing Spark, the datasets stored in **HDFS** were loaded into **Spark DataFrames**.

This enables:

- distributed queries
- parallel transformations
- large-scale analytics

---

### 🔹 Reading datasets from HDFS

<p align="center">
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/data-Ingestion-%26-Exploration/images/reading-data-from-hdfs.png?raw=true" width="900" alt="Reading dataset from HDFS using PySpark">
</p>

Each dataset was read using:

- `spark.read.csv()`
- `header=True`
- `inferSchema=True`

These parameters allow Spark to:

- automatically detect **column names**
- infer **data types**
- load datasets into **Spark DataFrames**

---

# 🔎 Distributed Data Exploration (PySpark)

Once the datasets were loaded into Spark DataFrames, several **data exploration tasks** were performed to better understand the dataset and detect potential data quality issues.

### 📊 Exploration tasks included:

- 📏 **Checking dataset sizes**
- 🔁 **Identifying duplicate records**
- ❓ **Detecting null values**
- 💳 **Analyzing payment methods**
- 📦 **Examining order status distribution**
- 🏆 **Identifying top-selling products**
- 🚚 **Calculating delivery time**

These insights help validate the dataset before moving to the **Data Cleaning and Transformation stage**.

---

# 📊 Data Quality Checks

## 🔹 Checking for Data Leakage or Missing Rows

<p align="center">
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/data-Ingestion-%26-Exploration/images/Data-exploration-check-data-Lekage-or-drop.png?raw=true" width="900" alt="Checking dataset row counts">
</p>

This step verifies that **no data was lost during ingestion into HDFS**.

---

## 🔹 Checking for Duplicate Records

<p align="center">
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/data-Ingestion-%26-Exploration/images/Data-exploration-check-duplicates.png?raw=true" width="900" alt="Checking duplicate records">
</p>

Duplicate checks were performed on key identifiers such as:

- `customer_id`
- `order_id`
- `product_id`

This ensures **data integrity before further processing**.

---

## 🔹 Checking for Null Values in Columns

<p align="center">
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/data-Ingestion-%26-Exploration/images/Data-exploration-check-nulls-in-every-columns.png?raw=true" width="900" alt="Checking null values in dataset columns">
</p>

Null analysis helps identify columns that require:

- data cleaning
- value imputation
- transformation

---

# 📈 Exploratory Analysis

## 💳 Most Preferred Payment Method

<p align="center">
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/data-Ingestion-%26-Exploration/images/Data-exploration-most-preferred-payment.png?raw=true" width="900" alt="Payment method distribution">
</p>

This analysis shows the **distribution of payment types used by customers**.

---

## 📦 Order Status Distribution

<p align="center">
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/data-Ingestion-%26-Exploration/images/Data-exploration-Order-status-distribution.png?raw=true" width="900" alt="Order status distribution">
</p>

This analysis provides insights into how many orders were:

- 📦 delivered
- 🚚 shipped
- ❌ canceled
- ⚠️ unavailable
- 🔄 processing

---

## 🏆 Top Selling Products

<p align="center">
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/data-Ingestion-%26-Exploration/images/data-exploration-top-selling-products.png?raw=true" width="900" alt="Top selling products analysis">
</p>

Product sales were aggregated using Spark to identify the **highest revenue-generating products**.

---

## 🚚 Total Delivery Time Analysis

<p align="center">
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/data-Ingestion-%26-Exploration/images/data-exploration-total-delivery-time.png?raw=true" width="900" alt="Delivery time analysis">
</p>

Delivery time was calculated using:

This helps evaluate:

- logistics efficiency
- delivery delays
- fulfillment performance

---

# 🚀 Next Step

The next stage of this project focuses on:

## 3️⃣🧹 Data Cleaning & Transformation

This stage includes:

- 🧹 handling missing values  
- 🔧 correcting inconsistent data  
- 🧾 fixing data types  
- 📉 removing outliers  
- 🔗 joining cleaned datasets  
- 📊 preparing the data for analytics and storage  

These steps ensure that the dataset becomes **clean, consistent, reliable, and ready for large-scale analytics and downstream processing**.

---

## 🔹 Reading the Data from HDFS

<p align="center">
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/Data-Cleaning-%26-Transformation/images/data-cleaning-reading-data.png?raw=true" width="900" alt="Reading the Olist dataset from HDFS using PySpark">
</p>

The first step in data cleaning and transformation is loading all raw CSV files from **HDFS** into PySpark DataFrames.

The following datasets were read from `/data/olist`:

- `olist_customers_dataset.csv`
- `olist_orders_dataset.csv`
- `olist_order_items_dataset.csv`
- `olist_order_payments_dataset.csv`
- `olist_order_reviews_dataset.csv`
- `olist_products_dataset.csv`
- `olist_sellers_dataset.csv`
- `olist_geolocation_dataset.csv`
- `product_category_name_translation.csv`

This establishes the working DataFrames needed for cleaning and transformation.

---

## 🔹 Identifying Missing Values with a Custom Function

<p align="center">
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/Data-Cleaning-%26-Transformation/images/data-transforming-identifying-missing-values-with-own-define-function.png?raw=true" width="900" alt="Identifying missing values using a custom PySpark function">
</p>

A custom function was created to inspect each DataFrame and count the number of null values per column.

This made it easier to:

- detect missing values efficiently
- compare completeness across all tables
- decide which columns require dropping, filling, or imputation

This step is important before applying any cleaning rules.

---

## 🔹 Dropping Rows with Missing Critical Fields in `orders_df`

<p align="center">
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/Data-Cleaning-%26-Transformation/images/data-transforming-drop-order-df-data-if-missing-order-id-customer-id-order-status.png?raw=true" width="900" alt="Dropping rows with missing critical fields in orders dataframe">
</p>

Rows with missing values in critical columns were removed from `orders_df`, specifically:

- `order_id`
- `customer_id`
- `order_status`

These fields are essential because without them, the order record becomes incomplete and unreliable for joining and analysis.

This helps preserve **data integrity** in the transformed dataset.

---

## 🔹 Removing Duplicate Records in `customer_df`

<p align="center">
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/Data-Cleaning-%26-Transformation/images/data-transformation-removing-duplicates-in-customer-id.png?raw=true" width="900" alt="Removing duplicate customer records using customer_id">
</p>

Duplicate rows in `customer_df` were removed based on the `customer_id` column.

This ensures that:

- each customer record is unique
- duplicate customer entries do not affect joins
- the cleaned customer table remains consistent for integration

Removing duplicates is a core part of improving dataset quality before combining tables.

---

## 🔹 Casting `customer_zip_code_prefix` to String

<p align="center">
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/Data-Cleaning-%26-Transformation/images/data-transforming-casting-the-right-data-type-for-zip-code-in-customer-df.png?raw=true" width="900" alt="Casting customer zip code prefix to string">
</p>

The `customer_zip_code_prefix` column was converted from integer to string.

This transformation is necessary because zip codes are **identifiers**, not values for mathematical computation.

Casting it to string helps:

- preserve formatting correctly
- avoid losing leading digits
- prepare the field for grouping, filtering, and location-based analysis

---

## 🔹 Converting `payment_type` into More Readable Labels

<p align="center">
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/Data-Cleaning-%26-Transformation/images/data-transforming-convert-the-payment-type-to-more-readable.png?raw=true" width="900" alt="Converting payment type values into readable labels">
</p>

The values in `payment_type` were transformed into more readable and understandable labels.

Examples include converting raw values such as:

- `credit_card` → `Credit Card`
- `boleto` → `Bank Transfer`
- `debit_card` → `Debit Card`

This improves readability for:

- reports
- dashboards
- analytics outputs
- business presentation of the dataset

---

## 🔹 Removing Outliers in `order_items_df` Using `approxQuantile`

<p align="center">
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/Data-Cleaning-%26-Transformation/images/data-transformation-removing-outliers-in-order-items-price.png?raw=true" width="900" alt="Removing outliers in order item prices using approxQuantile">
</p>

Outliers in the `price` column of `order_items_df` were removed using `approxQuantile()`.

This method was used to determine:

- lower cutoff
- upper cutoff

Then, rows outside the acceptable price range were filtered out.

This helps:

- reduce noise in the data
- avoid extreme price values affecting analysis
- improve the quality of revenue and pricing insights

---

## 🔹 Learning Imputation by Creating a New Nullable Payment Column

<p align="center">
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/Data-Cleaning-%26-Transformation/images/data-transforming-purposely-make-a-new-column-with-null-value-to-learn-imputer.png?raw=true" width="900" alt="Using PySpark Imputer on a purposely created nullable payment column">
</p>

To demonstrate and practice missing value imputation, a new version of the `payment_value` column was intentionally created with null values.

Then, the PySpark `Imputer` from `pyspark.ml.feature` was used to fill those missing values.

This step was done for learning purposes to understand how PySpark handles numerical imputation in practice.

It shows how imputation can be applied to:

- continuous numerical values
- incomplete numeric columns
- machine learning preprocessing workflows

---

## 🔹 Joining the Cleaned DataFrames into `order_with_details`

<p align="center">
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/Data-Cleaning-%26-Transformation/images/data-transformation-joining-cleaned-df.png?raw=true" width="900" alt="Joining cleaned dataframes into order_with_details">
</p>

After cleaning the individual tables, the transformed DataFrames were joined to create a consolidated DataFrame called `order_with_details`.

This join combines important information from multiple datasets, including:

- orders
- order items
- payments
- customers

This integrated table serves as the main analytical dataset for later processing and reporting.

---

## 🔹 Calculating Total Revenue per Seller

<p align="center">
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/Data-Cleaning-%26-Transformation/images/data-transformation-getting-the-total-revenue-per-seller-by-joining-order-item-cleaned-df-and-seller-df.png?raw=true" width="900" alt="Calculating total revenue per seller">
</p>

A seller-level revenue DataFrame was created by grouping records by `seller_id` and summing the `price` column.

This produced `total_revenue_per_seller`, which helps identify:

- high-performing sellers
- seller contribution to total sales
- revenue distribution across sellers

This aggregation is useful for business analytics and seller performance reporting.

---

## 🔹 Joining Total Revenue per Seller into `order_with_details`

<p align="center">
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/Data-Cleaning-%26-Transformation/images/joing-the-total-revenue-per-seller-to-order-with-details.png?raw=true" width="900" alt="Joining seller total revenue into order_with_details">
</p>

The `total_revenue_per_seller` DataFrame was then joined back into `order_with_details` using `seller_id`.

By doing this, each order-level record can also include the seller’s total accumulated revenue.

This enriches the dataset and makes it more useful for:

- seller-based analytics
- ranking sellers
- order-level revenue analysis with seller context

---

## 🔹 Saving the Final Cleaned Dataset in Parquet Format

<p align="center">
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/Data-Cleaning-%26-Transformation/images/last-creating-and-saving-order-with-details-in-HDFS-in-parquet-format.png?raw=true" width="900" alt="Saving cleaned order_with_details dataframe to HDFS in parquet format">
</p>

Finally, a new folder was created in HDFS and the cleaned `order_with_details` DataFrame was saved in **Parquet** format.

This step is important because Parquet is:

- columnar
- compressed
- efficient for analytics workloads
- well-suited for Spark and big data environments

Saving the transformed data in Parquet prepares it for:

- faster querying
- downstream analytics
- data warehousing
- scalable processing pipelines

---

## ✅ Outcome of the Data Cleaning & Transformation Stage

At the end of this stage, the raw e-commerce datasets were transformed into a cleaner and more analysis-ready dataset by:

- identifying and handling missing values
- removing duplicate records
- correcting data types
- improving categorical readability
- filtering outliers
- practicing numerical imputation
- integrating multiple cleaned tables
- generating seller-level revenue metrics
- storing the final dataset in optimized Parquet format

This makes the dataset more reliable and ready for the next stages of the data engineering workflow such as **data integration, aggregation, optimization, and serving**.

---

# 🚀 Next Stage

The next stage of this project will focus on:

## 🔗 Data Integration & Aggregation

This stage focuses on combining and organizing the cleaned datasets into structured analytical datasets.

Key objectives of this stage include:

- 🔗 integrating multiple cleaned datasets  
- 📊 aggregating metrics across different dimensions  
- 🧮 computing business-level KPIs  
- 🧑‍💼 analyzing seller performance  
- 🛍️ analyzing customer purchasing behavior  
- 🌍 exploring geographic patterns in orders and deliveries  

Through these steps, the pipeline will transform the cleaned raw datasets into **analytics-ready datasets** that support deeper insights into the e-commerce platform.

This stage prepares the data for:

- 📈 business intelligence dashboards  
- 📊 large-scale analytical queries  
- 🧠 advanced data analysis and reporting  

---
