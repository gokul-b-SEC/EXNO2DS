# EXNO2DS
# AIM:
      To perform Exploratory Data Analysis on the given data set.
      
# EXPLANATION:
  The primary aim with exploratory analysis is to examine the data for distribution, outliers and anomalies to direct specific testing of your hypothesis.
  
# ALGORITHM:
STEP 1: Import the required packages to perform Data Cleansing,Removing Outliers and Exploratory Data Analysis.

STEP 2: Replace the null value using any one of the method from mode,median and mean based on the dataset available.

STEP 3: Use boxplot method to analyze the outliers of the given dataset.

STEP 4: Remove the outliers using Inter Quantile Range method.

STEP 5: Use Countplot method to analyze in a graphical method for categorical data.

STEP 6: Use displot method to represent the univariate distribution of data.

STEP 7: Use cross tabulation method to quantitatively analyze the relationship between multiple variables.

STEP 8: Use heatmap method of representation to show relationships between two variables, one plotted on each axis.

## CODING AND OUTPUT

```
# Step 1: Import the Required Packages

import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt


# Step 2: Load the Dataset

data = pd.read_csv('titanic_dataset.csv')

data


# Step 3: Data Cleansing - Replace Null Values

# Use mean for numeric and mode for categorical values

for column in data.columns:
    if pd.api.types.is_numeric_dtype(data[column]):
        data[column] = data[column].fillna(data[column].mean())
    else:
        data[column] = data[column].fillna(data[column].mode()[0])

print("Missing values handled.")

# Check missing values
data.isnull().sum()


# Step 4: Boxplot to Analyze Outliers

sns.boxplot(x=data['Fare'])

plt.title("Boxplot - Fare")
plt.xlabel("Fare")
plt.show()


# Step 5: Remove Outliers Using IQR Method

def remove_outliers_iqr(df, column):
    Q1 = df[column].quantile(0.25)
    Q3 = df[column].quantile(0.75)
    IQR = Q3 - Q1
    lower = Q1 - 1.5 * IQR
    upper = Q3 + 1.5 * IQR
    return df[(df[column] >= lower) & (df[column] <= upper)]


# Apply IQR method on Fare

data = remove_outliers_iqr(data, 'Fare')

print("Outliers removed using IQR method.")


# Step 6: Countplot for Categorical Data

sns.countplot(x='Sex', data=data)

plt.title("Countplot - Gender Distribution")
plt.xlabel("Gender")
plt.ylabel("Count")
plt.show()


# Step 7: Displot for Univariate Distribution

sns.displot(data['Age'], kde=True)

plt.title("Displot - Age Distribution")
plt.xlabel("Age")
plt.ylabel("Frequency")
plt.show()


# Step 8: Cross Tabulation to Analyze Relationships

# Gender vs Survived

crosstab_result = pd.crosstab(data['Sex'], data['Survived'])

print("\nCross Tabulation Result:")
print(crosstab_result)


# Step 9: Heatmap to Show Relationships

# Only numeric columns are considered for correlation

correlation_matrix = data.select_dtypes(include=np.number).corr()

sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm')

plt.title("Correlation Heatmap")
plt.show()
```

<img width="593" height="742" alt="image" src="https://github.com/user-attachments/assets/a5d15d06-c8a0-429a-822d-b65a02687b60" />
<img width="598" height="462" alt="image" src="https://github.com/user-attachments/assets/a2163c9f-4f72-4d5e-8d54-c2904327cbe9" />
<img width="597" height="382" alt="image" src="https://github.com/user-attachments/assets/93245fe5-4dc2-489c-9c92-02407ce7a41f" />



# RESULT

Thus the program to implement Exploratory Data Analysis
has been successfully completed using the Titanic dataset.
Missing values were handled, outliers were removed using
the IQR method, and data visualization was performed
using Countplot, Displot, Cross Tabulation and Heatmap.
