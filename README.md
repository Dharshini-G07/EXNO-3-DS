## EXNO-3-DS

# AIM:
To read the given data and perform Feature Encoding and Transformation process and save the data to a file.

# ALGORITHM:
STEP 1:Read the given Data.
STEP 2:Clean the Data Set using Data Cleaning Process.
STEP 3:Apply Feature Encoding for the feature in the data set.
STEP 4:Apply Feature Transformation for the feature in the data set.
STEP 5:Save the data to the file.

# FEATURE ENCODING:
1. Ordinal Encoding
An ordinal encoding involves mapping each unique label to an integer value. This type of encoding is really only appropriate if there is a known relationship between the categories. This relationship does exist for some of the variables in our dataset, and ideally, this should be harnessed when preparing the data.
2. Label Encoding
Label encoding is a simple and straight forward approach. This converts each value in a categorical column into a numerical value. Each value in a categorical column is called Label.
3. Binary Encoding
Binary encoding converts a category into binary digits. Each binary digit creates one feature column. If there are n unique categories, then binary encoding results in the only log(base 2)ⁿ features.
4. One Hot Encoding
We use this categorical data encoding technique when the features are nominal(do not have any order). In one hot encoding, for each level of a categorical feature, we create a new variable. Each category is mapped with a binary variable containing either 0 or 1. Here, 0 represents the absence, and 1 represents the presence of that category.

# Methods Used for Data Transformation:
  # 1. FUNCTION TRANSFORMATION
• Log Transformation
• Reciprocal Transformation
• Square Root Transformation
• Square Transformation
  # 2. POWER TRANSFORMATION
• Boxcox method
• Yeojohnson method

# CODING AND OUTPUT:
```
 import pandas as pd
 df=pd.read_csv("Encoding Data.csv")
 df
```
<img width="347" height="434" alt="Screenshot 2025-09-30 104457" src="https://github.com/user-attachments/assets/497ff89d-05cf-404c-b671-946586623d1a" />


```
 from sklearn.preprocessing import LabelEncoder,OrdinalEncoder
 pm=['Hot','Warm','Cold']
 e1=OrdinalEncoder(categories=[pm])
 e1.fit_transform(df[["ord_2"]])
```
<img width="184" height="235" alt="Screenshot 2025-09-30 104524" src="https://github.com/user-attachments/assets/d9976027-0fd4-40b5-bf63-228071732358" />

```
 df['bo2']=e1.fit_transform(df[["ord_2"]])
 df
```
<img width="384" height="420" alt="Screenshot 2025-09-30 104555" src="https://github.com/user-attachments/assets/22bf8413-acea-4f68-b1b9-bb653992f09e" />

```
 le=LabelEncoder()
 dfc=df.copy()
 dfc['ord_2']=le.fit_transform(dfc['ord_2'])
 dfc
```
<img width="363" height="415" alt="Screenshot 2025-09-30 104624" src="https://github.com/user-attachments/assets/0b5a10e6-61c1-4db0-afcf-edb036f81b92" />


```
 from sklearn.preprocessing import OneHotEncoder
 ohe=OneHotEncoder(sparse_output=False)
 df2=df.copy()
 enc=pd.DataFrame(ohe.fit_transform(df2[["nom_0"]]))
 df2=pd.concat([df2,enc],axis=1)
 df2
```


<img width="499" height="424" alt="Screenshot 2025-09-30 104649" src="https://github.com/user-attachments/assets/86f74f05-ff64-4d8d-8b96-1e6e035dc0ab" />

```
 pd.get_dummies(df2,columns=["nom_0"])
```

<img width="743" height="433" alt="Screenshot 2025-09-30 104718" src="https://github.com/user-attachments/assets/fe701646-891b-408d-8096-fd896a1c5609" />


```
 from category_encoders import BinaryEncoder
 df=pd.read_csv("data.csv")
 df
```
<img width="553" height="433" alt="Screenshot 2025-09-30 104742" src="https://github.com/user-attachments/assets/19cb95e1-f5f0-4ca1-b47e-a5d707ec709b" />


```
 be=BinaryEncoder()
 nd=be.fit_transform(df['Ord_2'])
 df
```
<img width="540" height="427" alt="Screenshot 2025-09-30 104803" src="https://github.com/user-attachments/assets/ae1dd512-df79-448e-ba87-5844fbaa972d" />

```
 dfb=pd.concat([df,nd],axis=1)
 dfb
```
<img width="751" height="411" alt="Screenshot 2025-09-30 104835" src="https://github.com/user-attachments/assets/76b0a726-3dd6-46f5-81af-c0a01551f9e9" />

```

 from category_encoders import TargetEncoder
 te=TargetEncoder()
 CC=df.copy()
 new=te.fit_transform(X=CC["City"],y=CC["Target"])
 CC=pd.concat([CC,new],axis=1)
 CC
```

<img width="609" height="426" alt="Screenshot 2025-09-30 104901" src="https://github.com/user-attachments/assets/f931ceae-9737-45e0-b5cf-02ac1e76bf51" />

```
 import pandas as pd
 from scipy import stats
 import numpy as np
 df=pd.read_csv("Data_to_Transform.csv")
 df
```

<img width="861" height="511" alt="Screenshot 2025-09-30 104934" src="https://github.com/user-attachments/assets/a72551da-8285-4b30-bbcc-ad2d1344a67d" />

```
 df.skew()
```

<img width="352" height="124" alt="Screenshot 2025-09-30 105009" src="https://github.com/user-attachments/assets/93cf8649-ee53-4b4a-9927-d21ef3b6e097" />

```
np.log(df["Highly Positive Skew"])
```

<img width="538" height="256" alt="Screenshot 2025-09-30 105034" src="https://github.com/user-attachments/assets/36ab49a9-e6ef-43a7-a332-8e3854eb7ec3" />

```
 np.reciprocal(df["Moderate Positive Skew"])
```

<img width="608" height="269" alt="image" src="https://github.com/user-attachments/assets/586a6a9d-2f32-4adf-9a45-78f926a3a6ca" />


```
 np.sqrt(df["Highly Positive Skew"])
```


<img width="554" height="266" alt="image" src="https://github.com/user-attachments/assets/993473c9-defd-4cc1-a103-15e11f174796" />


```
 np.square(df["Highly Positive Skew"])
```


<img width="576" height="262" alt="image" src="https://github.com/user-attachments/assets/73fad986-30cb-4bc1-a05b-32c07200217a" />


```
 df["Highly Positive Skew_boxcox"], parameters=stats.boxcox(df["Highly Positive Skew"])
 df
```



<img width="1108" height="508" alt="image" src="https://github.com/user-attachments/assets/1d3426bb-22c6-485d-b643-beb98f29d90a" />


```
 df.skew()
```



<img width="414" height="150" alt="image" src="https://github.com/user-attachments/assets/e04ff10e-eabd-4916-a74c-0ef07302ef8c" />


```
 df["Highly Negative Skew_yeojohnson"],parameters=stats.yeojohnson(df["Highly Negative Skew"])
 df.skew()
```


<img width="465" height="161" alt="image" src="https://github.com/user-attachments/assets/b2920718-f1fc-43f4-ac6b-5e95bc8da855" />


```
 from sklearn.preprocessing import QuantileTransformer
 qt=QuantileTransformer(output_distribution='normal')
 df["Moderate Negative Skew_1"]=qt.fit_transform(df[["Moderate Negative Skew"]])
 df
```


<img width="1417" height="527" alt="image" src="https://github.com/user-attachments/assets/80fbb29c-db91-443c-8569-6c93e1da2b12" />

```
 import seaborn as sns
 import statsmodels.api as sm
 import matplotlib.pyplot as plt
 sm.qqplot(df["Moderate Negative Skew"],line='45')
 plt.show()
```

<img width="778" height="548" alt="image" src="https://github.com/user-attachments/assets/70235e60-f741-403c-a1a9-4220d6bfbe6f" />


```
 sm.qqplot(np.reciprocal(df["Moderate Negative Skew"]),line='45')
 plt.show()
```

<img width="808" height="536" alt="image" src="https://github.com/user-attachments/assets/24911172-bee5-4877-8722-4a44c1c57c49" />


```
 from sklearn.preprocessing import QuantileTransformer
 qt=QuantileTransformer(output_distribution='normal',n_quantiles=891)
 df["Moderate Negative Skew"]=qt.fit_transform(df[["Moderate Negative Skew"]])
 sm.qqplot(df["Moderate Negative Skew"],line='45')
 plt.show()
```

<img width="761" height="532" alt="image" src="https://github.com/user-attachments/assets/fef4e088-2967-49f5-aa53-d3037830d9cc" />

```
 df["Highly Negative Skew_1"]=qt.fit_transform(df[["Highly Negative Skew"]])
 sm.qqplot(df["Highly Negative Skew"],line='45')
 plt.show()
```


<img width="755" height="530" alt="image" src="https://github.com/user-attachments/assets/84f992d8-57b3-4f7c-94bf-c5c22da5fb1d" />

```
dt=pd.read_csv("titanic_dataset.csv")
dt
from sklearn.preprocessing import QuantileTransformer
qt=QuantileTransformer(output_distribution='normal',n_quantiles=891)
dt["Age_1"]=qt.fit_transform(dt[["Age"]])
sm.qqplot(dt['Age'],line='45') 
plt.show()
```

<img width="764" height="536" alt="image" src="https://github.com/user-attachments/assets/1e697e14-af19-4d6b-b12e-7d025c597660" />

```
 sm.qqplot(df["Highly Negative Skew_1"],line='45')
 plt.show()
```

<img width="773" height="537" alt="image" src="https://github.com/user-attachments/assets/2494c9c0-dc02-47ba-af33-a654bbd24293" />

















































































































# RESULT:
 Thus the given data, Feature Encoding, Transformation process and save the data to a file
 was performed successfully.

       
