# 🚢 Titanic Data Engineering Pipeline (Pandas vs. PySpark)

An end-to-end Data Cleaning, Transformation, and Feature Engineering pipeline applied to the famous **Titanic Dataset**. 

The goal of this project is to compare implementation patterns, performance, and methodologies between **Pandas** (single-node processing) and **PySpark** (distributed data processing), organized into dedicated modules.

---

## 📁 Repository Structure

```text
├── 📂 pandas_pipeline/
│   └── 📄 pandas_titanic.ipynb      # Complete data pipeline using Pandas
├── 📂 pyspark_pipeline/
│   └── 📄 pyspark_titanic.ipynb     # Complete data pipeline using PySpark
└── 📄 README.md                     # Project documentation

## 🛠️ Tech Stack & Dependencies

* **Language**: Python 3.x
* **Data Processing**: 
  * `pandas` & `numpy` (for local dataframe operations)
  * `pyspark` (Spark SQL & Functions for distributed processing)
* **Environment**: Jupyter Notebook / Google Colab / Databricks

---

##  Key Implementation Highlights

Both folders follow the same structured pipeline to ensure an accurate side-by-side comparison:

1. **Data Cleaning & Imputation**:
   * **Age**: Imputed missing values using the `median`.
   * **Embarked**: Imputed missing values using the `mode`.
   * **Cabin**: Standardized missing values with `"Unknown"`.

2. **Data Type Casting**:
   * Converted numerical types (e.g., `Fare`) from `float` to `Integer`.

3. **Feature Engineering**:
   * **Title Extraction**: Extracted titles (`Mr`, `Mrs`, `Miss`, etc.) from passenger names using Regular Expressions (`Regex`).
   * **Family Size**: Calculated total family members using `SibSp + Parch + 1`.
   * **Fare Categorization**: Binned continuous fare values into discrete levels (`Low`, `Medium`, `High`) using conditional logic (`np.select` vs. `when/otherwise`).

4. **Aggregation & Relational Operations**:
   * Grouped metrics (`max`, `min`, `mean`/`avg`) per embarkation port.
   * Merged/Joined lookup tables to enrich passenger class descriptions.

---

##  Syntax Comparison Summary

| Operation | Pandas Implementation | PySpark Implementation |
| :--- | :--- | :--- |
| **Missing Imputation** | `df['Age'].fillna(df['Age'].median())` | `df.fillna({"Age": median_val})` |
| **Type Casting** | `df['Fare'].astype(int)` | `col("Fare").cast("integer")` |
| **Regex Extraction** | `df['Name'].str.extract(...)` | `regexp_extract(col("Name"), ...)` |
| **Conditional Binning** | `np.select(conditions, choices)` | `when(...).otherwise(...)` |
| **Aggregation** | `df.groupby('Embarked').agg(...)` | `df.groupBy('Embarked').agg(...)` |
| **Joins** | `pd.merge(df1, df2, on='key')` | `df1.join(df2, on='key', how='inner')` |

