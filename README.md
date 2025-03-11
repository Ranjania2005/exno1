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
```
#READ CSV FILE HERE
```
df=pd.read_csv("Data_set.csv")
df
```

#DISPLAY THE INFORMATION ABOUT CSV AND RUN THE BASIC DATA ANALYSIS FUNCTIONS
```
df.head()
```
```
df.tail()
```
```
df.info()
```
```
df.describe()
```

#CHECK OUT NULL VALUES IN DATA SET USING FUNCTION
```
df.isnull()
```
```
df.notnull()
```

#DISPLAY THE SUM ON NULL VALUES IN EACH ROWS
```
sum_of_df=df.isnull().sum(axis=1)
sum_of_df
```
#DROP NULL VALUES
```
drop_null=df.dropna()
drop_null
```
#FILL NULL VALUES WITH CONSTANT VALUE "O"
```
fill_null_value=df.fillna(0)
fill_null_value
```
#FILL NULL VALUES WITH ffill or bfill METHOD
```
null_with_ffill=df.fillna(method='ffill')
null_with_ffill
```
```
null_with_bfill=df.fillna(method='bfill')
null_with_bfill
```

#CALCULATE MEAN VALUE OF A COLUMN AND FILL IT WITH NULL VALUES
```
mean_value = df['num_episodes'].mean()
mean_value
df['num_episodes'] = df['num_episodes'].fillna(mean_value)
df.head()
```
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
#USE BOXPLOT FUNCTION HERE TO DETECT OUTLIER

```
sns.boxplot(data=af)
```
```
sns.scatterplot(data=af)
```

#PERFORM IQR METHOD AND DETECT OUTLIER VALUES
```
q1=af.quantile(0.75)
q2=af.quantile(0.5)
q3=af.quantile(0.25)
irq=q3-q1
irq
```
```
Q1=np.percentile(af,25)
Q3=np.percentile(af,75)
IQR=Q3-Q1
IQR
```
```
lower_bound=Q1-1.5*IQR
upper_bound=Q3+1.5*IQR
lower_bound
```
```
upper_bound
```
#REMOVE OUTLIERS
```
outliers=[x for x in age if x<lower_bound or x>upper_bound]
outliers
```
```
af=af[((af>=lower_bound)&(af<=upper_bound))]
af
```
```
af.dropna()
```

#USE BOXPLOT FUNCTION HERE TO CHECK OUTLIER IS REMOVED
```
sns.boxplot(data=af)
```
```
sns.scatterplot(data=af)
```
from scipy import stats #STATS METHOD IS USED TO IMPLEMENT Z SCORE METHOD
# Result
          <<include your Result here>>
