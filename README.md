# TASK---01-DATA-ANALYST-
INTERNSHIP PROJECTS
import pandas as pd

# Load the dataset
df = pd.read_csv("marketing_campaign.csv1.csv")

# Display basic info before cleaning
print("Original Dataset Info:")
print(df.info())
print("Missing values before cleaning:", df.isnull().sum())

# ----------------------------
# Cleaning Steps

#  Drop duplicates
df.drop_duplicates(inplace=True)

#  Handle missing values - drop rows with missing data 
df.dropna(inplace=True)

#  Change 'Dt_Customer' to datetime if present
if 'Dt_Customer' in df.columns:
    df['Dt_Customer'] = pd.to_datetime(df['Dt_Customer'], errors='coerce')

#  Strip whitespace from column names
df.columns = df.columns.str.strip()

#  Drop columns with constant values (if any)
df = df.loc[:, df.nunique() > 1]

# dropoe the single column
df = df.drop(columns=['Dt_Customer'])


# ----------------------------
# Summary of Cleaning
# ----------------------------
print("Cleaned Dataset Info:")
print(df.info())
print("Missing values after cleaning:", df.isnull().sum())

print("\nSummary of changes made:")
print("Removed duplicate rows")
print("Dropped rows with missing values")
print("Converted 'Dt_Customer' to datetime format")
print("Stripped whitespace from column names")

# cleaned dataset
df.to_csv("marketing_campaign.csv1.csv", index=False)
df
