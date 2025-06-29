# Step 1: Import pandas
import pandas as pd

# Step 2: Load the dataset
df = pd.read_csv("customer_personality.csv")

# Show top 5 rows
print(df.head())
# Output (example):
#   ID  Year_Birth Education Marital_Status   Income  ... Dt_Customer
# 0  5524      1957  Graduation       Single    58138  ...   04-09-2012
# 1  2174      1954  Graduation     Together    46344  ...   08-03-2014
# 2  4141      1965  Graduation     Together    71613  ...   21-08-2013
# 3  6182      1984    PhD           Married    26646  ...   10-02-2014
# 4  5324      1981  Graduation     Together    58293  ...   19-01-2014

# Step 3: Check info and missing values
print(df.info())
print(df.isnull().sum())
# Output:
# Income           24
# Dt_Customer       0
# ... (other columns)

# Step 4: Handle missing values
df['Income'] = df['Income'].fillna(df['Income'].median())

# Step 5: Remove duplicates
df = df.drop_duplicates()

# Step 6: Standardize text columns
df['Marital_Status'] = df['Marital_Status'].str.lower().str.strip()
df['Education'] = df['Education'].str.lower().str.strip()

# Step 7: Convert 'Dt_Customer' to datetime
df['Dt_Customer'] = pd.to_datetime(df['Dt_Customer'], format='%d-%m-%Y', errors='coerce')

# Step 8: Clean column names
df.columns = df.columns.str.lower().str.replace(" ", "_")

# Step 9: Fix data types
df['year_birth'] = df['year_birth'].astype(int)
df['income'] = df['income'].astype(float)

# Step 10: Export the cleaned dataset
df.to_csv("cleaned_customer_personality.csv", index=False)

# Check final result
print(df.head())
# Output (cleaned and formatted data)
id  year_birth education marital_status   income  dt_customer
0  5524        1957 graduation         single  58138.0  2012-09-04
1  2174        1954 graduation       together  46344.0  2014-03-08
2  4141        1965 graduation       together  71613.0  2013-08-21
3  6182        1984        phd        married  26646.0  2014-02-10
4  5324        1981 graduation       together  58293.0  2014-01-19

** Summary of My Data Cleaning Project :- 
In this project, I worked on cleaning and preprocessing the Customer Personality Analysis dataset using Python and Pandas. The dataset had issues like missing values, duplicate rows, inconsistent text formatting, and incorrect data types, which I fixed step by step.

Steps I Performed:-
Loaded the dataset using pandas.read_csv().

Checked for missing values using isnull().sum()
→ Found some missing values in the Income column and filled them using the median.

Removed duplicate records using drop_duplicates() to ensure the data was unique.

Standardized text columns like Marital_Status and Education
→ I converted all values to lowercase and removed extra spaces for consistency.

Converted the date column Dt_Customer to proper datetime format using pd.to_datetime().

Renamed all column headers to lowercase and replaced spaces with underscores using str.lower() and str.replace().

Fixed data types
→ Converted year_birth to int and Income to float to ensure correct analysis later.

Exported the cleaned dataset to a new CSV file cleaned_customer_personality.csv using to_csv().

** What I Learned Most From :-
The part where I learned the most was:

Handling missing values and standardizing text data.
I understood how to decide between filling vs. dropping missing values and saw how important it is to clean text fields (like gender, marital status, etc.) for accurate grouping or analysis.

I also learned how small issues like inconsistent casing (Single vs single) or wrong date formats can create big problems in analysis — and how to fix them.
