# Exno:1
Data Cleaning Process

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

# READ CSV FILE HERE
```
from google.colab import files
import pandas as pd
uploaded = files.upload()
df = pd.read_csv('Data_set.csv')
df.head()
```
![image](https://github.com/user-attachments/assets/66d8d8d9-affc-4e6e-9709-67d95c72cdd6)


# DISPLAY THE INFORMATION ABOUT CSV AND RUN THE BASIC DATA ANALYSIS FUNCTIONS
```
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
from scipy import stats

exp=pd.read_csv("Data_set.csv")
exp.head()
```
![Screenshot 2025-03-06 155846](https://github.com/user-attachments/assets/6fed09d9-9cb3-4904-8b66-5fbd1958a250)



# CHECK OUT NULL VALUES IN DATA SET USING FUNCTION
```
df.info()
print()
df.describe()
```
![image](https://github.com/user-attachments/assets/b6b0903a-0945-4e45-9176-0361987acec3)


# DISPLAY THE SUM ON NULL VALUES IN EACH ROWS
```
df.isnull().sum()
```
![image](https://github.com/user-attachments/assets/69633293-a574-4ee1-a12d-35b01f4c4a0c)


# DROP NULL VALUES
```
df.isnull().sum(axis=1)
```
![image](https://github.com/user-attachments/assets/15e4d8f6-97ea-4aa7-bb95-53cbf50c68ca)

# FILL NULL VALUES WITH CONSTANT VALUE "O"
```
df_dropna = df.dropna()
df_dropna
```
![image](https://github.com/user-attachments/assets/827b1f15-b82b-4ac2-ac51-d26b900bf2a5)

# FILL NULL VALUES WITH ffill or bfill METHOD
```
df_filled_const = df.fillna("O")
df_filled_const
```
![image](https://github.com/user-attachments/assets/2a76d21e-8e52-41fb-93bf-f3c232552948)

# CALCULATE MEAN VALUE OF A COLUMN AND FILL IT WITH NULL VALUES
```
df_ffill = df.ffill()
df_bfill = df.bfill()
(df_ffill)
(df_bfill)
```
![image](https://github.com/user-attachments/assets/a8aa2575-332e-4188-9d91-f15cc9109857)

# DROP NULL VALUES
```
column_name = "your_column" 
if column_name in df.columns and df[column_name].dtype in ['int64', 'float64']:
    df[column_name].fillna(df[column_name].mean(), inplace=True)
df
```
![image](https://github.com/user-attachments/assets/ea91e288-65d1-4a54-a193-2895ad53326f)

 
```
age = [1, 3, 28, 27, 25, 92, 30, 39, 40, 50, 26, 24, 29, 94]
af = pd.DataFrame(age, columns=['Age'])
af
```
![image](https://github.com/user-attachments/assets/60dd6ec9-c492-4ae5-abc1-74fc5e59af51)


```
plt.figure(figsize=(5, 4))
sns.boxplot(y=af["Age"])
plt.title("Boxplot Before Removing Outliers")
plt.show()
```
![image](https://github.com/user-attachments/assets/3e057adb-708b-422b-b3e3-bddc3d06ebc6)

# USE BOXPLOT FUNCTION HERE TO DETECT OUTLIER
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

# PERFORM IQR METHOD AND DETECT OUTLIER VALUES
```
af_no_outliers = af[(af["Age"] >= lower_bound) & (af["Age"] <= upper_bound)]
af_no_outliers
```
![image](https://github.com/user-attachments/assets/338dbe49-0c8e-4597-bfa9-6eb7c944cfa2)

# Result
Hence the data was cleaned , outliers were detected and removed.
