# Personal Payments Data Analysis with Medallion Architecture

A detailed technical project showcasing end-to-end data processing on Azure using Databricks, ADLS2, and PySpark. This project transforms a personal payments Excel file into a highly optimized dataset for further analytical use, leveraging a medallion-based architecture.

---

## Project Overview

This project ingests a three-month history of personal transactions stored in `payments.xlsx`. The main goals are to:
- **Practice Spark-based data transformations** using Databricks.
- **Optimize data storage** by reducing redundancy and overall size (~32% reduction).
- **Analyze transactional data** with visualizations using Matplotlib.

---

## Tech Stack

- **Cloud Platform:** Azure
- **Compute & Processing:** Databricks
- **Storage:** Azure Data Lake Storage Gen2 (ADLS2)
- **Data Processing:** PySpark (RDDs & DataFrames)
- **Visualization:** Matplotlib
- **Architecture:** Medallion (Raw, Bronze, Silver, Gold layers)

---

## Medallion Architecture Overview

The project utilizes a four-layer storage architecture:
- **Raw Layer:** Stores the original `payments.xlsx` file.
- **Bronze Layer:** (Optionally used) Ingests and stores raw data without transformations.
- **Silver Layer:** Transforms the Excel data to Parquet format using Databricks. Data cleansing, type enforcement, and initial optimizations occur here.
- **Gold Layer:** (Potential future extension) Models and aggregates the data for advanced analytics and business insights.

*Note: In this project, emphasis is on ingesting data into the raw container and transforming it into a silver-layer Parquet file.*

---

## Data Pipeline & Transformation

1. **Ingestion:**
   - Upload `payments.xlsx` to the **Raw** container in ADLS2.
   
2. **Transformation (Databricks):**
   - **Excel to Parquet Conversion:** Using PySpark, the Excel file is read and converted into Parquet format for efficient querying and storage.
   - **Data Optimization:** 
     - Extensive use of PySpark RDDs ensures resilient and scalable processing.
     - A specific challenge was handling columns (e.g., date) with many duplicate values.  
     - **Run-Length Encoding (RLE):** Applied to reduce redundancy and shrink dataset size by around 32%.

3. **Analysis:**
   - Visualized processed data using Matplotlib to extract meaningful insights from personal transactions.

---

## Technical Details

- **Azure Databricks Integration:**  
  Detailed notebooks automate data ingestion, transformation, and analysis.
  
- **ADLS2 Storage Setup:**  
  The storage container is partitioned into `raw`, `bronze`, `silver`, and `gold` folders to support the medallion design, ensuring a clean separation of raw data and processed outputs.

- **PySpark RDDs & DataFrames:**  
  Leveraged for distributed data processing to maintain fault tolerance and scalability.  
  *Consider: How might leveraging the DataFrame API further simplify some transformations compared to RDDs?*

- **Run-Length Encoding (RLE):**  
  Applied on columns with high duplicate rates (e.g., date column) to optimize storage and improve query performance.  
  *Questions: What other compression techniques did you consider? How does RLE compare in terms of efficiency and complexity for this dataset?*

- **Visualization with Matplotlib:**  
  Used for generating exploratory visual insights from the transformed data.  
  *Explore: Could integrating interactive visualization libraries further enhance data exploration?*

---

## Challenges & Solutions

- **High Duplication in Data Columns:**  
  - *Challenge:* Columns like the transaction date had repetitive values.
  - *Solution:* Implemented run-length encoding to minimize redundant storage and improve processing times.

- **Data Format Transformation:**  
  - *Challenge:* Converting an Excel file to a Parquet format while preserving data integrity.
  - *Solution:* Utilized PySpark's robust libraries to seamlessly convert and optimize data storage.

- **Scalability & Resilience:**  
  - *Challenge:* Ensuring the pipeline can handle larger datasets in the future.
  - *Solution:* Extensive use of PySpark RDDs provides a scalable and fault-tolerant processing framework.

---

## Future Enhancements & Deep-Dive Questions

### Potential Enhancements
- **Gold Layer Development:**  
  Extend the pipeline to create a gold layer with aggregated views and business-ready analytics.
  
- **Interactive Visualizations:**  
  Explore advanced visualization frameworks (e.g., Plotly, Seaborn) for interactive data exploration.
  
- **Performance Benchmarking:**  
  Implement monitoring and logging to benchmark the performance of different stages of the pipeline.

---

## Conclusion

This project demonstrates an effective application of a medallion-based architecture in processing and analyzing transactional data. The thoughtful design, from data ingestion to optimization and visualization, highlights the importance of scalability, data quality, and advanced processing techniques in modern data engineering.

---
