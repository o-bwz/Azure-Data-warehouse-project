# Azure Data Warehouse Pipeline: Bike Share Analytics Project

This project demonstrates the complete pipeline of designing and building a modern cloud-based data warehouse using Azure services. It includes direct data ingestion from local raw CSV files, automated batch processing via Python, schema validation, and loading into a star schema structure on Azure SQL / Synapse Analytics.

---

## 📌 Project Overview

### Business Case
A bike share company wants to analyze ride, payment, and station data for better customer insight and operations. This pipeline ingests operational data from raw CSV files, performs automated batch processing using a custom Python ETL script, and loads it into Azure for downstream star schema transformation to support reporting and business intelligence.

---

## 🛠️ Technologies Used

- **Azure SQL Database / Azure Synapse Analytics** – Data warehouse (OLAP) with Dedicated SQL Pools
- **Python (ETL Engine)** – Automated data extraction, type conversion, and high-performance loading
- **SQL (T-SQL)** – Schema definition, constraint management (`NOT ENFORCED`), and star schema transformation

### Python Libraries Used:
- **`pandas`** – Data manipulation, header-less CSV parsing, null-value alignment, and schema matching
- **`sqlalchemy`** – Database connection abstraction and bulk data routing
- **`pyodbc`** – ODBC driver interface to Azure SQL with high-speed execution (`fast_executemany`)
- **`urllib.parse`** – Safe URL-encoding for authentication credentials
- **`os`** – Dynamic local directory and path management (`data source` folder)

---

## 🚀 Pipeline Steps

### Task 1: Create Azure Resources
- Create Azure SQL Database / Synapse Analytics Instance.
- Configure Firewall Rules and Client IP Access.
- Install and configure **ODBC Driver 17 for SQL Server**.

### Task 2: Design Staging Tables & Constraints
- Create destination staging tables (`rider`, `payment`, `station`, `trip`).
- Set extended column lengths (`VARCHAR(255)` for addresses) to prevent string truncation.
- Implement `NOT ENFORCED` Primary Key constraints to comply with cloud pool enforcement rules.

### Task 3: Execute Python ETL Pipeline
- Place raw source CSV files inside the `data source` folder:
  - `riders.csv`
  - `payments.csv`
  - `stations.csv`
  - `trips.csv`
- Run the Python ETL script to:
  - Parse header-less CSV files and assign explicit column names.
  - Handle null values (`NaN` to `NULL`) and perform data type conversion (e.g., boolean to `BIT`/`INT`).
  - Perform high-speed bulk insertion using `fast_executemany=True` and optimized batch size (`chunksize=50000`) for large datasets (**1.9M+ records**).

### Task 4: Transform to Star Schema
- Apply SQL scripts in Azure to transform staging tables into the final analytical star schema:
  - **Fact Tables:** `fact_trip`, `fact_payment`
  - **Dimension Tables:** `dim_rider`, `dim_station`, `dim_date`

---

## 📐 Star Schema Overview

**Fact Tables**
- `fact_payment(payment_id, payment_date, payment_amount, rider_id)`
- `fact_trip(trip_id, ride_type, started_at, ended_at, start_station_id, end_station_id, duration, rider_id)`

**Dimension Tables**
- `dim_rider(rider_id, name, birthdate, is_member, account_start, account_end, rider_age)`
- `dim_station(station_id, address, lat, lon)`
- `dim_date(date_key, full_date, year, month, week, weekday,...so on)`

---

## ✅ Final Outcome

By the end of this project, you will have:
- Designed and implemented a robust star schema data model.
- Built a high-performance, automated Python ETL pipeline streaming local data directly to Azure.
- Resolved real-world cloud loading challenges (string truncation, header-less CSVs, null handling, bulk insert performance).
- Produced a clean, scalable cloud data warehouse ready for BI and analytical queries.

---

## 📚 Resources

- [Azure Synapse / Azure SQL Documentation](https://learn.microsoft.com/en-us/azure/azure-sql/)
- [pandas Documentation](https://pandas.pydata.org/docs/)
- [SQLAlchemy pyodbc Driver Support](https://docs.sqlalchemy.org/en/20/dialects/mssql.html)

---

## ✍️ Author

**Omar**  
Data Engineer | Cloud Analytics Specialist | Data Analyst

---

## 📝 License

This project is for educational purposes. Please cite if used.
