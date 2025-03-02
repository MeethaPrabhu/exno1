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
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
data = pd.read_csv("/content/SAMPLEIDS.csv")
data.head()
```
![alt text](image.png)
```data = pd.get_dummies(data)
data.isnull().sum()
```
![alt text](image-1.png)

```
columns_with_null = data.columns[data.isnull().any()]
import seaborn as sns
plt.figure(figsize=(10,10))
sns.barplot(columns_with_null)
plt.title("NULL VALUES")
plt.show()
```
![alt text](image-2.png)

```for column in columns_with_null:
    median = data[column].median()  
    data[column].fillna(median, inplace=True)
data.isnull().sum().sum()
```
![alt text](image-3.png)

## IQR
```
import pandas as pd
import seaborn as sns
ir = pd.read_csv("/content/iris.csv")
ir.head()
```
![alt text](image-4.png)

```
ir.describe()
```
![alt text](image-5.png)

```
sns.boxplot(x='sepal_width',data=ir)
```
![alt text](image-6.png)

```
c1=ir.sepal_width.quantile(0.25)
c3=ir.sepal_width.quantile(0.75)
iq=c3-c1
print(c3)
```
![alt text](image-7.png)

```
rid=ir[((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
rid['sepal_width']
```
![alt text](image-8.png)

```
delid=ir[~((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
delid
```
![alt text](image-9.png)

```
sns.boxplot(x='sepal_width',data=delid)
```
![image](https://github.com/MeethaPrabhu/exno1/assets/119401038/15039a67-a808-453d-b085-563d5a77c054)


## ZSCORE
```
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import scipy.stats as stats
dataset=pd.read_csv("/content/heights.csv")
dataset
```
![alt text](image-11.png)

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
![alt text](image-12.png)

```
low = q1 - 1.5*iqr
low
```
![alt text](image-13.png)

```
high = q3 + 1.5*iqr
high
```
![alt text](image-14.png)

```
df.duplicated()
```
![alt text](image-15.png)

```
df1 = df[((df['height'] >=low)& (df['height'] <=high))]
df1
```
![alt text](image-16.png)

```
z = np.abs(stats.zscore(df['height']))
z
```
![alt text](image-17.png)

# Result
Thus the outliers are detected and removed in the given file and the final data set is saved into the file.
