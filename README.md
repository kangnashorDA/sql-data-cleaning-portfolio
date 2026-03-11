# SQL Data Cleaning Project

This project demonstrates how messy real-world datasets can be investigated and repaired using SQL.

Skills demonstrated:
- Data auditing
- Handling NULL values
- Removing duplicates
- Fixing inconsistent formats
- Creating cleaned datasets

Tools used:

- PostgreSQL
- SQL
- pgAdmin

## Dataset Exploration & Cleaning Steps:
- Initial dataset inspection
- NULL value detection
- Missing value marker detection (NA)
- Data anomaly inspection
- Data type conversion

### 1. Initial Data Import
The dataset used in this project is the Hotel Booking Demand Dataset.
The initial goal was to import the CSV file into PostgreSQL for further analysis.

However, during the import process an error occurred:
> ERROR: invalid input syntax for type integer: "NA"\
> CONTEXT: COPY raw_hotel_bookings, line 40602, column children: "NA"

This error indicates that the column children contains the value **"NA"**, while the database expected an **integer type**.
This revealed an important data quality issue:
the dataset contains string markers for missing values, which prevents direct type casting.

### 2. Temporary Workaround
To investigate the dataset structure without import failures, the table was recreated with all columns defined as TEXT.
Example schema:
```
CREATE TABLE raw_hotel_bookings (
    hotel TEXT,
    is_canceled TEXT,
    lead_time TEXT,
    arrival_date_year TEXT,
    arrival_date_month TEXT,
    arrival_date_week_number TEXT,
    arrival_date_day_of_month TEXT,
    stays_in_weekend_nights TEXT,
    stays_in_week_nights TEXT,
    adults TEXT,
    children TEXT,
    babies TEXT
    -- remaining columns omitted for brevity
);
```
By using TEXT types temporarily, the dataset could be fully loaded without validation errors. This step allows exploratory data analysis before enforcing proper data types.

### 3. Initial Data Inspection
To understand the structure of the dataset, a small sample of the data was inspected.
``
SELECT *
FROM raw_hotel_bookings
LIMIT 20;
``
![Image of Raw Data](/screenshots/raw_data.png)
This helps verify:
column order
value format
categorical vs numeric fields

