# Retail Sales Data Pipeline (Bronze → Silver → Gold)

This project demonstrates a simple end-to-end data pipeline using Python and pandas.
It follows a layered data-engineering approach inspired by modern data lake design.

### Data Layers
#### Bronze Layer - Raw Data

The bronze layer contains the raw transactional data exactly as it was received, without any modifications.

`data/raw/retail_store_sales_raw.csv`

This data contains missing values, inconsistent fields and ureliable calculated columns.

#### Silver Layer - Cleaned & Validated Data

The silver layer contains cleaned and validated data that is safe for downstream analysis.

The following transformation was applied:

**1. Removed rows where Item was missing**

    Rows without item names were dropped because they cannot be reliably grouped, priced or analyzed.

**2. Recalculated Total Spent**

    The original total was not trusted. It was recalculated using:
    `Total Spent = Price Per Unit * Quantity`

**3. Filled Missing discounts**

    Missing values in *Discount Applied* were replaced with *False* first and the True and False values were converted into 1 and 0 for analytics purpose.

**4. Standardized data Types**

     *Transaction Date* was converted into proper datetime format for time-based analysis.

The cleaned dataset is saved as:


`data/processed/clean_sales.csv`

#### Gold Layer - Business Aggregates

In the Gold Layer, the cleaned Silver data is enriched and aggregated to produce business-ready metrics such as:
    1. Year-Month revenue
    2. Year wise category sales
    3. Discont and Non Discount sales

### Tech Stack
    * Python
    * Pandas
    * matplotlib (for validation plots)
    * GitHub for version control
