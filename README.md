================================================================================
                     AIR QUALITY DATASET – DATA CLEANING
================================================================================

1. DATASET SOURCE
--------------------------------------------------------------------------------
The dataset used for this project is an Air Quality dataset (airquality.csv)
containing weather and environmental measurements such as temperature, 
pressure, humidity, wind speed, and weather condition.

The dataset was loaded into Python using the Pandas library and processed using 
Google Colab.


2. DATASET SIZE BEFORE PREPROCESSING
--------------------------------------------------------------------------------
Before preprocessing, the dataset contained:
  - Rows: 3,500
  - Columns: 11

Columns List:
   1. record_id
   2. date
   3. time
   4. season
   5. month
   6. day_of_week
   7. temperature
   8. pressure
   9. humidity
  10. wind_speed
  11. weather_condition

The initial dataset dimensions were checked using Pandas df.shape.


3. PROBLEMS IDENTIFIED
--------------------------------------------------------------------------------
The following data-quality issues were identified:

3.1 Missing Values:
    Missing values were present in several columns, including:
      • date
      • time
      • temperature
      • pressure
      • humidity
      • wind_speed
      • weather_condition

    The preprocessing code specifically identifies non-numerical columns and 
    removes rows containing missing values in those columns.

3.2 Outliers:
    Potential outliers in numerical data were identified using the Interquartile 
    Range (IQR) method.

    The IQR method uses:
      • Q1 = 25th percentile
      • Q3 = 75th percentile
      • IQR = Q3 − Q1
      • Lower Bound = Q1 − 1.5 × IQR
      • Upper Bound = Q3 + 1.5 × IQR

    Values outside these boundaries were treated as potential outliers.


4. PREPROCESSING TECHNIQUES APPLIED
--------------------------------------------------------------------------------
4.1 Handling Missing Categorical/Time Values:
    Non-numerical columns were identified and rows containing missing values in 
    these columns were removed.
    This was done using: dropna(subset=cat_time_cols)

4.2 Outlier Detection:
    The IQR method was used to identify potential outliers in numerical columns.

4.3 Outlier Replacement:
    Detected numerical outliers were replaced with NaN so that they could be 
    processed during the next step.

4.4 Interpolation:
    Linear interpolation was applied to numerical columns to fill missing 
    values created during outlier removal. The interpolation was performed in 
    both directions to handle missing values at the beginning or end of the 
    dataset.

4.5 Mean Imputation:
    If any numerical missing values remained after interpolation, they were 
    replaced with the mean value of the respective column.


5. DATASET SIZE AFTER PREPROCESSING
--------------------------------------------------------------------------------
After preprocessing, the cleaned dataset contains:
  - Rows: 2,565
  - Columns: 11

Therefore:
  - Rows removed = 3,500 − 2,565 = 935 rows

The number of columns remained unchanged because the preprocessing process 
removed problematic rows rather than deleting columns.


6. FINAL CLEANED DATASET
--------------------------------------------------------------------------------
The final cleaned dataset is:
  filename: airquality_cleaned.csv

Key Characteristics:
  • 2,565 rows
  • 11 columns
  • No remaining missing values
  • The original 11 features are retained

The cleaned dataset was saved as a CSV file after preprocessing. The code also 
prints the final dataset dimensions after cleaning.


7. SUMMARY
--------------------------------------------------------------------------------
Summary Table:
+----------------------+-------+---------+
| Stage                | Rows  | Columns |
+----------------------+-------+---------+
| Before preprocessing | 3,500 | 11      |
| After preprocessing  | 2,565 | 11      |
| Rows removed         |   935 |  0      |
+----------------------+-------+---------+

Preprocessing Step-by-Step Flow:
  1. Missing categorical/time values   -->  Removed affected rows
  2. Numerical outliers                -->  Detected using IQR
  3. Outliers                          -->  Replaced with NaN
  4. Missing numerical values          -->  Linear interpolation
  5. Remaining numerical missing values-->  Mean imputation
  6. Final dataset                     -->  airquality_cleaned.csv


8. TOOLS USED
--------------------------------------------------------------------------------
  • Python
  • Pandas
  • NumPy
  • Matplotlib
  • Seaborn
  • Google Colab

The cleaning script also generates a correlation heatmap and a distribution 
plot after preprocessing.
================================================================================
