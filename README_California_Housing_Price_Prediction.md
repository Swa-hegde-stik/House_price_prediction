# California Housing Price Prediction

## Project Overview

This project builds and compares regression models for predicting California housing prices using the **California Housing dataset** from `sklearn.datasets`.

A key focus of the project is understanding how **missing data and imputation methods affect regression performance**.

## Dataset

- **Rows:** 20,640
- **Features:** 8
- **Target:** `Price`
- **Features:** `MedInc`, `HouseAge`, `AveRooms`, `AveBedrms`, `Population`, `AveOccup`, `Latitude`, `Longitude`
- The original dataset contains no missing values.

## Project Workflow

```text
California Housing Dataset
          |
          v
   Data Exploration
          |
          v
 Introduce 5% Missing Data
          |
          v
Compare Imputation Methods
 Mean / Median / KNN
          |
          v
 Regression Models
          |
          v
 Hyperparameter Tuning
          |
          v
     Final Evaluation
```

## 1. Data Loading and Exploration

The dataset was loaded using `sklearn.datasets.fetch_california_housing()` and converted into a Pandas DataFrame.

Exploratory analysis included:

- Dataset shape and structure
- Missing-value checks
- Histograms of numerical variables
- Correlation analysis using a heatmap

## 2. Introducing Missing Values

To study the effect of incomplete data, **5% of the feature values** were randomly replaced with `NaN` using a fixed random seed (`100`).

The target variable `Price` was kept unchanged.

## 3. Missing-Value Imputation

Three approaches were investigated:

- **Mean imputation** using `SimpleImputer`
- **Median imputation** using `SimpleImputer`
- **KNN imputation** using `KNNImputer(n_neighbors=5)`

The imputers were fitted on the training data and then applied to the test data to avoid data leakage.

## 4. Regression Models

The following regression models were compared:

- Linear Regression
- Lasso Regression
- Ridge Regression
- Decision Tree Regressor
- Random Forest Regressor
- XGBoost Regressor

### Baseline Performance on Original Data

| Model | R² Score |
|---|---:|
| Linear Regression | 0.576 |
| Lasso | 0.284 |
| Ridge | 0.576 |
| Decision Tree | 0.622 |
| Random Forest | 0.804 |
| XGBoost | 0.837 |

XGBoost produced the highest baseline R² score in the notebook.

## 5. Hyperparameter Tuning

RandomizedSearchCV was used to tune:

- Decision Tree
- Random Forest
- XGBoost

The search used:

- `n_iter=5`
- `cv=2`
- `random_state=42`

The final tuned models were evaluated using the KNN-imputed test data.

### Tuned Model Results

| Model | Test R² |
|---|---:|
| XGBoost | 0.777 |
| Random Forest | 0.771 |
| Decision Tree | 0.668 |

The tuned XGBoost model achieved a test R² of approximately **0.777** on the missing-value/KNN-imputed dataset.

## Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- XGBoost

## Key Concepts Demonstrated

- Exploratory Data Analysis
- Correlation analysis
- Missing-data simulation
- Mean, median and KNN imputation
- Data leakage prevention
- Regression modelling
- Model comparison
- Cross-validation
- Randomized hyperparameter search
- R²-based model evaluation

## Important Note

The notebook contains an intermediate comparison section where the variable named `results_knn` is actually fitted using the median-imputed training data. The final hyperparameter-tuning section correctly uses the **KNN-imputed training and test data**, and its reported test results are the figures used in this README.

## Project Structure

```text
California-Housing-Price-Prediction/
│
├── House_price_prediction.ipynb
├── README.md
└── California_Housing_Price_Prediction_Presentation.pptx
```

## Conclusion

The project demonstrates an end-to-end regression workflow and focuses on an important practical issue: **real-world datasets may contain missing values, and the choice of imputation method can influence model performance**.

The analysis compares traditional regression models with tree-based ensemble methods and uses randomized hyperparameter tuning to improve the final models.
