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
![image](https://github.com/user-attachments/assets/75598ef8-0c24-4e00-bcc0-e588f975bfac)
```
from sklearn.preprocessing import LabelEncoder,OrdinalEncoder
pm=['Hot','Warm','Cold']
e1=OrdinalEncoder(categories=[pm])
e1.fit_transform(df[["ord_2"]])
```
![image](https://github.com/user-attachments/assets/2c510d83-1242-48a6-ada8-80e26e57b201)
```
df['bo2']=e1.fit_transform(df[["ord_2"]])
df
```
![image](https://github.com/user-attachments/assets/ee942dd5-2614-48aa-b531-8804691e60b2)
```
le=LabelEncoder()
dfc=df.copy()
dfc['ord_2']=le.fit_transform(dfc['ord_2'])
dfc
```
![image](https://github.com/user-attachments/assets/68d2ea2f-e5b9-449f-99bc-a40f52da5ab0)
```
from sklearn.preprocessing import OneHotEncoder
# Use sparse_output=False instead of sparse=False
ohe = OneHotEncoder(sparse_output=False)
df2 = df.copy()
enc = pd.DataFrame(ohe.fit_transform(df2[["nom_0"]]))
```
```
df2=pd.concat([df2,enc],axis=1)
df2
```
![image](https://github.com/user-attachments/assets/1440df78-a366-4d0a-87fe-5b00c69d8a01)
```
pd.get_dummies(df2,columns=["nom_0"])
```
![image](https://github.com/user-attachments/assets/2a5b1519-6425-49c6-af0f-4cf0409b5037)
```
pip install --upgrade category_encoders
```
```
from category_encoders import BinaryEncoder
df=pd.read_csv("dt.csv")
df
```
![image](https://github.com/user-attachments/assets/9951ebb1-d6c5-4346-8ae5-53c326d8606e)
```
from category_encoders import TargetEncoder
te=TargetEncoder()
cc=df.copy()
new=te.fit_transform(X=cc["City"],y=cc["Target"])
cc=pd.concat([cc,new],axis=1)
cc
```
![image](https://github.com/user-attachments/assets/cb1e9b28-d4a5-4d20-904a-39f76c158f44)
```
df.skew()
```
![image](https://github.com/user-attachments/assets/be13e245-7941-4047-9c63-69f292e25d37)
```
df["Highly Positive Skew"]=np.log(df["Highly Positive Skew"])
df
```
![image](https://github.com/user-attachments/assets/e16ed47a-3c20-4027-a5e6-aaf37af5f521)
```
df["Moderate Positive Skew"]=np.reciprocal(df["Moderate Positive Skew"])
df
```
![image](https://github.com/user-attachments/assets/090c06c0-e1a1-40c3-8622-10d1515fa4e6)
```
df["Moderate Negative Skew_yeojohnson"],parameter=stats.yeojohnson(df["Moderate Negative Skew"])
df
```
![image](https://github.com/user-attachments/assets/ae0d7274-81e9-44dc-8bef-ea5841252c26)
```
import seaborn as sns
import statsmodels.api as sm
import matplotlib.pyplot as plt
sm.qqplot(df["Moderate Negative Skew"],line='45')
plt.show()
```
![image](https://github.com/user-attachments/assets/522d914b-6248-4c5e-8bc0-abd29553df39)
```
sm.qqplot(np.reciprocal(df["Moderate Negative Skew"]),line='45')
plt.show()
```
![image](https://github.com/user-attachments/assets/b3f8c6ac-1a11-45ae-802b-4f72ad8d43b7)
```
from sklearn.preprocessing import QuantileTransformer
qt=QuantileTransformer(output_distribution='normal',n_quantiles=891)
df["Moderate Negative Skew"]=qt.fit_transform(df[["Moderate Negative Skew"]])
sm.qqplot(df["Moderate Negative Skew"],line='45')
plt.show()
```
![image](https://github.com/user-attachments/assets/979f9117-443f-4a7e-8c6f-66ede7e3db79)
```
sm.qqplot(np.reciprocal(df["Moderate Negative Skew"]),line='45')
plt.show()
```
![image](https://github.com/user-attachments/assets/3c7156f7-9791-423c-aa76-e97651438a63)

## RESULT:
        Thus the given data, Feature Encoding, Transformation process and save the data to a file was performed successfully. 

       
