# Online Retail Data Analysis Notebook

## Initial Setup

- Imports standard data science libraries:
  - NumPy
  - Pandas
  - Matplotlib
  - Seaborn
  - Plotly
- Sets up notebook display configurations:
  - `%matplotlib inline`
  - `sns.set()`
- Initializes Plotly for interactive visualizations
- Suppresses warnings for cleaner output

## Data Loading & Initial Exploration

- Loads data from `'online_retail_II.xlsx'` into a DataFrame
- Shows:
  - First 5 rows
  - Random 10-row sample
- Dataset dimensions: 525,461 rows × 8 columns
- Features:
  - Invoice
  - StockCode
  - Description
  - Quantity
  - InvoiceDate
  - Price
  - Customer ID
  - Country

## Data Quality Assessment

- Missing values identified:
  - Description: 2,928 missing
  - Customer ID: 107,927 missing
- Extreme values noted:
  - Quantity range: -9600 to 19152
  - Price range: -53594 to 25111
- Special invoice prefixes analyzed:
  - NaN
  - 'C'
  - 'A' (indicating cancellations/credits)
- Non-standard StockCodes examined:
  - POST
  - D
  - BANK CHARGES
  - etc.

## Data Cleaning Process

1. **Invoice filtering**:
   - Keeps only numeric invoice numbers
2. **StockCode standardization**:
   - Retains 5-digit codes
   - Keeps 'PADS' code
3. **Missing data handling**:
   - Drops rows with missing Customer IDs
4. **Negative values treatment**:
   - Handles negative quantities/prices (likely returns/refunds)
5. **Final cleaned dataset**:
   - 406,337 rows remaining

## Feature Engineering

- Created new features:
  - `Total_value` = Quantity × Price
- Generated customer-level aggregates:
  - **Monetary_value**: Sum of all purchases
  - **Frequency**: Count of unique invoices
## Machine Learning Steps

###  K-Means Clustering
- The notebook applies the **K-Means algorithm** to group data into clusters.
- The **Elbow Method** is used to determine the optimal number of clusters (`K`).
- **Silhouette Score** is calculated to evaluate clustering performance.

###  DBSCAN Clustering
- The **DBSCAN algorithm** is used as an alternative to K-Means for density-based clustering.
- Different values of `eps` and `min_samples` are tested to optimize clustering.
- The best configuration is selected based on the **silhouette score**.
- DBSCAN also detects **outliers** and labels them as `-1`.
