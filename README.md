# Exno:1
***Data Cleaning Process***

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output

![Screenshot 2025-03-06 155455](https://github.com/user-attachments/assets/117d5c37-04bb-40d1-ac79-2e4d341bed03)

# IMPORT CSV FILE HERE
```
from google.colab import files
import pandas as pd
uploaded = files.upload()
df = pd.read_csv('Data_set.csv')
df.head()
```
![image](https://github.com/user-attachments/assets/66d8d8d9-affc-4e6e-9709-67d95c72cdd6)

# READ CSV FILE HERE
```
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
from scipy import stats

exp=pd.read_csv("Data_set.csv")
exp.head()
```
![Screenshot 2025-03-06 155846](https://github.com/user-attachments/assets/6fed09d9-9cb3-4904-8b66-5fbd1958a250)


# DISPLAY THE INFORMATION ABOUT CSV AND RUN THE BASIC DATA ANALYSIS FUNCTIONS
```
df.info()
print()
df.describe()
```
![image](https://github.com/user-attachments/assets/b6b0903a-0945-4e45-9176-0361987acec3)

# CHECK OUT NULL VALUES IN DATA SET USING FUNCTION

```
df.isnull().sum()
```
![image](https://github.com/user-attachments/assets/69633293-a574-4ee1-a12d-35b01f4c4a0c)

# DISPLAY THE SUM ON NULL VALUES IN EACH ROWS
```
df.isnull().sum(axis=1)
```
![image](https://github.com/user-attachments/assets/15e4d8f6-97ea-4aa7-bb95-53cbf50c68ca)

# DROP NULL VALUES
```
df_dropna = df.dropna()
df_dropna
```
![image](https://github.com/user-attachments/assets/827b1f15-b82b-4ac2-ac51-d26b900bf2a5)

# FILL NULL VALUES WITH CONSTANT VALUE "O"
```
df_filled_const = df.fillna("O")
df_filled_const
```
![image](https://github.com/user-attachments/assets/2a76d21e-8e52-41fb-93bf-f3c232552948)

# FILL NULL VALUES WITH ffill or bfill METHOD
```
df_ffill = df.ffill()
df_bfill = df.bfill()
(df_ffill)
(df_bfill)
```
![image](https://github.com/user-attachments/assets/a8aa2575-332e-4188-9d91-f15cc9109857)

# CALCULATE MEAN VALUE OF A COLUMN AND FILL IT WITH NULL VALUES
```
column_name = "your_column" 
if column_name in df.columns and df[column_name].dtype in ['int64', 'float64']:
    df[column_name].fillna(df[column_name].mean(), inplace=True)
df
```
![image](https://github.com/user-attachments/assets/ea91e288-65d1-4a54-a193-2895ad53326f)

 # OUTLIER DETECTION USING BOXPLOT (AGE DATA)
```
age = [1, 3, 28, 27, 25, 92, 30, 39, 40, 50, 26, 24, 29, 94]
af = pd.DataFrame(age, columns=['Age'])
af
```
![image](https://github.com/user-attachments/assets/60dd6ec9-c492-4ae5-abc1-74fc5e59af51)

# USE BOXPLOT FUNCTION HERE TO DETECT OUTLIER
```
plt.figure(figsize=(5, 4))
sns.boxplot(y=af["Age"])
plt.title("Boxplot Before Removing Outliers")
plt.show()
```
![image](https://github.com/user-attachments/assets/3e057adb-708b-422b-b3e3-bddc3d06ebc6)

# PERFORM IQR METHOD AND DETECT OUTLIER VALUES
```
Q1 = af["Age"].quantile(0.25)
Q3 = af["Age"].quantile(0.75)
IQR = Q3 - Q1

lower_bound = Q1 - 1.5 * IQR
upper_bound = Q3 + 1.5 * IQR

outliers = af[(af["Age"] < lower_bound) | (af["Age"] > upper_bound)]
outliers
```
![image](https://github.com/user-attachments/assets/7f2d7d3b-9691-4422-a1b7-22fec0d96ce3)

# REMOVE OUTLIERS
```
af_no_outliers = af[(af["Age"] >= lower_bound) & (af["Age"] <= upper_bound)]
af_no_outliers
```
![image](https://github.com/user-attachments/assets/338dbe49-0c8e-4597-bfa9-6eb7c944cfa2)

# BOXPLOT AFTER OUTLIER REMOVAL
```
plt.figure(figsize=(5, 4))
sns.boxplot(y=af_no_outliers["Age"])
plt.title("Boxplot After Removing Outliers")
plt.show()
```
![420003761-4e9f275c-c264-4a74-9743-a59815ef998e](https://github.com/user-attachments/assets/39636477-efd7-4f9a-af3b-e8c894c14e33)

# OUTLIER DETECTION USING Z-SCORE METHOD
```
data = [1, 12, 15, 18, 21, 24, 27, 30, 33, 36, 39, 42, 45, 48, 51, 54, 57, 60,
        63, 66, 69, 72, 75, 78, 81, 84, 87, 90, 93, 96, 99, 158]
df = pd.DataFrame(data, columns=["Values"])
df
```
![420004920-d4394422-7b8a-410c-895c-0bf017fe8287](https://github.com/user-attachments/assets/773d53d3-5fca-4517-88de-d47932ffa5da)

# BOXPLOT BEFORE Z-SCORE OUTLIER REMOVAL
```
plt.figure(figsize=(5, 4))
sns.boxplot(y=df["Values"])
plt.title("Boxplot Before Removing Z-Score Outliers")
plt.show()
```
![420005861-2d26cb30-e644-4159-9af1-84bdebd09f59](https://github.com/user-attachments/assets/361d0650-7460-4f56-aa6d-4323d01b4d8c)

# CALCULATE Z-SCORES
```
from scipy import stats 
df["Z_Score"] = stats.zscore(df["Values"])

```
![420006695-5fd82c9b-4b95-47d1-b5b8-1e24372cd59e](https://github.com/user-attachments/assets/f142912b-7885-4726-ae90-156c588d4def)

# SET THRESHOLD TO DETECT OUTLIERS (|Z| > 3)
```
outliers_z = df[abs(df["Z_Score"]) > 3]
outliers_z
```
![420007943-e56af5c3-c5a0-407d-805f-34f43635deb0](https://github.com/user-attachments/assets/ea669b6b-9c9b-489d-8eac-cc2589cfebc5)

# REMOVE OUTLIERS BASED ON Z-SCORE
```
df_no_outliers = df[abs(df["Z_Score"]) <= 3].drop(columns=["Z_Score"])
df_no_outliers
```
![420009275-5422ed7b-e60e-4285-b4e1-afc682cd97be](https://github.com/user-attachments/assets/d195167e-62ad-4302-9fec-d4e0ac759a99)

# BOXPLOT AFTER Z-SCORE OUTLIER REMOVAL
```
plt.figure(figsize=(5, 4))
sns.boxplot(y=df_no_outliers["Values"])
plt.title("Boxplot After Removing Z-Score Outliers")
plt.show()
```
![420009713-9a1df7c6-6ef9-4e3d-b3cb-0286338f6ced](https://github.com/user-attachments/assets/463af1c0-a9ca-4a48-9395-baa88e07893e)



# Result
Hence the data was cleaned , outliers were detected and removed.
