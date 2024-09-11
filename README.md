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
## Data Cleaning
```
import pandas as pd
df=pd.read_csv("/content/SAMPLEIDS.csv")
df

```
![Screenshot 2024-09-11 220924](https://github.com/user-attachments/assets/baffbdb3-2c0c-4ef0-9596-b73b9ab5b348)

```
df.isnull().sum()
```
![Screenshot 2024-09-11 220940](https://github.com/user-attachments/assets/b5788085-cfcc-4777-a1d9-2e51a9179e79)

```
df.isnull().any()
```
![Screenshot 2024-09-11 220951](https://github.com/user-attachments/assets/69aacd1e-2642-4487-a9e3-67803b377474)

```
df.dropna()
```
![Screenshot 2024-09-11 221004](https://github.com/user-attachments/assets/debc8845-888e-4cc6-97dd-15d6eff0a954)

```
df.fillna(0)
```
![Screenshot 2024-09-11 221026](https://github.com/user-attachments/assets/7a66c8df-815e-4c02-9922-013576476dc0)

```
df.fillna(method = "ffill")
```
![Screenshot 2024-09-11 221115](https://github.com/user-attachments/assets/b756f272-700c-4544-96f2-97b5ab55daa1)

```
df.fillna(method = 'bfill')
```
![Screenshot 2024-09-11 221144](https://github.com/user-attachments/assets/99f75cc1-0d5e-479c-aefc-aa7f9104578d)

```
df_dropped = df.dropna()
df_dropped
```
![Screenshot 2024-09-11 221204](https://github.com/user-attachments/assets/c8a0f31a-c42a-4cd0-8312-46eff3867519)

```
df.fillna({'GENDER':'MALE','NAME':'SRI','ADDRESS':'POONAMALEE','M1':98,'M2':87,'M3':76,'M4':92,'TOTAL':305,'AVG':89.999999})
```
![Screenshot 2024-09-11 221239](https://github.com/user-attachments/assets/9ecf6b32-6b79-4bf7-ba90-b7966d8663ea)

## IQR(Inter Quartile Range)
```
ir=pd.read_csv('iris.csv')
ir
```
![Screenshot 2024-09-11 221250](https://github.com/user-attachments/assets/e2b2fa34-6ee1-4030-a678-537dd3508329)

```
ir.describe()
```
![Screenshot 2024-09-11 221259](https://github.com/user-attachments/assets/22e7bd1b-79ae-4c5e-94d9-6bcf97bd35ed)

```
import seaborn as sns
import matplotlib.pyplot as plt
sns.boxplot(x='sepal_width',data=ir)
plt.show()

```
![Screenshot 2024-09-11 221311](https://github.com/user-attachments/assets/e35ee3ca-dd7a-49b0-bb7c-18605a4051f5)

```
 c1=ir.sepal_width.quantile(0.25)
 c3=ir.sepal_width.quantile(0.75)
 iq=c3-c1
 print(c3)
```
![Screenshot 2024-09-11 221318](https://github.com/user-attachments/assets/ea557748-e774-46c7-b912-500cb8424bd3)

```
rid=ir[((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
rid['sepal_width']
```
![Screenshot 2024-09-11 221330](https://github.com/user-attachments/assets/0e56c2ba-bc23-4bcd-8c70-8fd918a88e3f)

```
delid=ir[~((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
delid
```
![Screenshot 2024-09-11 221337](https://github.com/user-attachments/assets/09130590-f413-4b29-81c5-c4c1d13d3563)

```
sns.boxplot(x='sepal_width',data=delid)
```
![Screenshot 2024-09-11 221345](https://github.com/user-attachments/assets/3af32730-94e0-4737-ab7a-637f2d98f7df)


## Z - Score
```
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import scipy.stats as stats
dataset=pd.read_csv("heights.csv")
dataset
```
![Screenshot 2024-09-11 221353](https://github.com/user-attachments/assets/6d1c04cc-9d2a-4db2-9fa8-05d501adf1f6)

```
df = pd.read_csv("heights.csv")
q1 = df['height'].quantile(0.25)
q2 = df['height'].quantile(0.5)
q3 = df['height'].quantile(0.75)
iqr = q3-q1
iqr
```
![Screenshot 2024-09-11 221410](https://github.com/user-attachments/assets/3d4f5c7b-d2b8-4ee6-9e7c-8ed53219fb61)

```
low = q1- 1.5*iqr
low
```
![Screenshot 2024-09-11 221421](https://github.com/user-attachments/assets/506f1d13-e89b-41da-a6fb-62aa7b44894a)

```
high = q3 + 1.5*iqr
high
```
![Screenshot 2024-09-11 221428](https://github.com/user-attachments/assets/8c9d640b-8d16-4d7e-b12a-a661a1b4a691)

```
df1 = df[((df['height'] >=low)& (df['height'] <=high))]
df1
```
![Screenshot 2024-09-11 221436](https://github.com/user-attachments/assets/2d7a0a26-45ae-4f8b-9bfb-dbf27be4df9a)

```
z = np.abs(stats.zscore(df['height']))
z
```
![Screenshot 2024-09-11 221444](https://github.com/user-attachments/assets/50048ddd-ebc5-4e27-84d2-47bfbc9b2fd4)

```
df1 = df[z<3]
df1
```
![Screenshot 2024-09-11 221450](https://github.com/user-attachments/assets/15dde685-9871-4065-8a2e-82556ede2d6f)

# Result
Thus we have cleaned the data and removed the outliers by detection using IQR and Z-score method.
