Exno:1
Data Cleaning Process

AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

Coding and Output

Screenshot 2025-03-06 155455

IMPORT CSV FILE HERE
from google.colab import files
import pandas as pd
uploaded = files.upload()
df = pd.read_csv('Data_set.csv')
df.head()
image

READ CSV FILE HERE
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
from scipy import stats

exp=pd.read_csv("Data_set.csv")
exp.head()
Screenshot 2025-03-06 155846

DISPLAY THE INFORMATION ABOUT CSV AND RUN THE BASIC DATA ANALYSIS FUNCTIONS
df.info()
print()
df.describe()
image

CHECK OUT NULL VALUES IN DATA SET USING FUNCTION
df.isnull().sum()
image

DISPLAY THE SUM ON NULL VALUES IN EACH ROWS
df.isnull().sum(axis=1)
image

DROP NULL VALUES
df_dropna = df.dropna()
df_dropna
image

FILL NULL VALUES WITH CONSTANT VALUE "O"
df_filled_const = df.fillna("O")
df_filled_const
image

FILL NULL VALUES WITH ffill or bfill METHOD
df_ffill = df.ffill()
df_bfill = df.bfill()
(df_ffill)
(df_bfill)
image

CALCULATE MEAN VALUE OF A COLUMN AND FILL IT WITH NULL VALUES
column_name = "your_column" 
if column_name in df.columns and df[column_name].dtype in ['int64', 'float64']:
    df[column_name].fillna(df[column_name].mean(), inplace=True)
df
image

OUTLIER DETECTION USING BOXPLOT (AGE DATA)
age = [1, 3, 28, 27, 25, 92, 30, 39, 40, 50, 26, 24, 29, 94]
af = pd.DataFrame(age, columns=['Age'])
af
image

USE BOXPLOT FUNCTION HERE TO DETECT OUTLIER
plt.figure(figsize=(5, 4))
sns.boxplot(y=af["Age"])
plt.title("Boxplot Before Removing Outliers")
plt.show()
image

PERFORM IQR METHOD AND DETECT OUTLIER VALUES
Q1 = af["Age"].quantile(0.25)
Q3 = af["Age"].quantile(0.75)
IQR = Q3 - Q1

lower_bound = Q1 - 1.5 * IQR
upper_bound = Q3 + 1.5 * IQR

outliers = af[(af["Age"] < lower_bound) | (af["Age"] > upper_bound)]
outliers
image

REMOVE OUTLIERS
af_no_outliers = af[(af["Age"] >= lower_bound) & (af["Age"] <= upper_bound)]
af_no_outliers
image

BOXPLOT AFTER OUTLIER REMOVAL
plt.figure(figsize=(5, 4))
sns.boxplot(y=af_no_outliers["Age"])
plt.title("Boxplot After Removing Outliers")
plt.show()
420003761-4e9f275c-c264-4a74-9743-a59815ef998e

OUTLIER DETECTION USING Z-SCORE METHOD
data = [1, 12, 15, 18, 21, 24, 27, 30, 33, 36, 39, 42, 45, 48, 51, 54, 57, 60,
        63, 66, 69, 72, 75, 78, 81, 84, 87, 90, 93, 96, 99, 158]
df = pd.DataFrame(data, columns=["Values"])
df
420004920-d4394422-7b8a-410c-895c-0bf017fe8287

BOXPLOT BEFORE Z-SCORE OUTLIER REMOVAL
plt.figure(figsize=(5, 4))
sns.boxplot(y=df["Values"])
plt.title("Boxplot Before Removing Z-Score Outliers")
plt.show()
420005861-2d26cb30-e644-4159-9af1-84bdebd09f59

CALCULATE Z-SCORES
from scipy import stats 
df["Z_Score"] = stats.zscore(df["Values"])

420006695-5fd82c9b-4b95-47d1-b5b8-1e24372cd59e

SET THRESHOLD TO DETECT OUTLIERS (|Z| > 3)
outliers_z = df[abs(df["Z_Score"]) > 3]
outliers_z
420007943-e56af5c3-c5a0-407d-805f-34f43635deb0

REMOVE OUTLIERS BASED ON Z-SCORE
df_no_outliers = df[abs(df["Z_Score"]) <= 3].drop(columns=["Z_Score"])
df_no_outliers
420009275-5422ed7b-e60e-4285-b4e1-afc682cd97be

BOXPLOT AFTER Z-SCORE OUTLIER REMOVAL
plt.figure(figsize=(5, 4))
sns.boxplot(y=df_no_outliers["Values"])
plt.title("Boxplot After Removing Z-Score Outliers")
plt.show()
420009713-9a1df7c6-6ef9-4e3d-b3cb-0286338f6ced

Result
Hence the data was cleaned , outliers were detected and removed.
