# Exno:1 Data Cleaning Process

# AIM:
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation:
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
```
# READ CSV FILE HERE
```
df=pd.read_csv("Data_set.csv")
df
```
![Screenshot 2025-03-12 140032](https://github.com/user-attachments/assets/696b420c-a977-46af-87b8-d4a7cb12b901)

# DISPLAY THE INFORMATION ABOUT CSV AND RUN THE BASIC DATA ANALYSIS FUNCTIONS
```
df.head()
```
![Screenshot 2025-03-12 140403](https://github.com/user-attachments/assets/b6c551df-b164-4c30-abd5-661639cf6d5b)

```
df.tail()
```
![Screenshot 2025-03-12 140456](https://github.com/user-attachments/assets/bba033f0-abbb-4b46-a216-38c7688da822)

```
df.info()
```
![Screenshot 2025-03-12 141008](https://github.com/user-attachments/assets/b7324a18-ac58-4067-8766-65059ab42fad)

```
df.describe()
```
![Screenshot 2025-03-12 141016](https://github.com/user-attachments/assets/07ad29c0-f41b-4249-b055-faf60352c4fe)


# CHECK OUT NULL VALUES IN DATA SET USING FUNCTION
```
df.isnull()
```
![Screenshot 2025-03-12 141127](https://github.com/user-attachments/assets/41dfbf9a-050b-4dd0-99b1-c1c5971ea20a)

```
df.notnull()
```
![Screenshot 2025-03-12 141137](https://github.com/user-attachments/assets/c4294214-05cf-4822-b544-8e1c3a67ec14)


# DISPLAY THE SUM ON NULL VALUES IN EACH ROWS
```
sum_of_df=df.isnull().sum(axis=1)
sum_of_df
```
![Screenshot 2025-03-12 141145](https://github.com/user-attachments/assets/509a5352-a9ab-4e2d-b6b9-3bd97a27f4d2)

# DROP NULL VALUES
```
drop_null=df.dropna()
drop_null
```
![Screenshot 2025-03-12 141157](https://github.com/user-attachments/assets/c3b1f9ff-3045-42aa-9df2-87189169c59a)

# FILL NULL VALUES WITH CONSTANT VALUE "O"
```
fill_null_value=df.fillna(0)
fill_null_value
```
![Screenshot 2025-03-12 141215](https://github.com/user-attachments/assets/2b0fa1f2-0a86-44e2-bd2e-747dfd44dccd)

# FILL NULL VALUES WITH ffill or bfill METHOD
```
null_with_ffill=df.fillna(method='ffill')
null_with_ffill
```
![Screenshot 2025-03-12 141229](https://github.com/user-attachments/assets/959e83aa-e594-443f-9c56-cfee491efabf)

```
null_with_bfill=df.fillna(method='bfill')
null_with_bfill
```
![Screenshot 2025-03-12 141239](https://github.com/user-attachments/assets/c9d9891b-4c36-4ccb-86a1-15381d1ff418)

# CALCULATE MEAN VALUE OF A COLUMN AND FILL IT WITH NULL VALUES
```
mean_value = df['num_episodes'].mean()
mean_value
df['num_episodes'] = df['num_episodes'].fillna(mean_value)
df.head()
```
![Screenshot 2025-03-12 141250](https://github.com/user-attachments/assets/03b82c1e-081c-4086-be5f-66c803120f4f)

```
import pandas as pd
import numpy as np
import seaborn as sns
```
```
age=[1,3,28,27,25,92,30,39,40,50,26,24,29,94]
af=pd.DataFrame(age)
af
```
![Screenshot 2025-03-12 141531](https://github.com/user-attachments/assets/b6606ae2-4d22-44bf-9c00-8b5a5c226114)

# USE BOXPLOT FUNCTION HERE TO DETECT OUTLIER

```
sns.boxplot(data=af)
```
![Screenshot 2025-03-12 141538](https://github.com/user-attachments/assets/59b66dc6-d5a9-4fdc-8ce8-14fbb700c0f5)

```
sns.scatterplot(data=af)
```
![Screenshot 2025-03-12 141544](https://github.com/user-attachments/assets/ba8d6d82-0495-46f2-add0-ca203d73a0da)

# PERFORM IQR METHOD AND DETECT OUTLIER VALUES
```
q1=af.quantile(0.75)
q2=af.quantile(0.5)
q3=af.quantile(0.25)
irq=q3-q1
irq
```
![Screenshot 2025-03-12 141551](https://github.com/user-attachments/assets/35d5583c-4818-463c-89ef-12a4fed74617)

```
Q1=np.percentile(af,25)
Q3=np.percentile(af,75)
IQR=Q3-Q1
IQR
```
![Screenshot 2025-03-12 141556](https://github.com/user-attachments/assets/8c3c322e-2b95-4906-841d-5bb6ff6376c0)

```
lower_bound=Q1-1.5*IQR
upper_bound=Q3+1.5*IQR
lower_bound
```
![Screenshot 2025-03-12 141602](https://github.com/user-attachments/assets/1a342717-0c1d-4c85-855b-943733a3adf5)

```
upper_bound
```
![Screenshot 2025-03-12 141606](https://github.com/user-attachments/assets/676930ff-0f77-49cf-8e5c-1b5b18ac6df5)

# REMOVE OUTLIERS
```
outliers=[x for x in age if x<lower_bound or x>upper_bound]
outliers
```
![Screenshot 2025-03-12 141612](https://github.com/user-attachments/assets/6d04c995-d216-48c3-bde6-72c16a5b0e31)

```
af=af[((af>=lower_bound)&(af<=upper_bound))]
af
```
![Screenshot 2025-03-12 141618](https://github.com/user-attachments/assets/7758e394-6bf4-4576-b782-1d135f727373)

```
af.dropna()
```
![Screenshot 2025-03-12 141624](https://github.com/user-attachments/assets/61283903-a260-4c2b-a832-f5d194e8f54a)


# USE BOXPLOT FUNCTION HERE TO CHECK OUTLIER IS REMOVED
```
sns.boxplot(data=af)
```
![Screenshot 2025-03-12 141631](https://github.com/user-attachments/assets/a21d3f93-56a8-4fa4-b653-590647072cb7)

```
sns.scatterplot(data=af)
```
![Screenshot 2025-03-12 141637](https://github.com/user-attachments/assets/511edcc2-145a-4c4f-9147-92ae79242d43)
# STATS METHOD IS USED TO IMPLEMENT Z SCORE METHOD
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from scipy import stats
```
```
data = [1, 12, 15, 18, 21, 24, 27, 30, 33, 36, 39, 42, 45, 48, 51, 54, 57, 60,
        63, 66, 69, 72, 75, 78, 81, 84, 87, 90, 93, 96, 99, 158]
df = pd.DataFrame(data,columns=['Value'])
df
```
![Screenshot 2025-03-12 142332](https://github.com/user-attachments/assets/df6e322f-b4fc-49ff-909d-cbc0c2b9913f)

# USE BOXPLOT FUNCTION HERE TO DETECT OUTLIER
     
```
sns.boxplot(data=df)
plt.show()
```
![Screenshot 2025-03-12 142340](https://github.com/user-attachments/assets/506ce79b-a0eb-4370-bef3-2e2e85dc5122)

# PERFORM Z SCORE METHOD AND DETECT OUTLIER VALUES
```
z_scores = np.abs(stats.zscore(df['Value']))
outliers = df[z_scores > 3]
print( outliers['Value'].tolist())
```
![Screenshot 2025-03-12 142346](https://github.com/user-attachments/assets/d6ceb438-a835-445c-a5bb-aa50e3565275)

# REMOVE OUTLIERS
```
df_clean = df[z_scores <= 3]
```

# USE BOXPLOT FUNCTION HERE TO CHECK OUTLIER IS REMOVED
```
sns.boxplot(data=df_clean)  
plt.show()
```
![Screenshot 2025-03-12 142355](https://github.com/user-attachments/assets/990cfa62-32a5-44a1-8277-ec4f68b63f57)

# Result

Thus we have cleaned the data and removed the outliers by detection using IQR and Z-score method.
