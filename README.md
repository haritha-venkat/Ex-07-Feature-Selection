# Ex-07-Feature-Selection
## AIM

To Perform the various feature selection techniques on a dataset and save the data to a file.
## Explanation

Feature selection is to find the best set of features that allows one to build useful models. Selecting the best features helps the model to perform well.
## ALGORITHM
### STEP 1

Read the given Data
### STEP 2

Clean the Data Set using Data Cleaning Process
### STEP 3

Apply Feature selection techniques to all the features of the data set
### STEP 4

Save the data to the file
## CODE-Done for "titanic_dataset.csv"
```python
Developed By: HARITHASHREE.V
Reg.No: 212222230046

import pandas as pd
import numpy as np
df = pd.read_csv("titanic_dataset.csv")
df

df.isnull().sum()

from sklearn.preprocessing import LabelEncoder
from sklearn.impute import SimpleImputer
from sklearn.feature_selection import SelectKBest
from sklearn.feature_selection import chi2
df.drop(['PassengerId', 'Name', 'Ticket', 'Cabin'], axis=1, inplace=True)
le = LabelEncoder()
df['Sex'] = le.fit_transform(df['Sex'])
df['Embarked'] = le.fit_transform(df['Embarked'].astype(str))
imputer = SimpleImputer(missing_values=np.nan, strategy='median')
df[['Age']] = imputer.fit_transform(df[['Age']])
print("Feature selection")
X = df.iloc[:, :-1]
y = df.iloc[:, -1]
selector = SelectKBest(chi2, k=3)
X_new = selector.fit_transform(X, y)
print(X_new)
df_new = pd.DataFrame(X_new, columns=['Pclass', 'Age', 'Fare'])
df_new['Survived'] = y.values
df_new.to_csv('titanic_transformed.csv', index=False)
print(df_new)

```
## OUTPUT:
![image](https://github.com/haritha-venkat/Ex-07-Feature-Selection/assets/121285701/0f0485ff-c873-4dea-bb7f-573403baaa95)
![image](https://github.com/haritha-venkat/Ex-07-Feature-Selection/assets/121285701/6cda61e7-b3fa-42c2-9ccc-36e7ca7c9261)
![image](https://github.com/haritha-venkat/Ex-07-Feature-Selection/assets/121285701/78c656f1-ea8e-4eea-84b1-9cedf7852b53)

## CODE-Done for "CarPrice.csv"
```python
Developed By: HARITHASHREE.V
Reg.No: 212222230046

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
df = pd.read_csv("CarPrice.csv")
df

df.isnull().sum()

from sklearn.model_selection import train_test_split
from sklearn.preprocessing import LabelEncoder
from sklearn.feature_selection import SelectKBest, f_regression
from sklearn.ensemble import ExtraTreesRegressor
df = df.drop(['car_ID', 'CarName'], axis=1)
le = LabelEncoder()
df['fueltype'] = le.fit_transform(df['fueltype'])
df['aspiration'] = le.fit_transform(df['aspiration'])
df['doornumber'] = le.fit_transform(df['doornumber'])
df['carbody'] = le.fit_transform(df['carbody'])
df['drivewheel'] = le.fit_transform(df['drivewheel'])
df['enginelocation'] = le.fit_transform(df['enginelocation'])
df['enginetype'] = le.fit_transform(df['enginetype'])
df['cylindernumber'] = le.fit_transform(df['cylindernumber'])
df['fuelsystem'] = le.fit_transform(df['fuelsystem'])
X = df.iloc[:, :-1]
y = df.iloc[:, -1]
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2,
random_state=1)
print("Univariate Selection")
selector = SelectKBest(score_func=f_regression, k=10)
X_train_new = selector.fit_transform(X_train, y_train)
mask = selector.get_support()
selected_features = X_train.columns[mask]
model = ExtraTreesRegressor()
model.fit(X_train, y_train)
importance = model.feature_importances_
indices = np.argsort(importance)[::-1]
selected_features = X_train.columns[indices][:10]
df_new = pd.concat([X_train[selected_features], y_train], axis=1)
df_new.to_csv('CarPrice_new.csv', index=False)
print(df_new)
```
## OUTPUT:
![image](https://github.com/haritha-venkat/Ex-07-Feature-Selection/assets/121285701/ead281b8-2501-429e-8661-7b43d1bcb276)
![image](https://github.com/haritha-venkat/Ex-07-Feature-Selection/assets/121285701/f0f9c162-4ff3-406f-818e-c2c4b3e81024)
![image](https://github.com/haritha-venkat/Ex-07-Feature-Selection/assets/121285701/e0a3a4a3-a18c-438b-826b-c1f52788ff0f)


## RESULT:
    Hence various feature selection techniques are applied to the given data set successfully and saved the data into a file.
