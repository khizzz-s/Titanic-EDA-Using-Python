# Titanic Data Analysis and Visualization

This repository contains an exploratory data analysis (EDA) project on the Titanic dataset.
The goal is to understand passenger survival patterns by analyzing factors such as age, gender, and class using Python.

## Project Overview

The project follows 22 guided analysis questions (outlined in `Titanic Case-study.pdf`).
Key steps include:

* Data loading and exploration
* Handling missing values and mapping categorical variables
* Visualization of survival rates and demographic patterns
* Focused analysis on specific passenger groups

The notebook (`Titanic EDA.ipynb`) serves as both a report and reproducible code, combining technical analysis and clear visual storytelling.

---

## Files in this Repository

| File                     | Description                                                        |
| ------------------------ | ------------------------------------------------------------------ |
| `Titanic.csv`            | Dataset containing passenger details and survival status           |
| `Titanic EDA.ipynb`      | Jupyter notebook with step-by-step analysis and visualizations     |
| `Titanic Case-study.pdf` | Document listing the 22 guided questions addressed in the notebook |

---

## Summary of the Code and Analysis

### 1. Data Loading and Exploration

The notebook starts by loading the dataset, displaying the first and last rows, and checking its shape and data types.

```python
import pandas as pd

df = pd.read_csv("Titanic.csv")
print(df.head())
print(df.tail())
print(df.shape)
print(df.info())
```

---

### 2. Data Cleaning

Handles missing data and drops irrelevant columns:

* Replaces missing `Age` values with the median.
* Drops `Cabin`, `Ticket`, and `Name` columns.

```python
df['Age'].fillna(df['Age'].median(), inplace=True)
df.drop(['Cabin', 'Ticket', 'Name'], axis=1, inplace=True)
```

---

### 3. Categorical Mapping

Maps the `Sex` column from text to numeric for analysis.

```python
df['Sex'] = df['Sex'].map({'male': 1, 'female': 0})
```

---

### 4. Visual Analysis

Creates plots to visualize survival rates and passenger characteristics.

#### Survival distribution

```python
import matplotlib.pyplot as plt

df['Survived'].value_counts().plot(kind='pie', autopct='%1.1f%%')
plt.title("Survival Distribution")
plt.show()
```

#### Survival by class

```python
import seaborn as sns

sns.countplot(x='Pclass', hue='Survived', data=df)
plt.title("Survival by Passenger Class")
plt.show()
```

#### Age distribution by survival status

```python
df[df['Survived']==1]['Age'].plot(kind='hist', bins=20, alpha=0.6, label='Survived')
df[df['Survived']==0]['Age'].plot(kind='hist', bins=20, alpha=0.6, label='Not Survived')
plt.title("Age Distribution by Survival")
plt.xlabel("Age")
plt.legend()
plt.show()
```

---

### 5. Answering Specific Questions

The notebook also analyzes:

* Number of first-class female passengers
* Survivors under 30 and male survivors over 40
* Class-wise survival patterns
* Combined subplots for class and gender survival comparisons

Example:

```python
len(df[(df['Sex']==0) & (df['Pclass']==1)])
```

---

## Key Findings

* Females had a significantly higher survival rate than males.
* First-class passengers were more likely to survive than those in lower classes.
* Passengers under age 30 had higher survival rates compared to older passengers.
* Most passengers traveled in third class, which had the lowest survival rate.
* Visualization made these patterns clear and easier to communicate.

---

## Technologies Used

* Python
* Pandas
* Matplotlib
* Seaborn
* Jupyter Notebook

## Author

**Syed Ateeb Shah**
