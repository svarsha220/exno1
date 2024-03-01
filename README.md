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

## DATA CLEANING
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
data = pd.read_csv("/content/SAMPLEIDS.csv")
data.head()
```
![image](https://github.com/svarsha220/exno1/assets/127709117/ab891d93-87db-43d3-a536-1ae61ddb1805)
```
data = pd.get_dummies(data)
data.isnull().sum()
```
![image](https://github.com/svarsha220/exno1/assets/127709117/32f5c820-1345-48b9-b90c-6df47ddfcf0a)
```
columns_with_null = data.columns[data.isnull().any()]
import seaborn as sns
plt.figure(figsize=(10,10))
sns.barplot(columns_with_null)
plt.title("NULL VALUES")
plt.show()
```
![image](https://github.com/svarsha220/exno1/assets/127709117/c5b290b9-e8fc-4ff8-a62a-3f69d023f613)
```
for column in columns_with_null:
    median = data[column].median()  
    data[column].fillna(median, inplace=True)
data.isnull().sum().sum()
```
![image](https://github.com/svarsha220/exno1/assets/127709117/4afd8788-f4be-4344-b2ca-c16df4003229)

## IQR
```
import pandas as pd
import seaborn as sns
ir = pd.read_csv("/content/iris (1).csv")
ir.head()
```
![image](https://github.com/Yamunaasri/exno1/assets/115707860/93d4d44c-8a8e-42ba-b50e-0d427a929e41)
```
ir.describe()
```
![image](https://github.com/svarsha220/exno1/assets/127709117/694f0b0b-da98-47d1-9270-fb6c7d09f147)

```
sns.boxplot(x='sepal_width',data=ir)
```
![image](https://github.com/svarsha220/exno1/assets/127709117/dadebcec-c0a2-4aa4-9661-0d9c0c520c11)
```
c1=ir.sepal_width.quantile(0.25)
c3=ir.sepal_width.quantile(0.75)
iq=c3-c1
print(c3)
```
![image](https://github.com/svarsha220/exno1/assets/127709117/6a02c574-ee45-41c2-bbde-0fd03d0c7a2a)
```
rid=ir[((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
rid['sepal_width']
```
![image](https://github.com/svarsha220/exno1/assets/127709117/b752a2bf-02e1-4819-baa5-19fed06f0384)
```
delid=ir[~((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
delid
```
![image](https://github.com/svarsha220/exno1/assets/127709117/6dce4791-81ab-44c1-a280-1f786b6c2aa1)

```
sns.boxplot(x='sepal_width',data=delid)
```
![image](https://github.com/svarsha220/exno1/assets/127709117/fa9e350c-18e4-4fe8-b460-d595d42c8944)

## Z SCORE
```
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import scipy.stats as stats
dataset=pd.read_csv("/content/heights.csv")
dataset
```
![image](https://github.com/svarsha220/exno1/assets/127709117/5b873813-33c7-43be-b564-5d781cf05e51)

```
df = pd.read_csv("heights.csv")
q1 = df['height'].quantile(0.25)
q2 = df['height'].quantile(0.5)
q3 = df['height'].quantile(0.75)
```
```
iqr = q3-q1
iqr
```
![image](https://github.com/svarsha220/exno1/assets/127709117/e825d2fd-63e5-45c0-bbf5-35371887d875)

```
low = q1 - 1.5*iqr
low
```
![image](https://github.com/svarsha220/exno1/assets/127709117/fd373b56-6a17-45f0-8014-9cc5756903fc)

```
high = q3 + 1.5*iqr
high
```
![image](https://github.com/svarsha220/exno1/assets/127709117/4d6208fa-61e6-412e-9402-32457a193600)

```
df1 = df[((df['height'] >=low)& (df['height'] <=high))]
df1
```
![image](https://github.com/svarsha220/exno1/assets/127709117/68195ac1-f477-41a4-9366-08408c504576)

```
z = np.abs(stats.zscore(df['height']))
z
```
![image](https://github.com/svarsha220/exno1/assets/127709117/018aae84-3a43-4c6c-842c-c5dffc813722)

# Result
Thus the outliers are detected and removed in the given file and the final data set is saved into the file.
