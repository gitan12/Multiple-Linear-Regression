# Predicting Car Prices Using Multiple Linear Regression

In this project, we used a dataset to predict car prices based on various features using multiple linear regression.

## Table of Contents
1. Introduction
2. Objectives
3. Dataset Information
4. Prerequisites
5. Steps Involved in data preprocesing and model development
    1. Importing Libraries
    2. Loading the Dataset
    3. Data Exploration
    4. Exploratory Data Analysis
    5. Pre-processing
    6. Splitting Data into Training and Testing Sets
    7. Building and Training the Multiple Linear Regression Model
    8. Making Predictions
    9. Evaluating Model Performance
7. Conclusion

## 1. Introduction
Multiple linear regression extends simple linear regression by allowing for multiple independent variables to predict the dependent variable. This project focuses on predicting car prices based on various attributes of the cars.

## 2. Objectives
The main objectives of this project are:
- To understand the relationship between car features and their prices.
- To build a model that can predict car prices based on these features.
- To evaluate the model's performance using various metrics.

## 3. Dataset Information
The dataset contains the following columns:
- **symboling**
- **normalized_losses**
- **make**
- **fuel_type**
- **aspiration**
- **num_doors**
- **body_style**
- **drive_wheels**
- **engine_location**
- **wheel_base**
- **length**
- **width**
- **height**
- **curb_weight**
- **engine_type**
- **num_cylinders**
- **engine_size**
- **fuel_system**
- **bore**
- **stroke**
- **compression_ratio**
- **horsepower**
- **peak_rpm**
- **city_mpg**
- **highway_mpg**
- **price** (target variable)

## 4. Prerequisites
To run this project, you'll need:
- Python installed on your computer.
- Basic understanding of Python programming.
- Libraries: pandas, matplotlib, seaborn, sklearn

## 5. Steps Involved in Data Preprocessing and Model Development

### A. Importing Libraries

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error, mean_absolute_error, r2_score
import warnings
warnings.filterwarnings('ignore')
```
First, we import the necessary libraries that are essential for data processing, model training, and assessment. This includes **Pandas** for data manipulation, **Matplotlib** and **Seaborn** for visualization, and various modules from **scikit-learn** for model building and evaluation.

### B. Loading the Dataset

```python
df = pd.read_csv("CarPrice_Assignment.csv")
```
We load our dataset from a CSV file using the Pandas library. This command reads the file and stores its content in a DataFrame, which allows us to manipulate and analyze the data.

### C. Data Exploration

```python
print(df.head())
print(df.shape)
print(df.isnull().sum())
print(df.describe().T)
```
To explore our dataset and gain insights into its structure, we:
- Print the first few rows to get an initial understanding of the data.
- Check the dimensions of the dataset (number of rows and columns).
- Identify and count any missing values.
- Generate descriptive statistics for numerical columns to understand their distribution, central tendency, and dispersion.

### D. Exploratory Data Analysis
We analyze the distribution of the target variable (price) and explore correlations among features.

#### 1. Distribution of Target Variable (Price)

```python
plt.figure(figsize=(8, 5))
sns.histplot(df['price'], kde=True)
plt.xlabel("Price")
plt.ylabel("Frequency")
plt.title("Distribution of Car Prices")
plt.grid(True)
plt.show()
```
We create a histogram to visualize the distribution of car prices in the dataset, which helps us understand the range and frequency of prices.

#### 2. Correlation Heatmap

```python
plt.figure(figsize=(15, 10))
sns.heatmap(df.corr(), annot=True, cmap='coolwarm')
plt.title("Correlation Heatmap")
plt.show()
```
We use a heatmap to illustrate the correlation between different features in the dataset. This helps identify which features have strong relationships with the target variable (price).

### E. Pre-processing

#### 1. Handling Missing Values

```python
df = df.dropna()
```
We drop any rows with missing values to ensure the dataset is complete and ready for analysis.

#### 2. Encoding Categorical Variables

```python
df = pd.get_dummies(df, drop_first=True)
```
We convert categorical variables into numerical format using one-hot encoding, which creates binary columns for each category, excluding the first to avoid multicollinearity.

#### 3. Splitting Features and Target

```python
X = df.drop('price', axis=1)
y = df['price']
```
We separate the dataset into features (X) and the target variable (y). The features include all columns except the target column 'price'.

### F. Splitting Data into Training and Testing Sets

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)
```
We partition the dataset into training and testing subsets, with 70% of the data used for training and 30% for testing. This split allows us to train the model on one set and evaluate its performance on another.

### G. Building and Training the Multiple Linear Regression Model

```python
LR = LinearRegression()
LR.fit(X_train, y_train)
```
We create a linear regression model and train it using the training data. The model learns the relationship between the features and the target variable.

### H. Making Predictions

```python
y_pred = LR.predict(X_test)
```
We use the trained model to predict car prices for the test set.

### I. Evaluating Model Performance
We evaluate the model using various metrics.

#### 1. Mean Squared Error (MSE)

```python
MSE = mean_squared_error(y_test, y_pred)
print("Mean Squared Error:", MSE)
```
We calculate the Mean Squared Error (MSE) to measure the average squared difference between the predicted and actual prices.

#### 2. Mean Absolute Error (MAE)

```python
MAE = mean_absolute_error(y_test, y_pred)
print("Mean Absolute Error:", MAE)
```
We calculate the Mean Absolute Error (MAE) to measure the average absolute difference between the predicted and actual prices.

#### 3. Root Mean Squared Error (RMSE)

```python
from math import sqrt
RMSE = sqrt(mean_squared_error(y_test, y_pred))
print("Root Mean Squared Error:", RMSE)
```
We compute the Root Mean Squared Error (RMSE), which is the square root of the Mean Squared Error, providing error in the same units as the target variable.

#### 4. R² Score

```python
R2_score = r2_score(y_test, y_pred)
print("R² Score:", R2_score)
```
The R² score indicates the proportion of the variance in the dependent variable that is predictable from the independent variables. It measures how well the regression model fits the observed data.

## 6. Conclusion
- The multiple linear regression model provides insights into how various car attributes influence the price.
- The evaluation metrics (MSE, MAE, RMSE, and R²) help us understand the model's accuracy and reliability.
- Further improvements can be made by feature selection, outlier removal, or using more advanced regression techniques.

## Important Points to Remember
- Multiple linear regression assumes a linear relationship between the independent and dependent variables.
- The model's performance can be evaluated using metrics such as MSE, MAE, RMSE, and R² Score.
- Understanding the data and checking for assumptions (linearity, independence, homoscedasticity, and normality) is crucial for building a reliable model.

This project serves as a practical introduction to multiple linear regression, showcasing how machine learning can be used to make predictions based on data.
