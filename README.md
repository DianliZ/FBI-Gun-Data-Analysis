# FBI-Gun-Data-Analysis

## Project: FBI Gun Data Analysis
 
### Table of Contents
#### Introduction
#### Data Wrangling
#### Exploratory Data Analysis
#### Conclusions

### Introduction
#### The data comes from the FBI's National Instant Criminal Background Check System. The NICS is used by to determine whether a prospective buyer is eligible to buy firearms or explosives. Gun shops call into this system to ensure that each customer does not have a criminal record or isn’t otherwise ineligible to make a purchase.

#### This dataset investigation will focus on below questions: Which state has the highest purchase in gun registrations? What is the overall trend of gun purchases?

#### The dataset is downloaded from https://s3.amazonaws.com/video.udacity-data.com/topher/2018/July/5b57919a_data-set-options/data-set-options.pdf with the original source on Github

#### References:

>https://stackoverflow.com/;

>https://www.w3schools.com/python/default.asp;

>https://www.programiz.com/python-programming;

>https://www.geeksforgeeks.org/python-programming-language/;

>http://ipython.readthedocs.io/en/stable/interactive/magics.html


*import statements for all of the packages that plan to use.*
```
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
% matplotlib inline
```

### Data Wrangling
#### Load in the data, check for cleanliness, and then trim and clean dataset for analysis.

**General Properties**
*Load data and print out a few lines.*
```
df_Census=pd.read_csv('U.S. Census Data.csv')
df_Census.head()
```

*check the data shape*
```
df_Census.shape
```

*look up data details*
```
df_Census.describe
```

*look for instances of missing or possibly errant data*
```
df_Census.info()
```

*drop null and check the result*
```
df_Census.dropna(inplace=True)
df_Census.info()
```

*data not useful. Data transpose.*
```
df_Census_trans=np.transpose(df_Census)
```
*print out a few lines.* 
```
df_Census_trans.head()
```

*drop rows and print out few lines.*
```
df_Census_trans.drop(df_Census_trans.index[[1]], inplace=True)
df_Census_trans.head()
```

*drop rows and rename the header*
```
T_df=df_Census_trans.rename(columns=df_Census_trans.iloc[0]).drop(df_Census_trans.index[0])
T_df.head()
```

>census data seems not helpful to the questions listed in the instructions
*Load data and print out a few lines.* 
```
df_gundata=pd.read_csv('gun_data.csv')
df_gundata.head()
```

*check the data shape*
```
df_gundata.shape
```

*look up data in details*
```
df_gundata.describe()
```

*look up data in details*
```
df_gundata.info()
```

*quantize on average*
```
df_gundata.groupby('state').totals.mean()
```


### Exploratory Data Analysis
#### Which state has the highest purchase in gun registrations?
*data visualize for higheset purchase*
```
TM=df_gundata.groupby('state').totals.mean().plot(kind='bar');
plt.title("Average by State")
Text(0.5,1,'Average by State')

```

*highest purchase number*
```
sorted(df_gundata.groupby('state').totals.mean(), reverse=True)[0]
```

#### What is the overall trend in gun purchase?
*data visualize for purchase trend*
```
df_gundata.groupby('month').totals.mean().plot(kind='line');
plt.legend();
plt.title("Gun Purchase Trend")
Text(0.5,1,'Gun Purchase Trend')
```


### Conclusions
#### Based on the gun data, Kentucky is the state that has the highest gun registration of 131,112 on average.

#### And the gun purchase trend is increasing overall.

