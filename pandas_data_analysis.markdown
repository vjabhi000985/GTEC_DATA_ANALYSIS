# Pandas for Data Analysis

Pandas is a powerful Python library for data manipulation and analysis, built on top of NumPy. It provides flexible data structures like `Series` (1D) and `DataFrame` (2D) for handling tabular data, making it ideal for data analysis tasks in finance, science, and business. This section covers reading data from various sources, basic analysis, data cleaning, filtering, time series analysis, merging/joining, and advanced data manipulation.

## 1. Reading Different Sources of Files
Pandas supports reading data from multiple file formats and sources, enabling seamless data import for analysis.

- **Common Functions**:
  - `pd.read_csv(file_path)`: Read CSV files.
  - `pd.read_excel(file_path)`: Read Excel files.
  - `pd.read_json(file_path)`: Read JSON files.
  - `pd.read_sql(query, connection)`: Read from SQL databases.
- **Key Parameters**:
  - `sep`: Delimiter for CSV (default: `,`).
  - `header`: Row number for column names (default: 0).
  - `index_col`: Column to set as index.
  - `dtype`: Specify column data types.
  - `na_values`: Values to treat as NaN.

**Example Setup**:
For the examples below, assume the following sample files exist:
- `data.csv`: Contains columns `Name, Age, City`.
- `data.xlsx`: Similar structure in Excel format.
- `data.json`: JSON data with similar fields.
- SQLite database with a `users` table.

## 2. Reading JSON, SQL, CSV, and Excel
### CSV
- Syntax: `pd.read_csv(file_path, sep=',', header=0, index_col=None)`
- Example:
  ```python
  import pandas as pd

  # Sample CSV content: Name,Age,City
  # Alice,25,New York
  # Bob,30,London
  df_csv = pd.read_csv("data.csv")
  print(df_csv)
  #     Name  Age     City
  # 0  Alice   25  New York
  # 1    Bob   30   London
  ```

### Excel
- Requires `openpyxl` or `xlrd`: `pip install openpyxl`
- Syntax: `pd.read_excel(file_path, sheet_name=0)`
- Example:
  ```python
  df_excel = pd.read_excel("data.xlsx", sheet_name="Sheet1")
  print(df_excel)
  # Similar output to CSV
  ```

### JSON
- Syntax: `pd.read_json(file_path, orient='records')`
- Example (assuming `data.json`: `[{"Name": "Alice", "Age": 25, "City": "New York"}, {"Name": "Bob", "Age": 30, "City": "London"}]`)
  ```python
  df_json = pd.read_json("data.json")
  print(df_json)
  #     Name  Age     City
  # 0  Alice   25  New York
  # 1    Bob   30   London
  ```

### SQL
- Requires `sqlalchemy`: `pip install sqlalchemy`
- Syntax: `pd.read_sql(query, connection)`
- Example:
  ```python
  from sqlalchemy import create_engine
  engine = create_engine("sqlite:///database.db")
  df_sql = pd.read_sql("SELECT * FROM users", engine)
  print(df_sql)
  # Similar output to CSV
  ```

**Note**: Always ensure proper file paths and dependencies are installed.

## 3. Basic Analysis Commands
Pandas provides methods to quickly summarize and explore data in a `DataFrame`.

- **Key Methods**:
  - `df.head(n)`: View first `n` rows (default: 5).
  - `df.tail(n)`: View last `n` rows.
  - `df.info()`: Display column names, dtypes, and non-null counts.
  - `df.describe()`: Summary statistics (count, mean, std, min, max, quartiles).
  - `df.shape`: Tuple of (rows, columns).
  - `df.columns`: List of column names.
  - `df.value_counts()`: Count unique values in a column.

**Example**:
```python
# Sample DataFrame
data = pd.DataFrame({
    "Name": ["Alice", "Bob", "Charlie"],
    "Age": [25, 30, 35],
    "City": ["New York", "London", "Paris"]
})
print(data.head(2))  # First 2 rows
#     Name  Age     City
# 0  Alice   25  New York
# 1    Bob   30   London

print(data.info())
# <class 'pandas.core.frame.DataFrame'>
# RangeIndex: 3 entries, 0 to 2
# Data columns (total 3 columns):
#  #   Column  Non-Null Count  Dtype 
# ---  ------  --------------  ----- 
#  0   Name    3 non-null      object
#  1   Age     3 non-null      int64 
#  2   City    3 non-null      object
# dtypes: int64(1), object(2)

print(data.describe())
#             Age
# count  3.000000
# mean  30.000000
# std    5.000000
# min   25.000000
# 25%   27.500000
# 50%   30.000000
# 75%   32.500000
# max   35.000000

print(data["City"].value_counts())
# New York    1
# London      1
# Paris       1
# Name: City, dtype: int64
```

## 4. Data Cleaning Steps
Data cleaning ensures data quality by handling missing values, duplicates, and inconsistencies.

- **Handling Missing Values**:
  - `df.isna()`: Detect missing values.
  - `df.fillna(value)`: Fill missing values.
  - `df.dropna()`: Remove rows/columns with missing values.
- **Removing Duplicates**:
  - `df.duplicated()`: Identify duplicate rows.
  - `df.drop_duplicates()`: Remove duplicates.
- **Data Type Conversion**:
  - `df.astype(dtype)`: Convert column types.
  - `pd.to_numeric()`, `pd.to_datetime()`: Convert to numeric or datetime.
- **String Cleaning**:
  - `df.str.strip()`, `df.str.lower()`: Clean string columns.

**Example**:
```python
# Sample DataFrame with issues
data = pd.DataFrame({
    "Name": ["Alice", "Bob", "Alice", None],
    "Age": [25, None, 25, 30],
    "City": [" New York ", "London", "New York", " Paris "]
})

# Check missing values
print(data.isna())
#     Name    Age   City
# 0  False  False  False
# 1  False   True  False
# 2  False  False  False
# 3   True  False  False

# Fill missing values
data["Age"].fillna(data["Age"].mean(), inplace=True)
data["Name"].fillna("Unknown", inplace=True)

# Remove duplicates
data = data.drop_duplicates()

# Clean strings
data["City"] = data["City"].str.strip().str.lower()

# Convert types
data["Age"] = data["Age"].astype(int)

print(data)
#      Name  Age     City
# 0   Alice   25  new york
# 1     Bob   27   london
# 3  Unknown   30    paris
```

## 5. Filtering and Selecting Columns
Pandas allows flexible data selection and filtering.

- **Selecting Columns**:
  - Single column: `df["column"]` (returns Series).
  - Multiple columns: `df[["col1", "col2"]]`.
  - Dot notation: `df.col1` (if column name is valid).
- **Filtering Rows**:
  - Boolean indexing: `df[condition]`.
  - `df.loc[label]`: Label-based indexing.
  - `df.iloc[index]`: Integer-based indexing.
  - `df.query(expr)`: Filter using query expression.

**Example**:
```python
# Sample DataFrame
data = pd.DataFrame({
    "Name": ["Alice", "Bob", "Charlie"],
    "Age": [25, 30, 35],
    "City": ["New York", "London", "Paris"]
})

# Select columns
names = data["Name"]  # Series
subset = data[["Name", "City"]]  # DataFrame
print(names)
# 0      Alice
# 1        Bob
# 2    Charlie
# Name: Name, dtype: object

# Filter rows
adults = data[data["Age"] >= 30]
print(adults)
#      Name  Age   City
# 1     Bob   30  London
# 2  Charlie   35   Paris

# Using loc and iloc
print(data.loc[1, "City"])  # London
print(data.iloc[0:2, 0:2])  # First 2 rows, first 2 columns
#     Name  Age
# 0  Alice   25
# 1    Bob   30

# Query
print(data.query("Age > 25"))
#      Name  Age   City
# 1     Bob   30  London
# 2  Charlie   35   Paris
```

## 6. Time Series Analysis: Working with Dates and Times
Pandas excels at handling time series data, with robust support for date parsing, manipulation, and resampling.

### Working with Dates and Times
- **Parsing Dates**:
  - `pd.to_datetime(column)`: Convert to datetime.
  - Set index: `df.set_index("date_column")`.
- **Date Components**:
  - Access via `.dt`: `.dt.year`, `.dt.month`, `.dt.day`, etc.
- **Date Arithmetic**:
  - Add/subtract: `df["date"] + pd.Timedelta(days=1)`.

**Example**:
```python
# Sample time series data
data = pd.DataFrame({
    "Date": ["2025-01-01", "2025-01-02", "2025-01-03"],
    "Sales": [100, 150, 200]
})
data["Date"] = pd.to_datetime(data["Date"])

# Set Date as index
data.set_index("Date", inplace=True)

# Extract components
data["Year"] = data.index.year
data["Month"] = data.index.month
print(data)
#             Sales  Year  Month
# Date                         
# 2025-01-01    100  2025      1
# 2025-01-02    150  2025      1
# 2025-01-03    200  2025      1

# Date arithmetic
data["NextDay"] = data.index + pd.Timedelta(days=1)
print(data["NextDay"])
# Date
# 2025-01-01   2025-01-02
# 2025-01-02   2025-01-03
# 2025-01-03   2025-01-04
# Name: NextDay, dtype: datetime64[ns]
```

### Resampling and Frequency Conversion
- **Resampling**:
  - `df.resample(rule)`: Aggregate data over time intervals (e.g., "D" for daily, "M" for monthly).
  - Methods: `mean()`, `sum()`, `count()`, etc.
- **Frequency Conversion**:
  - `df.asfreq(freq)`: Convert to specified frequency, filling missing values if needed.

**Example**:
```python
# Sample time series with hourly data
dates = pd.date_range("2025-01-01", periods=24, freq="H")
data = pd.DataFrame({"Sales": np.random.randint(50, 150, 24)}, index=dates)

# Resample to daily mean
daily = data.resample("D").mean()
print(daily)
#                      Sales
# 2025-01-01  99.583333

# Convert to 6-hour frequency
six_hourly = data.asfreq("6H", method="ffill")
print(six_hourly)
#                      Sales
# 2025-01-01 00:00:00     87
# 2025-01-01 06:00:00    123
# 2025-01-01 12:00:00     95
# 2025-01-01 18:00:00    102
```

## 7. Merging and Joining DataFrames
Pandas supports combining DataFrames using merging, joining, and concatenation.

- **Concatenation**:
  - Syntax: `pd.concat([df1, df2], axis=0)` (stack vertically) or `axis=1` (horizontally).
- **Merging**:
  - Syntax: `pd.merge(df1, df2, on="key", how="inner")`
  - `how`: `"inner"`, `"left"`, `"right"`, `"outer"`.
- **Joining**:
  - Syntax: `df1.join(df2, how="inner")` (requires index alignment).

**Example**:
```python
# Sample DataFrames
df1 = pd.DataFrame({
    "Name": ["Alice", "Bob"],
    "Age": [25, 30]
})
df2 = pd.DataFrame({
    "Name": ["Alice", "Charlie"],
    "City": ["New York", "Paris"]
})

# Concatenate vertically
concat = pd.concat([df1, df2], ignore_index=True)
print(concat)
#      Name  Age   City
# 0   Alice   25    NaN
# 1     Bob   30    NaN
# 2   Alice  NaN  New York
# 3  Charlie  NaN    Paris

# Merge
merged = pd.merge(df1, df2, on="Name", how="outer")
print(merged)
#      Name  Age     City
# 0   Alice   25  New York
# 1     Bob   30      NaN
# 2  Charlie  NaN    Paris

# Join (set index first)
df1.set_index("Name", inplace=True)
df2.set_index("Name", inplace=True)
joined = df1.join(df2, how="inner")
print(joined)
#         Age     City
# Name                
# Alice    25  New York
```

## 8. Advanced Data Manipulation
### Applying Functions Row-wise or Column-wise
Pandas allows applying functions to rows, columns, or entire DataFrames using `apply`, `map`, and `applymap`.

- **Series.map()**: Apply function to each element in a Series.
  - Syntax: `series.map(function)`
- **DataFrame.apply()**: Apply function along an axis (0 for columns, 1 for rows).
  - Syntax: `df.apply(function, axis=0)`
- **DataFrame.applymap()**: Apply function to every element in DataFrame (deprecated in favor of `map` for Series or `apply` with lambda; use `df.map()` in newer versions for element-wise operations).

**Example**:
```python
# Sample DataFrame
data = pd.DataFrame({
    "Name": ["Alice", "Bob"],
    "Age": [25, 30],
    "Salary": [50000, 60000]
})

# Series.map: Transform single column
data["Name"] = data["Name"].map(str.upper)
print(data["Name"])
# 0    ALICE
# 1      BOB
# Name: Name, dtype: object

# DataFrame.apply: Apply to rows or columns
data["Age_Salary_Sum"] = data[["Age", "Salary"]].apply(sum, axis=1)
print(data)
#      Name  Age  Salary  Age_Salary_Sum
# 0  ALICE   25   50000           50025
# 1    BOB   30   60000           60030

# Element-wise with lambda (applymap replacement)
data[["Age", "Salary"]] = data[["Age", "Salary"]].map(lambda x: x * 2)
print(data)
#      Name  Age  Salary  Age_Salary_Sum
# 0  ALICE   50  100000           50025
# 1    BOB   60  120000           60030

# Custom function with apply
def categorize_age(row):
    return "Senior" if row["Age"] > 55 else "Junior"
data["Category"] = data.apply(categorize_age, axis=1)
print(data)
#      Name  Age  Salary  Age_Salary_Sum Category
# 0  ALICE   50  100000           50025   Junior
# 1    BOB   60  120000           60030   Senior
```

## 9. Practical Data Analysis Example
Let’s combine these concepts to analyze a sample dataset (inspired by real-world datasets like wine quality).

**Scenario**: Analyze sales data from a CSV file with columns `Date`, `Product`, `Sales`, and `Region`.

**Code**:
```python
import pandas as pd
import numpy as np

# Sample CSV data
data = pd.DataFrame({
    "Date": ["2025-01-01", "2025-01-01", "2025-01-02", None],
    "Product": ["A", "B", "A", "B"],
    "Sales": [100, 150, 200, np.nan],
    "Region": ["East", "West", "East", "West"]
})

# Save and read CSV
data.to_csv("sales.csv", index=False)
df = pd.read_csv("sales.csv")

# Data cleaning
df["Date"] = pd.to_datetime(df["Date"])
df["Sales"].fillna(df["Sales"].mean(), inplace=True)
df.dropna(subset=["Date"], inplace=True)

# Basic analysis
print(df.describe())
#             Sales
# count    3.000000
# mean   150.000000
# std     50.000000
# min    100.000000
# 25%    125.000000
# 50%    150.000000
# 75%    175.000000
# max    200.000000

# Filtering
east_sales = df[df["Region"] == "East"]
print(east_sales)
#         Date Product  Sales Region
# 0 2025-01-01       A  100.0   East
# 2 2025-01-02       A  200.0   East

# Time series: Resample by day
df.set_index("Date", inplace=True)
daily_sales = df["Sales"].resample("D").sum()
print(daily_sales)
# Date
# 2025-01-01    250.0
# 2025-01-02    200.0
# Freq: D, Name: Sales, dtype: float64

# Apply function
df["Sales_Doubled"] = df["Sales"].map(lambda x: x * 2)
print(df[["Product", "Sales", "Sales_Doubled"]])
#            Product  Sales  Sales_Doubled
# Date                                  
# 2025-01-01       A  100.0          200.0
# 2025-01-01       B  150.0          300.0
# 2025-01-02       A  200.0          400.0
```

## 10. Resources for Learning Pandas
- Official Documentation: [pandas.pydata.org/docs](https://pandas.pydata.org/docs)
- Pandas Cheat Sheet: [DataCamp](https://www.datacamp.com)
- Tutorials: [Dataquest Pandas Tutorial](https://www.dataquest.io)
- Practice: [Kaggle Pandas Exercises](https://www.kaggle.com)
- X Posts: Highlight Pandas as essential for data cleaning, time series, and integration with Matplotlib for visualization.

**Conclusion**: Pandas is a cornerstone of Python data analysis, offering intuitive tools for data import, cleaning, filtering, time series analysis, and advanced manipulation. Its integration with NumPy and other libraries like Matplotlib and Scikit-learn makes it indispensable for data scientists.