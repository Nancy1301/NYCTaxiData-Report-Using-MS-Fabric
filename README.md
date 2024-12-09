# **NYC Taxi Data Project: End-to-End Solution with Microsoft Fabric**

## **Overview**
This project demonstrates an end-to-end data pipeline and analytics solution using Microsoft Fabric. It combines **data engineering**, **data warehousing**, **data pipelines**, and **Power BI visualization** to analyze New York City Yellow Taxi (Medallion Taxi) trip records for 2024. The solution showcases how Microsoft Fabric enables seamless integration of various tools for modern data workflows.

---

## **Dataset**

### **Yellow Taxi Trip Records**
- **Source**: NYC Government Open Data Portal.
- **Format**: Parquet (optimized for big data analytics).
- **Content**: Monthly files (January–May 2024) containing:
  - Vendor ID
  - Pickup/Drop-off Datetime
  - Passenger Count
  - Trip Distance
  - Pickup/Drop-off Zone IDs
  - Payment Type
  - Total Trip Amount

### **Taxi Zone Lookup Table**
- **Source**: Static CSV file.
- **Content**: Contains geographic zone information, enabling spatial analysis.

---

## **Workflow**

### **1. Storage in Fabric Data Lakehouse**
- The **Lakehouse** serves as the storage layer for raw data files.
- Parquet files and the Taxi Zone Lookup Table are uploaded to the Lakehouse.

### **2. Data Factory Pipeline for Ingestion**
- **Copy Activity**: Moves data from the Lakehouse to the **staging tables** in the Data Warehouse.
  - `NYC_Yellow_Taxi_Staging`: Stores raw trip data temporarily.
  - `Taxi_Zone_Lookup`: A static lookup table loaded once.

### **3. Data Cleansing and Processing**
- **Data Flow Gen 2 Activity**:
  - Cleans data and removes invalid records.
  - Joins `NYC_Yellow_Taxi_Staging` with `Taxi_Zone_Lookup`.
- **Stored Procedures**: Replace the data flow in later stages for better performance and scalability.

### **4. Data Warehouse and Presentation Layer**
- Data is processed and loaded into the **Presentation Layer** for reporting and analytics.
- This project skips an intermediate layer for simplicity.

### **5. Power BI Integration**
- **Semantic Data Model**: Built on top of the presentation tables.
- **Dashboards and Reports**:
  - Analyze trip patterns.
  - Identify revenue trends.
  - Visualize popular pickup/drop-off zones.

### **6. Automation and Metadata Management**
- **Processing Log Table**:
  - Tracks rows processed in staging and presentation layers.
  - Logs the latest date of processed data.
- **Automated Pipelines**:
  - Delete old staging data before processing new monthly data.
  - Append new data to the presentation layer while maintaining historical records.

---

## **Technology Stack**

- **Microsoft Fabric**:
  - **Lakehouse**: Centralized storage for raw data.
  - **Data Factory**: Automates data ingestion and cleansing.
  - **Data Warehouse**: Stores processed and structured data for analysis.
  - **Power BI**: Creates dashboards and reports.
- **Parquet Format**: Efficient columnar storage for big data.
- **SQL Stored Procedures**: For efficient data processing and transformations.

---

## **Folder Structure**

