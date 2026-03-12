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
  <img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/understanding-the-data/images/1.png" width="900" alt="Downloading dataset in Google Colab">
</p>

### 🔹 Extracting the dataset
<p align="center">
  <img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/understanding-the-data/images/2.png" width="900" alt="Extracting dataset in Google Colab">
</p>

### 🔹 Inspecting extracted files
This step verifies that all CSV files were successfully extracted.

<p align="center">
  <img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/understanding-the-data/images/3.png" width="900" alt="Listing extracted CSV files">
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
  <img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/understanding-the-data/images/4.png" width="900" alt="Creating Spark Session">
</p>

<p align="center">
  <img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/understanding-the-data/images/5.png" width="900" alt="Reading dataset using PySpark">
</p>

<p align="center">
  <img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/understanding-the-data/images/6.png" width="900" alt="Printing schema of dataset">
</p>

### 🔹 Automated output for all datasets

<p align="center">
  <img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/understanding-the-data/images/7.png" width="900" alt="Showing sample rows of dataset">
</p> 

<p align="center">
  <img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/understanding-the-data/images/8.png" width="900" alt="Gemini automation code for repetitive PySpark tasks">
</p>

<p align="center">
  <img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/understanding-the-data/images/10.png" width="900" alt="Automated schema and table preview output">
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
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/data-Ingestion-%26-Exploration/images/data-ingestion-to-hdfs.png" width="900" alt="Uploading dataset to HDFS">
</p>

<p align="center">
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/data-Ingestion-%26-Exploration/images/data-ingestion-hdfs.png" width="900" alt="HDFS directory containing ingested datasets">
</p>

This step ensures that all datasets are stored in a **distributed storage system instead of the local filesystem**.

---

# ⚡ Creating the Spark Environment

Once the datasets were stored in HDFS, a **Spark environment** was initialized inside the Dataproc cluster.

Spark allows distributed processing across **multiple worker nodes**, making it suitable for handling **large-scale datasets**.

### 🔹 Starting Spark Session

<p align="center">
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/data-Ingestion-%26-Exploration/images/starting-spark-session.png" width="900" alt="Starting Spark Session in Dataproc">
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
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/data-Ingestion-%26-Exploration/images/reading-data-from-hdfs.png" width="900" alt="Reading dataset from HDFS using PySpark">
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
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/data-Ingestion-%26-Exploration/images/Data-exploration-check-data-Lekage-or-drop.png" width="900" alt="Checking dataset row counts">
</p>

This step verifies that **no data was lost during ingestion into HDFS**.

---

## 🔹 Checking for Duplicate Records

<p align="center">
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/data-Ingestion-%26-Exploration/images/Data-exploration-check-duplicates.png" width="900" alt="Checking duplicate records">
</p>

Duplicate checks were performed on key identifiers such as:

- `customer_id`
- `order_id`
- `product_id`

This ensures **data integrity before further processing**.

---

## 🔹 Checking for Null Values in Columns

<p align="center">
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/data-Ingestion-%26-Exploration/images/Data-exploration-check-nulls-in-every-columns.png" width="900" alt="Checking null values in dataset columns">
</p>

Null analysis helps identify columns that require:

- data cleaning
- value imputation
- transformation

---

# 📈 Exploratory Analysis

## 💳 Most Preferred Payment Method

<p align="center">
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/data-Ingestion-%26-Exploration/images/Data-exploration-most-preferred-payment.png" width="900" alt="Payment method distribution">
</p>

This analysis shows the **distribution of payment types used by customers**.

---

## 📦 Order Status Distribution

<p align="center">
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/data-Ingestion-%26-Exploration/images/Data-exploration-Order-status-distribution.png" width="900" alt="Order status distribution">
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
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/data-Ingestion-%26-Exploration/images/data-exploration-top-selling-products.png" width="900" alt="Top selling products analysis">
</p>

Product sales were aggregated using Spark to identify the **highest revenue-generating products**.

---

## 🚚 Total Delivery Time Analysis

<p align="center">
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/data-Ingestion-%26-Exploration/images/data-exploration-total-delivery-time.png" width="900" alt="Delivery time analysis">
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
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/Data-Cleaning-%26-Transformation/images/data-cleaning-reading-data.png" width="900" alt="Reading the Olist dataset from HDFS using PySpark">
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
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/Data-Cleaning-%26-Transformation/images/data-transforming-identifying-missing-values-with-own-define-function.png" width="900" alt="Identifying missing values using a custom PySpark function">
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
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/Data-Cleaning-%26-Transformation/images/data-transforming-drop-order-df-data-if-missing-order-id-customer-id-order-status.png" width="900" alt="Dropping rows with missing critical fields in orders dataframe">
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
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/Data-Cleaning-%26-Transformation/images/data-transformation-removing-duplicates-in-customer-id.png" width="900" alt="Removing duplicate customer records using customer_id">
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
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/Data-Cleaning-%26-Transformation/images/data-transforming-casting-the-right-data-type-for-zip-code-in-customer-df.png" width="900" alt="Casting customer zip code prefix to string">
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
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/Data-Cleaning-%26-Transformation/images/data-transforming-convert-the-payment-type-to-more-readable.png" width="900" alt="Converting payment type values into readable labels">
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
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/Data-Cleaning-%26-Transformation/images/data-transformation-removing-outliers-in-order-items-price.png" width="900" alt="Removing outliers in order item prices using approxQuantile">
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
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/Data-Cleaning-%26-Transformation/images/data-transforming-purposely-make-a-new-column-with-null-value-to-learn-imputer.png" width="900" alt="Using PySpark Imputer on a purposely created nullable payment column">
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
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/Data-Cleaning-%26-Transformation/images/data-transformation-joining-cleaned-df.png" width="900" alt="Joining cleaned dataframes into order_with_details">
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
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/Data-Cleaning-%26-Transformation/images/data-transformation-getting-the-total-revenue-per-seller-by-joining-order-item-cleaned-df-and-seller-df.png" width="900" alt="Calculating total revenue per seller">
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
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/Data-Cleaning-%26-Transformation/images/last-creating-and-saving-order-with-details-in-HDFS-in-parquet-format.png" width="900" alt="Saving cleaned order_with_details dataframe to HDFS in parquet format">
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

# 4️⃣ Data integration, advanced aggregation, and enrichment

This stage focuses on building a single analytics-ready dataset from the cleaned e-commerce tables, then extending that dataset through advanced aggregations and data enrichment.

The workflow in this stage covers three core parts:

- integrating multiple DataFrames into one consolidated dataset
- creating advanced aggregated metrics for customers, sellers, products, and revenue trends
- enriching the dataset with new analytical columns for time, status, segmentation, and revenue logic

By the end of this stage, the project produces a stronger analytical foundation for reporting, dashboarding, and deeper business analysis.

---

## 🔹 Reading the datasets from HDFS

<p align="center">
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/data-Integration-%26-aggregation/images/data-integration-read-the-from-HDFS.png?raw=true" width="900" alt="Reading datasets from HDFS">
</p>

The cleaned source datasets were loaded from HDFS into Spark DataFrames to prepare them for large-scale processing.

These datasets include:

- `customer_df`
- `orders_df`
- `order_items_df`
- `payments_df`
- `reviews_df`
- `products_df`
- `sellers_df`
- `geolocation_df`
- `product_category_df`

Loading the data from HDFS makes the pipeline ready for distributed joins, aggregations, and feature enrichment using PySpark.

---

## 🔹 Joining all DataFrames into a unified analytical dataset

<p align="center">
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/data-Integration-%26-aggregation/images/joining-all-data-frames-optimized.png?raw=true" width="900" alt="Joining all DataFrames with broadcast and cache optimization">
</p>

The DataFrames were joined step by step to create a consolidated dataset called `full_orders_df`.

This integration combines important business information from multiple tables, including:

- orders
- order items
- products
- sellers
- customers
- geolocation
- reviews
- payments

To improve performance, smaller reference tables were optimized using `broadcast()` joins, and the final integrated DataFrame was cached using `cache()`.

This unified dataset becomes the main source for advanced aggregation and enrichment tasks across the project.

---

## 🔹 Customer retention analysis using first and last order dates

<p align="center">
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/data-Integration-%26-aggregation/images/advance%20-%20agg%20%20Customer%20Retention%20Analysis%20(%20First%20%26%20Last%20Order).png?raw=true" width="900" alt="Customer retention analysis using first and last order dates">
</p>

An advanced aggregation was created to analyze customer retention behavior by identifying each customer’s `first_order_date` and `last_order_date`.

This aggregation also includes:

- total number of orders per customer
- average order value per customer

This helps measure how active customers are over time and gives a clearer view of repeat purchasing behavior.

---

## 🔹 Monthly revenue and order count trend

<p align="center">
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/data-Integration-%26-aggregation/images/advance-agg%20%20Monthly%20Revenue%20and%20Order%20Count%20Trend.png?raw=true" width="900" alt="Monthly revenue and order count trend">
</p>

A monthly trend DataFrame was created by grouping records by `seller_id` and purchase month.

This aggregation calculates:

- total orders
- total revenue
- average order value
- minimum order value
- maximum order value

This makes it easier to track revenue movement over time and compare seller performance across different months.

---

## 🔹 Product popularity metrics

<p align="center">
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/data-Integration-%26-aggregation/images/advance-agg%20Product%20Popularity%20Metrics.png?raw=true" width="900" alt="Product popularity metrics">
</p>

A product-level aggregation was built to measure how well each product performs in the marketplace.

The generated metrics include:

- total sales count
- total revenue
- average price
- price volatility
- unique sellers offering the product

This helps identify best-selling products, products with unstable pricing, and products sold across multiple sellers.

---

## 🔹 Seller performance metrics

<p align="center">
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/data-Integration-%26-aggregation/images/advance-agg-Seller%20Performance%20Metrics%20(Revenue%2C%20Average%20Review%2C%20Order%20Count).png?raw=true" width="900" alt="Seller performance metrics">
</p>

A seller-level performance DataFrame was created to summarize seller activity and quality indicators.

This aggregation includes:

- total orders
- total revenue
- average review score
- price variability

These metrics help compare sellers not only by sales volume, but also by customer feedback and pricing behavior.

---

## 🔹 Total revenue and average order value per customer

<p align="center">
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/data-Integration-%26-aggregation/images/advance-agg-Total%20Revenue-%26-Average-Order-Value-(AOV)-per-Customer.png?raw=true" width="900" alt="Total revenue and average order value per customer">
</p>

A customer spending DataFrame was created to summarize each customer’s purchasing activity.

This aggregation calculates:

- total orders
- total amount spent
- average order value or `AOV`

This gives a quick view of customer value and supports later customer segmentation tasks.

---

## 🔹 Customer segmentation based on spending

<p align="center">
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/data-Integration-%26-aggregation/images/data%20-%20enrichment%20Customer%20Segmentation%20based%20on%20spending.png?raw=true" width="900" alt="Customer segmentation based on spending">
</p>

The customer spending dataset was enriched by creating a `customer_segment` column based on average order value.

Customers were grouped into segments such as:

- `High-Value`
- `Medium-Value`
- `Low-Value`

This enrichment helps make customer analysis more actionable and supports targeted reporting and segmentation strategies.

---

## 🔹 Hourly order distribution

<p align="center">
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/data-Integration-%26-aggregation/images/data%20-%20enrichment%20Hourly%20Order%20Distribution.png?raw=true" width="900" alt="Hourly order distribution">
</p>

A new column called `hour_of_day` was created from `order_purchase_timestamp` to capture the hour when each order was placed.

This enrichment helps analyze:

- peak ordering hours
- customer buying patterns during the day
- time-based sales behavior

This field is useful for time-series exploration and hourly trend analysis.

---

## 🔹 Order status flags

<p align="center">
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/data-Integration-%26-aggregation/images/data%20-%20enrichment%20Order%20Status%20Flags.png?raw=true" width="900" alt="Order status flags">
</p>

Binary flag columns were added to simplify order status analysis.

These new columns include:

- `is_delivered`
- `is_cancelled`

This makes the dataset easier to use in downstream analysis, especially for filtering, KPI reporting, and operational dashboards.

---

## 🔹 Weekday vs weekend order classification

<p align="center">
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/data-Integration-%26-aggregation/images/data%20-%20enrichment%20Weekday%20vs%20Weekend%20Order.png?raw=true" width="900" alt="Weekday vs weekend order classification">
</p>

A new column called `order_day_type` was created to classify each purchase as either a weekday order or a weekend order.

This enrichment helps compare:

- weekday buying behavior
- weekend buying behavior
- order timing patterns across the week

This is useful for trend reporting and customer behavior analysis.

---

## 🔹 Order revenue calculation

<p align="center">
<img src="https://github.com/LeynardPenaranda/Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/data-Integration-%26-aggregation/images/data%20enrichment%20Order%20Revenue%20Calculation.png?raw=true" width="900" alt="Order revenue calculation">
</p>

A new column called `order_revenue` was created by combining `price` and `freight_value`.

This enrichment gives a more complete revenue measure at the order level and helps support:

- revenue analysis
- seller-level reporting
- customer spending analysis
- order profitability exploration

This field makes the integrated dataset more useful for financial and operational analytics.

---

## 🔹 What this stage delivers

This stage transforms the cleaned raw tables into a richer analytical environment by combining full DataFrame integration, advanced business aggregations, and feature-level enrichment.

As a result, the project now has a stronger dataset for:

- business intelligence dashboards
- customer and seller analytics
- product performance analysis
- trend reporting
- advanced Spark-based analytics

# 🔚 Data Optimization and Data Serving

## 🔹 Read the Data from HDFS and Read the `full_orders_df` in Parquet from HDFS

<p align="center">
  <img src="https://github.com/LeynardPenaranda/Big-Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/Process-Optimization-Data-Serving/images/reading%20the%20data%20from%20HDFS%20and%20full_orders_df%20in%20parquet%20inside%20HDFS.png" width="900" alt="Reading the data from HDFS and full_orders_df in parquet inside HDFS">
</p>

---

## 🔹 Spark Configuration for Optimization

<p align="center">
  <img src="https://github.com/LeynardPenaranda/Big-Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/Process-Optimization-Data-Serving/images/spark%20configuration%20to%20be%20optimized.png" width="900" alt="Spark configuration to be optimized">
</p>

---

## 🔹 Optimized Join Strategies

<p align="center">
  <img src="https://github.com/LeynardPenaranda/Big-Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/Process-Optimization-Data-Serving/images/Optimized%20Join%20Strategies.png" width="900" alt="Optimized Join Strategies">
</p>

---

## 🔹 Saving `full_orders_df` in Google Cloud Storage Bucket

<p align="center">
  <img src="https://github.com/LeynardPenaranda/Big-Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/Process-Optimization-Data-Serving/images/saved%20full_orders_df%20in%20Google%20cloud%20storage%20bucket.png" width="900" alt="Saving full_orders_df in Google Cloud Storage Bucket">
</p>

---

## 🔹 Image of the Bucket

<p align="center">
  <img src="https://github.com/LeynardPenaranda/Big-Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/Process-Optimization-Data-Serving/images/data%20serving%20-saved%20in%20google%20cloud%20storage%20-%20Bucket.png" width="900" alt="Image of the Bucket in Google Cloud Storage">
</p>

---

## 🔹 Save `full_orders_df` as a Persistent Table in Hive

<p align="center">
  <img src="https://github.com/LeynardPenaranda/Big-Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/Process-Optimization-Data-Serving/images/save%20full_orders_df%20as%20a%20persistent%20table%20in%20hive.png" width="900" alt="Save full_orders_df as a Persistent Table in Hive">
</p>

---

## 🔹 Save `full_orders_df` as a CSV in HDFS

<p align="center">
  <img src="https://github.com/LeynardPenaranda/Big-Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/Process-Optimization-Data-Serving/images/saved%20full_orders_df%20in%20HDFS%20as%20CSV.png" width="900" alt="Save full_orders_df as CSV in HDFS">
</p>

---

## 🔹 Saving `full_orders_df` as Parquet in HDFS

<p align="center">
  <img src="https://github.com/LeynardPenaranda/Big-Data-Engineering-Real-World-Project-Ecommerce-Dataset/blob/main/Process-Optimization-Data-Serving/images/Saving%20full_orders_df%20in%20HDFS%20as%20a%20parquet.png" width="900" alt="Saving full_orders_df in HDFS as a Parquet">
</p>

This stage ensures that all the processed and optimized data is saved in both **Google Cloud Storage** and **HDFS**, ready for further analysis or serving.

---

## 🔹 Conclusion

By the end of this stage, the dataset has been:

- Optimized using efficient **join strategies**.
- Stored across multiple storage locations: **HDFS** and **Google Cloud Storage**.
- Saved as both **CSV** and **Parquet** formats, which are optimized for large-scale data processing.

This final dataset is now ready to serve as a source for business analytics, reporting, and deeper insights into the **e-commerce business operations**.
