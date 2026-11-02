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

df = pd.read_csv("Data_set.csv")

print("\nOriginal Data:\n", df.head(10))
print("\nMissing values:\n", df.isnull().sum())

clean = df.copy()

for col in clean.select_dtypes(include="number").columns:
    clean[col] = clean[col].fillna(clean[col].median())

for col in clean.select_dtypes(include="object").columns:
    if not clean[col].mode().empty:
        clean[col] = clean[col].fillna(clean[col].mode()[0])

print("\nMissing values after cleaning:\n", clean.isnull().sum())
print("\nCleaned Data:\n", clean.head(10))

clean.to_csv("Data_set_cleaned.csv", index=False)
print("\nSaved Data_set_cleaned.csv")
```
<img width="641" height="606" alt="image" src="https://github.com/user-attachments/assets/1b82391c-3ea1-43ee-9b4c-2a20562e80aa" />

```
import pandas as pd
import numpy as np

df = pd.read_csv("SAMPLEIDS.csv")

print("\nOriginal Data:\n", df.head(10))
print("\nDuplicate rows:", df.duplicated().sum())

clean = df.drop_duplicates().copy()
for col in clean.select_dtypes(include="object").columns:
    clean[col] = clean[col].str.strip()
    print("\nUnique values in", col)
    print(clean[col].unique())

print("\nDuplicate rows after removal:", clean.duplicated().sum())
print("\nCleaned Data:\n", clean.head(10))

clean.to_csv("SAMPLEIDS_cleaned.csv", index=False)
print("\nSaved SAMPLEIDS_cleaned.csv")
```
### OUTPUT:
<img width="599" height="532" alt="image" src="https://github.com/user-attachments/assets/8d066edb-d7fa-4224-88f4-dd8608e54750" />

```
import pandas as pd
import numpy as np
from scipy import stats
import matplotlib.pyplot as plt

df = pd.read_csv("heights.csv")

print("\nOriginal Data:\n", df.head(10))

for col in df.select_dtypes(include="number").columns:

    values = df[col].dropna()

    if values.empty:
        continue

    q1 = values.quantile(0.25)
    q3 = values.quantile(0.75)
    iqr = q3 - q1

    lower = q1 - 1.5 * iqr
    upper = q3 + 1.5 * iqr

    outliers = values[(values < lower) | (values > upper)]

    print("\nIQR results for", col)
    print("Lower limit:", lower)
    print("Upper limit:", upper)
    print("Unusual measurements:\n", outliers)

for col in df.select_dtypes(include="number").columns:
    plt.figure()
    plt.boxplot(df[col].dropna())
    plt.title("Unusual measurements in " + col)
    plt.ylabel(col)
    plt.show()
```
### OUTPUT

<img width="759" height="676" alt="image" src="https://github.com/user-attachments/assets/e84f0cd8-b3de-4792-a6b5-fb64f0a96dec" />


```
import pandas as pd
import numpy as np
from scipy import stats
df = pd.read_csv("iris.csv")

print("\nOriginal Data:\n", df.head(10))


for col in df.select_dtypes(include="number").columns:

    values = df[col].dropna()

    if values.empty:
        continue

    q1 = values.quantile(0.25)
    q3 = values.quantile(0.75)
    iqr = q3 - q1

    lower = q1 - 1.5 * iqr
    upper = q3 + 1.5 * iqr

    outliers = values[(values < lower) | (values > upper)]

    print("\nIQR outliers in", col)
    print(outliers if not outliers.empty else "None")

# STEP 3: Z-SCORE OUTLIER DETECTION
for col in df.select_dtypes(include="number").columns:

    values = df[col].dropna()

    if len(values) < 2:
        continue

    z = np.abs(stats.zscore(values))
    outliers = values[z > 3]

    print("\nZ-score outliers in", col)
    print(outliers if not outliers.empty else "None")
```
### OUTPUT 

<img width="653" height="614" alt="image" src="https://github.com/user-attachments/assets/711f31fe-1743-4cdd-bb39-13ab4a4d6964" />


```
import pandas as pd
import numpy as np
from scipy import stats
df = pd.read_csv("iris.csv")

print("\nOriginal Data:\n", df.head(10))


for col in df.select_dtypes(include="number").columns:

    values = df[col].dropna()

    if values.empty:
        continue

    q1 = values.quantile(0.25)
    q3 = values.quantile(0.75)
    iqr = q3 - q1

    lower = q1 - 1.5 * iqr
    upper = q3 + 1.5 * iqr

    outliers = values[(values < lower) | (values > upper)]

    print("\nIQR outliers in", col)
    print(outliers if not outliers.empty else "None")

# STEP 3: Z-SCORE OUTLIER DETECTION
for col in df.select_dtypes(include="number").columns:

    values = df[col].dropna()

    if len(values) < 2:
        continue

    z = np.abs(stats.zscore(values))
    outliers = values[z > 3]

    print("\nZ-score outliers in", col)
    print(outliers if not outliers.empty else "None")
```
### OUTPUT

<img width="602" height="654" alt="image" src="https://github.com/user-attachments/assets/e0aca13d-e87c-4c88-a2bf-d9d0b297b675" />

# Result

 The given data was read, cleaned by removing missing and duplicate values, and saved to a file successfully.

